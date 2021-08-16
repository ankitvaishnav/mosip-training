# Location
There are 2 tables that stores location related data in masterdata:
* loc_hierarchy_list
* location

**loc_hierarchy_list**: 

Contains the hierarchy related information.

For example:

| hierarchy_level | hierarchy_level_name | lang_code|
| --------------- | ------------------- | --------- |
| 0 | Country | eng
| 0 | Pays | fra
| 1 | State | eng
| 1 | Prefecture | fra
| 2 | City | eng
| 2 | ville | fra

**location**

Location table contains the location data with hierarchy in multi-language.

For example:

```text
- country (hierarchy_level 0)
    - state (hierarchy_level 1)
        - city (hierarchy_level 2)
```
