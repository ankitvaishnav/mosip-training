# ID Schema
Read about ID schema from the following URL[https://docs.mosip.io/platform/modules/registration-processor/mosip-id-object-definition#id-schema](https://docs.mosip.io/platform/modules/registration-processor/mosip-id-object-definition#id-schema)

There are 3 customs types in ID schema:
* simpleType: for storing values of multi-lang fields
* documentType: for storing values of documents
* biometricsType: for string values of biometrics

Below is a sample json block for name.
```json
{
    "name": {
        "bioAttributes": [],
        "validators": [
            {
                "validator": "^(?=.{3,50}$).*",
                "arguments": [],
                "type": "regex"
            }
        ],
        "fieldCategory": "pvt",
        "format": "none",
        "fieldType": "default",
        "$ref": "#/definitions/simpleType"
    }
}
```

## Practice questions

*For all the question, assume that the country has primary language as english (eng) and secondary language as french (fra)*

1) Define json block for firstName and lastName

2) Define json block for age