# Registration UI spec.

Read about Registration UI spec from the following URL [https://docs.mosip.io/platform/modules/registration-client/ui-specification-for-registration-client](https://docs.mosip.io/platform/modules/registration-client/ui-specification-for-registration-client)

Below are sample json block for dateOfBirth and parentOrGuardianName. We want parent or guardian related information to be shown only for child and we achieved that using requiredOn, visible fields of parentOrGuardianName 

```json
[
{
    "id": "dateOfBirth",
    "description": "dateOfBirth",
    "label": {
      "primary": "Date de Birth"
    },
    "type": "string",
    "minimum": 0,
    "maximum": 0,
    "controlType": "ageDate",
    "fieldType": "default",
    "format": "none",
    "fieldCategory": "pvt",
    "inputRequired": true,
    "validators": [
      {
        "type": "regex",
        "validator": "^(1869|18[7-9]\\d|19\\d\\d|20\\d\\d)/([0][1-9]|1[0-2])/([0][1-9]|[1-2]\\d|3[0-1])$",
        "arguments": []
      }
    ],
    "bioAttributes": null,
    "subType": null,
    "contactType": null,
    "group": null,
    "alignmentGroup": null,
    "visible": null,
    "changeAction": null,
    "required": true
  },
  {
    "id": "parentOrGuardianName",
    "description": "parentOrGuardianName",
    "label": {
      "primary": "Parent or guardian name"
    },
    "type": "simpleType",
    "minimum": 0,
    "maximum": 0,
    "controlType": "textbox",
    "fieldType": "default",
    "format": "none",
    "fieldCategory": "default",
    "inputRequired": true,
    "validators": [
      {
        "type": "regex",
        "validator": "^(?=.{0,120}$).*",
        "arguments": []
      }
    ],
    "bioAttributes": null,
    "requiredOn": [
      {
        "engine": "MVEL",
        "expr": "( identity.isNew && identity.isChild ) || ( identity.isUpdate && identity.isChild )"
      }
    ],
    "subType": null,
    "contactType": null,
    "group": null,
    "alignmentGroup": null,
    "visible": {
      "engine": "MVEL",
      "expr": "identity.age < 6"
    },
    "changeAction": null,
    "required": false
  }
]
```
## Practice questions

*For all the question, assume that the country has primary language as english (eng) and secondary language as french (fra)*

1) Define json blocks for firstName and lastName:
    * Both are mandatory

2) Define json block for age:
    * Mandatory field

3) Define json blocks for email & phone, where any one of them is mandatory to fill.