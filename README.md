# Custom Objects

The CustomObject Agent will contain all agent-methods related to working with Custom Objects.

We want to provide a REST API for working with CustomObjects as well, and this document outlines some options and suggestions for how it might look. Feedback is expected from those who want to use the API.

Note: All responses can be expected to be encoded values [according to our documentation](https://docs.superoffice.com/en/api/netserver/archive-providers/encoded-values.html).

## Disclaimer

Some endpoints are currently not supported, as it requires some changes to NetServer to be able to create tables and fields. The document will link to this heading for the relevant endpoints that have this restriction.

## Archive - GET /api/v1/CustomObject/

OData list of all CustomObjectEntity.

Can be sorted and further filtered using OData conventions:

    CustomObject?$select=col1,col2,abc/col3
    CustomObject?$filter=col1 eq 'foo' and startswith(col2, 'baz')
    CustomObject?$orderby=abc/col3,col1
    CustomObject?$top=1000
    CustomObject?$mode=full

OData returns XML or JSON carriers depending on the Accept headers.

Calls the Archive service using the "CustomObject" archive.

### Request

`GET /api/v1/CustomObject/`

### Response

```json
{
  "odata.metadata": "https://www.example.com/api/v1/archive$metadata",
  "odata.nextLink": "soluta",
  "value": [
    {
        "PrimaryKey": [I:42],
        "EntityName": "y_equipment",
        "Title": "Equipment Registry",
        "DisplayField": "Equipment",
        "Description": "This table contains information about equipments",
        "IconId": [I:1],
        "Flags": [I:1],
        "Fields": [
            {
            "Name": "x_equipment_id",
            "Type": "int",
            "DisplayName": "Something",
            "Description": "This is a description",
            "UseDefaultValue": [I:0],
            "DefaultValue": "This uses default value",
            "Rank": [I:1]
            },
            {
            "Name": "x_equipment_type",
            "FieldType": "string",
            "DisplayName": "Something",
            "Description": "This is a description",
            "UseDefaultValue": [I:0],
            "DefaultValue": "This uses default value",
            "Rank": [I:2]
            }
        ],
        "Data": [
            {
            "x_equipment_id": [I:1],
            "x_equipment_type": "Hammer"
            },
            {
            "x_equipment_id": [I:2],
            "x_equipment_type": "Nail"
            }
        ]
    }
  ]
}
```

## POST - /api/v1/CustomObject/ - [note](#disclaimer)

Creates a new CustomObjectEntity

Calls the CustomObject agent service SaveCustomObjectEntity.

#### Request

`POST ../api/v1/CustomObject`

```json
{
  "Id": 0,
  "Name": "y_equipment",
  "Title": "Equipment Registry",
  "DisplayField": "Equipment",
  "Description": "This table contains information about equipments",
  "IconId": 1,
  "Flags": 1,
  "Fields": [
    {
      "Name": "x_equipment_id",
      "Type": "int",
      "DisplayName": "Something",
      "Description": "This is a description",
      "UseDefaultValue": 1,
      "DefaultValue": "This uses default value",
      "Rank": 1
    },
    {
      "Name": "x_equipment_type",
      "FieldType": "string",
      "DisplayName": "Something",
      "Description": "This is a description",
      "UseDefaultValue": 0,
      "DefaultValue": "This uses default value",
      "Rank": 2
    }
  ]
}
```

Note: It has been decided, at least for now, to not permit sending in Data in this step.

#### Response

```json
{
  "Id": 1,
  "Name": "y_equipment",
  "Title": "Equipment Registry",
  "DisplayField": "Equipment",
  "Description": "This table contains information about equipments",
  "IconId": [I:1],
  "Flags": [I:1],
  "Fields": [
    {
      "Id": [I:1]
      "Name": "x_equipment_id",
      "Type": "int",
      "DisplayName": "Something",
      "Description": "This is a description",
      "UseDefaultValue": [I:1],
      "DefaultValue": "This uses default value",
      "Rank": [I:1]
    },
    {
      "Id": [I:2]
      "Name": "x_equipment_type",
      "FieldType": "string",
      "DisplayName": "Something",
      "Description": "This is a description",
      "UseDefaultValue": [I:0],
      "DefaultValue": "This uses default value",
      "Rank": [I:2]
    }
  ]
}
```

## Option 1

This option keeps CustomObject definition and data on the same controller. The CustomObjectEntity contains information about the definition (table and fields) and data (rows in the table).

We could also skip `/data/` as part of the path, for working with data-objects, to simplify this URL.

### GET - /api/v1/CustomObject/{entity_id}

Gets a CustomObjectEntity object.

Calls the CustomObject agent service GetCustomObjectEntity.

#### Request

`GET ../api/v1/CustomObject/42`

#### Response

```json
{
  "Id": [I:42],
  "Name": "y_equipment",
  "Title": "Equipment Registry",
  "DisplayField": "Equipment",
  "Description": "This table contains information about equipments",
  "IconId": [I:1],
  "Flags": [I:1],
  "Fields": [
    {
      "Name": "x_equipment_id",
      "Type": "int",
      "DisplayName": "Something",
      "Description": "This is a description",
      "UseDefaultValue": [I:0],
      "DefaultValue": "This uses default value",
      "Rank": [I:1]
    },
    {
      "Name": "x_equipment_type",
      "FieldType": "string",
      "DisplayName": "Something",
      "Description": "This is a description",
      "UseDefaultValue": [I:0],
      "DefaultValue": "This uses default value",
      "Rank": [I:2]
    }
  ],
  "Data": [
    {
        "x_equipment_id": [I:1],
        "x_equipment_type": "Hammer"
    },
    {
        "x_equipment_id": [I:2],
        "x_equipment_type": "Nail"
    }
  ]
}
```

### GET - /api/v1/CustomObject/{entity_id}/fields

OData list of field definitions for a specific CustomObjectEntity.

Can be sorted and further filtered using OData conventions:

* CustomObject/1234/fields?$select=col1,col2,abc/col3
* CustomObject/1234/fields?$filter=col1 eq 'foo' and startswith(col2, 'baz')
* CustomObject/1234/fields?$orderby=abc/col3,col1
* CustomObject/1234/fields?$top=1000
* CustomObject/1234/fields?$mode=full

OData returns XML or JSON carriers depending on the HTTP Accept header.

Calls the Archive service using the "CustomObject" archive provider.

#### Request

Get - `/api/v1/CustomObject/42/fields`

#### Response

```json
{
  "odata.metadata": "https://www.example.com/api/v1/archive$metadata",
  "odata.nextLink": "repellendus",
  "value": [
    {
      "PrimaryKey": [I:1],
      "EntityName": "x_equipment_id",
      "Type": "int",
      "DisplayName": "Something",
      "Description": "This is a description",
      "UseDefaultValue": [I:0],
      "DefaultValue": "This uses default value",
      "Rank": [I:1]
    },
    {
      "PrimaryKey": [I:2],
      "EntityName": "x_equipment_type",
      "FieldType": "string",
      "DisplayName": "Something",
      "Description": "This is a description",
      "UseDefaultValue": [I:0],
      "DefaultValue": "This uses default value",
      "Rank": [I:2]
    }
  ]
}
```

### POST - /api/v1/CustomObject/{entity_id}/fields - [note](#disclaimer)

Add an array of field definitions for a CustomObjectEntity.

#### Request

`POST ../api/v1/CustomObject/42/fields`

```json
[
  {
    "Name": "x_equipment_id",
    "Type": "int",
    "DisplayName": "Something",
    "Description": "This is a description",
    "UseDefaultValue": 1,
    "DefaultValue": "This uses default value",
    "Rank": 1
  },
  {
    "Name": "x_equipment_type",
    "FieldType": "string",
    "DisplayName": "Something",
    "Description": "This is a description",
    "UseDefaultValue": 0,
    "DefaultValue": "This uses default value",
    "Rank": 2
  }
]
```

#### Response

```json
[
  {
    "Id": [I:1],
    "Name": "x_equipment_id",
    "Type": "int",
    "DisplayName": "Something",
    "Description": "This is a description",
    "UseDefaultValue": [I:1],
    "DefaultValue": "This uses default value",
    "Rank": [I:1]
  },
  {
    "Id": [I:2],
    "Name": "x_equipment_type",
    "FieldType": "string",
    "DisplayName": "Something",
    "Description": "This is a description",
    "UseDefaultValue": [I:0],
    "DefaultValue": "This uses default value",
    "Rank": [I:2]
  }
]
```

### PUT - /api/v1/CustomObject/{entity_id}/fields - [note](#disclaimer)

Updates field definitions for a CustomObjectEntity. All omitted fields (with its data) will be removed from the database! Risky?

#### Request

`PUT /api/v1/CustomObject/42/fields`

```json
[
  {
    "Id": 1,
    "Name": "x_equipment_id",
    "Type": "int",
    "DisplayName": "Something",
    "Description": "This is a NEW description",
    "UseDefaultValue": 1,
    "DefaultValue": "This uses default value",
    "Rank": 1
  }
]
```

#### Response

```json
[
  {
    "Id": [I:1],
    "Name": "x_equipment_id",
    "Type": "int",
    "DisplayName": "Something",
    "Description": "This is a NEW description",
    "UseDefaultValue": [I:1],
    "DefaultValue": "This uses default value",
    "Rank": [I:1]
  }
]
```

### PATCH - /api/v1/CustomObject/{entity_id}/fields/{field_id}

Update a field definition on a CustomObjectEntity with changes, as described in a JSON Patch or a JSON Merge Patch document.
`Id`, `Name` and `Type` cannot be changed here, as they are set on creation.

#### Request

`PATCH /api/v1/CustomObject/42/fields/1`

`JSON PATCH`:
[ { "op": "replace", "path": "/Description", "value": "This is a new description" } ]

`JSON MERGE PATCH`:
{ "Description": "This is a new description" }

#### Response

```json
  {
    "Id": [I:1],
    "Name": "x_equipment_id",
    "Type": "int",
    "DisplayName": "Something",
    "Description": "This is a new description",
    "UseDefaultValue": [I:1],
    "DefaultValue": "This uses default value",
    "Rank": [I:1]
  }
```

### GET - /api/v1/CustomObject/{entity_id}/data

OData list of data for a specific CustomObjectEntity.

Can be sorted and further filtered using OData conventions:

* CustomObject/1234/data?$select=col1,col2,abc/col3
* CustomObject/1234/data?$filter=col1 eq 'foo' and startswith(col2, 'baz')
* CustomObject/1234/data?$orderby=abc/col3,col1
* CustomObject/1234/data?$top=1000
* CustomObject/1234/data?$mode=full

OData returns XML or JSON carriers depending on the HTTP Accept header.

Calls the Archive service using the "CustomObject" archive provider.

#### Request

GET `../api/v1/CustomObject/42/data`

#### Response

```json
{
  "odata.metadata": "https://www.example.com/api/v1/archive$metadata",
  "odata.nextLink": "repellendus",
  "value": [
    {
        "x_foo": "This is row1 data",
        "x_bar": [I:2]
    },
        {
        "x_foo": "This is row2 data",
        "x_bar": [I:3]
    }
  ]
}
```

### POST - /api/v1/CustomObject/{entity_id}/data

Add an array of data to a CustomObjectEntity.

#### Request

`POST ../api/v1/CustomObject/42/data`

```json
[
    {
        "x_foo": "This is row1 data",
        "x_bar": 2
    },
        {
        "x_foo": "This is row2 data",
        "x_bar": 3
    }
]
```

#### Response

```json
[
    {
        "id": [I:1]
        "x_foo": "This is row1 data",
        "x_bar": [I:2]
    },
    {
        "id": [I:2]
        "x_foo": "This is row2 data",
        "x_bar": [I:3]
    }
]
```

### GET - /api/v1/CustomObject/{entity_id}/data/{data_id}

Gets a CustomObjectEntity data object.

Calls the CustomObject agent service GetCustomObjectData.

#### Request

`GET ../api/v1/CustomObject/42/data/123`

#### Response

```json
{
    "x_foo": "This is row1 data",
    "x_bar": [I:2]
}
```

### PATCH - /api/v1/CustomObject/{entity_id}/data/{data_id}

Update a value on a data-object on a CustomObjectEntity with changes, as described in a JSON Patch or a JSON Merge Patch document.

#### Request

`PATCH /api/v1/CustomObject/42/data/1`

`JSON PATCH`:
[ { "op": "replace", "path": "/x_foo", "value": "I want to update this" } ]

`JSON MERGE PATCH`:
{ "x_foo": "I want to update this" }

#### Response

```json
{
    "id": [I:1],
    "x_foo": "I want to update this",
    "x_bar": [I:2]
}
```

## Option 2

This option separates CustomObjectDefinitions and CustomObjectData on 2 different controllers. This means you have to use `CustomObjectDefinition` to handle table and fields, and only get data back from the `CustomObject`-endpoints. It makes it a little easier to understand what a CustomObject is (is it the definition itself or an object of a typeOf definition?).

### GET - /api/v1/CustomObjectDefinition/{definition_id}

Gets an existing CustomObject definition.

### POST - /api/v1/CustomObjectDefinition/ - [note](#disclaimer)

Creates a new CustomObject definition.

### PUT - /api/v1/CustomObjectDefinition/{definition_id} - [note](#disclaimer)

Updates an existing CustomObject definition.

### GET - /api/v1/CustomObject/{definition_id}/{object_id}

Gets a CustomObjectEntity.

### POST - /api/v1/CustomObject/{definition_id}

Creates a new CustomObjectEntity.

### PATCH - /api/v1/CustomObject/{definition_id}/{object_id}

Updates a CustomObjectEntity.
