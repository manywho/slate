## Common Objects

#### GroupAuthorization

> Example JSON:

```json
{
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
}
```

*Set the authorization context for your Flow.*

The Group Authorization object is used to configure the authorization context of the Flow or a Group Element (Swimlane) in your Flow. The authorization context information that can be used is determined by the Service. Builders should refer to the documentation of the Service being used.

Key | Description
--- | -----------
**serviceElementId**<br/>string | The unique identifier for the Service that will be used to authenticate the running user(s).
**globalAuthenticationType**<br/>string | The type of authentication the Service should perform when validating the running user(s). Valid values are:<ul><li>**PUBLIC**: All users can gain access to the Flow. If a Group Element is set to PUBLIC, the Flow must also be PUBLIC as the permissions cascade.</li><li>**ALL_USERS**: All users within the Service directory can gain access to the Flow or Group Element.</li><li>**SPECIFIED**: All users within the Service directory can gain access to the Flow or Group dependent on the specified configuration of users, groups, and/or locations.</li></ul>
**streamBehaviourType**<br/>string | On entry into this Group Authorization the following operations can be performed on a stream (e.g. social feed like Chatter):<ul><li>**USE_EXISTING**: Use an existing collaboration stream when the user enters, or create a new one if one does not yet exist.</li><li>**CREATE_NEW**: Create a new collaboration stream every time the user enters.</li><li>**NONE**: Do not provide a collaboration stream for this Group Authorization.</li></ul>
**groups**<br/>array | The array of Groups that the running user(s) must be a member to gain access. Each Group entry has the following keys:<br/><br/>**authenticationId** (string):<br/>The unique identifier for the Group, as specified by the Service directory.<br/><br/>**attribute** (string):<br/>The unique name for the Group attribute. E.g. MEMBER.
**users**<br/>array | The array of Users that the running user(s) must be a member to gain access. Each Group entry has the following keys:<br/><br/>**authenticationId** (string):<br/>The unique identifier for the User, as specified by the Service directory.<br/><br/>**attribute** (string):<br/>The unique name for the User attribute. E.g. DELEGATES.<br/><br/>**runningUser** (boolean):<br/>Indicates that the first person who has accessed this Group Authorization should act as the reference point with respect to the above attribute.
**locations**<br/>array | (reserved for future development)


#### ObjectDataRequest

> Example JSON:

```json
{
  "objectDataRequest": {
    "typeElementId": "{id}",
    "typeElementBindingId": "{id}",
    "listFilter": {
      "filterId": {
        "id": "{id}",
        "typeElementPropertyId": {id},
        "command": null
      },
      "comparisonType": "AND",
      "where": [
        {
          "columnTypeElementPropertyId": "{id}",
          "criteriaType": "EQUAL",
          "valueElementToReferenceId": {
            "id": "{id}",
            "typeElementPropertyId": "{id}",
            "command": null
          }
        }
      ],
      "orderByTypeElementPropertyId": "{id}",
      "orderByDirectionType": "DESC",
      "limit": 250,
      "filterByProvidedObjects": false
    },
    "command": {
      "commandType": null,
      "properties": {
        "key1": "value1",
        "key2": "value2"
      }
    }
  }
}
```

*Performing data operations on a Service.*

The Object Data Request object is used in a couple of places in the platform to configure save, load, and/or delete operations on a Service. In particular, this object is used:

* in Data Actions as part of a Map Element, or
* to load data into a Page/Layout component such as a table or combobox.

The goal of the Object Data Request object is to provide a standard notation for managing data, without creating strong dependencies with the underlying Service and the various approaches for handling data (e.g. SQL vs SOQL vs ZOQL, etc).

The base configuration of the Object Data Request object is outlined below:

Key | Description
--- | -----------
**typeElementId**<br/>string | The unique identifier for the Type of data being referenced in the underlying Service. E.g. the unique identifier for the "Account" Type is using the Salesforce Service.
**typeElementBindingId**<br/>string | The unique identifier for the specific binding that should be used for the chosen Type. Each Type can have a set of bindings which map the data in your Flow Values back to the underlying fields in the Service. E.g. an "Account" Type could have a binding for the Salesforce Service and also a binding for the Exact Target Service. The structure of the Type may be the same, but the data would be stored in different fields depending on the selected Service.

In addition to the above keys, the Object Data Request object also supports a "listFilter" key. This is used for LOAD operations when a sub-set of data is needed:

##### ListFilter

Key | Description
--- | -----------
**filterId**<br/>object | The ValueElementId pointing to the Value that holds the unique identifier for a particular record. This option should only be used if you know the identifier of the record you wish to load from. This is basically a convenience option for scenarios where you do not wish to configure all of the "where" clauses and you know only one record will be returned. The platform will perform additional validation - e.g. if more than one record is returned the platform will throw an error.
**comparisonType**<br/>string | The type of comparison that should be used when evaluating the set of "where" entries. Valid values are:<ul><li>**AND**: Each "where" entry must be true for the object to be returned from the Service.</li><li>**OR**: Any "where" entry must be true for the object to be returned from the Service.</li></ul>
**where**<br/>array | The array of "where" entries needed to perform the filter. Each Where entry has the following keys:<br/><br/>**columnTypeElementPropertyId** (string):<br/>The unique identifier for the property in the Type that should be filtered by. E.g. for an "Account" Type, a property might be "Name".<br/><br/>**valueElementToReferenceId** (object):<br/>The ValueElementId pointing to the Value holding the actual data for the "where" entry. For example, if you have a Value that holds "Acme Inc." if filtering "Account" objects.<br/><br/>**criteriaType** (string):<br/>The type of criteria that should be used when evaluating the "where" entry. Valid values are:<ul><li>**EQUAL**: {column} is equal to {value}</li><li>**NOT_EQUAL**: {column} is not equal to {value}</li><li>**GREATER_THAN**: {column} is greater than {value}</li><li>**GREATER_THAN_OR_EQUAL**: {column} is greater than or equal to {value}</li><li>**LESS_THAN**: {column} is less than {value}</li><li>**LESS_THAN_OR_EQUAL**: {column} is less than or equal to {value}</li><li>**CONTAINS**: {column} contains the characters in {value}</li><li>**STARTS_WITH**: {column} starts with the characters in {value}</li><li>**ENDS_WITH**: {column} ends with the characters in {value}</li></ul>
**orderByTypeElementPropertyId**<br/>string | The unique identifier for the property in the Type that should be used for ordering. E.g. for an "Account" Type, a property might be "Name".
**orderByDirectionType**<br/>string | The direction in which to oder the results. Valid values are:<ul><li>**ASC**: Order the returned objects in ascending order based on the orderByTypeElementPropertyId.</li><li>**DESC**: Order the returned objects in descending order based on the orderByTypeElementPropertyId.</li></ul>
**limit**<br/>integer | The maximum number of objects that should be returned from the Service in this request. If the limit is set to zero, the Service will return all objects.
**filterByProvidedObjects**<br/>boolean | In various use-cases, it can be useful to "hydrate" a set of existing objects that have been gathered from the Service, but do not adhere to a simple query. Use this option when wishing to provide the set of objects that the Service should "hydrate" with the latest information for all properties.
**command**<br/>object | The command object can be used to perform implementation specific operations on a Service. As a result, the command object configuration varies depending on the Service. Builders should refer to the documentation of the Service being used. The Command object has the following keys:<br/><br/>**commandType** (string):<br/>The type of command being performed. E.g. for the Salesforce Service, this could be "SOQL".<br/><br/>**properties** (object):<br/>Key/value pairs that provide additional information for the command to be executed. E.g. for the Salesforce Service, this could be: "soql": "SELECT Max(Revenue) FROM Opportunity WHERE (CloseDate = NEXT_N_DAYS:365 OR Availability_Date__c <= TODAY)"


#### PageTag

> Example JSON:

```json
{
  
}
```

*Blah blah.*

Blah blah.


#### ValueElementId

> Example JSON:

```json
{
  "id": "{id}",
  "typeElementPropertyId": "{id}",
  "command": "GET_FIRST"
}
```

*References to Values in your Flow.*

The Value Element Id object is used in many places in the configuration of your Flow. All of the data used in your Flow is stored in Values. As a result, if you need to perform any operation using data:

* collected from the user in a Page/Layout,
* gathered from a Data Action, or
* input/output from a Message Action

you use the Value Element Id to tell the Flow which Value you're referring to. Value Element Id objects are indicated by JSON keys that start with "valueElement..."

Key | Description
--- | -----------
**id**<br/>string | The unique identifier of the Value being referenced. Every Value in your Flow has a unique identifier that never changes.
**typeElementPropertyId**<br/>string | For Values of Type Object or List, you can refer to specific properties. E.g. for an Object Value of Type "Account", a property might be "Name". If this key is null, the platform will assume you are referring to the whole Value. If this key contains a valid identifier for a property in the Type, the platform will refer to that particular property in the Object or List Value.
**command**<br/>string | As part of referencing or applying an operation to a Value, it is sometimes necessary to perform a command on that Value. Supported commands are:<ul><li>**ADD**: Adds an Object to a List Value. If the Object exists in the List, the Object is updated. If it is not already in the List, it's added.</li><li>**REMOVE**: Removes an Object from a List Value.</li><li>**GET_FIRST**: Gets the first Object from a List Value.</li><li>**GET_NEXT**: Gets the next Object from a List Value. List Values maintain a "pointer" so that each time the GET_NEXT command is executed in the Flow, the List Value remembers which is the next Value.</li><li>**FILTER**: Executes a filter on a List Value. For the FILTER command to execute correctly, additional properties must be provided.</li><li>**GET_LENGTH**: Gets the length of a List Value.</li><li>**NEW**: Creates a new instance of the Value.</li><li>**EMPTY**: Sets the Value equal to nothing.</li><li>**DETACH**: Removes the external identifier from the root Object so that it will not be "remembered" when updating Lists or saving back to a remote Service.</li></ul>
