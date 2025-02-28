---
editable: false

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---


# DiskType
A set of methods to retrieve information about disk types.
## JSON Representation {#representation}
```json 
{
  "id": "string",
  "description": "string",
  "zoneIds": [
    "string"
  ]
}
```
 
Field | Description
--- | ---
id | **string**<br><p>ID of the disk type.</p> 
description | **string**<br><p>Description of the disk type. 0-256 characters long.</p> 
zoneIds[] | **string**<br><p>Array of availability zones where the disk type is available.</p> 

## Methods {#methods}
Method | Description
--- | ---
[get](get.md) | Returns the information about specified disk type.
[list](list.md) | Retrieves the list of disk types for the specified folder.