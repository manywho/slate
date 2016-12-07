## Flow States

> Flow State JSON:

```json
{
  "id": "{id}",
  "parentId": null,
  "dateCreated": "0001-01-00T00:00:00Z",
  "dateModified": "0001-01-01T00:00:00Z",
  "currentFlowId": {
    "id": "{id}",
    "versionId": "{id}"
  },
  "currentFlowDeveloperName": "Customer Application",
  "currentMapElementId": "{id}",
  "currentMapElementDeveloperName": "Reviewing Application",
  "currentStreamId": null,
  "currentRunningUserId": "{id}",
  "currentRunningUserEmail": "paul.smith@mycompany.com",
  "externalIdentifier": null,
  "manywhoTenantId": "{id}",
  "annotations": null,
  "stateEntries": null,
  "precommitStateEntry": {
    "id": "{id}",
    "flowId": {
      "id": "{id}",
      "versionId": "{id}"
    },
    "flowDeveloperName": null,
    "mapElementId": "{id}",
    "mapElementDeveloperName": null,
    "dateCommitted": "0001-01-01T00:00:00Z",
    "values": null,
    "userInteractions": [
      {
        "manywhoUserId": "{id}",
        "latitude": 0,
        "longitude": 0,
        "accuracy": 0,
        "altitude": 0,
        "altitudeAccuracy": 0,
        "heading": 0,
        "speed": 0,
        "time": "0001-01-01T00:00:00Z"
      }
    ]
  },
  "values": null,
  "authorizationHeader": null,
  "isDone": false,
  "log": null
}
```

*The Flow State object provides data about a specific instance of a running Flow.*

The Flow State provides in-depth information about how Users have interacted with the Flow, from the data that has been collected in Values, to the path of Map Elements that were travelled, to the users who have interacted with the Flow at the various stages of its execution. This Flow State data is only available for active Flows that have not yet completed. This API should also not be used for reporting purposes as we have a separate reporting API and reporting infrastructure.

### Get Flow States

> Example 200 OK Response

```json
{
  "_meta": {
    "total": 269,
    "pageSize": 1,
    "page": 1
  },
  "_links": {
    "previous": null,
    "next": "/api/admin/1/states/?page=2",
    "first": "/api/admin/1/states/?page=1",
    "last": "/api/admin/1/states/?page=27"
  },
  "items": [
    {
      "id": "0128d523-1001-450d-ae1c-38f4aee01158",
      "parentId": null,
      "dateCreated": "2015-10-23T10:44:44Z",
      "dateModified": "2015-10-23T10:44:47Z",
      "currentFlowId": {
        "id": "fb382ebd-6560-424d-bfe2-b718680d71ec",
        "versionId": "fbb83828-e5ec-4e63-aed4-45d0f838bd94"
      },
      "currentFlowDeveloperName": "Customer Application",
      "currentMapElementId": "6531a010-503f-4479-bbce-e39c05db314f",
      "currentMapElementDeveloperName": "Reviewing Application",
      "currentStreamId": null,
      "currentRunningUserId": "52df1a90-3826-4508-b7c2-cde8aa5b72cf",
      "currentRunningUserEmail": "paul.smith@mycompany.com",
      "externalIdentifier": null,
      "manywhoTenantId": "a692def4-5aba-49e4-b07d-cb32ed72c414",
      "annotations": null,
      "stateEntries": null,
      "precommitStateEntry": {
        "id": "e98ea86e-f090-4c7d-bef8-293209f45799",
        "flowId": {
          "id": "fb382ebd-6560-424d-bfe2-b718680d71ec",
          "versionId": "fbb83828-e5ec-4e63-aed4-45d0f838bd94"
        },
        "flowDeveloperName": null,
        "mapElementId": "6531a010-503f-4479-bbce-e39c05db314f",
        "mapElementDeveloperName": null,
        "dateCommitted": "0001-01-01T00:00:00Z",
        "values": null,
        "userInteractions": [
          {
            "manywhoUserId": "52df1a90-3826-4508-b7c2-cde8aa5b72cf",
            "latitude": 0,
            "longitude": 0,
            "accuracy": 0,
            "altitude": 0,
            "altitudeAccuracy": 0,
            "heading": 0,
            "speed": 0,
            "time": "2015-10-23T10:44:47Z"
          }
        ]
      },
      "values": null,
      "authorizationHeader": null,
      "isDone": false,
      "log": null
    }
  ]
}
```

Used to get the list of all persisted Flow States for the Tenant.

#### HTTP Request

`GET /api/admin/1/states?pageSize=10&page=1`

#### Parameters

Key | Description
--- | -----------
**pageSize**<br/>integer | The number of Flow State records to return in this request.
**page**<br/>integer | The current page of Flow State records.


### Get Flow States by Flow

> Example 200 OK Response

```json
{
  "_meta": {
    "total": 269,
    "pageSize": 1,
    "page": 1
  },
  "_links": {
    "previous": null,
    "next": "/api/admin/1/states/?page=2",
    "first": "/api/admin/1/states/?page=1",
    "last": "/api/admin/1/states/?page=27"
  },
  "items": [
    {
      "id": "0128d523-1001-450d-ae1c-38f4aee01158",
      "parentId": null,
      "dateCreated": "2015-10-23T10:44:44Z",
      "dateModified": "2015-10-23T10:44:47Z",
      "currentFlowId": {
        "id": "fb382ebd-6560-424d-bfe2-b718680d71ec",
        "versionId": "fbb83828-e5ec-4e63-aed4-45d0f838bd94"
      },
      "currentFlowDeveloperName": "Customer Application",
      "currentMapElementId": "6531a010-503f-4479-bbce-e39c05db314f",
      "currentMapElementDeveloperName": "Reviewing Application",
      "currentStreamId": null,
      "currentRunningUserId": "52df1a90-3826-4508-b7c2-cde8aa5b72cf",
      "currentRunningUserEmail": "paul.smith@mycompany.com",
      "externalIdentifier": null,
      "manywhoTenantId": "a692def4-5aba-49e4-b07d-cb32ed72c414",
      "annotations": null,
      "stateEntries": null,
      "precommitStateEntry": {
        "id": "e98ea86e-f090-4c7d-bef8-293209f45799",
        "flowId": {
          "id": "fb382ebd-6560-424d-bfe2-b718680d71ec",
          "versionId": "fbb83828-e5ec-4e63-aed4-45d0f838bd94"
        },
        "flowDeveloperName": null,
        "mapElementId": "6531a010-503f-4479-bbce-e39c05db314f",
        "mapElementDeveloperName": null,
        "dateCommitted": "0001-01-01T00:00:00Z",
        "values": null,
        "userInteractions": [
          {
            "manywhoUserId": "52df1a90-3826-4508-b7c2-cde8aa5b72cf",
            "latitude": 0,
            "longitude": 0,
            "accuracy": 0,
            "altitude": 0,
            "altitudeAccuracy": 0,
            "heading": 0,
            "speed": 0,
            "time": "2015-10-23T10:44:47Z"
          }
        ]
      },
      "values": null,
      "authorizationHeader": null,
      "isDone": false,
      "log": null
    }
  ]
}
```

Used to get the list of all persisted Flow States for the Tenant and specific Flow.

#### HTTP Request

`GET /api/admin/1/states/flow/{flow_id}/{flow_version_id}?pageSize=10&page=1`

#### Parameters

Key | Description
--- | -----------
**flow_id**<br/>string | Unique identifier for the Flow.
**flow_version_id**<br/>string | Unique identifier for the Flow Version. If this part of the path is not included, Flow States for all versions will be returned.
**pageSize**<br/>integer | The number of Flow State objects to return in this request.
**page**<br/>integer | The current page of Flow State objects.


### Get Flow State

> Example 200 OK Response

```json
{
  "id": "0128d523-1001-450d-ae1c-38f4aee01158",
  "parentId": null,
  "dateCreated": "2015-10-23T10:44:44Z",
  "dateModified": "2015-10-23T10:44:47Z",
  "currentFlowId": {
    "id": "fb382ebd-6560-424d-bfe2-b718680d71ec",
    "versionId": "fbb83828-e5ec-4e63-aed4-45d0f838bd94"
  },
  "currentFlowDeveloperName": "Customer Application",
  "currentMapElementId": "6531a010-503f-4479-bbce-e39c05db314f",
  "currentMapElementDeveloperName": "Reviewing Application",
  "currentStreamId": null,
  "currentRunningUserId": "52df1a90-3826-4508-b7c2-cde8aa5b72cf",
  "currentRunningUserEmail": "paul.smith@mycompany.com",
  "externalIdentifier": null,
  "manywhoTenantId": "a692def4-5aba-49e4-b07d-cb32ed72c414",
  "annotations": null,
  "stateEntries": null,
  "precommitStateEntry": {
    "id": "e98ea86e-f090-4c7d-bef8-293209f45799",
    "flowId": {
      "id": "fb382ebd-6560-424d-bfe2-b718680d71ec",
      "versionId": "fbb83828-e5ec-4e63-aed4-45d0f838bd94"
    },
    "flowDeveloperName": null,
    "mapElementId": "6531a010-503f-4479-bbce-e39c05db314f",
    "mapElementDeveloperName": null,
    "dateCommitted": "0001-01-01T00:00:00Z",
    "values": null,
    "userInteractions": [
      {
        "manywhoUserId": "52df1a90-3826-4508-b7c2-cde8aa5b72cf",
        "latitude": 0,
        "longitude": 0,
        "accuracy": 0,
        "altitude": 0,
        "altitudeAccuracy": 0,
        "heading": 0,
        "speed": 0,
        "time": "2015-10-23T10:44:47Z"
      }
    ]
  },
  "values": null,
  "authorizationHeader": null,
  "isDone": false,
  "log": null
}
```

Used to get an individual Flow State object.

#### HTTP Request

`GET /api/admin/1/states/{id}`

#### Parameters

Key | Description
--- | -----------
**id**<br/>string | Unique identifier for the State.


### Delete Flow State

> Success 204 No Content Response

Used to delete an individual State object.

#### HTTP Request

`DELETE /api/admin/1/states/{id}`

#### Parameters

Key | Description
--- | -----------
**id**<br/>string | Unique identifier for the Flow State.


### Delete Multiple Flow States

> Flow State Identifiers array JSON:

```json
[
  "{id}",
  "{id}"
]
```

Used to delete multiple Flow State objects.

#### HTTP Request

`DELETE /api/admin/1/states`

#### Body

The raw JSON for the array of Flow State identifiers.

#### Flow State Identifiers array

Key | Description
--- | -----------
**id**<br/>array | An array of unique identifiers for each Flow State.
