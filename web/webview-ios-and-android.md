---
description: >-
  The WebView option allows individuals to verify their identity in a mobile app
  with the Android WebView or iOS WKWebView.
---

# WebView iOS and Android

### Android Webview

To launch the WebView, create a `WebView` and pass in the path specified in the magic user link

```java
// inside Activity#onCreate
// assuming some WebView called "webView"
WebSettings settings = webView.getSettings();
settings.setDomStorageEnabled(true);
settings.setJavaScriptEnabled(true);
settings.setMediaPlaybackRequiresUserGesture(false);

final Uri trustswiftlyUrl = new Uri.Builder()
    .scheme("https")
    .encodedAuthority("<COMPANY_URL>.trustswiftly.com")
    .path("<MAGIC_URL_PATH>")
    .appendQueryParameter("is-webview", "true")
    .build();
```

In addition to adding to the Manifest file, you'll need to override onPermissionRequest and onShowFileChooser depending on your use case. See an example below.

```java
// set fields on your Activity
public static final int INPUT_FILE_REQUEST_CODE = 1;
private static final int CAMERA_PERMISSION_REQUEST = 1111;
private PermissionRequest cameraPermission;
private ValueCallback<Uri[]> filePathCallback;
private String cameraPhotoPath;

@Override
public void onActivityResult(int requestCode, int resultCode, Intent data) {
  if (requestCode != INPUT_FILE_REQUEST_CODE || filePathCallback == null) {
    super.onActivityResult(requestCode, resultCode, data);
    return;
  }

  Uri[] results = null;

  // Check that the response is a good one
  if (resultCode == Activity.RESULT_OK) {
    if (data == null) {
      // If there is not data, then we may have taken a photo
      if (cameraPhotoPath != null) {
        results = new Uri[] { Uri.parse(cameraPhotoPath) };
      }
    } else {
      String dataString = data.getDataString();
      if (dataString != null) {
        results = new Uri[] { Uri.parse(dataString) };
      }
    }
  }

  filePathCallback.onReceiveValue(results);
  filePathCallback = null;
}

// in the Activity#onCreate method
webView.setWebChromeClient(new WebChromeClient() {
  @Override
  public void onPermissionRequest(final PermissionRequest request) {
    if (request.getOrigin().toString().equals("https://<COMPANY_URL>.trustswiftly.com/")) {
      ActivityCompat.requestPermissions(MainActivity.this,
          new String[] { Manifest.permission.CAMERA }, CAMERA_PERMISSION_REQUEST);
      cameraPermission = request;
    } else {
      request.deny();
    }
  }
  
  @Override
  public boolean onShowFileChooser(
    WebView webView, ValueCallback<Uri[]> newFilePathCallback,
    FileChooserParams fileChooserParams) {

    if (filePathCallback != null) {
      filePathCallback.onReceiveValue(null);
    }
    filePathCallback = newFilePathCallback;

    Intent takePictureIntent = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);
    if (takePictureIntent.resolveActivity(getPackageManager()) != null) {
      // Create the File where the photo should go
      File photoFile = null;
      // Create an image file name
      String timeStamp = new SimpleDateFormat("yyyyMMdd_HHmmss", Locale.US).format(new Date());
      String imageFileName = "JPEG_" + timeStamp + "_";
      File storageDir =
        Environment.getExternalStoragePublicDirectory(Environment.DIRECTORY_PICTURES);
      try {
        photoFile = File.createTempFile(imageFileName, ".jpg", storageDir);
      } catch (IOException ex) {
        // Error occurred while creating the File
      }

      // Continue only if the File was successfully created
      if (photoFile != null) {
        cameraPhotoPath = "file:" + photoFile.getAbsolutePath();
        takePictureIntent.putExtra(MediaStore.EXTRA_OUTPUT,
                                   Uri.fromFile(photoFile));
      } else {
        takePictureIntent = null;
      }
    }

    Intent contentSelectionIntent = new Intent(Intent.ACTION_GET_CONTENT);
    contentSelectionIntent.addCategory(Intent.CATEGORY_OPENABLE);
    contentSelectionIntent.setType("image/*");

    Intent[] intentArray;
    if (takePictureIntent != null) {
      intentArray = new Intent[] { takePictureIntent };
    } else {
      intentArray = new Intent[0];
    }

    Intent chooserIntent = new Intent(Intent.ACTION_CHOOSER);
    chooserIntent.putExtra(Intent.EXTRA_INTENT, contentSelectionIntent);
    chooserIntent.putExtra(Intent.EXTRA_TITLE, "Image Chooser");
    chooserIntent.putExtra(Intent.EXTRA_INITIAL_INTENTS, intentArray);

    startActivityForResult(chooserIntent, INPUT_FILE_REQUEST_CODE);

    return true;
  }
});

// overwriting your AppCompatActivity's #onRequestPermissionsResult
@Override
public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions,
    @NonNull int[] grantResults) {
  super.onRequestPermissionsResult(requestCode, permissions, grantResults);
  if (requestCode == CAMERA_PERMISSION_REQUEST) {
    if (grantResults[0] == PackageManager.PERMISSION_GRANTED) {
      cameraPermission.grant(cameraPermission.getResources());
    } else {
      cameraPermission.deny();
    }
  }
}
```

**Permissions**

Be sure to add the required permissions for your use case to your AndroidManifest file. For example:

<pre><code>&#x3C;uses-permission android:name="android.permission.CAMERA" />

<strong>&#x3C;!-- Microphone permissions are not usually required, except when using a verify method that records video. -->
</strong>&#x3C;!--  &#x3C;uses-permission android:name="android.permission.RECORD_AUDIO" />-->
&#x3C;!--  &#x3C;uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />-->
</code></pre>

### iOS WKWebView

To use WKWebView to launch the magic link flow from a UIViewController

```swift
import SwiftUI
import WebKit

struct ContentView: View {
    @State var magic_link=""
    @State private var showWebView = false

    var body: some View {
        VStack {
            Form{
                Section(){
                    TextField("Magic Link",text:
                                $magic_link)
                }
                Section(){
                    Button(action:{
                        self.showWebView.toggle()
                    }){
                        Text("Open Magic Link")
                            
                    }.sheet(isPresented: $showWebView){
                        WebView(url: URL(string:self.magic_link)!)
                    }
                }
            }
        }
        .padding()
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}

struct WebView : UIViewRepresentable{
    var url: URL
    func makeUIView(context: Context) -> WKWebView {
        let webConfiguration = WKWebViewConfiguration()
        webConfiguration.allowsInlineMediaPlayback=true
        webConfiguration.mediaTypesRequiringUserActionForPlayback=[]
        return WKWebView(frame:.zero, configuration: webConfiguration)
    }
    func updateUIView(_ webView: WKWebView, context: Context) {
        let request = URLRequest(url: url)
        webView.load(request)
    }
}

```

**Permissions**

The webcam access can auto be allowed as seen in this Apple Demo and code. [https://stackoverflow.com/questions/75310858/browser-also-asks-camera-permission-in-ios-webview](https://stackoverflow.com/questions/75310858/browser-also-asks-camera-permission-in-ios-webview)

```swift
import WebKit

@available(iOS 15.0, *)
public class TrustSwiftlyWebViewDelegate: NSObject, WKUIDelegate {
	public func webView(
		_ webView: WKWebView,
		requestMediaCapturePermissionFor origin: WKSecurityOrigin,
		initiatedByFrame frame: WKFrameInfo,
		type: WKMediaCaptureType,
		decisionHandler: @escaping (WKPermissionDecision) -> Void
	) {
		decisionHandler(.grant)
	}
}
```

**Common Issues**

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
> The WebView Flow requires access to the device camera. Please include the `NSCameraUsageDescription` key your app's `Info.plist` file as described in the [Apple Developer documentation](https://developer.apple.com/documentation/avfoundation/cameras\_and\_media\_capture/requesting\_authorization\_for\_media\_capture\_on\_ios).

> ❗️Allow External Network Requests
>
> Trust Swiftly makes external network calls within the Inquiry Flow that need to be allowlisted for the flow to properly function. Certain frameworks such as [Cordova](https://cordova.apache.org/docs/en/11.x/guide/appdev/allowlist/index.html#network-request-allow-list) require such requests to be allow listed. Please include `*.trustswiftly.com/*` in such an allow list if needed
