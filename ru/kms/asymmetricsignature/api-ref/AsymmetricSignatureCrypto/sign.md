---
editable: false
sourcePath: en/_api-ref/kms/v1/asymmetricsignature/api-ref/AsymmetricSignatureCrypto/sign.md
---

# Key Management Service API, REST: AsymmetricSignatureCrypto.Sign

Signs data specified KMS key.

## HTTP request

```
POST https://{{ api-host-kms }}/kms/v1/asymmetricSignatureKeys/{keyId}:sign
```

## Path parameters

#|
||Field | Description ||
|| keyId | **string**

Required field. ID of the asymmetric KMS key to use for signature. ||
|#

## Body parameters {#yandex.cloud.kms.v1.asymmetricsignature.AsymmetricSignRequest}

```json
{
  "message": "string"
}
```

#|
||Field | Description ||
|| message | **string** (bytes)

Required field. Message to sign.
Should be encoded with base64. ||
|#

## Response {#yandex.cloud.kms.v1.asymmetricsignature.AsymmetricSignResponse}

**HTTP Code: 200 - OK**

```json
{
  "keyId": "string",
  "signature": "string"
}
```

#|
||Field | Description ||
|| keyId | **string**

ID of the asymmetric KMS key that was used for signature. ||
|| signature | **string** (bytes)

Value of signature.
Signature value is produced in accordance with RFC 8017 for RSA
and is a DER-encoded object as defined by ANSI X9.62-2005 and RFC 3279 Section 2.2.3 for ECDSA. ||
|#