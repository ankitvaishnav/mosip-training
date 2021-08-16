# Location
There are 2 tables that stores location related data in masterdata:
* loc_hierarchy_list
* location

**loc_hierarchy_list**: 

Contains the hierarchy related information.

For example:

| hierarchy_level | hierarchy_level_name | lang_code|
| --------------- | -------------------- | -------- |
| 0 | Country | eng
| 0 | Pays | fra
| 1 | State | eng
| 1 | Prefecture | fra
| 2 | City | eng
| 2 | Ville | fra

**location**

Location table contains the location data with hierarchy in multi-language.

For example:

code | name | hierarchy_level | hierarchy_level_name | parent_loc_code | lang_code |
|----|------|---------------- | -------------------- | --------------- | ----------|
| IND | India | 0 | Country | IND | eng
| IND | Inde | 0 | Pays | IND | fra
| MH | Maharashtra | 0 | State | | eng
| MH | Maharashtra | 0 | Prefecture | | fra
| IND | Mumbai | 0 | City | | eng
| IND | Mumbai | 0 | Ville | | fra

