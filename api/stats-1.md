---
description: >-
  Create verification jobs through the API to analyze identities without going
  through Trust Swiftly's UI. Use the document status API to retrieve the
  results.
---

# Documents

The documents endpoint is useful for customers looking to control the branding experience or have asynchronous tasks to verify an identity. Use the below API to create a job to verify an ID document such as a DL or Passport. Ensure you have a template and workflow setup for the document to verify.

## Create Document Verification Job

<mark style="color:green;">`POST`</mark>`https://{sub-domain}.trustswiftly.com/api/verify/document`

#### Request Header

<table><thead><tr><th width="169">Name</th><th width="108">Type</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td>string</td><td><p><a href="../authentication.md"><strong>API Key</strong></a></p><p>is used for server-to-server communication to fetch sensitive data that you already have access to.</p></td></tr></tbody></table>

#### Multi-part Form Parameters

<table><thead><tr><th width="173">Name</th><th width="102">Type</th><th>Description</th></tr></thead><tbody><tr><td>template_id</td><td>string</td><td>The verification template id that has the single document workflow assigned to the user.</td></tr><tr><td>user_id</td><td>string</td><td>The user id of the user on Trust Swiftly.</td></tr><tr><td>verify_image</td><td>file</td><td>Full local path of image to analyze (JPG, PNG, PDF formats)</td></tr></tbody></table>

_\*Make sure the user is already created with the template\_id assigned to them._

{% tabs %}
{% tab title="200 " %}
```json
{
    "success": true,
    "doc_id": "313237"
}
```
{% endtab %}

{% tab title="Failure" %}
{

&#x20;  'error\_type' => 'api\_template\_error',

&#x20;  'error\_message' => 'Invalid templateId provided.',

}

{

&#x20;  'error\_type' => 'api\_user\_error',

&#x20;  'error\_message' => 'User Not Found'

}
{% endtab %}
{% endtabs %}



{% tabs %}
{% tab title="cURL" %}
```bash
curl --request POST \
  --url https://{sub-domain}.trustswiftly.com/api/verify/document \
  --header 'Authorization: Bearer {api_key}' \
  --header 'Content-Type: multipart/form-data' \
  --header 'User-Agent: insomnium/1.0' \
  --form template_id=tmpl_MTA \
  --form user_id=645 \
  --form 'verify_image=@C:\Users\123\photo5827714315489229223.jpg'
```
{% endtab %}
{% endtabs %}

## Get Status of Document Verification Job

The document status can be checked using polling via the below endpoint or can await a webhook for completion status. Typically, response times require a few seconds to analyze the document.&#x20;

<mark style="color:green;">`POST`</mark>`https://{sub-domain}.trustswiftly.com/api/verify/document/status`

#### Request Header

<table><thead><tr><th width="169">Name</th><th width="108">Type</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td>string</td><td><p><a href="../authentication.md"><strong>API Key</strong></a></p><p>is used for server-to-server communication to fetch sensitive data that you already have access to.</p></td></tr></tbody></table>

#### Request Body JSON

<table><thead><tr><th width="203">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td>doc_id</td><td>string</td><td>The doc_id from the original request to verify an image.</td></tr><tr><td>user_id</td><td>string</td><td>The user id of the user on Trust Swiftly from the original request.</td></tr></tbody></table>

{% tabs %}
{% tab title="200 " %}
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
{% endtab %}

{% tab title="Failure" %}
{

&#x20;  "error\_type": "invalid\_document\_id",

&#x20;  "error\_message": "Invalid Document Id"

}

{ "success": false, "doc\_id": "31323930", "document\_status": "Failed", "reason": null }
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --request POST \
  --url https://{sub-domain}.trustswiftly.com/api/verify/document/status \
  --header 'Authorization: Bearer {api_key}' \
  --header 'Content-Type: application/json' \
  --header 'User-Agent: insomnium/1.0' \
  --data '{
  "doc_id": "31323930",
  "user_id": "645"
}'
```
{% endtab %}
{% endtabs %}
