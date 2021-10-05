# Mock ABIS

[https://github.com/mosip/mosip-mock-services/tree/develop/mock-abis](https://github.com/mosip/mosip-mock-services/tree/develop/mock-abis)

## Matching logic

* BDB hash matching
* findDuplicate flag
* Expectation (used for scenario testing)

### 1) BDB hash matching

Mock ABIS caches the hashes of the biometrics during insert request:

```text
Biometrics -> multiple BDB -> hash.sha256(BDB) -> save hashes to in memory db
```

User 1 (referenceId - x): Biometrics{F, LI, RI, LIF, LMF, LRF, LLF, ...}

Database (in-memory)

| referenceId | hash |
| ----------- | ---- |
| x | hx1 |
| x | hx2 |
| x | hx3 |
| x | hx4 |
| y | hy1 |
| y | hy2 |
| y | hy3 |
| z | hz1 |
| z | hz2 |

Identify: refId - x
* Take all hashes where refenceId = x
* Match all the hashes from above with entire in memory db for refenceId != x

```txt
if hx1 == hz1:
    response[candidaList].addReferenceId(z)
```

### 2) findDuplicate flag

```text
findDuplicate == true
	BDB hash matching
findDuplicate == false
	candidateList = 0
```

### 3) Expectation (for scenario testing)

```json
{
  "id": "<Hash of the biometric>",
  "version": "xxxxx",
  "requesttime": "2021-05-05T05:44:58.525Z",
  "actionToInterfere": "Identify/ Insert",
  "forcedResponse": "Error",
  "errorCode": "",
  "delayInExecution": "",
  "gallery": {
    "referenceIds": [
      {
        "referenceId": "<Hash of the duplicate biometric>"
      }
    ]
  }
}
```

| referenceId | hash |
| ----------- | ---- |
| x | hx1 |
| x | hx2 |
| x | hx3 |
| x | hx4 |
| y | hy1 |
| y | hy2 |
| y | hy3 |
| z | hz1 |
| z | hz2 |

-> id (hash of biometric) -> referenceId (x)

-> (Hash of the duplicate biometric h1`) -> referenceId (y)

```text
response: {
  candidateList: [
    {
      referenceId: "y"
    }
  ]
}
```