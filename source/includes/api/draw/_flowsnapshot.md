## Flow SnapShot

*The Flow SnapShot object is the package that is sent to the Platform runtime engine.*

Without a Flow SnapShot, a Flow cannot be accessed by running users. The Flow SnapShot contains all, fully versioned, Elements that are needed for the Flow to execute (excluding sub-Flows). In the Draw Tool, each time a Flow is run or published, a Flow SnapShot is taken. This means you then have a version of the Flow that can also be reverted if Flow Builders make a range of mistakes and would like to go back to a previous SnapShot.

The Flow SnapShot also acts as a version system as all metadata for the Flow can be accessed and external tools can be used to 'diff' for changes. Equally, for compliance, a customer can access the Flow SnapShots to get a complete picture of which Flow the running user(s) were running at any particular point in time.

#### Flow SnapShot

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
**isActive**<br/>boolean | Indicates if the Flow is active (available for runtime users).
**isDefault**<br/>boolean | Indicates if the Flow is default (the default version of the Flow when a version is not explicitly provided).
**comment**<br/>string | As part of activation, the comment that was provided by the Flow Builder.
**groupElements**<br/>array | The array of Group Elements in the Flow. Each Group Element entry has all properties provided. See Group Elements for more information.
**mapElements**<br/>array | The array of Map Elements in the Flow. Each Map Element entry has all properties provided. See Map Elements for more information.
**navigationElements**<br/>array | The array of Navigation Elements in the Flow. Each Navigation Element entry has all properties provided. See Navigation Elements for more information.
**pageElements**<br/>array | The array of Page Elements in the Flow. Each Page Element entry has all properties provided. See Page Elements for more information.
**tagElements**<br/>array | The array of Tag Elements in the Flow. Each Tag Element entry has all properties provided. See Tag Elements for more information.
**macroElements**<br/>array | The array of Macro Elements in the Flow. Each Macro Element entry has all properties provided. See Macro Elements for more information.
**valueElements**<br/>array | The array of Value Elements in the Flow. Each Value Element entry has all properties provided. See Value Elements for more information.
**typeElements**<br/>array | The array of Type Elements in the Flow. Each Type Element entry has all properties provided. See Type Elements for more information.
**serviceElements**<br/>array | The array of Service Elements in the Flow. Each Service Element entry has all properties provided. See Service Elements for more information.


### Create Flow SnapShot

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
  "comment": "First attempt at creating the Flow",
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
  },
  "groupElements": null,
  "mapElements": null,
  "navigationElements": null,
  "pageElements": null,
  "tagElements": null,
  "macroElements": null,
  "valueElements": null,
  "typeElements": null,
  "serviceElements": null
}
```

Used to create a Flow SnapShot object. The Flow SnapShot object is the package that is sent to the Platform runtime engine.

#### HTTP Request

`POST /api/draw/1/flow/snap/{id}`

Key | Description
--- | -----------
**id**<br/>string | The unique identifier for the Flow


### Get Flow SnapShots

> Example 200 OK Response

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
    "comment": "First attempt at creating the Flow",
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
    },
    "groupElements": null,
    "mapElements": null,
    "navigationElements": null,
    "pageElements": null,
    "tagElements": null,
    "macroElements": null,
    "valueElements": null,
    "typeElements": null,
    "serviceElements": null
  },
  {
    "dateCreated": "0001-01-00T00:00:00Z",
    "dateModified": "0001-01-00T00:00:00Z",
    "whoCreated": null,
    "whoModified": null,
    "whoOwner": null,
    "alertEmail": null,
    "isActive": false,
    "isDefault": false,
    "comment": "Got it right this time after user feedback",
    "editingToken": "19299bca-8a07-4b35-97f4-4cca598856d9",
    "id": {
      "id": "b7e2a056-35dd-4973-b279-c85aeafb299c",
      "versionId": "a7594dc0-he7a-47il-asd8-7lf15e219e12"
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
    },
    "groupElements": null,
    "mapElements": null,
    "navigationElements": null,
    "pageElements": null,
    "tagElements": null,
    "macroElements": null,
    "valueElements": null,
    "typeElements": null,
    "serviceElements": null
  }
]
```

Used to get the list of all Flow SnapShots for a particular Flow. The Flow SnapShot object is the package that is sent to the Platform runtime engine.

#### HTTP Request

`GET /api/draw/1/flow/snap/{id}`

#### Parameters

Key | Description
--- | -----------
**id**<br/>string | The unique identifier for the Flow


### Get Flow SnapShots

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
  "comment": "First attempt at creating the Flow",
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
  },
  "groupElements": [ { groupElements } ],
  "mapElements": [ { mapElements } ],
  "navigationElements": [ { navigationElements } ],
  "pageElements": [ { pageElements } ],
  "tagElements": [ { tagElements } ],
  "macroElements": [ { macroElements } ],
  "valueElements": [ { valueElements } ],
  "typeElements": [ { typeElements } ],
  "serviceElements": [ { serviceElements } ]
}
```

Used to get the Flow SnapShot for a particular Flow Version. The Flow SnapShot object is the package that is sent to the Platform runtime engine.

#### HTTP Request

`GET /api/draw/1/flow/snap/{id}/{version_id}`

#### Parameters

Key | Description
--- | -----------
**id**<br/>string | The unique identifier for the Flow
**version_id**<br/>string | The unique identifier for the Flow Version


### Activating a Flow SnapShot

> Example 200 OK Response

```json
{
  "dateCreated": "0001-01-00T00:00:00Z",
  "dateModified": "0001-01-00T00:00:00Z",
  "whoCreated": null,
  "whoModified": null,
  "whoOwner": null,
  "alertEmail": null,
  "isActive": true,
  "isDefault": true,
  "comment": "First attempt at creating the Flow",
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
  },
  "groupElements": null,
  "mapElements": null,
  "navigationElements": null,
  "pageElements": null,
  "tagElements": null,
  "macroElements": null,
  "valueElements": null,
  "typeElements": null,
  "serviceElements": null
}
```

Used to activate and/or make default a Flow SnapShot version. The Flow SnapShot object is the package that is sent to the Platform runtime engine.

#### HTTP Request

`POST /api/draw/1/flow/activation/{id}/{version_id}/{is_default}/{is_activated}`

#### Parameters

Key | Description
--- | -----------
**id**<br/>string | The unique identifier for the Flow
**version_id**<br/>string | The unique identifier for the Flow Version
**is_default**<br/>boolean | Indicates if this Flow SnapShot should be the default version for running users.
**is_activated**<br/>boolean | Indicates if this Flow ShapShot is accessible to running users to run.


### Reverting a Flow SnapShot

> Example 200 OK Response

```json
{
  "dateCreated": "0001-01-00T00:00:00Z",
  "dateModified": "0001-01-00T00:00:00Z",
  "whoCreated": null,
  "whoModified": null,
  "whoOwner": null,
  "alertEmail": null,
  "isActive": true,
  "isDefault": true,
  "comment": "First attempt at creating the Flow",
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
  },
  "groupElements": null,
  "mapElements": null,
  "navigationElements": null,
  "pageElements": null,
  "tagElements": null,
  "macroElements": null,
  "valueElements": null,
  "typeElements": null,
  "serviceElements": null
}
```

Used to take an Flow SnapShot and apply it to the current Flow being modelled. This is equivalent to undoing changes to a Flow for Flow Builders. To revert a Flow SnapShot for running users, simply activate and make default the appropriate previous Flow SnapShot version. The Flow SnapShot object is the package that is sent to the Platform runtime engine.

#### HTTP Request

`POST /api/draw/1/flow/revert/{id}/{version_id}`

#### Parameters

Key | Description
--- | -----------
**id**<br/>string | The unique identifier for the Flow
**version_id**<br/>string | The unique identifier for the Flow Version

<aside class="warning">
<b>Warning</b><br/>
If the Flow being actively edited by Flow Builders does not have a Flow SnapShot, all changes will be lost. The Platform can only recover old Flow versions from SnapShots.
</aside>
