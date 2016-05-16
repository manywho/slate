## Navigation Element

> Example Request:

```json
{
  "label": "Incident Flow",
  "navigationItems": [
    {
      "locationMapElementId": "{id}",
      "developerName": "My Navigation Item",
      "developerSummary": "Links to a Map Element in my Flow",
      "label": "My Navigation Item",
      "navigationItems": null,
      "order": 0,
      "tags": null
    }
  ],
  "tags": null,
  "updateByName": false,
  "elementType": "NAVIGATION",
  "developerName": "My Navigation",
  "developerSummary": "Provides unstructured navigation around my Flow"
}
```

*The Navigation Element object provides a menu or navigation structure allowing users to move around your Flow application in an unstructured way.*

Navigation Elements are used to set out the structure and Map Element locations which users can jump to directly. As a result, your Map Elements act more like web pages on a website than steps in a process. The base properties of the Navigation Element are outlined here.

#### Navigation Element

Key | Description
--- | -----------
**id**<br/>string | A unique identifier field assigned by the platform. This value should not be included for new Navigation Elements.
**elementType**<br/>string | A unique element type for the Navigation Element. Valid values are:<ul><li>**NAVIGATION**: Navigation Element.</li></ul>
**developerName**<br/>string | The name for the Navigation Element. This is typically a helpful name to remind builders of the purpose of the Navigation Element.
**developerSummary**<br/>string | The summary for the Navigation Element. This is typically additional information that will help explain the purpose of the Navigation Element.
**label**<br/>string | The label for the Navigation Element. This will appear to the running user(s).
**navigationItems**<br/>array | The array of Navigation Items that should be displayed to the running users so they can link directly to the specified Map Elements at any time during the use of the Flow. Each Navigation Item entry has the following keys:<br/><br/>**id** (string):<br/>A unique identifier field assigned by the platform. This value should not be included for new Navigation Items.<br/><br/>**locationMapElementId** (string):<br/>The unique identifier for a Map Element in the Flow. When the running user(s) select this Navigation Item, they will be taken directly to this Map Element.<br/><br/>**developerName** (string):<br/>The name for the Navigation Item. This is typically a helpful name to remind builders of the purpose of the Navigation Item.<br/><br/>**developerSummary** (string):<br/>The summary for the Navigation Item. This is typically additional information that will help explain the purpose of the Navigation Item.<br/><br/>**label** (string):<br/>The label for the Navigation Item. This will appear to the running user(s).<br/><br/>**navigationItems** (array):<br/>The array of nested Navigation Item objects associated with this parent Navigation Item.<br/><br/>**order** (integer):<br/>The order in which the Navigation Item should be shown to running user(s) in relation to other Navigation Items. The order must be greater than or equal to zero. If Navigation Items have the same order, they will be rendered in random order.<br/><br/>**tags** (array):<br/>The configuration of the tags associated with the Navigation Item. See PageTags for details.
**tags**<br/>array | The configuration of the tags associated with the Navigation Element. See PageTags for details.
**updateByName**<br/>boolean | When working with Navigation Element objects through the modeling API, this setting should be set to true if you do not have a unique identifier for a Navigation Element but wish to update any Navigation Element in the system that has this same name. This key is typically only used when scripting updates to Flows as part of a migration tool.


### Create/Update Navigation Elements

> Example 200 OK Response

```json
{
  "dateCreated": "0001-01-01T00:00:00Z",
  "dateModified": "0001-01-01T00:00:00Z",
  "whoCreated": null,
  "whoModified": null,
  "whoOwner": null,
  "label": "Incident Flow",
  "navigationItems": [
    {
      "id": "b03ce29f-d447-495b-9451-255e6805027b",
      "locationMapElementId": "5f299faf-dca0-4ea4-8407-8ec427229910",
      "developerName": "Open",
      "developerSummary": "",
      "label": "Open",
      "navigationItems": null,
      "order": 0,
      "tags": null
    },
    {
      "id": "48109bbd-f98c-4009-bb01-7c02aced91f7",
      "locationMapElementId": "2fadd4d9-4aec-44d9-b976-390e4788a92d",
      "developerName": "Op Risk",
      "developerSummary": "",
      "label": "Op Risk",
      "navigationItems": null,
      "order": 1,
      "tags": null
    },
    {
      "id": "d83fc074-88db-430e-bb62-18e13b4f5fc0",
      "locationMapElementId": "19038db7-bc20-4def-b844-86bb55ec5486",
      "developerName": "Business Head",
      "developerSummary": "",
      "label": "Bus Head",
      "navigationItems": null,
      "order": 2,
      "tags": null
    },
    {
      "id": "80319478-79a7-4285-b1f9-c6dcfa57d830",
      "locationMapElementId": "ba1bceb3-a119-4ad5-83d3-e3bbd34117b5",
      "developerName": "Done",
      "developerSummary": "",
      "label": "Done",
      "navigationItems": null,
      "order": 3,
      "tags": null
    }
  ],
  "tags": null,
  "updateByName": false,
  "id": "3c257f03-6932-4f1e-b71c-26560f883c4d",
  "elementType": "NAVIGATION",
  "developerName": "Incident",
  "developerSummary": ""
}
```

Used to create new Navigation Element objects or update existing ones. The Navigation Element object provides a menu or navigation structure allowing users to move around your Flow application in an unstructured way.

#### HTTP Request

`POST /api/draw/1/{flow_id}/{editing_token}/navigation`

#### Parameters

Key | Description
--- | -----------
**flow_id**<br/>string | Unique identifier for the Flow containing the Navigation Element
**editing_token**<br/>string | The active Editing Token for the Flow being edited


#### Body

The raw JSON for the Navigation Element.

<aside class="notice">
<b>Create vs Update</b><br/>
If the "id" property is included in the request, the platform will update the Element with the matching unique identifier. If the "updateByName" property is set to true, the platform will update the Element with the matching "developerName" property.
</aside>


### Query Navigation Elements

> Example 200 OK Response

```json
[
  {
    "dateCreated": "0001-01-01T00:00:00Z",
    "dateModified": "0001-01-01T00:00:00Z",
    "whoCreated": null,
    "whoModified": null,
    "whoOwner": null,
    "label": "Incident Flow",
    "navigationItems": [
      {
        "id": "b03ce29f-d447-495b-9451-255e6805027b",
        "locationMapElementId": "5f299faf-dca0-4ea4-8407-8ec427229910",
        "developerName": "Open",
        "developerSummary": "",
        "label": "Open",
        "navigationItems": null,
        "order": 0,
        "tags": null
      },
      {
        "id": "48109bbd-f98c-4009-bb01-7c02aced91f7",
        "locationMapElementId": "2fadd4d9-4aec-44d9-b976-390e4788a92d",
        "developerName": "Op Risk",
        "developerSummary": "",
        "label": "Op Risk",
        "navigationItems": null,
        "order": 1,
        "tags": null
      },
      {
        "id": "d83fc074-88db-430e-bb62-18e13b4f5fc0",
        "locationMapElementId": "19038db7-bc20-4def-b844-86bb55ec5486",
        "developerName": "Business Head",
        "developerSummary": "",
        "label": "Bus Head",
        "navigationItems": null,
        "order": 2,
        "tags": null
      },
      {
        "id": "80319478-79a7-4285-b1f9-c6dcfa57d830",
        "locationMapElementId": "ba1bceb3-a119-4ad5-83d3-e3bbd34117b5",
        "developerName": "Done",
        "developerSummary": "",
        "label": "Done",
        "navigationItems": null,
        "order": 3,
        "tags": null
      }
    ],
    "tags": null,
    "updateByName": false,
    "id": "3c257f03-6932-4f1e-b71c-26560f883c4d",
    "elementType": "NAVIGATION",
    "developerName": "Incident",
    "developerSummary": ""
  }
]
```

Used to filter existing Navigation Element objects. The Navigation Element object provides a menu or navigation structure allowing users to move around your Flow application in an unstructured way.

#### HTTP Request

`GET /api/draw/1/{flow_id}/{editing_token}/navigation?filter={filter}`

#### Parameters

Key | Description
--- | -----------
**flow_id**<br/>string | Unique identifier for the Flow containing the Navigation Element
**editing_token**<br/>string | The active Editing Token for the Flow being edited
**filter**<br/>string | The filter for querying Navigation Elements

<aside class="notice">
<b>Filter</b><br/>
The filter can take the following formats:
<ul><li><b>developerName eq '{developer_name}'</b>: Filter the list of Elements where the "developerName" property exactly matches the provided developer name (case insensitive)</li><li><b>substringof(developerName, '{developer_name}')</b>: Filter the list of Elements where the "developerName" property partially matches the provided developer name (case insensitive)</li></ul>
</aside>


### Get Navigation Element

> Example 200 OK Response

```json
{
  "dateCreated": "0001-01-01T00:00:00Z",
  "dateModified": "0001-01-01T00:00:00Z",
  "whoCreated": null,
  "whoModified": null,
  "whoOwner": null,
  "label": "Incident Flow",
  "navigationItems": [
    {
      "id": "b03ce29f-d447-495b-9451-255e6805027b",
      "locationMapElementId": "5f299faf-dca0-4ea4-8407-8ec427229910",
      "developerName": "Open",
      "developerSummary": "",
      "label": "Open",
      "navigationItems": null,
      "order": 0,
      "tags": null
    },
    {
      "id": "48109bbd-f98c-4009-bb01-7c02aced91f7",
      "locationMapElementId": "2fadd4d9-4aec-44d9-b976-390e4788a92d",
      "developerName": "Op Risk",
      "developerSummary": "",
      "label": "Op Risk",
      "navigationItems": null,
      "order": 1,
      "tags": null
    },
    {
      "id": "d83fc074-88db-430e-bb62-18e13b4f5fc0",
      "locationMapElementId": "19038db7-bc20-4def-b844-86bb55ec5486",
      "developerName": "Business Head",
      "developerSummary": "",
      "label": "Bus Head",
      "navigationItems": null,
      "order": 2,
      "tags": null
    },
    {
      "id": "80319478-79a7-4285-b1f9-c6dcfa57d830",
      "locationMapElementId": "ba1bceb3-a119-4ad5-83d3-e3bbd34117b5",
      "developerName": "Done",
      "developerSummary": "",
      "label": "Done",
      "navigationItems": null,
      "order": 3,
      "tags": null
    }
  ],
  "tags": null,
  "updateByName": false,
  "id": "3c257f03-6932-4f1e-b71c-26560f883c4d",
  "elementType": "NAVIGATION",
  "developerName": "Incident",
  "developerSummary": ""
}
```

Used to get an existing Navigation Element object. The Navigation Element object provides a menu or navigation structure allowing users to move around your Flow application in an unstructured way.

#### HTTP Request

`GET /api/draw/1/{flow_id}/{editing_token}/navigation/{id}`

#### Parameters

Key | Description
--- | -----------
**flow_id**<br/>string | Unique identifier for the Flow containing the Navigation Element
**editing_token**<br/>string | The active Editing Token for the Flow being edited
**id**<br/>string | The unique identifier for the Navigation Element


### Delete Navigation Element

> Success 204 No Content Response

Used to delete an existing Navigation Element object. The Navigation Element object provides a menu or navigation structure allowing users to move around your Flow application in an unstructured way.

#### HTTP Request

`DELETE /api/draw/1/{flow_id}/{editing_token}/navigation/{id}`

#### Parameters

Key | Description
--- | -----------
**flow_id**<br/>string | Unique identifier for the Flow containing the Navigation Element
**editing_token**<br/>string | The active Editing Token for the Flow being edited
**id**<br/>string | The unique identifier for the Navigation Element