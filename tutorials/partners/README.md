# Partners

Partner domains:
* AUTH
* DEVICE
* FTM (?)

Auth_Partner
Device_Provider
Credential_Partner
Partner_Admin
FTM_Provider
Online_Verification_Partner
ABIS_Partner
Manual_Adjudication
MISP_Partner


Auth partners:
* ABIS
* Resident
* Print
* Manual adjudication

Device partners:
* MDS provider
* 

FTM
* Auth ftm provider


1) Types of partners
2) Find the requests for all partners

API for creating partners

URL: v1/partnermanager/partners

```json
{
  "id": "string",
  "metadata": {},
  "request": {
    "address": "string",
    "contactNumber": "string",
    "emailId": "string",
    "organizationName": "string",
    "partnerId": "string",
    "partnerType": "?",
    "policyGroup": "string"
  },
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "version": "string"
}
```
3) How system using the partner domains

4) MDS, print partner (Kannan)

5) Auth partner for auth demo UI (Ganesh)
