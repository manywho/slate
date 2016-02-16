## Map Element

> Example Request:

```json
{
  "id": null,
  "developerName": "My Map Element",
  "developerSummary": "An example Map Element configuration",
  "x": 250,
  "y": 350,
  "groupElementId": "{id}",
  "pageElementId": "{id}",
  "dataActions": [
    {
      "developerName": "Save My Account",
      "crudOperationType": "SAVE",
      "isSmartSave": true,
      "order": 0,
      "valueElementToReferenceId": {
        "id": "{id}",
        "typeElementPropertyId": "{id}",
        "command": null
      },
      "valueElementToApplyId": {
        "id": "{id}",
        "typeElementPropertyId": "{id}",
        "command": null
      },
      "objectDataRequest": {
        "typeElementId": "{id}",
        "typeElementBindingId": "{id}",
        "listFilter": {
          "filterId": {
            "id": "{id}",
            "typeElementPropertyId": "{id}",
            "command": null
          },
          "comparisonType": "AND",
          "where": [
            {
              "columnTypeElementPropertyId": "{id}",
              "criteriaType": "EQUAL",
              "valueElementToReferenceId": {
                "id": "{id}",
                "typeElementPropertyId": "{id}",
                "command": null
              }
            }
          ],
          "orderByTypeElementPropertyId": "{id}",
          "orderByDirectionType": "DESC",
          "limit": 250,
          "filterByProvidedObjects": false
        },
        "command": {
          "commandType": null,
          "properties": {
            "key1": "value1",
            "key2": "value2"
          }
        }
      }
    }
  ],
  "listeners": [
    {
      "developerName": "My Listener",
      "serviceElementId": "{id}",
      "listenerType": null,
      "valueElementToReferenceForListeningId": {
        "id": "{id}",
        "typeElementPropertyId": "{id}",
        "command": null
      },
      "attributes": {
        "key1": "attribute1",
        "key2": "attribute2"
      }
    }
  ],
  "messageActions": [
    {
      "developerName": "Send Message",
      "serviceElementId": "{id}",
      "uriPart": null,
      "inputs": [
        {
          "developerName": "Hello",
          "contentType": "ContentString",
          "typeElementId": "{id}",
          "valueElementToReferenceId": {
            "id": "{id}",
            "typeElementPropertyId": "{id}",
            "command": null
          },
          "order": 0
        }
      ],
      "outputs": [
        {
          "developerName": "World",
          "contentType": "ContentString",
          "typeElementId": "{id}",
          "valueElementToApplyId": {
            "id": "{id}",
            "typeElementPropertyId": "{id}",
            "command": null
          },
          "order": 0
        }
      ],
      "attributes": {
        "key1": "attribute1",
        "key2": "attribute2"
      },
      "order": 0
    }
  ],
  "navigationOverrides": [
    {
      "navigationElementId": "{id}",
      "navigationItemId": "{id}",
      "locationMapElementId": "{id}",
      "isEnabled": false,
      "isVisible": true
    }
  ],
  "operations": [
    {
      "valueElementToApplyId": {
        "id": "{id}",
        "typeElementPropertyId": "{id}",
        "command": null
      },
      "valueElementToReferenceId": {
        "id": "{id}",
        "typeElementPropertyId": "{id}",
        "command": null
      },
      "macroElementToExecuteId": "{id}",
      "order": 0
    }
  ],
  "outcomes": [
    {
      "id": null,
      "developerName": "Next",
      "developerSummary": null,
      "label": "Next",
      "nextMapElementId": "{id}",
      "pageActionType": "SAVE",
      "isBulkAction": false,
      "pageActionBindingType": "EDIT",
      "pageObjectBindingId": "{id}",
      "order": 0,
      "comparison": {
        "comparisonType": "AND",
        "rules": [
          {
            "leftValueElementToReferenceId": {
              "id": "{id}",
              "typeElementPropertyId": "{id}",
              "command": null
            },
            "criteriaType": "EQUAL_TO",
            "rightValueElementToReferenceId": {
              "id": "{id}",
              "typeElementPropertyId": "{id}",
              "command": null
            }
          }
        ],
        "comparisons": null,
        "order": 0
      },
      "flowOut": {
        "valueElementStateId": {
          "id": "{id}",
          "typeElementPropertyId": "{id}",
          "command": null
        },
        "valueElementFlowId": {
          "id": "{id}",
          "typeElementPropertyId": "{id}",
          "command": null
        },
        "flowId": {
          "id": "{id}",
          "versionId": "{id}"
        },
        "valueElementExternalIdentifierId": {
          "id": "{id}",
          "typeElementPropertyId": "{id}",
          "command": null
        }
      },
      "controlPoints": [
        {
          "x": 0,
          "y": 0
        }
      ]
    }
  ],
  "viewMessageAction": null,
  "vote": {
    "voteType": null,
    "minimumCount": 0,
    "minimumPercent": 0,
    "attributes": {
      "key1": "attribute1",
      "key2": "attribute2"
    }
  },
  "clearNavigationOverrides": false,
  "postUpdateToStream": false,
  "postUpdateWhenType": "not sure what this is",
  "postUpdateMessage": "The Flow has progressed to this step",
  "statusMessage": "The Flow is currently busy doing some work",
  "notAuthorizedMessage": "You are not authenticated for the swimlane",
  "userContent": "This is my content",
  "updateByName": false
}
```

*The Map Element object represents any node or Element in your Flow diagram.*

Map Elements are used to set out the actions and journey of your Flow. Each Map Element performs an action - which may be to present the user with information, collect information, or perform logical actions such as inserting records into a database, executing business rules, or sending messages to a 3rd party application. There's a lot of functionality packed into Map Elements, and that has been separated out in the sections below. The base properties of the Map Element are outlined here.

#### Object

##### Map Element

Key | Description
--- | -----------
**id**<br/>string | A unique identifier field assigned by the platform. This value should not be included for new Map Elements.
**elementType**<br/>string | A unique element type for the Map Element. Valid values are:<ol><li>**START**: Start Element.</li><li>**STEP**: Step Element.</li><li>**INPUT**: Page Element.</li><li>**DECISION**: Decision Element.</li><li>**OPERATOR**: Operator Element.</li><li>**MESSAGE**: Message Element.</li><li>**DATABASE_SAVE**: Database Save Element.</li><li>**DATABASE_LOAD**: Database Load Element.</li><li>**DATABASE_DELETE**: Database Delete Element.</li></ol>
**developerName**<br/>string | The name for the Map Element. This is typically a helpful name to remind builders of the purpose of the Map Element.
**developerSummary**<br/>string | The summary for the Map Element. This is typically additional information that will help explain the purpose of the Map Element.
**x**<br/>integer | The X coordinate of the Map Element in the Flow diagram. If the Map Element is contained inside a Group Element, this the X coordinate in relation to the Group Element.
**y**<br/>integer | The Y coordinate of the Map Element in the Flow diagram. If the Map Element is contained inside a Group Element, this the Y coordinate in relation to the Group Element.
**groupElementId**<br/>string | The unique identifier for the Group Element that holds this Map Element. This identifier is only required for Map Elements that are in a Group Element. E.g. if a Map Element is in a Swimlane, this will be the unique identifier of the Swimlane Group Element that is in charge of restricting access to this step in the Flow.
**pageElementId**<br/>string | The unique identifier for the Page Element that is associated with this Map Element. This identifier is only required for Map Elements that will render a Page Layout. E.g. if a Map Element is a Page, this will be the unique identifier of the Page Layout that should be shown to the user at this step in the Flow.
**clearNavigationOverrides**<br/>boolean | If any Navigation Overrides have been applied to the Navigation of the running Flow, this step should clear all of the overrides.
**postUpdateToStream**<br/>boolean | If the Flow is associated with a Stream (E.g. a social feed in Chatter), this boolean indicates that the Map Element should automatically post to the stream when reached.
**postUpdateWhenType**<br/>string | If the postUpdateToStream key is set to true, this value tells the platform when to perform the actual update. Valid values are:<ol><li>**ON_LOAD**: Post the update to the stream when the Map Element loads.</li><li>**ON_EXIT**: Post the update to the stream when the Map Element is finished (i.e. by clicking on an Outcome that moves the Flow to the next step).</li></ol>
**postUpdateMessage**<br/>string | If the postUpdateToStream key is set to true, this is the content of the message that will be posted to the stream.
**statusMessage**<br/>string | If the Flow is currently in a "WAIT" state as a result of a Message Action, this is the message that will be shown to the users while waiting. The status message can be overwritten by the Service at runtime.
**notAuthorizedMessage**<br/>string | If the running user(s) of the Flow does not have access to a particular section of the Flow (E.g. due to a Swimlane), this is the message that will be shown to the users who are not authorized to view the content or take action on a Map Element step.
**userContent**<br/>string | The content that should be displayed to the running user(s) of the Flow. This key is only used for Step Map Elements and is a quick way of building out content in a Flow without needing to build a Page Layout.
**updateByName**<br/>boolean | When working with Map Element objects through the modeling API, this setting should be set to true if you do not have a unique identifier for a Map Element but wish to update any Map Element in the system that has this same name. This key is typically only used when scripting updates to Flows as part of a migration tool.
**viewMessageAction**<br/>string | (reserved for future development)

##### Data Actions

> Example dataActions JSON:

```json
  [
    {
      "developerName": "Save My Account",
      "crudOperationType": "SAVE",
      "isSmartSave": true,
      "order": 0,
      "valueElementToReferenceId": {
        "id": "<id>",
        "typeElementPropertyId": "<id>",
        "command": null
      },
      "valueElementToApplyId": {
        "id": "<id>",
        "typeElementPropertyId": "<id>",
        "command": null
      },
      "objectDataRequest": {
        "typeElementId": "<id>",
        "typeElementBindingId": "<id>",
        "listFilter": {
          "filterId": {
            "id": "<id>",
            "typeElementPropertyId": "<id>",
            "command": null
          },
          "comparisonType": "AND",
          "where": [
            {
              "columnTypeElementPropertyId": "<id>",
              "criteriaType": "EQUAL",
              "valueElementToReferenceId": {
                "id": "<id>",
                "typeElementPropertyId": "<id>",
                "command": null
              }
            }
          ],
          "orderByTypeElementPropertyId": "<id>",
          "orderByDirectionType": "DESC",
          "limit": 250,
          "filterByProvidedObjects": false
        },
        "command": {
          "commandType": null,
          "properties": {
            "key1": "value1",
            "key2": "value2"
          }
        }
      }
    }
  ]
```

A Data Action is used to perform create, read, update, or delete (CRUD) type operations on a Service. There are a number of features that make data actions particularly powerful:

1. You do not need to manage INSERT vs UPDATE operations. We automatically track the objects in your Flow and know if it is a new object to be inserted or an update to an existing object. This is done using our "SAVE" operation. We do not separate INSERT and UPDATE.
2. You can configure filters using our common metadata. This means you do not need to understand the query language of the underlying Service, you can create queries using a standard notation and we automatically translate this notation into SQL (RDBMS), SOQL (Salesforce), ZOQL (Zuora), etc.
3. The Data Action automatically knows where the data needs to go. There is no need to map fields into the database as this is already configured in the Type. In addition, a number of Services also support "smart save" which does a smart merge of data collected/changed in the Flow with data already stored in the Service.
4. If you need advanced data management capabilities such as summary roll-ups or joined tables, you can configure this using "commands" (as supported by the underlying Service implementation).

<aside class="notice">
<b>Data Actions Support</b><br/>
Map Elements that support Data Actions are:
<ul>
<li>Database Save</li>
<li>Database Load</li>
<li>Database Delete</li>
</ul>
</aside>

Key | Description
--- | -----------
**developerName**<br/>string | The name for the Data Action. This is typically a helpful name to remind builders of the purpose of the Data Action.
**crudOperationType**<br/>string | This is the type of operation being performed. Valid values are:<ul><li>**SAVE**: Save the data in the referenced Value back to the Service. This is an create or update operation in CRUD.</li><li>**LOAD**: Load data from the Service into the referenced Value. This is a read operation in CRUD.</li><li>**DELETE**: Delete the data stored in the reference Value from the Service. This data action can only be performed in the Value was first loaded from the Service.</li></ul>
**isSmartSave**<br/>boolean | Indicates if the data should saved using tracked changes in the data. Smart save must be supported in the underlying Service as the platform will only send changed data back to the Service rather than the complete Object or List.
**order**<br/>integer | The order in which the Data Action should be performed in relation to other Data Actions. The order must be greater than or equal to zero. If Data Actions have the same order, they will be performed in parallel to improve Flow performance.
**valueElementToReferenceId**<br/>object | The ValueElementId pointing to the Object or List Value that should be saved or deleted. This property is only needed for SAVE or DELETE operations or for LOAD operations where filterByProvidedObjects is true. E.g. which Object or List Value are you saving or deleting from the Service.
**valueElementToApplyId**<br/>object | The ValueElementId pointing to the Object or List Value that should be changed as a result of the Data Action. This property is only needed for SAVE or LOAD operations. E.g. which Object or List Value should be populated as a result of executing the save or load on the Service. When objects are saved, we send back the resulting data as it can often include additional information due to formula fields, triggers, etc.
**objectDataRequest**<br/>object | The configuration of the data operation being performed. See ObjectDataRequest for details.


### Create/Update Map Elements

> Example 200 OK Response

```json
{
  "dateCreated": "0001-01-01T00:00:00Z",
  "dateModified": "0001-01-01T00:00:00Z",
  "whoCreated": null,
  "whoModified": null,
  "whoOwner": null,
  "updateByName": false,
  "groupElementId": null,
  "x": 170,
  "y": 450,
  "height": 250,
  "width": 2480,
  "authorization": {
    "serviceElementId": "4d39d405-7eca-43f0-a4cb-419d55d8910c",
    "globalAuthenticationType": "SPECIFIED",
    "streamBehaviourType": "USE_EXISTING",
    "groups": [
      {
        "authenticationId": "0F915000000TrafCAC",
        "attribute": "MEMBERS"
      }
    ],
    "users": null,
    "locations": null
  },
  "id": "7f31a72e-eb11-4378-b9f8-ba70d334b789",
  "elementType": "SWIMLANE",
  "developerName": "Compliance and Risk",
  "developerSummary": ""
}
```

Used to create new Group Element objects or update existing ones. The Group Element object represents any group or Element in your Flow diagram that can contain Map Elements.

#### HTTP Request

`POST /api/draw/1/{flow_id}/{editing_token}/group`

#### Parameters

Key | Description
--- | -----------
**flow_id**<br/>string | Unique identifier for the Flow containing the Group Element
**editing_token**<br/>string | The active Editing Token for the Flow being edited


#### Body

The raw JSON for the Group Element.

<aside class="notice">
<b>Create vs Update</b><br/>
If the "id" property is included in the request, the platform will update the Element with the matching unique identifier. If the "updateByName" property is set to true, the platform will update the Element with the matching "developerName" property.
</aside>


### Query Group Elements

> Example 200 OK Response

```json
[
  {
    "dateCreated": "0001-01-01T00:00:00Z",
    "dateModified": "0001-01-01T00:00:00Z",
    "whoCreated": null,
    "whoModified": null,
    "whoOwner": null,
    "updateByName": false,
    "groupElementId": null,
    "x": 170,
    "y": 450,
    "height": 250,
    "width": 2480,
    "authorization": {
      "serviceElementId": "4d39d405-7eca-43f0-a4cb-419d55d8910c",
      "globalAuthenticationType": "SPECIFIED",
      "streamBehaviourType": "USE_EXISTING",
      "groups": [
        {
          "authenticationId": "0F915000000TrafCAC",
          "attribute": "MEMBERS"
        }
      ],
      "users": null,
      "locations": null
    },
    "id": "7f31a72e-eb11-4378-b9f8-ba70d334b789",
    "elementType": "SWIMLANE",
    "developerName": "Compliance and Risk",
    "developerSummary": ""
  }
]
```

Used to filter existing Group Element objects. The Group Element object represents any group or Element in your Flow diagram that can contain Map Elements.

#### HTTP Request

`GET /api/draw/1/{flow_id}/{editing_token}/group?filter={filter}`

#### Parameters

Key | Description
--- | -----------
**flow_id**<br/>string | Unique identifier for the Flow containing the Group Element
**editing_token**<br/>string | The active Editing Token for the Flow being edited
**filter**<br/>string | The filter for querying Group Elements


### Get GroupElement

> Example 200 OK Response

```json
{
  "dateCreated": "0001-01-01T00:00:00Z",
  "dateModified": "0001-01-01T00:00:00Z",
  "whoCreated": null,
  "whoModified": null,
  "whoOwner": null,
  "updateByName": false,
  "groupElementId": null,
  "x": 170,
  "y": 450,
  "height": 250,
  "width": 2480,
  "authorization": {
    "serviceElementId": "4d39d405-7eca-43f0-a4cb-419d55d8910c",
    "globalAuthenticationType": "SPECIFIED",
    "streamBehaviourType": "USE_EXISTING",
    "groups": [
      {
        "authenticationId": "0F915000000TrafCAC",
        "attribute": "MEMBERS"
      }
    ],
    "users": null,
    "locations": null
  },
  "id": "7f31a72e-eb11-4378-b9f8-ba70d334b789",
  "elementType": "SWIMLANE",
  "developerName": "Compliance and Risk",
  "developerSummary": ""
}
```

Used to get an existing Group Element object. The Group Element object represents any group or Element in your Flow diagram that can contain Map Elements.

#### HTTP Request

`GET /api/draw/1/{flow_id}/{editing_token}/group/{id}`

#### Parameters

Key | Description
--- | -----------
**flow_id**<br/>string | Unique identifier for the Flow containing the Group Element
**editing_token**<br/>string | The active Editing Token for the Flow being edited
**id**<br/>string | The unique identifier for the Group Element


### Delete GroupElement

> Success 204 No Content Response

Used to delete an existing Group Element object. The Group Element object represents any group or Element in your Flow diagram that can contain Map Elements.

#### HTTP Request

`DELETE /api/draw/1/{flow_id}/{editing_token}/group/{id}`

#### Parameters

Key | Description
--- | -----------
**flow_id**<br/>string | Unique identifier for the Flow containing the Group Element
**editing_token**<br/>string | The active Editing Token for the Flow being edited
**id**<br/>string | The unique identifier for the Group Element