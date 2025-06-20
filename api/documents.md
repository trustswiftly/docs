---
description: >-
  Create verification jobs through the API to analyze identities without going
  through Trust Swiftly's UI. Use the document status API to retrieve the
  results.
---

# Documents

#### Direct Document Verification API

This API is for advanced use cases where you need to programmatically submit an identity document (e.g., a driver's license or passport) for analysis. This allows you to build your own document collection UI while still using Trust Swiftly's powerful verification engine on the backend.

{% hint style="danger" %}
**Warning: Advanced Use Only**\
By using this API, you are responsible for building your own secure document collection method. You may miss out on important security features and data collection checks provided by Trust Swiftly's hosted UI. We recommend our standard, hosted solution for the most secure and seamless experience.
{% endhint %}

***

#### How It Works: An Asynchronous Flow

Document verification is not instantaneous. The process is asynchronous and follows these steps:

1. **Prerequisite:** Ensure a user exists in Trust Swiftly and is assigned to a **Verification Template** that is configured for a single document check.
2. **Step 1: Create a Verification Job.** You upload the document image via a `multipart/form-data` request. The API accepts the job and immediately returns a unique `doc_id`.
3. **Step 2: Poll for Status.** You use the `doc_id` to periodically call the status endpoint. This endpoint will initially show a "processing" status.
4. **Step 3: Receive Results.** After a few seconds, the status endpoint will return a "Success" or "Failure" status, along with the complete analysis data. Alternatively, you can listen for a webhook to be notified of completion.

***

#### Prerequisite: Assign a Template to a User

Before you can submit a document for a user, that user must already exist in Trust Swiftly and be assigned to the correct **Verification Template**. This template tells our system what rules to apply to the document check.

You can do this by calling the Create User or Update User endpoint and providing the appropriate `template_id`.

***

#### Step 1: Create Document Verification Job

This endpoint accepts a document image and queues it for analysis.

<mark style="color:green;">`POST`</mark>`https://{sub-domain}.trustswiftly.com/api/verify/document`

**Request (multipart/form-data)**

<table><thead><tr><th width="147.33331298828125">Parameter</th><th width="97">Type</th><th width="94.333251953125">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>user_id</code></td><td>string</td><td>Yes</td><td>The user ID from Trust Swiftly (e.g., <code>645</code>).</td></tr><tr><td><code>template_id</code></td><td>string</td><td>Yes</td><td>The ID of the template assigned to the user (e.g., <code>tmpl_MTA</code>).</td></tr><tr><td><code>verify_image</code></td><td>file</td><td>Yes</td><td>The document image file (JPG, PNG, PDF). Must be less than 10MB.</td></tr></tbody></table>

**Example `cURL` Request**

**Note:** The `@` symbol before the file path tells `cURL` to upload the contents of the file.

```bash
curl --request POST \
  --url https://{sub-domain}.trustswiftly.com/api/verify/document \
  --header 'Authorization: Bearer YOUR_API_KEY' \
  --header 'Content-Type: multipart/form-data' \
  --form 'user_id=645' \
  --form 'template_id=tmpl_MTA' \
  --form 'verify_image=@/path/to/your/drivers_license.jpg'
```

**Success Response**

A successful request returns a `200 OK` status and the `doc_id` for your new verification job. You must store this ID to check the status in the next step.

```json
{
    "success": true,
    "doc_id": "313237"
}
```

***

#### Step 2: Get Status of Document Verification Job

After waiting a few seconds, begin polling this endpoint with the `doc_id` from Step 1 to check the job status and retrieve the results once complete.

<mark style="color:green;">`POST`</mark>` ``https://{sub-domain}.trustswiftly.com/api/verify/document/status`

**Request (application/json)**

<table><thead><tr><th width="128.3333740234375">Parameter</th><th width="90.6666259765625">Type</th><th width="92">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>user_id</code></td><td>string</td><td>Yes</td><td>The user ID from the original request.</td></tr><tr><td><code>doc_id</code></td><td>string</td><td>Yes</td><td>The document ID received from the job creation endpoint.</td></tr></tbody></table>

**Example `cURL` Request**

```bash
curl --request POST \
  --url https://{sub-domain}.trustswiftly.com/api/verify/document/status \
  --header 'Authorization: Bearer YOUR_API_KEY' \
  --header 'Content-Type: application/json' \
  --data '{
    "doc_id": "313237",
    "user_id": "645"
  }'
```

**Success Response**

When processing is complete, the `document_status` field will change from a processing state to `Success` or a failure state. The full extraction and analysis data is contained within the `document_data` object.

```json
{
  "success": true,
  "doc_id": "31323933",
  "document_status": "Success",
  "document_data": { ... }
}
```

***

#### Failure Response

```json
{
   "error_type": "invalid_document_id",
   "error_message": "Invalid Document Id"
}

Fail 2
{ "success": false, "doc_id": "31323930",
 "document_status": "Failed", "reason": null }
```

#### Understanding the `document_data` Object

The `document_data` object contains a rich set of information. Here are the key sections:

<details>

<summary><strong>Full Response Success (Click to expand)</strong></summary>

```json
{
  "success": true,
  "doc_id": "31323933",
  "document_status": "Success",
  "document_data": {
    "id": 1293,
    "name": "11/example@gmail.com_#11.jpg",
    "status": 1,
    "content": {
      "url": "https://sub-domain.trustswiftly.com/image/11?expires=11&signature=11",
      "hash": "a1efcda2122a20dda6d9ea89be9c62ac",
      "name": "11/example@gmail.com_#11.jpg",
      "size": 218545,
      "time": 1726768308,
      "type": "image/jpeg",
      "doc_type": "General process",
      "mrz_data": [],
      "exif_data": [],
      "extension": "jpg",
      "ai_analysis": {
        "name_match": {
          "full_name": false,
          "last_name": false
        },
        "selfie_check": true,
        "internet_detection": false,
        "internet_detection_location": {
          "guess_labels": [
            "document"
          ]
        }
      },
      "doc_type_id": 23,
      "dlp_analysis": {
        "info_types": [
          {
            "name": "US_STATE",
            "quote": "***",
            "likelihood": "VERY_LIKELY"
          },
          {
            "name": "US_DRIVERS_LICENSE_NUMBER",
            "quote": "***",
            "likelihood": "LIKELY"
          },
          {
            "name": "CREDIT_CARD_NUMBER",
            "quote": "***",
            "likelihood": "POSSIBLE"
          },
          {
            "name": "DATE",
            "quote": "08-29-1911",
            "likelihood": "LIKELY"
          },
          {
            "name": "DATE_OF_BIRTH",
            "quote": "08-29-1911",
            "likelihood": "LIKELY"
          },
          {
            "name": "PERSON_NAME",
            "quote": "Joe CHAMI",
            "likelihood": "LIKELY"
          },
          {
            "name": "FIRST_NAME",
            "quote": "Joe",
            "likelihood": "LIKELY"
          },
          {
            "name": "LAST_NAME",
            "quote": "CHAMI",
            "likelihood": "LIKELY"
          },
          {
            "name": "PERSON_NAME",
            "quote": "PAYNE",
            "likelihood": "LIKELY"
          },
          {
            "name": "LAST_NAME",
            "quote": "PAYNE",
            "likelihood": "LIKELY"
          },
          {
            "name": "STREET_ADDRESS",
            "quote": "111 PAYNE AVE EXAMPLE,MI 12345-1111",
            "likelihood": "LIKELY"
          },
          {
            "name": "DATE",
            "quote": "09-01-2017",
            "likelihood": "LIKELY"
          },
          {
            "name": "DATE",
            "quote": "08-29-2021",
            "likelihood": "LIKELY"
          },
          {
            "name": "DATE",
            "quote": "01-21-2011",
            "likelihood": "LIKELY"
          },
          {
            "name": "GENDER",
            "quote": "***",
            "likelihood": "POSSIBLE"
          }
        ]
      },
      "photoshopped": false,
      "original_name": "photo5827714315489229223_rotated.jpg",
      "valid_address": [],
      "dl_id_lookup_id": "",
      "face_annotation": {
        "joyLikelihood": "VERY_UNLIKELY",
        "angerLikelihood": "VERY_UNLIKELY",
        "sorrowLikelihood": "VERY_UNLIKELY",
        "blurredLikelihood": "VERY_UNLIKELY",
        "headwearLikelihood": "VERY_UNLIKELY",
        "surpriseLikelihood": "VERY_UNLIKELY",
        "underExposedLikelihood": "VERY_UNLIKELY"
      },
      "dl_id_lookup_data": "",
      "temporary_storage": "oss",
      "document_processor": {
        "Sex": {
          "value": "M",
          "confidence": 100
        },
        "age": {
          "value": 50,
          "confidence": 100
        },
        "Height": {
          "value": "170 cm",
          "confidence": 100
        },
        "Status": {
          "value": "Ok",
          "confidence": 100
        },
        "Address": {
          "value": "123 PAYNE AVE,EXAMPLE, MI 12345-1111",
          "confidence": 100
        },
        "DL Class": {
          "value": "O",
          "confidence": 100
        },
        "Position": {
          "value": {
            "x1": -3,
            "x2": 696,
            "y1": 11,
            "y2": 1034
          },
          "confidence": 100
        },
        "Full Name": {
          "value": "Joe CHAMI",
          "confidence": 100
        },
        "Eyes Color": {
          "value": "Brown",
          "confidence": 100
        },
        "DL Endorsed": {
          "value": "NONE",
          "confidence": 100
        },
        "countryName": {
          "value": "United States",
          "confidence": 100
        },
        "Address City": {
          "value": "EXAMPLE",
          "confidence": 100
        },
        "documentName": {
          "value": "Driver Licence",
          "confidence": 100
        },
        "Address State": {
          "value": "Michigan",
          "confidence": 100
        },
        "Date of Birth": {
          "value": "1911-08-29",
          "confidence": 100
        },
        "Date of Issue": {
          "value": "2012-09-01",
          "confidence": 100
        },
        "Document Name": {
          "value": "United States-Driver Licence",
          "confidence": 100
        },
        "Revision Date": {
          "value": "2011-01-11",
          "confidence": 100
        },
        "Address Street": {
          "value": "123 PAYNE AVE",
          "confidence": 100
        },
        "Date of Expiry": {
          "value": "2050-08-29",
          "confidence": 100
        },
        "Document Number": {
          "value": "111",
          "confidence": 100
        },
        "Portrait Position": {
          "value": {
            "x1": 26,
            "x2": 283,
            "y1": 167,
            "y2": 509
          },
          "confidence": 100
        },
        "Issuing State Code": {
          "value": "USA",
          "confidence": 100
        },
        "Issuing State Name": {
          "value": "United States",
          "confidence": 100
        },
        "Address Postal Code": {
          "value": "12345-1111",
          "confidence": 100
        },
        "DL Restriction Code": {
          "value": "NONE",
          "confidence": 100
        },
        "Document Discriminator": {
          "value": "11",
          "confidence": 100
        },
        "Address Jurisdiction Code": {
          "value": "MI",
          "confidence": 100
        }
      },
      "valid_user_address": []
    },
    "created_at": "2024-09-19T17:51:46.000000Z"
  }
}
```

</details>

<details>

<summary><strong>`document_processor` (Click to expand)</strong></summary>

This object contains the core data extracted from the document via Optical Character Recognition (OCR), such as name, date of birth, address, and document numbers, along with a confidence score for each field.

</details>

<details>

<summary><strong>`ai_analysis` (Click to expand)</strong></summary>

This provides signals about the authenticity of the document image itself, including checks for whether it's a picture of a screen (\`internet\_detection\`) or if it matches a known selfie (\`selfie\_check\`).

</details>

<details>

<summary><strong>`dlp_analysis` (Click to expand)</strong></summary>

This provides Data Loss Prevention (DLP) analysis, identifying all types of Personally Identifiable Information (PII) found in the document, such as names, addresses, and dates.

</details>

<details>

<summary><strong>`face_annotation` (Click to expand)</strong></summary>

If a face is present on the document, this provides analysis of the facial attributes, such as the likelihood of headwear or if the image is blurred.

</details>

