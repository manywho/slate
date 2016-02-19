## Type Element

> Example Request:

```json
{
  "properties": [
    {
      "id": "{id}",
      "developerName": "Full Name",
      "contentType": "ContentString",
      "contentFormat": null,
      "typeElementId": "{id}",
      "typeElementDeveloperName": null
    },
    {
      "id": "{id}",
      "developerName": "Twitter Handle",
      "contentType": "ContentString",
      "contentFormat": null,
      "typeElementId": "{id}",
      "typeElementDeveloperName": null
    }
  ],
  "bindings": null,
  "updateByName": false,
  "serviceElementId": "{id}",
  "id": "{id}",
  "elementType": "TYPE",
  "developerName": "Customer",
  "developerSummary": "A custom Type for Customers."
}
```

*The Type Element object defines the structure of Objects and Lists in the Flow.*

The purpose of the Type Element is to allow Flow builders to determine the business objects that will be used in the Flow. Often the Type Elements are provided when the Flow builder installs a new Service Element, however, Flow builders can define their own Type Elements as needed to support the objectives of the Flow. The Type Element also provides the bindings back to the Service Elements that can save, read or delete data of the same structure. As a result, the Type Element maps from friendly business objects to underlying storage implementations as provided by the Service Element. The base properties of the Type Element are outlined here.

#### Type Element

Key | Description
--- | -----------
**id**<br/>string | A unique identifier field assigned by the platform. This value should not be included for new Value Elements.
**elementType**<br/>string | A unique element type for the Type Element. Valid values are:<ul><li>**TYPE**: Type Element</li></ul>
**developerName**<br/>string | The name for the Type Element. This is typically a helpful name to remind builders of the purpose of the Type Element.
**developerSummary**<br/>string | The summary for the Type Element. This is typically additional information that will help explain the purpose of the Type Element.
**serviceElementId**<br/>string | The Service Element associated with this Type Element. This property is assigned if the Type Element was provided as part of installing the Service Element. It also means the Service Element has control to update the Type Element as needed. If Flow builders want to manage the Type Element structure and bindings independently of a Service Element, this property should be set to null.
**properties**<br/>array | The array of Properties associated with this Type. These might be called "columns" or "fields" and represent the data that should be associated with this business object or Type Element. For example, for a Type of "address", the Properties might be "street", "city", "region", etc. Each Property entry has the following keys:<br/><br/>**id** (string): A unique identifier field assigned by the platform. This value should not be included for new Properties.<br/><br/>**developerName** (string): The name for the Property. This is typically a helpful name to remind builders of the purpose of the Property.<br/><br/>**contentType** (string):The content type represented by the Value Element. Valid values are:<ul><li>**ContentString**: A string value</li><li>**ContentNumber**: A numeric value</li><li>**ContentPassword**: A hidden value</li><li>**ContentDateTime**: A date and time value</li><li>**ContentContent**: A rich content value</li><li>**ContentObject**: An object value</li><li>**ContentList**: A list value</li></ul><br/>**contentFormat** (string): The formatting that should be applied to values in this Property.<br/><br/>**typeElementId** (string): The Type of the Object or List value associated with this Property. This is only needed if the contentType property is set to ContentObject or ContentList.<br/><br/>**typeElementDeveloperName** (string): The developerName of the Type (used when the id has not yet been assigned to the referenced Type).
**bindings**<br/>array | The configuration of the Bindings that provide the mapping of data stored in this Type with the an underlying Service Element implementation. See Bindings below for details.
**updateByName**<br/>boolean | When working with Type Element objects through the modeling API, this setting should be set to true if you do not have a unique identifier for a Type Element but wish to update any Type Element in the system that has this same name. This key is typically only used when scripting updates to Flows as part of a migration tool.

##### Bindings

> Example bindings JSON:

```json
  [
    {
      "id": "{id}",
      "developerName": "Salesforce.com Binding",
      "developerSummary": "Saves the Customer back to Salesforce",
      "databaseTableName": "Account",
      "serviceElementId": "{id}",
      "propertyBindings": [
        {
          "databaseFieldName": "FullName",
          "typeElementPropertyId": "{id}",
          "typeElementPropertyDeveloperName": "Full Name",
          "databaseContentType": "string"
        },
        {
          "databaseFieldName": "Twitter_Handle__c",
          "typeElementPropertyId": "{id}",
          "typeElementPropertyDeveloperName": "Twitter Handle",
          "databaseContentType": "string"
        }
      ]
    }
  ]
```

A Binding is used to map Properties in the Type to database fields in the Service. The mapping does not need to be directly to database tables in the Service, however, the binding should provide unique identifier information necessary for the Service Element to put the provided values back to the correct storage locations. The Binding is typically pre-configured as part of the Type installation process. However, it is possible for Flow builders to define Bindings manually.

Key | Description
--- | -----------
**id**<br/>string | A unique identifier field assigned by the platform. This value should not be included for new Bindings.
**developerName**<br/>string | The name for the Binding. This is typically a helpful name to remind builders of the purpose of the Binding.
**developerSummary**<br/>string | The summary for the Binding. This is typically additional information that will help explain the purpose of the Binding.
**databaseTableName**<br/>string | The name of the underlying mapped table that tells the Service Element where the data should be stored. At runtime, all data provided to the Service Element will use this name.
**serviceElementId**<br/>string | The Service Element associated with this Binding. This is the Service Element that will be called at runtime if this binding is specified by the Flow builder.
**propertyBindings**<br/>array | The array of Property Bindings associated with this Type. Each Property Binding maps from a Property to the underlying mapped field that tells the Service Element which field the data should be stored. At runtime, the Property Binding will be provided to the Service Element, not the Property developerName for the Type. Each Property Binding entry has the following keys:<br/><br/>**databaseFieldName**: The name of the field in the Service Element where the data should be stored.<br/><br/>**typeElementPropertyId**: The associated Property unique identifier where the data in the Flow State is being sourced.<br/><br/>**typeElementPropertyDeveloperName**: In situations where the typeElementPropertyId has not yet been assigned (as above), this is the developerName of the Property being sourced.<br/><br/>**databaseContentType**: The contentType of this field as provided by the Service Element.


### Create/Update Type Elements

> Example 200 OK Response

```json
{
  "properties": [
    {
      "id": "6bed9cba-499c-4d4f-a679-6ec0ea77e822",
      "developerName": "Full Name",
      "contentType": "ContentString",
      "contentFormat": null,
      "typeElementId": null,
      "typeElementDeveloperName": null
    },
    {
      "id": "e64fbe8a-33b9-42e9-8e1c-da4c460870af",
      "developerName": "Twitter Handle",
      "contentType": "ContentString",
      "contentFormat": null,
      "typeElementId": null,
      "typeElementDeveloperName": null
    }
  ],
  "bindings": [
    {
      "id": "22e2c289-f400-451d-b907-1f6b3458fb83",
      "developerName": "Salesforce.com Binding",
      "developerSummary": "Saves the Customer back to Salesforce",
      "databaseTableName": "Account",
      "serviceElementId": "11e2c289-f400-451d-b907-1f6b3458fb76",
      "propertyBindings": [
        {
          "databaseFieldName": "FullName",
          "typeElementPropertyId": "6bed9cba-499c-4d4f-a679-6ec0ea77e822",
          "typeElementPropertyDeveloperName": "Full Name",
          "databaseContentType": "string"
        },
        {
          "databaseFieldName": "Twitter_Handle__c",
          "typeElementPropertyId": "e64fbe8a-33b9-42e9-8e1c-da4c460870af",
          "typeElementPropertyDeveloperName": "Twitter Handle",
          "databaseContentType": "string"
        }
      ]
    }
  ],
  "updateByName": false,
  "serviceElementId": "11e2c289-f400-451d-b907-1f6b3458fb76",
  "id": "ed206576-c91c-426c-988b-76dd14752da7",
  "elementType": "TYPE",
  "developerName": "Customer",
  "developerSummary": "A custom Type for Customers."
}
```

Used to create new Type Element objects or update existing ones. The Type Element object defines the structure of Objects and Lists in the Flow.

#### HTTP Request

`POST /api/draw/1/element/type`

#### Body

The raw JSON for the Type Element.

<aside class="notice">
<b>Create vs Update</b><br/>
If the "id" property is included in the request, the platform will update the Element with the matching unique identifier. If the "updateByName" property is set to true, the platform will update the Element with the matching "developerName" property.
</aside>


### Import Type Element

Used to import an existing Type Element object into a Flow. The Type Element object defines the structure of Objects and Lists in the Flow.

#### HTTP Request

`POST /api/draw/1/element/flow/{flow_id}/type/{id}`

#### Parameters

Key | Description
--- | -----------
**flow_id**<br/>string | Unique identifier for the Flow
**id**<br/>string | The unique identifier for the Type Element


### Query Type Elements

> Example 200 OK Response

```json
[
  {
    "properties": null,
    "bindings": null,
    "updateByName": false,
    "serviceElementId": "11e2c289-f400-451d-b907-1f6b3458fb76",
    "id": "ed206576-c91c-426c-988b-76dd14752da7",
    "elementType": "TYPE",
    "developerName": "Customer",
    "developerSummary": "A custom Type for Customers."
  }
]
```

Used to filter existing Type Element objects. The Type Element object defines the structure of Objects and Lists in the Flow.

#### HTTP Request

`GET /api/draw/1/element/type?filter={filter}`

#### Parameters

Key | Description
--- | -----------
**filter**<br/>string | The filter for querying Type Elements


### Get Type Element

> Example 200 OK Response

```json
{
  "properties": [
    {
      "id": "6bed9cba-499c-4d4f-a679-6ec0ea77e822",
      "developerName": "Full Name",
      "contentType": "ContentString",
      "contentFormat": null,
      "typeElementId": null,
      "typeElementDeveloperName": null
    },
    {
      "id": "e64fbe8a-33b9-42e9-8e1c-da4c460870af",
      "developerName": "Twitter Handle",
      "contentType": "ContentString",
      "contentFormat": null,
      "typeElementId": null,
      "typeElementDeveloperName": null
    }
  ],
  "bindings": [
    {
      "id": "22e2c289-f400-451d-b907-1f6b3458fb83",
      "developerName": "Salesforce.com Binding",
      "developerSummary": "Saves the Customer back to Salesforce",
      "databaseTableName": "Account",
      "serviceElementId": "11e2c289-f400-451d-b907-1f6b3458fb76",
      "propertyBindings": [
        {
          "databaseFieldName": "FullName",
          "typeElementPropertyId": "6bed9cba-499c-4d4f-a679-6ec0ea77e822",
          "typeElementPropertyDeveloperName": "Full Name",
          "databaseContentType": "string"
        },
        {
          "databaseFieldName": "Twitter_Handle__c",
          "typeElementPropertyId": "e64fbe8a-33b9-42e9-8e1c-da4c460870af",
          "typeElementPropertyDeveloperName": "Twitter Handle",
          "databaseContentType": "string"
        }
      ]
    }
  ],
  "updateByName": false,
  "serviceElementId": "11e2c289-f400-451d-b907-1f6b3458fb76",
  "id": "ed206576-c91c-426c-988b-76dd14752da7",
  "elementType": "TYPE",
  "developerName": "Customer",
  "developerSummary": "A custom Type for Customers."
}
```

Used to get an existing Type Element object. The Type Element object defines the structure of Objects and Lists in the Flow.

#### HTTP Request

`GET /api/draw/1/element/type/{id}`

#### Parameters

Key | Description
--- | -----------
**id**<br/>string | The unique identifier for the Type Element


### Delete Type Element

> Success 204 No Content Response

Used to delete an existing Type Element object. The Type Element object defines the structure of Objects and Lists in the Flow.

#### HTTP Request

`DELETE /api/draw/1/element/type/{id}`

#### Parameters

Key | Description
--- | -----------
**id**<br/>string | The unique identifier for the Type Element