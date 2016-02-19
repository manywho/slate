# Translate API


## Content Value Cultures

### Create/Update Content Value Culture

#### HTTP Request

`POST /api/translate/1/culture`


### Get Content Value Cultures

#### HTTP Request

`GET /api/translate/1/culture`


### Get Content Value Culture

#### HTTP Request

`GET /api/translate/1/culture/{id}`


### Delete Content Value Culture

#### HTTP Request

`DELETE /api/translate/1/culture/{id}`


## Flow Translation

### Get Flows for Translation

#### HTTP Request

`GET /api/translate/1/flow?filter={filter}`

### Get Flow Translation

#### HTTP Request

`GET /api/translate/1/flow/{id}`


## Page Element Translation

### Get Page Element Translation

#### HTTP Request

`GET /api/translate/1/element/page/{id}`


### Update Page Element Translation

#### HTTP Request

`POST /api/translate/1/element/page`


## Value Element Translation

### Get Value Element Translation

#### HTTP Request

`GET /api/translate/1/element/value/{id}`


### Update Value Element Translation

#### HTTP Request

`POST /api/translate/1/element/value`


## Map Element Translation

### Get Map Element Translation

#### HTTP Request

`GET /api/translate/1/flow/{flow_id}/{editing_token}/element/map/{id}`


### Update Map Element Translation

#### HTTP Request

`POST /api/translate/1/flow/{flow_id}/{editing_token}/element/map`


## Navigation Element Translation

### Get Navigation Element Translation

#### HTTP Request

`GET /api/translate/1/flow/{flow_id}/{editing_token}/element/navigation/{id}`


### Update Navigation Element Translation

#### HTTP Request

`POST /api/translate/1/flow/{flow_id}/{editing_token}/element/navigation`
