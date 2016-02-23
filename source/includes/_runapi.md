# Run API

## Authenticating Running Users

### Get Authentication Context

#### HTTP Request

`GET /api/run/1/authentication/{state_id}`


### Basic Authentication

#### HTTP Request

`GET /api/run/1/authentication/{state_id}`


### OAuth2 Authentication

#### HTTP Request

`GET /api/run/1/oauth2`


## Flow

### Query Flows

#### HTTP Request

`GET /api/run/1/flow?filter={filter}`


### Get Flow

#### HTTP Request

`GET /api/run/1/flow/{id}`


### Get Flow by Name

#### HTTP Request

`GET /api/run/1/flow/name/{name}`


## Flow State

### Initialize Flow State

#### HTTP Request

`POST /api/run/1`

### Invoke Flow State

#### HTTP Request

`POST /api/run/1/state/{id}`

### Join Flow State

#### HTTP Request

`GET /api/run/1/state/{state_id}`

### Flow Out

#### HTTP Request

`POST /api/run/1/state/out/{state_id}/{outcome_id}`

### Check Flow State Changes

#### HTTP Request

`GET /api/run/1/state/{state_id}/ping/{state_token}`

### Delete Flow State

#### HTTP Request

`DELETE /api/run/1/state/{id}`


## Navigation

### Get Navigation

#### HTTP Request

`GET /api/run/1/navigation/{state_id}`


## Flow Graph

### Get Flow Graph

#### HTTP Request

`GET /api/run/1/graph/flow/{state_id}`


## Flow State Values

### Get Flow State Values

#### HTTP Request

`GET /api/run/1/state/{state_id}/values`

### Get Flow State Value

#### HTTP Request

`GET /api/run/1/state/{state_id}/values/{id}`

### Get Flow State Value by Name

#### HTTP Request

`POST /api/run/1/state/{state_id}/values/name/{name}`

### Set Flow State Values

#### HTTP Request

`POST /api/run/1/state/{state_id}/values`


## Response

#### HTTP Request

`POST /api/run/1/response`


## Event

#### HTTP Request

`POST /api/run/1/event`


## Share

### Get Sharing Users

#### HTTP Request

`GET /api/run/1/state/{state_id}/share?filter={filter}`


### Add Sharing User

#### HTTP Request

`POST /api/run/1/state/{state_id}/share`


### Remove Sharing User

#### HTTP Request

`DELETE /api/run/1/state/{state_id}/share/{id}`


## State Listener/Webhook

### Add Listener

#### HTTP Request

`POST /api/run/1/state/{state_id}/listener`


### Remove Listener

#### HTTP Request

`DELETE /api/run/1/state/{state_id}/listener/{id}`


## Package State

### Export

#### HTTP Request

`GET /api/run/1/state/package/{state_id}`

### Import

#### HTTP Request

`POST /api/run/1/state/package`
