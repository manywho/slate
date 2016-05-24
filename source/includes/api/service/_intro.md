# Service

## Requests

### Get Requests

#### HTTP Request

`GET /api/service/1/requests`

### Get Request

#### HTTP Request

`GET /api/service/1/requests/{id}`

### Get Requests by Flow

#### HTTP Request

`GET /api/service/1/requests/flow/{flow_id}`

### Get Requests by Flow Version

#### HTTP Request

`GET /api/service/1/requests/flow/{flow_id}/{flow_version_id}`

### Get Requests by Flow State

#### HTTP Request

`GET /api/service/1/requests/state/{state_id}`

### Retry Request

#### HTTP Request

`POST /api/service/1/requests/{id}/retry`


## Data

### Get Data from Service

#### HTTP Request

`POST /api/service/1/data`


## Files

### Get Files from Service

#### HTTP Request

`POST /api/service/1/file`

### Upload File to Service

#### HTTP Request

`POST /api/service/1/file/content`

### Delete File from Service

#### HTTP Request

`POST /api/service/1/file/delete`
