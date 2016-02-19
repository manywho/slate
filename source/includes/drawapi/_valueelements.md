## Value Element

> Example Request:

```json
{
  "isFixed": false,
  "isVersionless": false,
  "access": "PRIVATE",
  "contentType": "ContentList",
  "contentFormat": null,
  "defaultContentValue": null,
  "defaultObjectData": null,
  "typeElementId": "{id}",
  "updateByName": false,
  "id": "{id}",
  "elementType": "VARIABLE",
  "developerName": "Approval Options",
  "developerSummary": null
}
```

*The Value Element object stores data collected in the Flow State.*

The purpose of the Value Element is to allow Flow builders to determine how data collected from running user(s) or external Services will be stored and used. The Value Element represents the memory for the Flow application so data gathered can be later saved, updated, or viewed. The base properties of the Value Element are outlined here.

#### Value Element

Key | Description
--- | -----------
**id**<br/>string | A unique identifier field assigned by the platform. This value should not be included for new Value Elements.
**elementType**<br/>string | A unique element type for the Value Element. Valid values are:<ul><li>**VARIABLE**: Value Element</li></ul>
**developerName**<br/>string | The name for the Value Element. This is typically a helpful name to remind builders of the purpose of the Value Element.
**developerSummary**<br/>string | The summary for the Value Element. This is typically additional information that will help explain the purpose of the Value Element.
**isFixed**<br/>boolean | Indicates if the value stored in the Value Element can be changed in the Flow State. If this is set to true, the Value Element acts like a 'constant'.
**access**<br/>string | The external access of this Value Element. A Flow is a bit like a code function or method. When called, data can be passed into the Flow State and when the Flow "finishes", data can be passed out of the Flow State. Valid values are:<ul><li>**INPUT**: The value for this Value Element can be assigned when the Flow is initialized (started).</li><li>**INPUT_OUTPUT**: The value for this Value Element can be assigned when the Flow is initialized (started) and the value will be returned with the Flow is finalized (finished).</li><li>**OUTPUT**: The value will be returned when the Flow is finalized (finished).</li><li>**PRIVATE**: The value for this Value Element can only be changed as per the configuration of the Flow builder (e.g. through Pages/Page Layouts, Operators, etc).</li></ul>
**contentType**<br/>string | The content type represented by the Value Element. Valid values are:<ul><li>**ContentString**: A string value</li><li>**ContentNumber**: A numeric value</li><li>**ContentPassword**: A hidden value</li><li>**ContentDateTime**: A date and time value</li><li>**ContentContent**: A rich content value</li><li>**ContentObject**: An object value</li><li>**ContentList**: A list value</li></ul>
**contentFormat**<br/>string | The formatting that should be applied to the value in this Value Element. This property does not apply for Values Elements with a contentType of ContentObject or ContentList. For Typed objects, the contentFormat is set for each Property in the Type.
**defaultContentValue**<br/>string | The default value for this Value Element. This is only needed if the contentType property is set to ContentObject or ContentList.
**defaultObjectData**<br/>array | The default object data for this Value Element. This is only needed if the contentType property is set to ContentObject or ContentList.
**initializationOperations**<br/>array | (Deprecated)
**typeElementId**<br/>string | The Type of the Object or List value being provided. This is only needed if the contentType property is set to ContentObject or ContentList.
**updateByName**<br/>boolean | When working with Value Element objects through the modeling API, this setting should be set to true if you do not have a unique identifier for a Value Element but wish to update any Value Element in the system that has this same name. This key is typically only used when scripting updates to Flows as part of a migration tool.


### Create/Update Value Elements

> Example 200 OK Response

```json
{
  "isFixed": false,
  "isVersionless": false,
  "access": "PRIVATE",
  "contentType": "ContentList",
  "contentFormat": null,
  "defaultContentValue": null,
  "defaultObjectData": [
    {
      "developerName": "Standard List Type",
      "typeElementId": "11e2c289-f400-451d-b907-1f6b3458fb76",
      "order": 0,
      "properties": [
        {
          "typeElementPropertyId": "6bed9cba-499c-4d4f-a679-6ec0ea77e822",
          "developerName": "Value",
          "contentValue": "REVIEW",
          "contentType": "ContentString",
          "contentFormat": null,
          "objectData": null
        },
        {
          "typeElementPropertyId": "e64fbe8a-33b9-42e9-8e1c-da4c460870af",
          "developerName": "Label",
          "contentValue": "Requires Review",
          "contentType": "ContentString",
          "contentFormat": null,
          "objectData": null
        }
      ],
      "isSelected": false
    },
    {
      "developerName": "Standard List Type",
      "typeElementId": "11e2c289-f400-451d-b907-1f6b3458fb76",
      "order": 1,
      "properties": [
        {
          "typeElementPropertyId": "6bed9cba-499c-4d4f-a679-6ec0ea77e822",
          "developerName": "Value",
          "contentValue": "APPROVE",
          "contentType": "ContentString",
          "contentFormat": null,
          "objectData": null
        },
        {
          "typeElementPropertyId": "e64fbe8a-33b9-42e9-8e1c-da4c460870af",
          "developerName": "Label",
          "contentValue": "Approve Application as Submitted",
          "contentType": "ContentString",
          "contentFormat": null,
          "objectData": null
        }
      ],
      "isSelected": false
    }
  ],
  "typeElementId": "11e2c289-f400-451d-b907-1f6b3458fb76",
  "updateByName": false,
  "id": "ed206576-c91c-426c-988b-76dd14752da7",
  "elementType": "VARIABLE",
  "developerName": "Approval Options",
  "developerSummary": null
}
```

Used to create new Value Element objects or update existing ones. The Value Element object stores data collected in the Flow State.

#### HTTP Request

`POST /api/draw/1/element/value`

#### Body

The raw JSON for the Value Element.

<aside class="notice">
<b>Create vs Update</b><br/>
If the "id" property is included in the request, the platform will update the Element with the matching unique identifier. If the "updateByName" property is set to true, the platform will update the Element with the matching "developerName" property.
</aside>


### Import Value Element

Used to import an existing Value Element object into a Flow. The Value Element object stores data collected in the Flow State.

#### HTTP Request

`POST /api/draw/1/element/flow/{flow_id}/value/{id}`

#### Parameters

Key | Description
--- | -----------
**flow_id**<br/>string | Unique identifier for the Flow
**id**<br/>string | The unique identifier for the Value Element


### Query Value Elements

> Example 200 OK Response

```json
[
  {
    "isFixed": false,
    "isVersionless": false,
    "access": "PRIVATE",
    "contentType": "ContentList",
    "contentFormat": null,
    "defaultContentValue": null,
    "defaultObjectData": null,
    "typeElementId": "11e2c289-f400-451d-b907-1f6b3458fb76",
    "updateByName": false,
    "id": "ed206576-c91c-426c-988b-76dd14752da7",
    "elementType": "VARIABLE",
    "developerName": "Approval Options",
    "developerSummary": null
  }
]
```

Used to filter existing Value Element objects. The Value Element object stores data collected in the Flow State.

#### HTTP Request

`GET /api/draw/1/element/value?filter={filter}`

#### Parameters

Key | Description
--- | -----------
**filter**<br/>string | The filter for querying Value Elements


### Get Value Element

> Example 200 OK Response

```json
{
  "isFixed": false,
  "isVersionless": false,
  "access": "PRIVATE",
  "contentType": "ContentList",
  "contentFormat": null,
  "defaultContentValue": null,
  "defaultObjectData": [
    {
      "developerName": "Standard List Type",
      "typeElementId": "11e2c289-f400-451d-b907-1f6b3458fb76",
      "order": 0,
      "properties": [
        {
          "typeElementPropertyId": "6bed9cba-499c-4d4f-a679-6ec0ea77e822",
          "developerName": "Value",
          "contentValue": "REVIEW",
          "contentType": "ContentString",
          "contentFormat": null,
          "objectData": null
        },
        {
          "typeElementPropertyId": "e64fbe8a-33b9-42e9-8e1c-da4c460870af",
          "developerName": "Label",
          "contentValue": "Requires Review",
          "contentType": "ContentString",
          "contentFormat": null,
          "objectData": null
        }
      ],
      "isSelected": false
    },
    {
      "developerName": "Standard List Type",
      "typeElementId": "11e2c289-f400-451d-b907-1f6b3458fb76",
      "order": 1,
      "properties": [
        {
          "typeElementPropertyId": "6bed9cba-499c-4d4f-a679-6ec0ea77e822",
          "developerName": "Value",
          "contentValue": "APPROVE",
          "contentType": "ContentString",
          "contentFormat": null,
          "objectData": null
        },
        {
          "typeElementPropertyId": "e64fbe8a-33b9-42e9-8e1c-da4c460870af",
          "developerName": "Label",
          "contentValue": "Approve Application as Submitted",
          "contentType": "ContentString",
          "contentFormat": null,
          "objectData": null
        }
      ],
      "isSelected": false
    }
  ],
  "typeElementId": "11e2c289-f400-451d-b907-1f6b3458fb76",
  "updateByName": false,
  "id": "ed206576-c91c-426c-988b-76dd14752da7",
  "elementType": "VARIABLE",
  "developerName": "Approval Options",
  "developerSummary": null
}
```

Used to get an existing Value Element object. The Value Element object stores data collected in the Flow State.

#### HTTP Request

`GET /api/draw/1/element/value/{id}`

#### Parameters

Key | Description
--- | -----------
**id**<br/>string | The unique identifier for the Value Element


### Delete Value Element

> Success 204 No Content Response

Used to delete an existing Value Element object. The Value Element object stores data collected in the Flow State.

#### HTTP Request

`DELETE /api/draw/1/element/value/{id}`

#### Parameters

Key | Description
--- | -----------
**id**<br/>string | The unique identifier for the Value Element