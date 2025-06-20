---
description: >-
  The WebView option allows individuals to verify their identity in a mobile app
  with the Android WebView or iOS WKWebView.
---

# WebView iOS and Android

## Mobile WebView Integration (iOS & Android)

For a seamless, in-app user experience, you can embed the Trust Swiftly verification flow within your native mobile app using a WebView component. This guide will walk you through the implementation for both Android and iOS.

The core technology is the same **Magic Link** used in web integrations, but with a specific pattern to control the user flow.

***

#### The Core Concept: The "Redirect-to-Close" Pattern

This is the most important concept for a successful WebView integration.

1. **Get the Link:** Your app gets a unique `magic_link` for a user from your backend.
2. **Provide a Redirect URL:** When your backend creates or requests the user link from the Trust Swiftly API, it **must** include a `redirect_url`. This URL should be a custom, non-existent URL that your app can uniquely identify (e.g., `https://yourapp.com/verification-complete`).
3. **Open the WebView:** Your app opens the `magic_link` in a full-screen WebView.
4. **User Completes Flow:** The user completes the verification steps inside the WebView.
5. **Trust Swiftly Redirects:** Upon completion, our server redirects the WebView to the `redirect_url` you provided.
6. **Your App Intercepts the Redirect:** Your app's native code must listen for navigation events within the WebView. When it detects the WebView attempting to navigate to your specific `redirect_url`, it knows the process is complete.
7. **Your App Closes the WebView:** Upon detecting the redirect, your app programmatically closes the WebView and returns the user to your native UI.

This pattern ensures a smooth transition back to your application without the user getting "stuck" on a "verification complete" page inside the WebView.

***

## Android `WebView` Guide

**Step 1: Configure Permissions & Manifest**

First, ensure your `AndroidManifest.xml` includes the necessary permissions for camera access and is configured to handle the WebView activity.

```xml
<!-- AndroidManifest.xml -->
<manifest ...>
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.CAMERA" />

    <application ...>
        <activity android:name=".TrustSwiftlyWebViewActivity" />
        <!-- ... other activities -->
    </application>
</manifest>
```

**Step 2: Implement the WebView Activity**

Create a dedicated `Activity` to host the `WebView`. This code provides a complete, robust implementation that handles permissions, file uploads, and the critical redirect-to-close pattern.

```java
// TrustSwiftlyWebViewActivity.java
import android.app.Activity;
import android.content.Intent;
import android.net.Uri;
import android.os.Bundle;
import android.webkit.PermissionRequest;
import android.webkit.ValueCallback;
import android.webkit.WebChromeClient;
import android.webkit.WebSettings;
import android.webkit.WebView;
import android.webkit.WebViewClient;
import androidx.appcompat.app.AppCompatActivity;

public class TrustSwiftlyWebViewActivity extends AppCompatActivity {

    public static final String EXTRA_MAGIC_LINK = "extra_magic_link";
    private static final String REDIRECT_URL = "https://yourapp.com/verification-complete"; // Your unique redirect URL

    private WebView webView;
    private ValueCallback<Uri[]> filePathCallback;
    // ... (Add other variables for file chooser logic from your original docs if needed)

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_webview); // Assume a simple layout with a WebView

        webView = findViewById(R.id.webView);
        String magicLink = getIntent().getStringExtra(EXTRA_MAGIC_LINK);

        // --- Basic WebView Settings ---
        WebSettings settings = webView.getSettings();
        settings.setJavaScriptEnabled(true);
        settings.setDomStorageEnabled(true);
        settings.setMediaPlaybackRequiresUserGesture(false);

        // --- The two most important clients ---
        webView.setWebViewClient(new TrustSwiftlyWebViewClient());
        webView.setWebChromeClient(new TrustSwiftlyWebChromeClient());

        if (magicLink != null) {
            webView.loadUrl(magicLink);
        }
    }

    // This client handles page navigation and the redirect-to-close pattern.
    private class TrustSwiftlyWebViewClient extends WebViewClient {
        @Override
        public boolean shouldOverrideUrlLoading(WebView view, String url) {
            // === THIS IS THE MOST IMPORTANT PART ===
            // Check if the WebView is being redirected to our special URL.
            if (url.startsWith(REDIRECT_URL)) {
                // The flow is complete. Set a result and finish this activity.
                setResult(Activity.RESULT_OK);
                finish();
                return true; // Stop the redirect from actually loading.
            }
            return super.shouldOverrideUrlLoading(view, url);
        }
    }

    // This client handles UI-related events like permissions and file choosers.
    private class TrustSwiftlyWebChromeClient extends WebChromeClient {
        // This is for requesting camera permission when needed by the webpage.
        @Override
        public void onPermissionRequest(PermissionRequest request) {
            // NOTE: This is a simplified example. A production app should handle
            // permission requests more gracefully.
            request.grant(request.getResources());
        }

        // This is for handling file uploads (e.g., uploading an ID document).
        @Override
        public boolean onShowFileChooser(WebView webView, ValueCallback<Uri[]> filePathCallback, FileChooserParams fileChooserParams) {
            TrustSwiftlyWebViewActivity.this.filePathCallback = filePathCallback;
            // (Your existing robust file chooser logic goes here)
            // ...
            return true;
        }
    }
    
    // (Your existing onActivityResult and onRequestPermissionsResult logic goes here)
    // ...
}
```

**Step 3: Launch the Activity**

From another part of your app, launch the `TrustSwiftlyWebViewActivity` and pass the `magic_link`.

```java
// In your main activity or fragment
Intent intent = new Intent(this, TrustSwiftlyWebViewActivity.class);
intent.putExtra(TrustSwiftlyWebViewActivity.EXTRA_MAGIC_LINK, "YOUR_MAGIC_LINK_FROM_API");
startActivityForResult(intent, YOUR_REQUEST_CODE);
```

***

## iOS `WKWebView` Guide

**Step 1: Configure Permissions (`Info.plist`)**

Your app must include an entry for `NSCameraUsageDescription` in its `Info.plist` file to explain why it needs camera access.

```xml
<!-- Info.plist -->
<key>NSCameraUsageDescription</key>
<string>We need access to your camera to verify your identity.</string>
```

**Step 2: Implement the WebView Controller**

Create a dedicated `UIViewController` to manage the `WKWebView`. This controller will handle loading the URL, delegating permissions, and intercepting the final redirect.

```swift
// TrustSwiftlyWebViewController.swift
import UIKit
import WebKit

class TrustSwiftlyWebViewController: UIViewController, WKNavigationDelegate, WKUIDelegate {

    var magicLink: URL!
    var webView: WKWebView!
    let redirectUrl = "https://yourapp.com/verification-complete" // Your unique redirect URL

    override func loadView() {
        let webConfiguration = WKWebViewConfiguration()
        webConfiguration.allowsInlineMediaPlayback = true // Prevents fullscreen video takeover
        webView = WKWebView(frame: .zero, configuration: webConfiguration)
        webView.navigationDelegate = self
        webView.uiDelegate = self
        view = webView
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        webView.load(URLRequest(url: magicLink))
    }

    // === THIS IS THE MOST IMPORTANT PART ===
    // This delegate method is called whenever the WebView decides to navigate.
    func webView(_ webView: WKWebView, decidePolicyFor navigationAction: WKNavigationAction, decisionHandler: @escaping (WKNavigationActionPolicy) -> Void) {
        if let urlString = navigationAction.request.url?.absoluteString, urlString.starts(with: redirectUrl) {
            // The flow is complete. Dismiss this view controller.
            self.dismiss(animated: true, completion: nil)
            decisionHandler(.cancel) // Stop the redirect from actually happening.
            return
        }
        decisionHandler(.allow) // Allow all other navigation.
    }
    
    // This delegate handles JavaScript UI, like permission requests.
    func webView(_ webView: WKWebView, requestMediaCapturePermissionFor origin: WKSecurityOrigin, initiatedByFrame frame: WKFrameInfo, type: WKMediaCaptureType, decisionHandler: @escaping (WKPermissionDecision) -> Void) {
        // Automatically grant camera permission to provide a smoother experience.
        decisionHandler(.grant)
    }
}
```

**Step 3: Present the Controller (SwiftUI Example)**

From your main application view, present the `TrustSwiftlyWebViewController` as a sheet.

```swift
// Your main SwiftUI View
import SwiftUI

struct ContentView: View {
    @State private var showVerification = false
    // In a real app, this would be fetched from your backend.
    let magicLink = "YOUR_MAGIC_LINK_FROM_API"

    var body: some View {
        Button("Start Verification") {
            self.showVerification.toggle()
        }
        .sheet(isPresented: $showVerification) {
            // Bridge to the UIKit ViewController
            VerificationView(magicLink: URL(string: magicLink)!)
        }
    }
}

// A helper to wrap our UIViewController for use in SwiftUI
struct VerificationView: UIViewControllerRepresentable {
    let magicLink: URL

    func makeUIViewController(context: Context) -> some UIViewController {
        return TrustSwiftlyWebViewController(magicLink: magicLink)
    }

    func updateUIViewController(_ uiViewController: UIViewControllerType, context: Context) {}
}
```

***

### **Common Issues**

> ❗️Multiple signups
>
> If testing your app and creating multiple verify sessions you should clear the cookies and cache of WKWebView inbetween new user sessions. (Refer to [this guide](https://stackoverflow.com/questions/27105094/how-to-remove-cache-in-wkwebview))
>
> ```swift
> WKWebsiteDataStore.default().removeData(ofTypes: [WKWebsiteDataTypeDiskCache, WKWebsiteDataTypeMemoryCache], modifiedSince: Date(timeIntervalSince1970: 0), completionHandler:{ })
> ```
>
>
>
> ❗️Webkit Inline Media Playback
>
> Please ensure `allowsInlineMediaPlayback` is enabled when creating a webview on a webkit browser (mobile Safari). This defaults to false and the camera preview will incorrectly open as a fullscreen live broadcast.

> ❗Camera Configuration
>
> The WebView Flow requires access to the device camera. Please include the `NSCameraUsageDescription` key your app's `Info.plist` file as described in the [Apple Developer documentation](https://developer.apple.com/documentation/avfoundation/cameras_and_media_capture/requesting_authorization_for_media_capture_on_ios).

> ❗️Allow External Network Requests
>
> Trust Swiftly makes external network calls within the Inquiry Flow that need to be allowlisted for the flow to properly function. Certain frameworks such as [Cordova](https://cordova.apache.org/docs/en/11.x/guide/appdev/allowlist/index.html#network-request-allow-list) require such requests to be allow listed. Please include `*.trustswiftly.com/*` in such an allow list if needed

Make sure permissions are correctly set for your app bundle.

* Camera and Microphone Permission

<figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>
