## Assets

### Lists all Assets

> Example 200 OK Response

```json
[
    {
        "contentType": null,
        "key": "bbeb742d-b6ea-402a-9578-c2cb7dd0ffa2/image.png",
        "modifiedAt": "2017-07-27T05:22:48+00:00",
        "name": null,
        "publicUrl": "https://files-manywho-com.s3.amazonaws.com/bbeb742d-b6ea-402a-9578-c2cb7dd0ffa2/image.png",
        "size": 2248160
    },
    {
        "contentType": null,
        "key": "bbeb742d-b6ea-402a-9578-c2cb7dd0ffa2/player.css",
        "modifiedAt": "2017-08-08T09:47:45+00:00",
        "name": null,
        "publicUrl": "https://files-manywho-com.s3.amazonaws.com/bbeb742d-b6ea-402a-9578-c2cb7dd0ffa2/player.css",
        "size": 96755
    }
]
```

Used to get a list of all the assets that exist for a Tenant.

#### HTTP Request

`GET /api/draw/1/assets`

### Create Folder

> 204 No Content

Used to create an empty folder.

#### HTTP Request

`POST /api/draw/1/assets`

#### Body

```json
{
    "key": "folder1/folder2"
}
```

### Delete Asset

> 204 No Content

Used to delete an asset (or a folder)

#### HTTP Request

`POST /api/draw/1/assets`

#### Body

```json
{
    "key": "folder1/folder2/key.png"
}
```

### Move Asset

> 204 No Content

Used to move an asset (or a folder)

#### HTTP Request

`PUT /api/draw/1/assets`

#### Body

```json
{
    "oldKey": "folder1",
    "newKey": "folder2"
}
```

### Upload Asset

> 204 No Content

Used to generate a signed upload URL, which should be used to submit the asset to (using `PUT`). A `contentType` is required in this request.

#### HTTP Request

`POST /api/draw/1/assets/upload`

#### Body

```json
{
    "contentType": "image/png",
    "key": "folder1/folder2/key.png"
}
```