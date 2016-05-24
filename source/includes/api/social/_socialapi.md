# Social

## Stream

### Create Stream

#### HTTP Request

`POST /api/social/1/{service_element_id}`

### Follow Stream

#### HTTP Request

`POST /api/social/1/stream/{stream_id}`

### Post Message to Stream

#### HTTP Request

`POST /api/social/1/stream/{stream_id}/message`

### Get Stream Messages

#### HTTP Request

`GET /api/social/1/stream/{stream_id}`

### Like Stream Message

#### HTTP Request

`POST /api/social/1/stream/{stream_id}/message`

### Delete Stream Message

#### HTTP Request

`DELETE /api/social/1/stream/{stream_id}/message/{message_id}`

### Upload File to Stream

#### HTTP Request

`POST /api/social/1/stream/{stream_id}/file`

### Delete Uploaded File

#### HTTP Request

`DELETE /api/social/1/stream/{stream_id}/file/{file_id}`


## User Info

### Get Current User Info

#### HTTP Request

`GET /api/social/1/stream/{stream_id}/user/me`

### Get User Info

#### HTTP Request

`GET /api/social/1/stream/{stream_id}/user/{id}`

### Get Stream Followers

#### HTTP Request

`GET /api/social/1/stream/{stream_id}/follower`


## Share

### Flow Link

#### HTTP Request

`POST /api/social/1/stream/{stream_id}/share`
