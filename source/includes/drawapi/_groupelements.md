## Group Element

> Example Request:

```json
{
  "id": "{id}",
  "elementType": "SWIMLANE",
  "developerName": "Compliance Team",
  "developerSummary": "Only for the compliance team",
  "x": 0,
  "y": 0,
  "height": 150,
  "width": 500,
  "groupElementId": "{id}",
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
  "updateByName": false
}
```

*The Group Element object represents any group or Element in your Flow diagram that can contain Map Elements.*

Group Elements are used to add additional behavior to Map Elements in your Flow. The Group Element currently only supports the ability to change the authentication context of the Map Elements it contains. This allows builders to change the permissions for Map Elements contained in the Group Element and restrict the ability for running users to edit or take action on any Outcomes. The properties of the Group Element are outlined here.

<aside class="notice">
<b>SWIMLANES</b><br/>It's important to note that the Swimlane Group Element assigns a new authorization context to the Map Elements it holds. This authorization context is passed up the stack to any integrated Services that can leverage this information to provide additional features. For example, the Salesforce Service uses the Swimlane information to determine the percentage of running users that have voted. It also uses this context to determine who should be notified or emailed.
</aside>

#### Group Element

Key | Description
--- | -----------
**id**<br/>string | A unique identifier field assigned by the platform. This value should not be included for new Group Elements.
**elementType**<br/>string | A unique element type for the Group Element. Valid values are:<br/><ul><li>**SWIMLANE**: Swimlane Element.</li></ul>
**developerName**<br/>string | The name for the Group Element. This is typically a helpful name to remind builders of the purpose of the Group Element.
**developerSummary**<br/>string | The summary for the Group Element. This is typically additional information that will help explain the purpose of the Group Element.
**x**<br/>integer | The X coordinate of the Group Element in the Flow diagram.
**y**<br/>integer |The Y coordinate of the Group Element in the Flow diagram.
**height**<br/>integer | The height of the Group Element in the Flow diagram.
**width**<br/>integer | The width of the Group Element in the Flow diagram.
**groupElementId**<br/>string | The unique identifier for the Group Element that holds this Group Element. The Swimlane Group Element does not support nested groupings.
**authorization**<br/>object | The configuration of the authorization context for this Group Element. See GroupAuthorization for details
**updateByName**<br/>boolean | When working with Group Element objects through the modeling API, this setting should be set to true if you do not have a unique identifier for a Group Element but wish to update any Group Element in the system that has this same name. This key is typically only used when scripting updates to Flows as part of a migration tool.


### Create/Update Group Elements

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

<aside class="notice">
<b>Filter</b><br/>
The filter can take the following formats:
<ul><li><b>developerName eq '{developer_name}'</b>: Filter the list of Elements where the "developerName" property exactly matches the provided developer name (case insensitive)</li><li><b>substringof(developerName, '{developer_name}')</b>: Filter the list of Elements where the "developerName" property partially matches the provided developer name (case insensitive)</li></ul>
</aside>


### Get Group Element

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


### Delete Group Element

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