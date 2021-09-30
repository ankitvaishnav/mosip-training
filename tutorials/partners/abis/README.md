# ABIS partner
Anyone who wants to provide ABIS service has to be registered as a partner in MOSIP

[Flow diagram](workflow.png)

## Setup

### 0) Login with role PARTNER_ADMIN

### 1) Create policy group
Create a policy group

POST - {{host}}/v1/policymanager/policies/group/new

Request (explained):
```json
{
  "id": "",
  "metadata": {},
  "request": {
    "desc": "Policy description",
    "name": "name of policy group (unique)"
  },
  "requesttime": "",
  "version": ""
}
```

Sample request:
```json
{
  "id": "string",
  "metadata": {},
  "request": {
    "desc": "PolicyGroup Description",
    "name": "samplePolicyGroupName"
  },
  "requesttime": "2021-08-20T07:26:10.180568",
  "version": "1.0"
}
```

Sample response:
```json
{
  "id": "string",
  "version": "1.0",
  "responsetime": "2021-08-20T07:26:11.180568",
  "response": {
    "id": "{{policyGroupID}}",
    "name": "samplePolicyGroupName",
    "desc": "PolicyGroup Description",
    "is_Active": true,
    "cr_by": "admin",
    "cr_dtimes": "2021-08-20T07:26:12.180568",
    "up_by": null,
    "upd_dtimes": null
  },
  "errors": []
}
```

### 2) Create policy
Create a policy

POST - {{host}}/v1/policymanager/policies

Request (explained):
```json
{
  "id": "",
  "metadata": {},
  "request": {
    "desc": "Description",
    "name": "Name of policy (for a particular policy group, name is unique)",
    "version" : "",
    "policies": {
      "shareableAttributes": [
        {
          "attributeName":"biometrics",
          "group":"CBEFF",
          "source":[
            {
              "attribute":"individualBiometrics",
              "filter":[
                {
                  "type":"Iris"
                },
                {
                  "type":"Finger"
                },
                {
                  "type":"Face"
                }
              ]
            }
          ],
          "encrypted":true,
          "format":"extraction"
        }
      ],
      "dataSharePolicies": {
        "typeOfShare": "Data Share",
        "validForInMinutes": "Time (in mins.) till data will be available after creation (after this, the url will expire)",
        "transactionsAllowed": "No. of times the datashare url can be accessed (after this limit the url will expire)",
        "encryptionType": "Partner Based/ None (If Partner Based If None then data will be not be encrypted)",
        "shareDomain": "sandbox.mosip.net (domain name of the MOSIP server. Datashare url will be created using this: http://<domain name>/xxxx )",
        "source": "Packet Manager"
      }
    },
    "policyGroupName": "samplePolicyGroupName",
    "policyType": "Datashare"
  },
  "requesttime": "",
  "version": ""
}
```

Sample request:
```json
{
  "id": "string",
  "metadata": {},
  "request": {
    "desc": "Policy description",
    "name": "samplePolicyName",
    "version" : "1.0",
    "policies": {
      "shareableAttributes": [
        {
          "attributeName":"biometrics",
          "group":"CBEFF",
          "source":[
            {
              "attribute":"individualBiometrics",
              "filter":[
                {
                  "type":"Iris"
                },
                {
                  "type":"Finger"
                },
                {
                  "type":"Face"
                }
              ]
            }
          ],
          "encrypted":true,
          "format":"extraction"
        }
      ],
      "dataSharePolicies": {
        "typeOfShare": "Data Share",
        "validForInMinutes": "30",
        "transactionsAllowed": "20000",
        "encryptionType": "Partner Based/ None",
        "shareDomain": "sandbox.mosip.net",
        "source": "Packet Manager"
      }
    },
    "policyGroupName": "samplePolicyGroupName",
    "policyType": "Datashare"
  },
  "requesttime": "2021-08-20T07:29:07.018Z",
  "version": "1.0"
}
```

Sample response:
```json
{
  "id": "string",
  "version": "1.0",
  "responsetime": "2021-08-20T07:29:08.018Z",
  "response": {
    "id": "{{policyID}}",
    "policyGroupName": "samplePolicyGroupName",
    "name": "samplePolicyName",
    "desc": "Policy description",
    "is_Active": false,
    "cr_by": "admin",
    "cr_dtimes": "",
    "up_by": null,
    "upd_dtimes": null
  },
  "errors": []
}
```

### 3) Publish policy (Map policy and policy group)

POST - {{host}}/v1/policymanager/policies/{{policyID}}/group/{{policyGroupID}}/publish

Sample response:
```json
{
  "id": null,
  "version": null,
  "responsetime": "2021-08-20T07:32:07.184Z",
  "response": {
    "policyGroupId": "{{policyGroupID}}",
    "policyGroupName": "samplePolicyGroupName",
    "policyGroupDesc": "PolicyGroup Description",
    "policyGroupStatus": true,
    "policyGroup_cr_by": "admin",
    "policyGroup_cr_dtimes": "2021-08-20T07:26:12.180568",
    "policyGroup_up_by": null,
    "policyGroup_upd_dtimes": null,
    "policyId": "{{policyID}}",
    "policyName": "samplePolicyName",
    "policyDesc": "Policy description",
    "policyType": "Datashare",
    "publishDate": "2021-08-20T07:29:08.767508",
    "validTill": "2022-02-16T07:32:07.254676",
    "status": "PUBLISHED",
    "version": "1.0",
    "schema": "https://schemas.mosip.io/v1/auth-policy",
    "is_Active": true,
    "cr_by": "admin",
    "cr_dtimes": "2021-08-20T07:29:08.767468",
    "up_by": "admin",
    "upd_dtimes": "2021-08-20T07:32:07.254684",
    "policies": {
      "shareableAttributes": [
        {
          "encrypted": true,
          "format": "extraction",
          "attributeName": "biometrics",
          "source": [
            {
              "filter": [
                {
                  "type": "Iris"
                },
                {
                  "type": "Finger"
                },
                {
                  "type": "Face"
                }
              ],
              "attribute": "individualBiometrics"
            }
          ],
          "group": "CBEFF"
        }
      ],
      "dataSharePolicies": {
        "typeOfShare": "Data Share",
        "transactionsAllowed": "20000",
        "shareDomain": "sandbox.mosip.net",
        "encryptionType": "Partner Based",
        "source": "Packet Manager",
        "validForInMinutes": "30"
      }
    }
  },
  "errors": []
}
```

### 4) Partner registration

POST - {{host}}/v1/partnermanager/partners

Sample request:
```json
{
  "id": "string",
  "metadata": {},
  "request": {
    "address": "address 1",
    "contactNumber": "9232121222",
    "emailId": "sample@mosip.io",
    "organizationName": "sampleOrganisation",
    "partnerId": "samplePartnerId",
    "partnerType": "ABIS_Partner",
    "policyGroup": "samplePolicyGroupName"
  },
  "requesttime": "2021-08-20T07:49:33.043Z",
  "version": "1.0"
}
```

Sample response:
```json
{
  "id": "string",
  "version": "1.0",
  "responsetime": "2021-08-20T07:49:33.043Z",
  "metadata": null,
  "response": {
    "partnerId": "samplePartnerId",
    "status": "InProgress"
  },
  "errors": []
}
```

### 5) Upload CA & Intermediate certificate

POST - {{host}}/v1/partnermanager/partners/certificate/ca/upload

Sample request:
```json
{
  "id": "string",
  "metadata": {},
  "request": {
    "certificateData":"-----BEGIN CERTIFICATE-----\r\nMIIDbDCCAlSgAwIBAgIIU/gMbefTNYowDQYJKoZIhvcNAQELBQAwVDELMAkGA1UE\r\nBhMCSU4xCzAJBgNVBAgMAktBMQwwCgYDVQQKDAM0MDMxGjAYBgNVBAsMEUlEQS1U\r\nRVNULU9SRy1VTklUMQ4wDAYDVQQDDAVDQS1ycDAeFw0yMTA4MjAwODAyMzlaFw0y\r\nMjA4MjAwODAyMzlaMFQxCzAJBgNVBAYTAklOMQswCQYDVQQIDAJLQTEMMAoGA1UE\r\nCgwDNDAzMRowGAYDVQQLDBFJREEtVEVTVC1PUkctVU5JVDEOMAwGA1UEAwwFQ0Et\r\ncnAwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCst9yvrdvRotF6hrde\r\nzkGUDy7vXim9PF15w8aXhZ/FsccJ10kCYyYJmpQSrE3uKQtCRw9Qac1MCb2kJOJe\r\nOr7elYnOAgx3TAai5PU5IOs7L+NG/rYcbtRHFbiGyl6SGZVizqzb4fPC/rIrjdSH\r\nBaaaXrbXi/8dglPPEHfI190NOarsmYWTl9XfVLrRp4ClEyFnKc029HTnGmXCu9AZ\r\nzgI2rGRrbVXUzjFDNJ3l6cD2NsiM38ugqFhHOQyD9UkmKWhVrcWXLx2JDTB4fMmL\r\nK+ARUizTS7MntDe0s5XJiSOTTUHTwUItVM+HoJ98H+nS7W6xp6M+abEgIDf+XaXO\r\nDsu9AgMBAAGjQjBAMA8GA1UdEwEB/wQFMAMBAf8wHQYDVR0OBBYEFGuEverUgpcj\r\nlYMxIxqHI6gPRd8PMA4GA1UdDwEB/wQEAwIChDANBgkqhkiG9w0BAQsFAAOCAQEA\r\nIFS5RLJHtMKKrXfqonkDbYdjtgIwAHbtg+lAyWdAJt/Ea5aH55loF21fYWjsFXEu\r\nQ9fdc72GFMJ/KZIKvAtVLP2Mm5kz4o8nhhEn0KRYUWkRg1YOtS7rKnmknFMgLhG6\r\ngIbBRuDWmGAd2VQVp1I4bNU+TJfsmz/hQKZL8uxLN5UV+TToM71GUFY9otEEDtAg\r\nceD8pjz0hKJW/rdIVB7J1I45JcVlT7Jx5mnJo4TU4bCb+wpYMW96KX1OPy6pV7qU\r\nZfjwK43CEjQGm5TKmJ9euMOln1Eo96+uPljlGrgyLklcYL3fuvqx/Lufly81MOOl\r\nYcjNymhUB8mGBCqoRxV2gw==\r\n-----END CERTIFICATE-----\r\n",
    "partnerDomain": "AUTH"
  },
  "requesttime": "2021-08-20T08:02:47.711Z",
  "version": "1.0"
}
```

Sample response:
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

### 6) Upload Partner certificate

POST - {{host}}/v1/partnermanager/partners/certificate/upload

Request:
```json
{
  "id": "string",
  "metadata": {},
  "request": {
    "certificateData":"-----BEGIN CERTIFICATE-----\r\nMIIDbDCCAlSgAwIBAgIIU/gMbefTNYowDQYJKoZIhvcNAQELBQAwVDELMAkGA1UE\r\nBhMCSU4xCzAJBgNVBAgMAktBMQwwCgYDVQQKDAM0MDMxGjAYBgNVBAsMEUlEQS1U\r\nRVNULU9SRy1VTklUMQ4wDAYDVQQDDAVDQS1ycDAeFw0yMTA4MjAwODAyMzlaFw0y\r\nMjA4MjAwODAyMzlaMFQxCzAJBgNVBAYTAklOMQswCQYDVQQIDAJLQTEMMAoGA1UE\r\nCgwDNDAzMRowGAYDVQQLDBFJREEtVEVTVC1PUkctVU5JVDEOMAwGA1UEAwwFQ0Et\r\ncnAwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCst9yvrdvRotF6hrde\r\nzkGUDy7vXim9PF15w8aXhZ/FsccJ10kCYyYJmpQSrE3uKQtCRw9Qac1MCb2kJOJe\r\nOr7elYnOAgx3TAai5PU5IOs7L+NG/rYcbtRHFbiGyl6SGZVizqzb4fPC/rIrjdSH\r\nBaaaXrbXi/8dglPPEHfI190NOarsmYWTl9XfVLrRp4ClEyFnKc029HTnGmXCu9AZ\r\nzgI2rGRrbVXUzjFDNJ3l6cD2NsiM38ugqFhHOQyD9UkmKWhVrcWXLx2JDTB4fMmL\r\nK+ARUizTS7MntDe0s5XJiSOTTUHTwUItVM+HoJ98H+nS7W6xp6M+abEgIDf+XaXO\r\nDsu9AgMBAAGjQjBAMA8GA1UdEwEB/wQFMAMBAf8wHQYDVR0OBBYEFGuEverUgpcj\r\nlYMxIxqHI6gPRd8PMA4GA1UdDwEB/wQEAwIChDANBgkqhkiG9w0BAQsFAAOCAQEA\r\nIFS5RLJHtMKKrXfqonkDbYdjtgIwAHbtg+lAyWdAJt/Ea5aH55loF21fYWjsFXEu\r\nQ9fdc72GFMJ/KZIKvAtVLP2Mm5kz4o8nhhEn0KRYUWkRg1YOtS7rKnmknFMgLhG6\r\ngIbBRuDWmGAd2VQVp1I4bNU+TJfsmz/hQKZL8uxLN5UV+TToM71GUFY9otEEDtAg\r\nceD8pjz0hKJW/rdIVB7J1I45JcVlT7Jx5mnJo4TU4bCb+wpYMW96KX1OPy6pV7qU\r\nZfjwK43CEjQGm5TKmJ9euMOln1Eo96+uPljlGrgyLklcYL3fuvqx/Lufly81MOOl\r\nYcjNymhUB8mGBCqoRxV2gw==\r\n-----END CERTIFICATE-----\r\n",
    "partnerDomain": "AUTH",
    "partnerId": "samplePartnerId"
  },
  "requesttime": "2021-08-20T08:02:47.876Z",
  "version": "1.0"
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

### 7) Stop/ Delete Mock ABIS

### 8) Update registration-processor properties

```text
registration.processor.policy.id=samplePolicyId
registration.processor.subscriber.id=samplePartnerId
```

Restart Regproc services

### 9) Provide following info to vendor

Login Credentials (ABIS will use these to authentication before fetching the biometrics):
```text
appId
clientId
secretKey
```

Queue details (ABIS will use it to consume and produce the message to queue):
```text
"brokerUrl": "tcp://sandbox.mosip.net:30616",
"inboundQueueName": "mosip-to-abis1",
"outboundQueueName": "abis1-to-mosip",
"userName": "<username>",
"password": "<password>",
"typeOfQueue": "ACTIVEMQ",
```

## Issues

### Packet stuck in biographic verification

#### ActiveMQ's mosip-to-abis queue message are not being consumed

* ABIS configuration might be wrong, it might be pointing to wrong queue
* ABIS is not running


#### ABIS is consuming but not producing messages in abis-to-mosip queue

* ABIS configuration might be wrong, check name of the queue the ABIS in writing to
* Check ABIS logs for possible errors

#### Issue with the MOSIP stages

Run the following sql query:
```sql
select * from regprc.abis_request where bio_ref_id in (
    select bio_ref_id from regprc.reg_bio_ref where reg_id = '<Registration ID>'
);
```

```text
If you don't get any rows: 
    issue might be in abis handler stage or biodedupe stage
else:
    issue with abis-middleware stage
```

## Support/ debugging tips

Query to check requests that has gone to ABIS:
```sql
select * from regprc.abis_request where bio_ref_id in (
    select bio_ref_id from regprc.reg_bio_ref where reg_id = '<Registration ID>'
);
```

Query to check responses from ABIS:
```sql
select * from regprc.abis_response where abis_req_id in (select id from regprc.abis_request where bio_ref_id in (
    select bio_ref_id from regprc.reg_bio_ref where reg_id = '<Registration ID>')
);
```
