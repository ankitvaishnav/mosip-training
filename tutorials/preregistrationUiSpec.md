# Pre-registration UI Spec

Read about Pre-registration UI spec from the following URL [https://docs.mosip.io/platform/modules/pre-registration/ui-specification-for-pre-registration](https://docs.mosip.io/platform/modules/pre-registration/ui-specification-for-pre-registration)

Below is a sample json block for name.
```json
{
    "id": "fullName",
    "description": "Enter Full Name",
    "labelName": {
        "eng": "Full Name",
        "ara": "الاسم الكامل",
        "fra": "Nom complet"
    },
    "controlType": "textbox",
    "inputRequired": true,
    "validators": [
        {
            "type": "regex",
            "validator": "^(?=.{0,50}$).*",
            "arguments": []
        }
    ],
    "required": true
}
```

## Practice questions

*For all the question, assume that the country has primary language as english (eng) and secondary language as french (fra)*

1) Define json blocks for firstName and lastName:
    * Both are mandatory

2) Define json block for age:
    * Mandatory field