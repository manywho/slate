## Flow Graph

> Example Flow Graph Request:

```json
{
  "id": {
    "id": "{id}",
    "versionId": "{id}"
  },
  "editingToken": "{id}",
  "developerName": "My Flow",
  "developerSummary": "My cool new flow",
  "startMapElementId": "{id}",
  "allowJumping": false,
  "authorization": {
    "serviceElementId": "{id}",
    "globalAuthenticationType": "SPECIFIED",
    "streamBehaviourType": "CREATE_NEW",
    "groups": [
  	  {
        "authenticationId": "id from directory",
        "attribute": "MEMBER"
      }
    ],
    "users": [
      {
        "authenticationId": "id from directory",
        "attribute": "DELEGATES"
      }
    ],
    "locations": null
  },
  "mapElements": [
    {
      "id": "{id}",
      "developerName": "My Map Element",
      "developerSummary": "An example Map Element configuration",
      "elementType": "STEP",
      "x": 250,
      "y": 350,
      "groupElementId": "{id}",
      "pageElementId": "{id}",
      "outcomes": [
        {
          "id": "{id}",
          "developerName": "Next",
          "developerSummary": null,
          "label": "Next",
          "nextMapElementId": "{id}",
          "pageActionType": "SAVE",
          "isBulkAction": false,
          "pageActionBindingType": "EDIT",
          "pageObjectBindingId": "{id}",
          "order": 0,
          "controlPoints": [
            {
              "x": 0,
              "y": 0
            }
          ]
        }
      ]
    }
  ],
  "groupElements": [
    {
      "id": "{id}",
      "elementType": "SWIMLANE",
      "developerName": "Compliance Team",
      "developerSummary": "Only for the compliance team",
      "x": 0,
      "y": 0,
      "height": 150,
      "width": 500,
      "groupElementId": "{id}"
    }
  ]
}
```

*The Flow Graph object provides the coordinate and basic configuration information of Map and Group Elements.*

The Flow Graph object is typically used for editing the layout of the Flow for Flow Builders. This API should not be used for creating new Flows, but rather to manage Map and Group Elements in an existing Flow. The focus of this API is to allow Flow Builders to make coordinate changes to these Elements while ensuring other Flow Builders are notified of these changes and can be updated in realtime.

#### Flow Graph

Key | Description
--- | -----------
**id**<br/>object | A composite unique identifier field assigned by the platform. This value should not be included for new Flows.<br/><br/>**id** (string):<br/>The unique identifier part that never changes for the lifetime of the Flow.<br/><br/>**versionId** (string):<br/>The unique identifier part for the version of the Flow. This changes every time a Map, Group, or Navigation Element is changed.
**editingToken**<br/>string | A unique identifier needed to perform any editing operations on a Flow or its contained Map, Group, or Navigation Elements.
**developerName**<br/>string | The name for the Flow. This is typically a helpful name to remind builders of the purpose of the Flow.
**developerSummary**<br/>string | The summary for the Flow. This is typically additional information that will help explain the purpose of the Flow.
**startMapElementId**<br/>string | The Map Element that should be used to start the Flow. This is always the START Map Element type.
**allowJumping**<br/>boolean | Indicates that the running user(s) can jump to any Map Element in the Flow (regardless of the Navigation).
**authorization**<br/>object | The configuration of the authorization context for this Flow. See GroupAuthorization for details.
**mapElements**<br/>array | The array of Map Elements in the Flow. Each Map Element entry has the basic properties of the Map Element and its Outcomes. See Map Elements for more information.
**groupElements**<br/>array | The array of Group Elements in the Flow. Each Group Element entry has the basic properties of the Group Element and its Outcomes. See Group Elements for more information.


### Update Flow Graph

> Example 200 OK Response

```json
{
  "id": {
    "id": "{id}",
    "versionId": "{id}"
  },
  "editingToken": "{id}",
  "developerName": "My Flow",
  "developerSummary": "My cool new flow",
  "startMapElementId": "{id}",
  "allowJumping": false,
  "authorization": {
    "serviceElementId": "{id}",
    "globalAuthenticationType": "SPECIFIED",
    "streamBehaviourType": "CREATE_NEW",
    "groups": [
  	  {
        "authenticationId": "id from directory",
        "attribute": "MEMBER"
      }
    ],
    "users": [
      {
        "authenticationId": "id from directory",
        "attribute": "DELEGATES"
      }
    ],
    "locations": null
  },
  "mapElements": [
    {
      "id": "{id}",
      "developerName": "My Map Element",
      "developerSummary": "An example Map Element configuration",
      "elementType": "STEP",
      "x": 250,
      "y": 350,
      "groupElementId": "{id}",
      "pageElementId": "{id}",
      "outcomes": [
        {
          "id": "{id}",
          "developerName": "Next",
          "developerSummary": null,
          "label": "Next",
          "nextMapElementId": "{id}",
          "pageActionType": "SAVE",
          "isBulkAction": false,
          "pageActionBindingType": "EDIT",
          "pageObjectBindingId": "{id}",
          "order": 0,
          "controlPoints": [
            {
              "x": 0,
              "y": 0
            }
          ]
        }
      ]
    }
  ],
  "groupElements": [
    {
      "id": "{id}",
      "elementType": "SWIMLANE",
      "developerName": "Compliance Team",
      "developerSummary": "Only for the compliance team",
      "x": 0,
      "y": 0,
      "height": 150,
      "width": 500,
      "groupElementId": "{id}"
    }
  ]
}
```

Used to update the Flow Graph object. The Flow Graph object provides the coordinate and basic configuration information of Map and Group Elements.

#### HTTP Request

`POST /api/draw/1/flow`

#### Body

The raw JSON for the Flow.

<aside class="notice">
<b>Updateable Properties</b><br/>
The only properties that can be updated in the Flow Graph object are:<ul><li>developerName</li><li>developerSummary</li><li>x</li><li>y</li><li>height</li><li>width</li></ul>
</aside>


### Get Flow Graph

> Example 200 OK Response

```json
{
  "id": {
    "id": "{id}",
    "versionId": "{id}"
  },
  "editingToken": "{id}",
  "developerName": "My Flow",
  "developerSummary": "My cool new flow",
  "startMapElementId": "{id}",
  "allowJumping": false,
  "authorization": {
    "serviceElementId": "{id}",
    "globalAuthenticationType": "SPECIFIED",
    "streamBehaviourType": "CREATE_NEW",
    "groups": [
  	  {
        "authenticationId": "id from directory",
        "attribute": "MEMBER"
      }
    ],
    "users": [
      {
        "authenticationId": "id from directory",
        "attribute": "DELEGATES"
      }
    ],
    "locations": null
  },
  "mapElements": [
    {
      "id": "{id}",
      "developerName": "My Map Element",
      "developerSummary": "An example Map Element configuration",
      "elementType": "STEP",
      "x": 250,
      "y": 350,
      "groupElementId": "{id}",
      "pageElementId": "{id}",
      "outcomes": [
        {
          "id": "{id}",
          "developerName": "Next",
          "developerSummary": null,
          "label": "Next",
          "nextMapElementId": "{id}",
          "pageActionType": "SAVE",
          "isBulkAction": false,
          "pageActionBindingType": "EDIT",
          "pageObjectBindingId": "{id}",
          "order": 0,
          "controlPoints": [
            {
              "x": 0,
              "y": 0
            }
          ]
        }
      ]
    }
  ],
  "groupElements": [
    {
      "id": "{id}",
      "elementType": "SWIMLANE",
      "developerName": "Compliance Team",
      "developerSummary": "Only for the compliance team",
      "x": 0,
      "y": 0,
      "height": 150,
      "width": 500,
      "groupElementId": "{id}"
    }
  ]
}
```

Used to get an existing Flow Graph object. The Flow Graph object provides the coordinate and basic configuration information of Map and Group Elements.

#### HTTP Request

`GET /api/draw/1/flow/{id}`

#### Parameters

Key | Description
--- | -----------
**id**<br/>string | The unique identifier for the Flow


### Check Flow Graph Changes

> Example 200 OK Response

```json
true
```

Used to check if the Flow Graph has been changed by any other Flow Builders. The Flow Graph object provides the coordinate and basic configuration information of Map and Group Elements.

#### HTTP Request

`GET /api/draw/1/graph/ping/flow/{flow_id}/{editing_token}`

#### Parameters

Key | Description
--- | -----------
**id**<br/>string | The unique identifier for the Flow
**editing_token**<br/>string | The unique identifier needed to perform any editing operations on a Flow or its contained Map, Group, or Navigation Elements.
