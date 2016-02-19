## Tag Element

> Example Request:

```json
{
  "contentType": "ContentObject",
  "typeElementId": "{id}",
  "updateByName": false,
  "id": "{id}",
  "elementType": "TAG",
  "developerName": "Car Details",
  "developerSummary": "Information needed to render a 3D view of a car so we can get the color selection."
}
```

*The Tag Element object provides additional runtime data to your Page Element Containers/Components and Navigation Elements/Items.*

The purpose of the Tag Element is to add flexibility to your Flow application user experience. The components, containers and navigation items in your Flow can benefit from having access to the Flow State to get more contextual information. For example, if you have a numeric input field, it may be useful to know the possible range or numeric values that can be provided by the end user - where that range depends on logic in the Flow. The components, containers and navigation items also supports "attributes" and these are often sufficient for many use-cases. As a result, only use the Tag Element if you need information that is very specific to the Flow State for particular running user(s). The base properties of the Tag Element are outlined here.

#### Page Element

Key | Description
--- | -----------
**id**<br/>string | A unique identifier field assigned by the platform. This value should not be included for new Tag Elements.
**elementType**<br/>string | A unique element type for the Tag Element. Valid values are:<ul><li>**TAG**: Tag Element</li></ul>
**developerName**<br/>string | The name for the Tag Element. This is typically a helpful name to remind builders of the purpose of the Tag Element.
**developerSummary**<br/>string | The summary for the Tag Element. This is typically additional information that will help explain the purpose of the Tag Element.
**contentType**<br/>string | The content type represented by the Tag Element. Valid values are:<ul><li>**ContentString**: A string value</li><li>**ContentNumber**: A numeric value</li><li>**ContentPassword**: A hidden value</li><li>**ContentDateTime**: A date and time value</li><li>**ContentContent**: A rich content value</li><li>**ContentObject**: An object value</li><li>**ContentList**: A list value</li></ul>
**typeElementId**<br/>string | The Type of the Object or List value being provided. This is only needed if the contentType property is set to ContentObject or ContentList.
**updateByName**<br/>boolean | When working with Tag Element objects through the modeling API, this setting should be set to true if you do not have a unique identifier for a Tag Element but wish to update any Tag Element in the system that has this same name. This key is typically only used when scripting updates to Flows as part of a migration tool.


### Create/Update Tag Elements

> Example 200 OK Response

```json
{
  "dateCreated": "0001-01-01T00:00:00Z",
  "dateModified": "0001-01-01T00:00:00Z",
  "whoCreated": null,
  "whoModified": null,
  "whoOwner": null,
  "contentType": "ContentObject",
  "typeElementId": "2b0886ce-e922-452d-937b-97e75778d557",
  "updateByName": false,
  "id": "8bf1fb42-5d5a-473b-b5bf-099305233672",
  "elementType": "TAG",
  "developerName": "Car Details",
  "developerSummary": "Information needed to render a 3D view of a car so we can get the color selection."
}
```

Used to create new Tag Element objects or update existing ones. The Tag Element object provides additional runtime data to your Page Element Containers/Components and Navigation Elements/Items.

#### HTTP Request

`POST /api/draw/1/element/tag`

#### Body

The raw JSON for the Tag Element.

<aside class="notice">
<b>Create vs Update</b><br/>
If the "id" property is included in the request, the platform will update the Element with the matching unique identifier. If the "updateByName" property is set to true, the platform will update the Element with the matching "developerName" property.
</aside>


### Import Tag Element

Used to import an existing Tag Element object into a Flow. The Tag Element object provides additional runtime data to your Page Element Containers/Components and Navigation Elements/Items.

#### HTTP Request

`POST /api/draw/1/element/flow/{flow_id}/tag/{id}`

#### Parameters

Key | Description
--- | -----------
**flow_id**<br/>string | Unique identifier for the Flow
**id**<br/>string | The unique identifier for the Tag Element


### Query Tag Elements

> Example 200 OK Response

```json
[
  {
    "dateCreated": "0001-01-01T00:00:00Z",
    "dateModified": "0001-01-01T00:00:00Z",
    "whoCreated": null,
    "whoModified": null,
    "whoOwner": null,
    "contentType": "ContentObject",
    "typeElementId": "2b0886ce-e922-452d-937b-97e75778d557",
    "updateByName": false,
    "id": "8bf1fb42-5d5a-473b-b5bf-099305233672",
    "elementType": "TAG",
    "developerName": "Car Details",
    "developerSummary": "Information needed to render a 3D view of a car so we can get the color selection."
  }
]
```

Used to filter existing Tag Element objects. The Tag Element object provides additional runtime data to your Page Element Containers/Components and Navigation Elements/Items.

#### HTTP Request

`GET /api/draw/1/element/tag?filter={filter}`

#### Parameters

Key | Description
--- | -----------
**filter**<br/>string | The filter for querying Tag Elements


### Get Tag Element

> Example 200 OK Response

```json
{
  "dateCreated": "0001-01-01T00:00:00Z",
  "dateModified": "0001-01-01T00:00:00Z",
  "whoCreated": null,
  "whoModified": null,
  "whoOwner": null,
  "contentType": "ContentObject",
  "typeElementId": "2b0886ce-e922-452d-937b-97e75778d557",
  "updateByName": false,
  "id": "8bf1fb42-5d5a-473b-b5bf-099305233672",
  "elementType": "TAG",
  "developerName": "Car Details",
  "developerSummary": "Information needed to render a 3D view of a car so we can get the color selection."
}
```

Used to get an existing Tag Element object. The Tag Element object provides additional runtime data to your Page Element Containers/Components and Navigation Elements/Items.

#### HTTP Request

`GET /api/draw/1/element/tag/{id}`

#### Parameters

Key | Description
--- | -----------
**id**<br/>string | The unique identifier for the Tag Element


### Delete Tag Element

> Success 204 No Content Response

Used to delete an existing Tag Element object. The Tag Element object provides additional runtime data to your Page Element Containers/Components and Navigation Elements/Items.

#### HTTP Request

`DELETE /api/draw/1/element/tag/{id}`

#### Parameters

Key | Description
--- | -----------
**id**<br/>string | The unique identifier for the Tag Element