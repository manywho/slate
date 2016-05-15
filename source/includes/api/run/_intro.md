# Run API

The Run API provides all of the features of your executing Flow applications. When you build a Flow on the ManyWho Platform, it is exposed through this API:

1. The Player UI code works with this API to generate the Pages, Navigation, Outcomes, etc.
2. A number of Services, such as the Twilio Service, use this API to generate text-to-speech versions of the UI.
3. Asynchronous messages and Listeners use this API to notify the Flow State of events.
4. Applications can use this API to query Flows available to Run.
5. 3rd party applications can use this API to authenticate Users and we can also provide SSO solutions information about the various authenticating end-points.

The Run API is perhaps the most important part of the Platform as it represents everything that is needed to run your Flow applications.

## Authenticating Running Users

Authentication as an end user has a couple of layers. This is because Flows can be constructed to leverage multiple identity Services - but also because we don't always deny the user complete access if they are not authorized. It works like this:

- **Flow authentication**: When a Flow is created, the Flow Builder must define the overall authentication for the Flow and the directory the user must authenticate against to gain access. The authentication process can rely on specific user access, group access or location requirements. If the user cannot authenticated at the Flow level, they are denied all access to the running of the Flow.
- **Swimlane authentication**: During the execution of the Flow, the user may enter into a Swimlane element (which is a group of elements that have a particular authentication configuration that differs from the Flow. In this situation, the default behavior of our runtimes is that the user will not be excluded from the Flow and can continue to get status updates and collaborate. However, the user cannot view any pages or take any actions.

The engine will provide you with the authorization context as part of the response. The authorization context can then be used against our authentication API to log the user in to the correct directory to get the required authentication token. The authorization context object will be returned for initialization, execution and join requests on the engine. We do not return the authorization context for "response" requests as part of an asynchronous execution.

#### Authentication Context

Key | Description
--- | -----------
**directoryName**<br/>string | The name of the directory the running user needs to login to.
**directoryId**<br/>string | The unique identifier for the directory the running user needs to login to.
**loginUrl**<br/>string | The Url that should be used for authentication. For basic authentication, this Url should be provided in the authentication object. For OAuth2 authentication, the user should be re-directed to this Url to initiate the OAuth2 sequence.
**authenticationType**<br/>string | The type of authentication that should be performed. Valid values are:<ul><li>**USERNAME_PASSWORD**: The user should login using our authentication API using their username/password to authenticate.</li><li>**OAUTH2**: The user should login using OAuth2. If the user is redirected to to the loginUrl address, ManyWho already provides support for the OAuth2 sequence.</ul>

#### Authentication Request

{
  "loginUrl":"https://salesforce.manywho.com/plugins/api/salesforce/1/authentication",
  "username":"steve.wood@manywho.com",
  "password":"not tellin",
  "token":"ThAnK5Chuc4M0rt1m0r3",
  "sessionToken":null,
  "sessionUrl":null,
  "instanceUrl":null
}


Key | Description
--- | -----------
**loginUrl**<br/>string | The loginUrl provided in the Authentication Context.
**username**<br/>string | The username for the running user for the particular underlying Service/Directory.
**password**<br/>string | The password for the running user for the particular underlying Service/Directory.
**token**<br/>string | An optional token to augment the username/password that may be required by the underlying Service/Directory.
**sessionToken**<br/>string | An existing session token for the underlying Service/Directory.
**sessionUrl**<br/>string | An existing session url for the underlying Service/Directory.
**instanceUrl**<br/>string | An existing instance for which the session information is associated.

### Get Authentication Context

> Example 200 OK Response

```json
{
  "directoryName":"ManyWho",
  "directoryId":"00DE0000000XtGrPLC",
  "loginUrl":"https://salesforce.manywho.com/plugins/api/salesforce/1/authentication"
  "authenticationType": "USERNAME_PASSWORD"
}
```

When you initialize a Flow, you are provided with the authentication context in the response. However, you can also retrieve and login to Services individually. It's important to note that despite authentication being done against a Flow state, the returned Runtime Authentication Token is valid across all Flow States. 

<aside class="notice">
<b>Re-using Authentication Tokens</b><br/>
There's no need to login each time the user starts a Flow once you have a valid Runtime Authentication Token. However, if you are not logged into all Services that require login, you will be prompted accordingly or those API calls will fail.
</aside>

#### HTTP Request

`GET /api/run/1/authentication/{state_id}?serviceElementId={service_element_id}`

#### Parameters

Key | Description
--- | -----------
**state_id**<br/>string | The unique identifier for an active Flow State that is associated with the Service the runtime user wants to authenticate against.
**service_element_id**<br/>string | The unique identifier for the Service Element providing the authentication.

### Basic Authentication

> Example 200 OK Response

```json
majqgTJf%2fffzUTTQZ2EhyikQanT%2b8j8SgBz%2furxCPJDYzUiYPdrYXBW3LB0AhdFd5%2b3c8AIcNG6L6AuI6nE4Lk48jwF35sX9DpuMBLRIzUM%3d
```

This API is typically used if the underlying Service/Directory does not currently support OAuth2 for authentication. However, it can also be used for session based authentication where the user already has an active authenticated session token and simply wants to re-use it to speed authentication - but also allow SSO.

<aside class="notice">
<b>Services</b><br/>
It's important to reference the documentation for the Service being used. The options available very much depend on the implementation of the Service.
</aside>

#### HTTP Request

`POST /api/run/1/authentication/{state_id}`

#### Parameters

Key | Description
--- | -----------
**state_id**<br/>string | The unique identifier for an active Flow State that is associated with the Service the runtime user wants to authenticate against.

#### Body

The raw JSON for the Map Element.

### OAuth2 Authentication

The OAuth2 API is not typically used directly. This API is the Callback URL that should be configured in the identity providing Service that will be performing the OAuth2 login. This API supports the standard OAuth2 parameters as part of the callback sequence.

#### HTTP Request

`GET /api/run/1/oauth2`

## Flow

As part of the Run API, integrated applications can query for the list of available Flow applications and can get basic details about how to access them.

### Query Flows

> Example 200 OK Response

```json
[
    {
        "dateCreated": "2016-03-10T22:35:42Z",
        "dateModified": "2016-03-26T06:14:01Z",
        "whoCreated": {
            "id": "914e2919-4c72-4b75-853e-85e060d49380",
            "firstName": "Paul",
            "lastName": "Smith",
            "email": "paul.smith@manywho.com",
            "username": null,
            "verified": false
        },
        "whoModified": {
            "id": "914e2919-4c72-4b75-853e-85e060d49380",
            "firstName": "Paul",
            "lastName": "Smith",
            "email": "paul.smith@manywho.com",
            "username": null,
            "verified": false
        },
        "whoOwner": {
            "id": "914e2919-4c72-4b75-853e-85e060d49380",
            "firstName": "Paul",
            "lastName": "Smith",
            "email": "paul.smith@manywho.com",
            "username": null,
            "verified": false
        },
        "alertEmail": null,
        "isActive": true,
        "isDefault": true,
        "comment": null,
        "editingToken": null,
        "id": {
            "id": "9a563d47-fa58-4a27-b633-f1fd6898ed07",
            "versionId": "85c93559-352d-4dfe-8c62-252e52003355"
        },
        "developerName": "Account Manager",
        "developerSummary": "",
        "startMapElementId": "4cfebe7e-f3a6-4379-94b0-a5a7285bd529",
        "allowJumping": true,
        "stateExpirationLength": 0,
        "authorization": null
    },
    {
        "dateCreated": "2015-11-30T04:44:34Z",
        "dateModified": "2016-03-26T07:05:22Z",
        "whoCreated": {
            "id": "914e2919-4c72-4b75-853e-85e060d49380",
            "firstName": "Paul",
            "lastName": "Smith",
            "email": "paul.smith@manywho.com",
            "username": null,
            "verified": false
        },
        "whoModified": {
            "id": "914e2919-4c72-4b75-853e-85e060d49380",
            "firstName": "Paul",
            "lastName": "Smith",
            "email": "paul.smith@manywho.com",
            "username": null,
            "verified": false
        },
        "whoOwner": {
            "id": "914e2919-4c72-4b75-853e-85e060d49380",
            "firstName": "Paul",
            "lastName": "Smith",
            "email": "paul.smith@manywho.com",
            "username": null,
            "verified": false
        },
        "alertEmail": null,
        "isActive": true,
        "isDefault": true,
        "comment": null,
        "editingToken": null,
        "id": {
            "id": "3ca32f1c-0278-477b-9ce1-ff88210be747",
            "versionId": "175cf7fe-e1ff-4b83-89bb-9f3e21c4e634"
        },
        "developerName": "Task Manager",
        "developerSummary": "A demo app showing task management.",
        "startMapElementId": "9467970b-6f7e-48e3-9f8b-ced3a24c93c5",
        "allowJumping": true,
        "stateExpirationLength": 0,
        "authorization": null
    }
]
```

Used to filter existing Flow applications that are active/default (e.g. "Published").

<aside class="notice">
<b>Flow Response</b><br/>
You can reference the Draw API documentation for information on the structure of the Flow Response objects returned by this API
</aside>

#### HTTP Request

`GET /api/run/1/flow?filter={filter}`

#### Parameters

Key | Description
--- | -----------
**filter**<br/>string | The filter for querying Flows.

<aside class="notice">
<b>Filter</b><br/>
The filter can take the following formats:
<ul><li><b>developerName eq '{developer_name}'</b>: Filter the list of Elements where the "developerName" property exactly matches the provided developer name (case insensitive)</li><li><b>substringof(developerName, '{developer_name}')</b>: Filter the list of Elements where the "developerName" property partially matches the provided developer name (case insensitive)</li></ul>
</aside>

### Get Flow

> Example 200 OK Response

```json
{
    "dateCreated": "2015-11-30T04:44:34Z",
    "dateModified": "2016-03-26T07:05:22Z",
    "whoCreated": {
        "id": "914e2919-4c72-4b75-853e-85e060d49380",
        "firstName": "Paul",
        "lastName": "Smith",
        "email": "paul.smith@manywho.com",
        "username": null,
        "verified": false
    },
    "whoModified": {
        "id": "914e2919-4c72-4b75-853e-85e060d49380",
        "firstName": "Paul",
        "lastName": "Smith",
        "email": "paul.smith@manywho.com",
        "username": null,
        "verified": false
    },
    "whoOwner": {
        "id": "914e2919-4c72-4b75-853e-85e060d49380",
        "firstName": "Paul",
        "lastName": "Smith",
        "email": "paul.smith@manywho.com",
        "username": null,
        "verified": false
    },
    "alertEmail": null,
    "isActive": true,
    "isDefault": true,
    "comment": null,
    "editingToken": null,
    "id": {
        "id": "3ca32f1c-0278-477b-9ce1-ff88210be747",
        "versionId": "175cf7fe-e1ff-4b83-89bb-9f3e21c4e634"
    },
    "developerName": "Task Manager",
    "developerSummary": "A demo app showing task management.",
    "startMapElementId": "9467970b-6f7e-48e3-9f8b-ced3a24c93c5",
    "allowJumping": true,
    "stateExpirationLength": 0,
    "authorization": null
}
```

Used to get an existing Flow application that is active/default (e.g. "Published") by using the identifier.

#### HTTP Request

`GET /api/run/1/flow/{id}`

#### Parameters

Key | Description
--- | -----------
**id**<br/>string | The unique identifier for the Flow.

### Get Flow by Name

> Example 200 OK Response

```json
{
    "dateCreated": "2015-11-30T04:44:34Z",
    "dateModified": "2016-03-26T07:05:22Z",
    "whoCreated": {
        "id": "914e2919-4c72-4b75-853e-85e060d49380",
        "firstName": "Paul",
        "lastName": "Smith",
        "email": "paul.smith@manywho.com",
        "username": null,
        "verified": false
    },
    "whoModified": {
        "id": "914e2919-4c72-4b75-853e-85e060d49380",
        "firstName": "Paul",
        "lastName": "Smith",
        "email": "paul.smith@manywho.com",
        "username": null,
        "verified": false
    },
    "whoOwner": {
        "id": "914e2919-4c72-4b75-853e-85e060d49380",
        "firstName": "Paul",
        "lastName": "Smith",
        "email": "paul.smith@manywho.com",
        "username": null,
        "verified": false
    },
    "alertEmail": null,
    "isActive": true,
    "isDefault": true,
    "comment": null,
    "editingToken": null,
    "id": {
        "id": "3ca32f1c-0278-477b-9ce1-ff88210be747",
        "versionId": "175cf7fe-e1ff-4b83-89bb-9f3e21c4e634"
    },
    "developerName": "Task Manager",
    "developerSummary": "A demo app showing task management.",
    "startMapElementId": "9467970b-6f7e-48e3-9f8b-ced3a24c93c5",
    "allowJumping": true,
    "stateExpirationLength": 0,
    "authorization": null
}
```

Used to get an existing Flow application that is active/default (e.g. "Published") by using the developerName as the identifier.

#### HTTP Request

`GET /api/run/1/flow/name/{name}`

#### Parameters

Key | Description
--- | -----------
**name**<br/>string | The exact developerName property of the Flow.

## Flow State

A Flow State represents an "instance" of your Flow Application. The Flow State contains the information that's collected from the running user(s), which step they're on, etc. If a Flow State is "shared" with another running user, it is automatically collaborative - allowing multiple running users to work on the same Flow State at the same time.

In most situations, a new Flow State is created each time the running user(s) start running a Flow. This Flow State usually only exists for the time that particular instance is used and then the Flow State is discarded.

### Initialize Flow State

Once you have the full Flow Identifier object, you can initialize your flow, ready to start executing. Initialization allows you to do a few things:

- **Pass Input Values into the Flow**: Inputs are related to Values in a Flow. If the Flow Builder has created Values that have an access setting of "Input" or "Input/Output", you can pass information into those Values at initialization. These might be things like the Id of an Account record in salesforce.com that the Flow relates to, or the phone number of the current caller.
- **Create annotations**: An annotation is a piece of data you want to attach to your flow, but is not actually passed in as an input. Often developers want to store additional information in the Flow State that helps with integration or more complex configuration. Think of annotations as session state that is read/write for the entire duration of the Flow execution.
- **Set the execution mode**: The "mode" allows you to run the flow in a couple of different debug configurations. This allows you to step through the Flow as a user would see it, but also step through the Flow Element by Element (even logical Elements). It's very powerful for debugging, particularly when Flows get more complex.

#### Initialization Request

The Initialization Request object is used to initialize the Flow.

Key | Description
--- | -----------
**id**<br/>object | This is a composite identifier that has the following properties:<ul><li>**id** (string): The unique identifier for the Flow.</li><li>**versionId** (string): The unique version identifier for the Flow. This is optional and should only be used if you wish to initialize a very specific version of a Flow.</li></ul>
**stateId**<br/>string | This is the identifier for an existing Flow State. This property should only be provided in the case where the Initialization Response required you to authenticate the running user before proceeding. This allows you to re-initialize the Flow State after authentication has been successful.
**parentStateId**<br/>string | The parent Flow State identifier for this Flow State. This property is populated by the platform when executing Sub-Flows or using the Flow Out feature. However, it can be manually assigned.
**externalIdentifier**<br/>string | An external identifier for this Flow State. This is an arbitrary string value that allows you to retrieve a Flow State based on a particular identifier.
**annotations**<br/>object | Key/value pairs that provide additional information that should be annotated on the Flow State.
**inputs**<br/>array | The array of inputs associated with the Flow. Each Input entry maps a Value in the Flow. Each Input entry has the following keys:<br/><br/>**developerName** or **valueElementId** (string):<br/>The developerName or unique identifier of the Value being assigned.<br/><br/>**contentType** (string):<br/>The content type of the data being provided (this allows the Platform to determine how the input data should be parsed if the input ContentType does not match the ContentType of the Value). Valid values are:<ul><li>**ContentString**: A string value</li><li>**ContentNumber**: A numeric value</li><li>**ContentPassword**: A hidden value</li><li>**ContentDateTime**: A date and time value</li><li>**ContentContent**: A rich content value</li><li>**ContentObject**: An object value</li><li>**ContentList**: A list value</li></ul><br/>**typeElementId** or **typeElementDeveloperName** (string):<br/>The unique identifier or developerName of the Type of the Object or List value being provided. This is only applicable for ContentObject and ContentList inputs.<br/><br/>**typeElementPropertyId** or **typeElementPropertyDeveloperName** (string):<br/>The unique identifier or developerName of the property of a Value in the Flow that is an Object. This allows you to assign a property in an Object Value.<br/><br/>**contentValue** (string): The value being provided for the input. This is only used if the Value being assigned is not ContentObject or ContentList.<br/><br/>**objectData** (array):<br/>The ObjectData that should be assigned into the Value in the Flow. This is only used if the Value being assigned is ContentObject or ContentList. See ObjectData for details.
**playerUrl**<br/>string | The URL for the Player that should be referenced for all running users wishing to initiate a Flow State for this Flow.
**joinPlayerUrl**<br/>string | The URL for the Player that should be referenced for all running users wishing to join this Flow State.
**mode**<br/>string | The mode in which the engine should run. Valid values are:<ul><li>*null*: Execute the Flow State as normal.</li><li>**DEBUG**: Execute the Flow State, exposing debug information about the Flow State.</li><li>**DEBUG_STEPTHROUGH**: Execute the Flow State, exposing debug information about the Flow State, and also stop the execution at each and every Map Element.</li><li>**LOG**: Produce logging information about the Flow State. See the Log API for details.</li></ul>
**reportingMode**<br/>string | The reporting mode that should be used for capturing and producing reports from this Flow State. Valid values are:<ul><li>*null*: Do not produce any reporting data.</li><li>**VALUES**: Report on Values in the Flow State.</li><li>**PATH**: Report on the path of execution in the FLow State. These are all of the Map Elements that have been executed, time stamps of execution, user access, etc. See the Reporting API for details.</li><li>**PATH_AND_VALUES**: Capture reporting on both of the above.</li></ul>

#### Initialization Response

Once a Flow State has been initialized, the Response object is returned.

Key | Description
--- | -----------
**culture**<br/>object | The internationalization Culture the Flow is running in. See the Translate API for details.
**stateId**<br/>string | This is the identifier for an existing Flow State. The state identifier is constant for the entire lifetime of the Flow State.
**stateToken**<br/>string | The unique identifier for this initialization response. The state token changes for each and every request made to the Flow State where that request can alter the Flow State.
**currentMapElementId**<br/>string | The unique identifier for the current Map Element. When a Flow State is initialized, this is the "Start" Map Element typically.
**currentStreamId**<br/>string | The unique identifier for the collaboration stream associated with this Flow State. This is provided if the Flow is configured to support collaboration.
**statusCode**<br/>string | The status code of the initialization based on HTTP authentication/status codes. Valid values are:<ul><li>**200**: The user is authenticated and can successfully execute the Flow State.</li><li>**401**: The use is not authenticated to execute the Flow State. As a result, the user should use the authenticationContext information to authenticate the user and then re-try the initialization of the Flow State. See Authenticating Running Users for details.</li></ul>
**authorizationContext**<br/>object | The authentication context required to access the Flow State. See Authenticating Running Users for details.
**navigationElementReferences**<br/>array | The array of Navigation Elements associated with this Flow State. Each Navigation Element Reference entry has the following keys:<br/><br/>**id** (string)<br/>The unique identifier for the Navigation Element that can be loaded to allow the running user(s) to move flexibly around the Flow State. See Navigation for details.<br/><br/>**developerName** (string)<br/>The developerName for the Navigation Element that can be loaded to allow the running user(s) to move flexibly around the Flow State. See Navigation for details.

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
