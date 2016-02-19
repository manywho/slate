## Flow

> Example Flow Request:

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
  "alertEmail": "paul.smith@mycompany.manywho.com",
  "isActive": false,
  "isDefault": false,
  "comment": "My activation comment."
}
```

*The Flow object represents an entire Flow application.*

Flows represent an atomic package of Elements that when run are fully versioned. Flows can reference other Flows using a Flow Out or messaging other Flows in the Tenant using the Runtime Service. When referencing Flows (parent or sub-Flows), the Platform will always take the latest activated and default version of the Flow.

When editing Elements in a Flow, you do not do this through the Flow part of the APIs. Each Element has its own API endpoint for managing objects, importing into the Flow, etc.

As with Group Elements, a Flow can also have permissions. However, unlike the Group Element, if a user cannot authenticate to a Flow, they cannot access any part of the Flow State. Effectively, the Flow authorization protects your Flow application from any access by running users that cannot successfully authenticate given the provided authorization criteria. Therefore any Group Elements act as a sub-set of authorization. The running users must first authenticate successfully into the Flow and subsequently authenticate into any Group Elements.  Further to this, there's no requirement that the Flow and Group Elements use the same Service Element for authentication. Flow Builders can build Flows that authenticate across multiple systems, move from unauthenticated to authenticated access, etc.

#### Flow

Key | Description
--- | -----------
**id**<br/>object | A composite unique identifier field assigned by the platform. This value should not be included for new Flows.<br/><br/>**id** (string):<br/>The unique identifier part that never changes for the lifetime of the Flow.<br/><br/>**versionId** (string):<br/>The unique identifier part for the version of the Flow. This changes every time a Map, Group, or Navigation Element is changed.
**editingToken**<br/>string | A unique identifier needed to perform any editing operations on a Flow or its contained Map, Group, or Navigation Elements.
**developerName**<br/>string | The name for the Flow. This is typically a helpful name to remind builders of the purpose of the Flow.
**developerSummary**<br/>string | The summary for the Flow. This is typically additional information that will help explain the purpose of the Flow.
**startMapElementId**<br/>string | The Map Element that should be used to start the Flow. This is always the START Map Element type.
**allowJumping**<br/>boolean | Indicates that the running user(s) can jump to any Map Element in the Flow (regardless of the Navigation).
**authorization**<br/>object | The configuration of the authorization context for this Flow. See GroupAuthorization for details.
**alertEmail**<br/>string | The email for the Flow Builder activating the Flow. This information if available at runtime.
**isActive**<br/>boolean | Indicates if the Flow is active (available for runtime users). This will always be false for the Draw API.
**isDefault**<br/>boolean | Indicates if the Flow is default (the default version of the Flow when a version is not explicitly provided). This will always be false for the Draw API.
**comment**<br/>string | As part of activation, the comment that was provided by the Flow Builder. This will always be null for the Draw API.


### Create/Update Flows

> Example 200 OK Response

```json
{
  "dateCreated": "0001-01-00T00:00:00Z",
  "dateModified": "0001-01-00T00:00:00Z",
  "whoCreated": null,
  "whoModified": null,
  "whoOwner": null,
  "alertEmail": null,
  "isActive": false,
  "isDefault": false,
  "comment": null,
  "editingToken": "19299bca-8a07-4b35-97f4-4cca598856d9",
  "id": {
    "id": "b7e2a056-35dd-4973-b279-c85aeafb299c",
    "versionId": "b6292dc0-ce7a-47de-bed8-7dd15e219e98"
  },
  "developerName": "Course Registration Flow",
  "developerSummary": "This is a simple course registration flow.",
  "startMapElementId": "3a0498ad-bf4f-4bba-bd4c-6975cd5e1c2a",
  "allowJumping": false,
  "stateExpirationLength": 0,
  "authorization": {
    "serviceElementId": "6388c4d1-cdae-4cc5-bb3b-a7083b71c8df",
    "globalAuthenticationType": "ALL_USERS",
    "streamBehaviourType": "USE_EXISTING",
    "groups": null,
    "users": null,
    "locations": null
  }
}
```

Used to create new Flow objects or update existing ones. The Flow object represents an entire Flow application.

#### HTTP Request

`POST /api/draw/1/flow`

#### Body

The raw JSON for the Flow.

<aside class="notice">
<b>Create vs Update</b><br/>
If the "id" property is included in the request, the platform will update the Flow with the matching unique identifier. If the "updateByName" property is set to true, the platform will update the Flow with the matching "developerName" property.
</aside>


### Query Flows

> Example 200 OK Response

```json
[
  {
    "dateCreated": "0001-01-00T00:00:00Z",
    "dateModified": "0001-01-00T00:00:00Z",
    "whoCreated": null,
    "whoModified": null,
    "whoOwner": null,
    "alertEmail": null,
    "isActive": false,
    "isDefault": false,
    "comment": null,
    "editingToken": "19299bca-8a07-4b35-97f4-4cca598856d9",
    "id": {
      "id": "b7e2a056-35dd-4973-b279-c85aeafb299c",
      "versionId": "b6292dc0-ce7a-47de-bed8-7dd15e219e98"
    },
    "developerName": "Course Registration Flow",
    "developerSummary": "This is a simple course registration flow.",
    "startMapElementId": "3a0498ad-bf4f-4bba-bd4c-6975cd5e1c2a",
    "allowJumping": false,
    "stateExpirationLength": 0,
    "authorization": {
      "serviceElementId": "6388c4d1-cdae-4cc5-bb3b-a7083b71c8df",
      "globalAuthenticationType": "ALL_USERS",
      "streamBehaviourType": "USE_EXISTING",
      "groups": null,
      "users": null,
      "locations": null
    }
  }
]
```

Used to filter existing Flow objects. The Flow object represents an entire Flow application.

#### HTTP Request

`GET /api/draw/1/flow?filter={filter}`

#### Parameters

Key | Description
--- | -----------
**filter**<br/>string | The filter for querying Flows


### Get Flow

> Example 200 OK Response

```json
{
  "dateCreated": "0001-01-00T00:00:00Z",
  "dateModified": "0001-01-00T00:00:00Z",
  "whoCreated": null,
  "whoModified": null,
  "whoOwner": null,
  "alertEmail": null,
  "isActive": false,
  "isDefault": false,
  "comment": null,
  "editingToken": "19299bca-8a07-4b35-97f4-4cca598856d9",
  "id": {
    "id": "b7e2a056-35dd-4973-b279-c85aeafb299c",
    "versionId": "b6292dc0-ce7a-47de-bed8-7dd15e219e98"
  },
  "developerName": "Course Registration Flow",
  "developerSummary": "This is a simple course registration flow.",
  "startMapElementId": "3a0498ad-bf4f-4bba-bd4c-6975cd5e1c2a",
  "allowJumping": false,
  "stateExpirationLength": 0,
  "authorization": {
    "serviceElementId": "6388c4d1-cdae-4cc5-bb3b-a7083b71c8df",
    "globalAuthenticationType": "ALL_USERS",
    "streamBehaviourType": "USE_EXISTING",
    "groups": null,
    "users": null,
    "locations": null
  }
}
```

Used to get an existing Flow object. The Flow object represents an entire Flow application.

#### HTTP Request

`GET /api/draw/1/flow/{id}`

#### Parameters

Key | Description
--- | -----------
**id**<br/>string | The unique identifier for the Flow


### Delete Flow

> Success 204 No Content Response

Used to delete an existing Flow object. The Flow object provides the structure of your pages or screens.

#### HTTP Request

`DELETE /api/draw/1/flow/{id}`

#### Parameters

Key | Description
--- | -----------
**id**<br/>string | The unique identifier for the Flow