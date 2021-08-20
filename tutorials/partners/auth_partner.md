# Auth partner
Anyone who wants to provide Auth and eKYC services to the customers has to register as a partner in MOSIP


## Setup

### 1) Create policy group & policy
A MOSIP User with the following roles will create policy group and policies

ROLES:
* POLICYMANAGER (default for all)
* PARTNER_ADMIN (default for all)
* CREDENTIAL_ISSUANCE, CREATE_SHARE
```text
 (get partner policy {partnerId, policyId})
```
* PARTNER, AUTH_PARTNER, CREDENTIAL_PARTNER
```text
Get policy group list with filters & pagination
```
* PARTNER, AUTH_PARTNER, CREDENTIAL_PARTNER, CREDENTIAL_ISSUANCE
```text
Get policy list with filters & pagination
```
* PARTNER, PMS_USER, AUTH_PARTNER, CREDENTIAL_PARTNER
```text
policyGroupFilterValues
```
* PARTNER, PMS_USER, AUTH_PARTNER, CREDENTIAL_PARTNER
```text
PolicyFilterValues
```

1) Create policy group

POST - {{host}}/v1/policymanager/policies/group/new

Request:
```json
{
  "id": "string",
  "metadata": {},
  "request": {
    "desc": "PolicyGroup",
    "name": "Financial"
  },
  "requesttime": "{{requesttime}}",
  "version": "string"
}
```

Response:
```json
{
    "id": "string",
    "version": "string",
    "responsetime": "2021-08-20T07:26:12.247Z",
    "response": {
        "id": "468464",
        "name": "Financial",
        "desc": "PolicyGroup",
        "is_Active": true,
        "cr_by": "ganeshauth",
        "cr_dtimes": "2021-08-20T07:26:12.180568",
        "up_by": null,
        "upd_dtimes": null
    },
    "errors": []
}
```

2) Create policy

POST - {{host}}/v1/policymanager/policies

Request:
```json
{
  "id": "string",
  "metadata": {},
  "request": {
    "desc": "Auth Policy",
    "name": "policy {{$randomInt}}",
    "version" : "1.0",
    "policies": {
      "allowedAuthTypes": [
        {
          "authSubType": "IRIS",
          "authType": "bio",
          "mandatory": false
        },
        {
          "authSubType": "FINGER",
          "authType": "bio",
          "mandatory": false
        },
        {
          "authSubType": "FACE",
          "authType": "bio",
          "mandatory": false
        },
        {
          "authSubType": "",
          "authType": "otp",
          "mandatory": false
        },
        {
           "authSubType": "",
           "authType": "otp-request",
           "mandatory": false
        },       
        {
          "authSubType": "",
          "authType": "kyc",
          "mandatory": false
        },
        {
          "authSubType": "",
          "authType": "demo",
          "mandatory": false
        }         
      ],
      "allowedKycAttributes": [
        {
          "attributeName": "fullName"
        },
         {
          "attributeName": "gender"
        },
         {
          "attributeName": "residenceStatus"
        },
        {
          "attributeName": "dateOfBirth"
        },
        {
          "attributeName": "photo"
        }
      ],
     "authTokenType": "policy"      
    },
    "policyGroupName": "{{policygroupname}}",
    "policyType": "Auth"
  },
  "requesttime": "{{requesttime}}",
  "version": "string"
}
```

Response:
```json
{
    "id": "string",
    "version": "string",
    "responsetime": "2021-08-20T07:29:08.018Z",
    "response": {
        "id": "163457",
        "policyGroupName": "34",
        "name": "policy 702",
        "desc": "Auth Policy",
        "is_Active": false,
        "cr_by": "ganeshauth",
        "cr_dtimes": "2021-08-20T07:29:08.767+0000",
        "up_by": null,
        "upd_dtimes": null
    },
    "errors": []
}
```

3) Publish policy (Map policy and policy group)

POST - {{host}}/v1/policymanager/policies/{{policyID}}/group/{{policygroupID}}/publish

Response:
```json
{
    "id": null,
    "version": null,
    "responsetime": "2021-08-20T07:32:07.184Z",
    "response": {
        "policyGroupId": "468464",
        "policyGroupName": "34",
        "policyGroupDesc": "PolicyGroup",
        "policyGroupStatus": true,
        "policyGroup_cr_by": "ganeshauth",
        "policyGroup_cr_dtimes": "2021-08-20T07:26:12.180568",
        "policyGroup_up_by": null,
        "policyGroup_upd_dtimes": null,
        "policyId": "163457",
        "policyName": "policy 702",
        "policyDesc": "Auth Policy",
        "policyType": "Auth",
        "publishDate": "2021-08-20T07:29:08.767508",
        "validTill": "2022-02-16T07:32:07.254676",
        "status": "PUBLISHED",
        "version": "1.0",
        "schema": "https://schemas.mosip.io/v1/auth-policy",
        "is_Active": true,
        "cr_by": "ganeshauth",
        "cr_dtimes": "2021-08-20T07:29:08.767468",
        "up_by": "ganeshauth",
        "upd_dtimes": "2021-08-20T07:32:07.254684",
        "policies": {
            "authTokenType": "policy",
            "allowedKycAttributes": [
                {
                    "attributeName": "fullName"
                },
                {
                    "attributeName": "gender"
                },
                {
                    "attributeName": "residenceStatus"
                },
                {
                    "attributeName": "dateOfBirth"
                },
                {
                    "attributeName": "photo"
                }
            ],
            "allowedAuthTypes": [
                {
                    "authSubType": "IRIS",
                    "authType": "bio",
                    "mandatory": false
                },
                {
                    "authSubType": "FINGER",
                    "authType": "bio",
                    "mandatory": false
                },
                {
                    "authSubType": "FACE",
                    "authType": "bio",
                    "mandatory": false
                },
                {
                    "authSubType": "",
                    "authType": "otp",
                    "mandatory": false
                },
                {
                    "authSubType": "",
                    "authType": "otp-request",
                    "mandatory": false
                },
                {
                    "authSubType": "",
                    "authType": "kyc",
                    "mandatory": false
                },
                {
                    "authSubType": "",
                    "authType": "demo",
                    "mandatory": false
                }
            ]
        }
    },
    "errors": []
}
```

### 2) Partner registration

1) Partner self registration

ROLES:
* PARTNER
* PARTNER_ADMIN
* AUTH_PARTNER
* CREDENTIAL_PARTNER

POST - {{host}}/v1/partnermanager/partners

Request:
```json
{
  "id": "string",
  "metadata": {},
  "request": {
    "address": "testaddrd",
    "contactNumber": "9232121222",
    "emailId": "{{$unique}}",
    "organizationName": "{{PARTNERID}}",
    "partnerId": "{{$unique}}",
    "partnerType": "Auth_Partner",
    "policyGroup": "{{policygroupname}}"
  },
  "requesttime": "2021-08-20T07:49:33.043Z",
  "version": "string"
}
```

Response:
```json
{
    "id": "string",
    "version": "string",
    "responsetime": "2021-08-20T07:49:33.043Z",
    "metadata": null,
    "response": {
        "partnerId": "499",
        "status": "InProgress"
    },
    "errors": []
}
```

2) Upload CA & Intermediate certificate

ROLES:
* PARTNERMANAGER
* PARTNER_ADMIN
* AUTH_PARTNER
* PMS_USER
* ID_AUTHENTICATION
* ONLINE_VERIFICATION_PARTNER

POST - {{host}}/v1/partnermanager/partners/certificate/ca/upload

Request:
```json
{
    "id": "string",
  "metadata": {},
  "request": {
    "certificateData":"-----BEGIN CERTIFICATE-----\r\nMIIDbDCCAlSgAwIBAgIIU/gMbefTNYowDQYJKoZIhvcNAQELBQAwVDELMAkGA1UE\r\nBhMCSU4xCzAJBgNVBAgMAktBMQwwCgYDVQQKDAM0MDMxGjAYBgNVBAsMEUlEQS1U\r\nRVNULU9SRy1VTklUMQ4wDAYDVQQDDAVDQS1ycDAeFw0yMTA4MjAwODAyMzlaFw0y\r\nMjA4MjAwODAyMzlaMFQxCzAJBgNVBAYTAklOMQswCQYDVQQIDAJLQTEMMAoGA1UE\r\nCgwDNDAzMRowGAYDVQQLDBFJREEtVEVTVC1PUkctVU5JVDEOMAwGA1UEAwwFQ0Et\r\ncnAwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCst9yvrdvRotF6hrde\r\nzkGUDy7vXim9PF15w8aXhZ/FsccJ10kCYyYJmpQSrE3uKQtCRw9Qac1MCb2kJOJe\r\nOr7elYnOAgx3TAai5PU5IOs7L+NG/rYcbtRHFbiGyl6SGZVizqzb4fPC/rIrjdSH\r\nBaaaXrbXi/8dglPPEHfI190NOarsmYWTl9XfVLrRp4ClEyFnKc029HTnGmXCu9AZ\r\nzgI2rGRrbVXUzjFDNJ3l6cD2NsiM38ugqFhHOQyD9UkmKWhVrcWXLx2JDTB4fMmL\r\nK+ARUizTS7MntDe0s5XJiSOTTUHTwUItVM+HoJ98H+nS7W6xp6M+abEgIDf+XaXO\r\nDsu9AgMBAAGjQjBAMA8GA1UdEwEB/wQFMAMBAf8wHQYDVR0OBBYEFGuEverUgpcj\r\nlYMxIxqHI6gPRd8PMA4GA1UdDwEB/wQEAwIChDANBgkqhkiG9w0BAQsFAAOCAQEA\r\nIFS5RLJHtMKKrXfqonkDbYdjtgIwAHbtg+lAyWdAJt/Ea5aH55loF21fYWjsFXEu\r\nQ9fdc72GFMJ/KZIKvAtVLP2Mm5kz4o8nhhEn0KRYUWkRg1YOtS7rKnmknFMgLhG6\r\ngIbBRuDWmGAd2VQVp1I4bNU+TJfsmz/hQKZL8uxLN5UV+TToM71GUFY9otEEDtAg\r\nceD8pjz0hKJW/rdIVB7J1I45JcVlT7Jx5mnJo4TU4bCb+wpYMW96KX1OPy6pV7qU\r\nZfjwK43CEjQGm5TKmJ9euMOln1Eo96+uPljlGrgyLklcYL3fuvqx/Lufly81MOOl\r\nYcjNymhUB8mGBCqoRxV2gw==\r\n-----END CERTIFICATE-----\r\n",
    "partnerDomain": "Auth"
  },
  "requesttime": "2021-08-20T08:02:47.711Z",
  "version": "string"
  }
```

Response:
```json
{
    "id": null,
    "version": null,
    "responsetime": "2021-08-20T08:02:48.876Z",
    "metadata": null,
    "response": {
        "status": "Upload Success.",
        "timestamp": "2021-08-20T08:02:48.990027"
    },
    "errors": []
}
```

3) Upload Partner certificate

ROLES:
* PARTNER
* DEVICE_PROVIDER
* FTM_PROVIDER
* CREDENTIAL_PARTNER
* CREDENTIAL_ISSUANCE
* PARTNER_ADMIN
* AUTH_PARTNER
* PMS_USER
* ID_AUTHENTICATION
* ONLINE_VERIFICATION_PARTNER

POST - {{host}}/v1/partnermanager/partners/certificate/upload

Request:
```json
{
  "id": "string",
  "metadata": {},
  "request": {
    "certificateData":"{{PARTNERCERT}}",
    "partnerDomain": "Auth",
    "partnerId": "{{PARTNERID}}"
  },
  "requesttime": "{{requesttime}}",
  "version": "string"
}
```

Response:
```json
{
    "id": null,
    "version": null,
    "responsetime": "2021-08-20T08:02:48.876Z",
    "metadata": null,
    "response": {
        "status": "Upload Success.",
        "timestamp": "2021-08-20T08:02:48.990027"
    },
    "errors": []
}
```

### 3) Get IDA auth related certs

1) Get ROOT certificate

ROLES:
* ZONAL_ADMIN
* GLOBAL_ADMIN
* INDIVIDUAL
* REGISTRATION_PROCESSOR
* REGISTRATION_ADMIN
* REGISTRATION_SUPERVISOR
* REGISTRATION_OFFICER
* ID_AUTHENTICATION
* TEST
* PRE-REGISTRATION_ADMIN
* RESIDENT

GET - {{host}}/v1/keymanager/getCertificate?applicationId=ROOT

Response:
```json
{
    "id": null,
    "version": null,
    "responsetime": "2021-08-20T08:23:10.758Z",
    "metadata": null,
    "response": {
        "certificate": "-----BEGIN CERTIFICATE-----\nMIIDl-----END CERTIFICATE-----\n",
        "certSignRequest": null,
        "issuedAt": "2021-07-28T15:01:57.000Z",
        "expiryAt": "2026-07-28T15:01:57.000Z",
        "timestamp": "2021-08-20T08:23:10.762Z"
    },
    "errors": null
}
```



ROLES:
* POLICYMANAGER (default for all)
* PARTNER_ADMIN (default for all)
* CREDENTIAL_ISSUANCE, CREATE_SHARE
```text
 (get partner policy {partnerId, policyId})
```
* PARTNER, AUTH_PARTNER, CREDENTIAL_PARTNER
```text
Get policy group list with filters & pagination
```
* PARTNER, AUTH_PARTNER, CREDENTIAL_PARTNER, CREDENTIAL_ISSUANCE
```text
Get policy list with filters & pagination
```
* PARTNER, PMS_USER, AUTH_PARTNER, CREDENTIAL_PARTNER
```text
policyGroupFilterValues
```
* PARTNER, PMS_USER, AUTH_PARTNER, CREDENTIAL_PARTNER
```text
PolicyFilterValues

####

## Auth UI

## Questions
1) What is mandatory mean in policies.allowedAuthTypes.mandatory