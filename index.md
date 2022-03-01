# 1saas Migration V1 to V2

- [1saas Migration V1 to V2](#1saas-migration-v1-to-v2)
- [1. Important Changes between 1saas V1 and V2](#1-important-changes-between-1saas-v1-and-v2)
  - [1.1. AI](#11-ai)
    - [1.1.1. Lang](#111-lang)
    - [1.1.2. Mood](#112-mood)
    - [1.1.3. translate](#113-translate)
    - [1.1.4. picture text recognition](#114-picture-text-recognition)
    - [1.1.5. picture object recognition](#115-picture-object-recognition)
    - [1.1.6. entity detection](#116-entity-detection)
  - [1.2. Files](#12-files)
    - [1.2.1. PDF Merger](#121-pdf-merger)
    - [1.2.2. HTML to PDF](#122-html-to-pdf)
    - [1.2.3. Split PDF](#123-split-pdf)
    - [1.2.4. Count PDF pages](#124-count-pdf-pages)
  - [1.3. Scheduler](#13-scheduler)
    - [1.3.1. add](#131-add)
    - [1.3.2. del](#132-del)
    - [1.3.3. list](#133-list)
  - [1.4. Python](#14-python)
  - [1.5. JavaScript](#15-javascript)
  - [1.6. QR](#16-qr)
  - [1.7. VAT Checker](#17-vat-checker)
  - [1.8. Crypto](#18-crypto)
    - [1.8.1. Encrypt](#181-encrypt)
    - [1.8.2. Decrypt](#182-decrypt)
    - [1.8.3. Hash](#183-hash)
  - [1.9. Gender detection](#19-gender-detection)
  - [1.10. Advanced Switch](#110-advanced-switch)
  - [1.11. BMI Calculator](#111-bmi-calculator)
  - [1.12. Random String](#112-random-string)
  - [1.13. Random Name](#113-random-name)
  - [1.14. Random City](#114-random-city)
  - [1.15. Random Picture](#115-random-picture)
  - [1.16. IP to geo](#116-ip-to-geo)
  - [1.17. Email Validator](#117-email-validator)
  - [1.14. URL shortener](#114-url-shortener)
    - [1.14.1. add](#1141-add)
    - [1.14.2. del](#1142-del)
    - [1.14.3. get](#1143-get)
    - [1.14.4. list](#1144-list)
    - [1.14.5. put](#1145-put)
- [2. New Features in V2](#2-new-features-in-v2)
  - [2.1. Business -> Validate](#21-business---validate)
    - [2.1.1 BIC](#211-bic)
    - [2.1.2 IBAN](#212-iban)
    - [2.1.3 VAT](#213-vat)

# 1. Important Changes between 1saas V1 and V2

## 1.1. AI

---

### 1.1.1. Lang

**V1**

> URL: https://api.1saas.co/v1/lang

Response body:

```json
{
  "languageResult": [
    {
      "id": "0",
      "warnings": [],
      "primaryLanguage": {
        "name": "Danish",
        "iso6391Name": "da",
        "confidenceScore": 1
      }
    }
  ]
}
```

**V2**

> URL: https://v2.1saas.co/ai/languagedetection

Response body:

```json
{
  "name": "English",
  "iso6391Name": "en",
  "confidenceScore": 1
}
```

---

### 1.1.2. Mood

**V1**

> URL: https://api.1saas.co/v1/mood

Response body:

```json
{
  "sentimentResult": [
    {
      "id": "0",
      "warnings": [],
      "sentiment": "mixed",
      "confidenceScores": {
        "positive": 0.5,
        "neutral": 0,
        "negative": 0.5
      },
      "sentences": [
        {
          "confidenceScores": {
            "positive": 0,
            "neutral": 0,
            "negative": 1
          },
          "sentiment": "negative",
          "text": "THIS IS A VERY NEGATIVE TEXT.",
          "offset": 0,
          "length": 29,
          "opinions": []
        },
        {
          "confidenceScores": {
            "positive": 0.99,
            "neutral": 0.01,
            "negative": 0
          },
          "sentiment": "positive",
          "text": "Good things are happening around the world.",
          "offset": 30,
          "length": 43,
          "opinions": []
        }
      ]
    }
  ]
}
```

**V2**

> URL: https://v2.1saas.co/ai/mooddetection

Response body:

```json
{
  "moodOverall": "mixed",
  "moodScore": {
    "positive": 0.5,
    "neutral": 0,
    "negative": 0.5
  },
  "moodPerSentence": [
    {
      "mood": "negative",
      "text": "THIS IS A VERY NEGATIVE TEXT."
    },
    {
      "mood": "positive",
      "text": "Good things are happening around the world."
    }
  ]
}
```

---

### 1.1.3. translate

**V1**

> URL: https://api.1saas.co/v1/tanslate

Response body:

```json
{
  "translations": ["Hello we are wemakefuture. We are here for you!"]
}
```

**V2**

> URL: https://v2.1saas.co/ai/translate

Response body:

```json
{
  "translation": "Hello we are wemakefuture. We are here for you!"
}
```

---

### 1.1.4. picture text recognition

**V1**

> URL: https://api.1saas.co/v1/ocr

Response body:

```json
{
  "detection": "How do functions\nbreak up?\nThey stop calling\neach other!\n"
}
```

**V2**

> URL: https://v2.1saas.co/ai/picturetextrecognition

Response body:

```json
{
  "recognizedTexts": [
    "How do functions break up?",
    "They stop calling each other! "
  ]
}
```

---

### 1.1.5. picture object recognition

**V1**

> URL: https://api.1saas.co/v1/pic

Response body:

```json
{
  "concepts": [
    {
      "id": "ai_GjVpxXrs",
      "name": "street",
      "value": 0.9886825084686279,
      "created_at": null,
      "language": "",
      "app_id": "main",
      "definition": "",
      "vocab_id": "",
      "visibility": null,
      "user_id": ""
    },
    ...
  ]
}
```

**V2**

> URL: https://v2.1saas.co/ai/pictureobjectrecognition

Response body:

```json
{
  "recognizedLabels": [
    "Tire",
    "Bicycle",
    "Wheel",
    "Automotive lighting",
    "Infrastructure",
    "Building",
    "Bicycle wheel",
    "Mode of transport",
    "Vehicle",
    "Electricity"
  ]
}
```

---

### 1.1.6. entity detection

**V1**

> URL: https://api.1saas.co/v1/entity

Response body:

```json
{
  "result": [
    {
      "text": "Now",
      "category": "DateTime",
      "offset": 0,
      "length": 3,
      "confidenceScore": 0.8
    },
    ...
  ]
}
```

**V2**

> URL: https://v2.1saas.co/ai/entityDetection

Response body:

```json
{
  "detections": [
    {
      "text": "Now",
      "category": "DateTime",
      "offset": 0,
      "length": 3,
      "confidenceScore": 0.8
    },
    ...
  ]
}
```

---

## 1.2. Files

### 1.2.1. PDF Merger

**V1**

> URL: https://api.1saas.co/v1/pdfmerger

**V2**

> URL: https://v2.1saas.co/pdf/merge

> The pages value in the files object now only accepts a string with a page range like "1-3" or "18-27" and a array of numbers like [1, 3, 15, 21, 31]. For clearer understanding: Here are the defined types:

```typescript
type FileProperties = {
  buffer?: Buffer;
  url?: string;
  pages: number[] | string;
};
```

```typescript
type Request body = {
  files: FileProperties[];
  getAsUrl?: boolean;
};
```

---

### 1.2.2. HTML to PDF

**V1**

> URL: https://api.1saas.co/v1/htmltopdf

**V2**

> URL: https://v2.1saas.co/pdf/html

---

### 1.2.3. Split PDF

**V1**

> URL: https://api.1saas.co/v1/splitpdf

**V2**

> URL: https://v2.1saas.co/pdf/split

---

### 1.2.4. Count PDF pages

**V1**

> URL: https://api.1saas.co/v1/py

**V2**

> URL: https://v2.1saas.co/pdf/count

---

## 1.3. Scheduler

The scheduler was splitted in multiple subfunctions: add, delete, list

**V1**

> URL: https://api.1saas.co/v1/scheduler

**V2**

### 1.3.1. add

> URL: https://v2.1saas.co/operator/scheduler/add

Request body:

```json
{
  "sendToWebhook": "https://hook.integromat.com/aafqn1jltvr5gfgthvok0rcrs8u9xuo8",
  "data": "{\"message\":{\"key\": \"value\"}}",
  "intervalOptions": ["1639220471"],
  "intervalType": 1
}
```

Response body:

```json
{
  "taskId": "TY3wX8R3QGCkTYh",
  "nextExecution": "2021-12-11T11:01:11.000Z"
}
```

### 1.3.2. del

> URL: https://v2.1saas.co/operator/scheduler/del

Request body:

```json
{
  "taskId": "TY3wX8R3QGCkTYh"
}
```

Response body:

```json
{
  "message": "Task with ID TY3wX8R3QGCkTYh was successfully deleted!"
}
```

### 1.3.3. list

> URL: https://v2.1saas.co/operator/scheduler/list

Response body:

```json
{
  "tasks": [
    {
      "taskId": "3SDc5N4aWT1065z",
      "webhook": "https://hook.integromat.com/aafqn1jltvr5gfgthvok0rcrs8u9xuo8",
      "nextExecution": "2022-04-01T07:26:15.000Z"
    }
  ]
}
```

---

## 1.4. Python

**V1**

> URL: https://api.1saas.co/v1/py

**V2**

> URL: https://v2.1saas.co/code/javascript

---

## 1.5. JavaScript

**V1**

> URL: https://api.1saas.co/v1/js

**V2**

> URL: https://v2.1saas.co/code/javascript

---

## 1.6. QR

**V1**

> URL: https://api.1saas.co/v1/qr

**V2**

QR Code got a small rework and is now splitted into encode and decode

> encode URL: https://v2.1saas.co/generate/qrcode/encode

Request body:

```json
{
  "data": "Let's put this data into a verrrrrry fancy QR code!"
}
```

Response body:

```json
{
  "imageUrl": "URL to Image"
}
```

> decode URL: https://v2.1saas.co/generate/qrcode/decode

Request body URL:

```json
{
  "url": "https://www.thedrinksbusiness.com/content/uploads/2012/05/sample-1024x1024.png"
}
```

Request body Buffer:

```json
{
  "buffer": "BUFFER"
}
```

Response body:

```json
{
  "data": "http://www.qrstuff.com/"
}
```

---

## 1.7. VAT Checker

**V1**

> URL: https://api.1saas.co/v1/vatcheck

Request body:

```json
{
  "vatID": "IE98765343"
}
```

Response body:

```json
{
  "result": {
    "countryCode": "IE",
    "vatNumber": "98765343",
    "Request bodyDate": "2022-02-25+01:00",
    "valid": false,
    "name": "---",
    "address": "---"
  }
}
```

**V2**

> URL: https://v2.1saas.co/business/validate/vat

Request body:

```json
{
  "id": "323734163",
  "countryCode": "DE"
}
```

Response body:

```json
{
  "countryCode": "DE",
  "vatNumber": "323734163",
  "Request bodyDate": "2022-02-25+01:00",
  "valid": true,
  "name": "---",
  "address": "---"
}
```

## 1.8. Crypto

**V1**

> URL: https://api.1saas.co/v1/crypto

**V2**

Crypto got splitted into multiple endpoints as well

### 1.8.1. Encrypt

> URL: https://v2.1saas.co/crypto/encrypt

Request body:

```json
{
  "message": "Hello, it's me Tim",
  "secretKey": "supersecretkey",
  "cryptoType": "AES"
}
```

Response body:

```json
{
  "encryptedText": "U2FsdGVkX1+ZDpSZgb+PJWvuginAA/qSd4Gzl/6pMqbILhoIpEj9aVHh+8iiyE0T"
}
```

### 1.8.2. Decrypt

> URL: https://v2.1saas.co/crypto/encrypt

Request body:

```json
{
  "ciphertext": "U2FsdGVkX19SFwdVBSgXVn35yS15Bb/9bzsoN9+nA8RsJobUCZi7zdxaXh48cIxi",
  "secretKey": "supersecretkey",
  "cryptoType": "AES"
}
```

Response body:

```json
{
  "decryptedText": "Hello, it's me Tim"
}
```

### 1.8.3. Hash

> URL: https://v2.1saas.co/crypto/encrypt

Request body:

```json
{
  "message": "Kevin always throws a Yahtzee",
  "secretKey": "supersecretkey",
  "hashType": "SHA256"
}
```

Response body:

```json
{
  "hashedText": "4bc985c86d020715e8d2860cb745d2e2387857510c53b7b8bc1e0f7d49a8e01b"
}
```

---

## 1.9. Gender detection

**V1**

> URL: https://api.1saas.co/v1/gnd

**V2**

> URL: https://v2.1saas.co/operator/gender

---

## 1.10. Advanced Switch

**V1**

> URL: https://api.1saas.co/v1/asw

**V2**

> URL: https://v2.1saas.co/operator/advancedswitch

---

## 1.11. BMI Calculator

**V1**

> URL: https://api.1saas.co/v1/bmi

**V2**

> URL: https://v2.1saas.co/calculate/bmi

---

## 1.12. Random String

**V1**

> URL: https://api.1saas.co/v1/string

**V2**

Random string now accepts a total of 7 types as listed here:

| type    | string contains                  |
| ------- | -------------------------------- |
| no type | characters and numbers           |
| 1       | numbers                          |
| 2       | characters                       |
| 3       | characters lowercase             |
| 4       | characters uppercase             |
| 5       | characters lowercase and numbers |
| 6       | characters uppercase and numbers |
| 7       | hex                              |

> URL: https://v2.1saas.co/generate/string

Request body:

```json
{
  "type": 1,
  "length": 8
}
```

---

## 1.13. Random Name

**V1**

> URL: https://api.1saas.co/v1/name

**V2**

> URL: https://v2.1saas.co/generate/name

You can optionally provide a gender in the Request body body

Request body:

```json
{
  "gender": "female"
}
```

---

## 1.14. Random City

**V1**

> URL: https://api.1saas.co/v1/city

**V2**

> URL: https://v2.1saas.co/generate/city

---

## 1.15. Random Picture

**V1**

> URL: https://api.1saas.co/v1/randpic

**V2**

> URL: https://v2.1saas.co/generate/picture

---

## 1.16. IP to geo

**V1**

> URL: https://api.1saas.co/v1/iptogeo

**V2**

> URL: https://v2.1saas.co/convert/iptogeo

---

## 1.17. Email Validator

**V1**

> URL: https://api.1saas.co/v1/email

**V2**

> URL: https://v2.1saas.co/business/validate/email

---

## 1.14. URL shortener

**V1**

> URL: https://api.1saas.co/v1/url

**V2**

The URL shortener got reworked in V2 as well. It was splitted into the following functions:

- add
- del
- get
- list
- put

### 1.14.1. add

> URL: https://v2.1saas.co/generate/shortendurl/add

You can optionally provide a custom identifier in the Request body by adding a key "custom" to the request body. The identifier is used for updating or deleting you configured shortend urls.

Request body:

```json
{
  "destination": "https://1saas.co",
  "custom": "custom identifier"
}
```

Response body:

```json
{
  "identifier": "custom identifier"
}
```

---

### 1.14.2. del

> URL: https://v2.1saas.co/generate/shortendurl/del

Request body:

```json
{
  "identifier": "identifier-id"
}
```

Response body:

```json
{
  "message": "Successfully deleted shortend url with identifier-id"
}
```

---

### 1.14.3. get

> URL: https://v2.1saas.co/generate/shortendurl/del

Request body:

```json
{
  "identifier": "QLJbH9aw2YlmvSJ"
}
```

Response body:

```json
{
  "destination": "https://1saas.co"
}
```

---

### 1.14.4. list

> URL: https://v2.1saas.co/generate/shortendurl/del

Response body:

```json
{
  "shortenedUrls": [
    {
      "identifier": "yP20LhL1",
      "lastUsed": "2022-02-22T13:18:35.800Z",
      "destination": "https://1saas.co"
    }
  ]
}
```

---

### 1.14.5. put

Updates the destination of a existing shortend url.

> URL: https://v2.1saas.co/generate/shortendurl/put

Request body:

```json
{
  "destination": "https://lyzee.de",
  "identifier": "yP20LhL1"
}
```

Response body:

```json
{
  "shortenedUrls": [
    {
      "identifier": "yP20LhL1",
      "lastUsed": "2022-02-22T13:18:35.800Z",
      "destination": "https://1saas.co"
    }
  ]
}
```

---

# 2. New Features in V2

---

## 2.1. Business -> Validate

> Documentation: https://documenter.getpostman.com/view/18297710/UVkntwBv#b74a1723-a32b-46a3-bdb4-2557436dcf4f

### 2.1.1 BIC

> URL: https://v2.1saas.co/business/validate/bic

### 2.1.2 IBAN

> URL: https://v2.1saas.co/business/validate/iban

### 2.1.3 VAT

> URL: https://v2.1saas.co/business/validate/vat
