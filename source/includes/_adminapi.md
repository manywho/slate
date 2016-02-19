# Admin API

## Provisioning and Flow Builders

### Provisioning

> Tenant Registration Request JSON:

```json
{
  "firstName":"Paul",
  "lastName":"Smith",
  "password":"pa$$word",
  "email":"paul.smith@mycompany.com",
  "username":"paul.smith@mycompany.manywho.com",
  "subdomain":"mycompany",
  "notification":{
    "reason":"My Company Tenant",
    "redirectUrl":"https://flow.manywho.com/draw",
    "notificationMessages":
    [
      {
        "mediaType":"text/plain",
        "message":"Username is paul.smith@mycompany.manywho.com, password is: pa$$word. Click here to complete: VERIFY_URL_HERE. You can login to the tooling here: https://manywho.com/log-in"
      }
    ]
  }
}
```

*Create new Tenants and provision the first Flow Builder in a single request*

When you provision a new tenant in ManyWho, there are a few things you need to be aware of:

1. If the email and username are the same, the Platform will provision the Tenant as a Domain Tenant. This means that additional Flow Builders can only be provisioned into this Tenant if they have the same email domain (e.g. @mycompany.com). In addition, the default permissions of the Tenant will allow any other Flow Builders from that same email domain to provision themselves, or self provision, into your Domain Tenant without permission from you. They are part of your email domain and therefore we do not impose restrictions on them gaining access independently.
2. If the email is different from the username, the username must follow the format: @{tenant name}.manywho.com (as shown in the example to the right). Using this format allows Flow Builders with the same email address to provision as many tenants as they like - as long as the {tenant name} is unique. In addition, the default permissions of the Tenant will not allow further Flow Builders to self provision. Any additional Flow Builders must be added by the first Flow builder that provisioned the Tenant or other Flow Builders that have an active account in that Tenant.

Once a tenant is provisioned, the Flow builder provisioning options can be changed. Please have a look at the Tenant API in this documentation for details. Further to this, each Tenant can have any number of sub-Tenants. The benefit of sub-Tenants is that a Flow builder can move between Tenants more easily using single sign-on. Please have a look at the Sub-Tenant API in this documentation for details.

If the type Tenant User Registration Settings (in the Tenant API) is set to MANUAL or SPECIFIC, this API will only work with a valid Flow builder Authorization header.

#### HTTP Request

`POST api/admin/1/provisioning`

#### Body

The raw JSON for the Tenant Registration Request:

Key | Description
--- | -----------
**firstName**<br/>string | The first name of the user registering the Tenant.
**lastName**<br/>string | The last name of the user registering the Tenant.
**email**<br/>string | The email of the user registering the Tenant.
**username**<br/>string | The chosen username for the user registering the Tenant. The username will determine the name of the tenant and further builder user provisioning.
**password**<br/>string | The chosen password fo the user registering the Tenant.
**subdomain**<br/>string | The optional subdomain being reserved for this Tenant. The subdomain must be globally unique.
**notification**<br/>object | The notification that should be sent as part of this Tenant registration. The notification will be sent to the user being registered.<br/><br/>**reason** (string): The reason for the notification. For email, this will be the email subject.<br/><br/>**redirectUrl** (string): The Url that the user should be redirected to when clicking on the verification Url.<br/><br/>**notificationMessages** (array): The list of notification messages (by media type) that should be sent to the user. Each Notification Message entry has the following keys:<ul><li>**mediaType** (string): The media type for the notification message. Currently supported values are "text/html" and "text/plain".</li><li>**message** (string): The message to be sent to the user. For email, this is the email body. To add the verification Url, simply add VERIFY_URL_HERE to the content of the message and the Platform will replace this with the actual verification callback Url which will then forward to the redirectUrl.</li></ul>

### Resetting a Flow Builder Password

The password reset API is only applicable to Flow Builders. For running users, the user identity is managed by the underlying Service (e.g. Salesforce, Box, Google), and therefore user resets should be performed on the underlying system, not within ManyWho. The password reset API requires two separate API calls to complete. The first API call sends the user the password reset notification. The second API call performs the actual password change, based on the token provided in the notification.

#### Perform the Password Reset Request

> Notification Request JSON:

```json
{
  "reason":"Password Reset Request!",
  "redirectUrl":"https://mysite.com/passwordreset?result={0}&callbackUri={1}&token=abcd",
  "notificationMessages":
  [
    {
      "mediaType":"text/html",
      "message":"<html><body><p>Hi Paul,<br/><br/>To reset your password, please click on the link below:<br/><br/>PASSWORD_URL_HERE<br/><br/>All the best,<br/><br/>ManyWho</p></body></html>"
    }
  ]
}
```

#### HTTP Request

`POST api/admin/1/directory/{tenant_domain}/user/password?username={username}`

#### Parameters

Key | Description
--- | -----------
**tenant_domain**<br/>string | The domain provided for the tenant. This is the domain part of any username used to login to the tenant. For example, for a username of: paul.smith@mycompany.manywho.com, the tenant_domain would be: @mycompany.manywho.com
**username**<br/>string | The username associated with the password. Following on from the example above, this would be: paul.smith@mycompany.manywho.com. It's important to note that this is not necessarily the users' email as a builder user can belong to more than one tenant.

#### Body

The raw JSON for the Notification Request (optional):

Key | Description
--- | -----------
**reason**<br/>string | The reason for the notification. For email, this will be the email subject.
**redirectUrl**<br/>string | The Url that the user should be redirected to when clicking on the password verification Url. The redirectUrl should include two parameters in the string for the notification result {0} and the password reset token {1}. The platform will automatically parse the notification result and callbackUri values at these positions in the redirection string. An example of this is: https://mysite.com/passwordreset?result={0}&callbackUri={1}&token=someothertoken. The result parameter has the following possible values:<ul><li>**OK**: The password reset was correctly processed.</li><li>**ALREADY_PROCESSED**: The password reset token has already been processed by the Platform and the user is re-using the link.</li></ul>
**notificationMessages**<br/>array | The list of notification messages (by media type) that should be sent to the user. Each Notification Message entry has the following keys:<br/><br/>**mediaType** (string): The media type for the notification message. Currently supported values are "text/html" and "text/plain".<br/><br/>**message** (string): The message to be sent to the user. For email, this is the email body. To add the password verification Url, simply add PASSWORD_URL_HERE to the content of the message and the Platform will replace this with the actual verification callback Url which will then forward to the redirectUrl.

#### Apply the Password Change

> Password Request JSON:

```json
{
  "password":"nottellin",
}
```

#### HTTP Request

`POST /api/admin/1/directory/{tenant_domain}/user/credential/{token}`

#### Parameters

Key | Description
--- | -----------
**tenant_domain**<br/>string | The domain provided for the tenant. This is the domain part of any username used to login to the tenant. For example, for a username of: paul.smith@mycompany.manywho.com, the tenant_domain would be: @mycompany.manywho.com
**token**<br/>string | The token that was provided to the user as part of the notification callback. The token is not provided in the email, but rather the token is provided after the user clicks on the notification email link. The token will either be parsed into the provided redirectUrl (if specified) or provided in the REST response from a GET request to the notification callback Url provided in the email.

#### Body

The raw JSON for the Password Request:

Key | Description
--- | -----------
**password**<br/>string | The new password to be applied to the Flow Builder account.


## Tenants and Sub-Tenants

> Tenant JSON:

```json
{
  "id": "{id}",
  "developerName": "@mycompany.manywho.com",
  "subTenants": [
    {
      "id": "{id}",
      "developerName": "@staging+mycompany.manywho.com",
      "subTenants": null,
      "developerSummary": null,
      "securitySettings": null,
      "subdomain": "mycompany-staging",
      "stateSettings": null,
      "tenantSettings": null
    },
    {
      "id": "{id}",
      "developerName": "@production+mycompany.manywho.com",
      "subTenants": null,
      "developerSummary": null,
      "securitySettings": null,
      "subdomain": "mycompany-production",
      "stateSettings": null,
      "tenantSettings": null
    }
  ],
  "developerSummary": "My root Tenant for building Flow templates",
  "securitySettings": {
    "isAdminRestrictedByIPRange": true,
    "authorizedAdminIPRanges": [
      "developerName": "Interal Network",
      "developerSummary": "Only allow access when inside the company firewall.",
      "startIPAddress": "195.3.5.56",
      "endIPAddress": "195.3.5.58"
    ],
    "isPackagingRestrictedByIPRange": false,
    "authorizedPackagingIPRanges": null,
    "isDrawRestrictedByIPRange": false,
    "authorizedDrawIPRanges": null,
    "isRunRestrictedByIPRange": false,
    "authorizedRunIPRanges": null,
    "isServiceRestrictedByRemoteSites": true,
    "authorizedServiceRemoteSites": [
      "developerName": "Salesforce Service",
      "developerSummary": "Only allow access to the production Salesforce Service.",
      "uri": "https://salesforce.manywho.com",
      "disableProtocolSecurity": false
    ],
    "userRegistrationSettings": {
      "type": "MANUAL",
      "notify": "ALL",
      "notificationWhoId": null
    }
  },
  "subdomain": "mycompany",
  "stateSettings": {
    "endpoint": "https://mycompany.com/api/report",
  	"persistToDatabase": false
  }
}
```

*The Tenant provides a central place for Flow Builders to build, manage and deploy Flows.*

Once a Tenant has been provisioned, there are various settings available to ensure security is correctly configured and data is properly managed for reporting purposes. The APIs below work for both Tenants and sub-Tenants. The only difference between a Tenant and and sub-Tenant is that Flow Builders can move between them using single sign-on and the Tenants are grouped together to ease management.

#### Tenant

Key | Description
--- | -----------
**id**<br/>string | A unique identifier assigned by the Platform.
**developerName**<br/>string | The name for the Tenant. This will be based on the username of the first provisioned Flow Builder. For example, for a username of: paul.smith@mycompany.manywho.com, the developerName would be: @mycompany.manywho.com
**developerSummary**<br/>string | The summary for the Tenant. This is typically additional information that will help explain the purpose of the Tenant.
**subTenants**<br/>array | The array of sub-Tenants (showing just the root properties of the Tenant object.
**securitySettings**<br/>object | The Security Settings that should be applied to this Tenant (not including sub-Tenants). The Security Settings object has the following keys:<br/><br/>**isAdminRestrictedByIPRange** (boolean):<br/>Indicates that the Admin APIs should be protected by the provided IP range in authorizedAdminIPRanges. Setting this to false will not remove the list of IP Range entries and will simply disable IP range restrictions.<br/><br/>**authorizedAdminIPRanges** (array):<br/>The array of IP Range entries that will be allowed to access the Admin APIs. The configuration of the IP Range object is provided in the section below.<br/><br/>**isPackagingRestrictedByIPRange** (boolean):<br/>Indicates that the Packaging APIs should be protected by the provided IP range in authorizedPackagingIPRanges. Setting this to false will not remove the list of IP Range entries and will simply disable IP range restrictions.<br/><br/>**authorizedPackagingIPRanges** (array):<br/>The array of IP Range entries that will be allowed to access the Packaging APIs. The configuration of the IP Range object is provided in the section below.<br/><br/>**isDrawRestrictedByIPRange** (boolean):<br/>Indicates that the Draw APIs should be protected by the provided IP range in authorizedDrawIPRanges. Setting this to false will not remove the list of IP Range entries and will simply disable IP range restrictions.<br/><br/>**authorizedDrawIPRanges** (array):<br/>The array of IP Range entries that will be allowed to access the Draw APIs. The configuration of the IP Range object is provided in the section below.<br/><br/>**isRunRestrictedByIPRange** (boolean):<br/>Indicates that the Run APIs should be protected by the provided IP range in authorizedRunIPRanges. Setting this to false will not remove the list of IP Range entries and will simply disable IP range restrictions.<br/><br/>**authorizedRunIPRanges** (array):<br/>The array of IP Range entries that will be allowed to access the Run APIs. The configuration of the IP Range object is provided in the section below.<br/><br/>**isServiceRestrictedByRemoteSites** (boolean):<br/>Indicates that Service Elements only be allowed to be installed and used based on Remote Site settings outlined in the authorizedServiceRemoteSites property. Setting this to false will not remove the existing Remote Site settings.<br/><br/>**authorizedServiceRemoteSites** (array):<br/>The array of Remote Site entries that will be allowed when installing and using Service Elements. Each Remote Site setting entry has the following keys:<ul><li>**developerName** (string): The name for the Remote Site. This is typically a helpful name to remind administrators of the purpose of the Remote Site.</li><li>**developerSummary** (string): The summary for the Remote Site. This is typically additional information that will help explain the purpose of the Remote Site.</li><li>**uri** (string): The Uri for the allowed Remote Site. This should be the base Uri allowed.</li><li>**disableProtocolSecurity** (string): Indicates if the Remote site can be accessed without encryption (SSL).</li></ul><br/>**userRegistrationSettings** (object):<br/>The Flow Builder registration settings that should be applied when provisioning. The User Registration Settings object has the following keys:<ul><li>**type** (string): The registration type determines how new Flow Builders are provisioned and the notifications that occur when that happens. Valid values are:</li><ul><li>**MANUAL**: Indicates that all Flow Builders must be provisioned manually by another Flow Builder (authenticated). This is the default setting for Domain Tenants that use the @{tenant name}.manywho.com notation for the username.</li><li>**REQUEST**: Indicates that all Flow Builders must be provisioned manually by another Flow Builder, however, existing Flow Builders will be notified that another Flow Builder is requesting access.</li><li>**SELF**: Indicates that all Flow Builders can self provision if their email and username match with the existing Tenant. This is the default setting for Domain Tenants that use the email to determine tenancy.</li></ul><li>**notify** (string): The notification settings for any Flow Builder provisioning requests. Valid values are:</li><ul><li>**ALL**: Indicates that all Flow Builders will be notified when another Flow Builders is requesting access to the Tenant.</li><li>**NONE**: Indicates that no Flow Builders will be notified if another Flow Builder is requesting access to the Tenant.</li><li>**SPECIFIC**: Indicates that a specific Flow Builder should be notified when another Flow Builder is requesting access to the Tenant. The Flow Builder being notified is specified in the notificationWhoId property.</li></ul><li>**notificationWhoId** (string): The unique identifier for the User on the Platform. This user will receive notifications when new Flow Builders are provisioned and the notify property is set to SPECIFIC.</li></ul>
**reportSettings**<br/>string | (deprecated)
**subdomain**<br/>string | The requested subdomain to register for this tenant. The subdomain can be null, but if provided must be unique for the entire Platform.
**stateSettings**<br/>object | The settings for State persistence and storage. The State Settings object has the following keys:<br/><br/>**endpoint** (string):<br/>The Uri for the State persistence implementation. This endpoint must implement our Reporting API interface. More details on that can be found on GitHub here: https://github.com/manywho/reporting<br/><br/>**persistToDatabase** (boolean):<br/>Indicates if the Tenant should retain any State data to disk. If this property is set to false, States will only be persisted in memory/cache. For long running Flow States, this should typically be set to true as the Platform memory is not guaranteed storage.


#### IP Range
Key | Description
--- | -----------
**developerName**<br/>string | The name for the IP Range. This is typically a helpful name to remind builders of the purpose of the IP Range.
**developerSummary**<br/>string | The summary for the IP Range. This is typically additional information that will help explain the purpose of the IP Range.
**startIPAddress**<br/>string | The valid start IP address.
**endIPAddress**<br/>string | The valid end IP address.


### Get Tenant

> Example 200 OK Response

```json
{
    "id": "80c1a97a-e31c-4ab1-a279-9742af17f31d",
    "developerName": "@mycompany.manywho.com",
    "subTenants": [
        {
            "id": "daa15237-bfd3-44b6-b5c4-68f31c448312",
            "developerName": "@staging+mycompany.manywho.com",
            "subTenants": null,
            "developerSummary": null,
            "securitySettings": null,
            "reportSettings": null,
            "subdomain": null,
            "stateSettings": null,
            "tenantSettings": null
        },
        {
            "id": "6a1a6c4d-ecb5-44a1-aab3-489cde964686",
            "developerName": "@production+mycompany.manywho.com",
            "subTenants": null,
            "developerSummary": null,
            "securitySettings": null,
            "reportSettings": null,
            "subdomain": null,
            "stateSettings": null,
            "tenantSettings": null
        }
    ],
    "developerSummary": null,
    "securitySettings": null,
    "reportSettings": null,
    "subdomain": null,
    "stateSettings": null,
}
```

Used to get the Tenant object for the current Tenant. The Tenant provides a central place for Flow Builders to build, manage and deploy Flows.

#### HTTP Request

`GET /api/admin/1/tenant`


### Set Tenant

> Example 200 OK Response

```json
{
    "id": "80c1a97a-e31c-4ab1-a279-9742af17f31d",
    "developerName": "@mycompany.manywho.com",
    "subTenants": null,
    "developerSummary": null,
    "securitySettings": null,
    "reportSettings": null,
    "subdomain": "mycompany",
    "stateSettings": null
}
```

Used to set the Tenant object for the current Tenant. The Tenant provides a central place for Flow Builders to build, manage and deploy Flows.

#### HTTP Request

`POST /api/admin/1/tenant`

#### Body

The raw JSON for the Tenant.


### Delete Tenant Data

> Success 204 No Content Response

```json
{
  "flows": true,
  "pageLayouts": true,
  "values": true,
  "types": true,
  "services": true,
  "tags": true,
  "snapshots": true,
  "states": true
}
```

<aside class="error">
<b>Careful!</b><br/>
Use this API with extreme caution. Though we do keep backups of Tenant data, recovering from Tenant delete operations takes time and is chargeable. A request to delete Tenant data does require verification via email before the actual delete is performed. However, make sure you check your settings carefully as dependency validations are ignored. You have been warned!
</aside>

#### HTTP Request

`POST /api/admin/1/tenant/data`

#### Body

The raw JSON for the Tenant Delete Request.

#### Tenant Delete Request

Key | Description
--- | -----------
**flows**<br/>boolean | Indicates if all Flow models should be deleted.
**pages**<br/>boolean | Indicates if all Page Elements should be deleted.
**values**<br/>boolean | Indicates if all Value Elements should be deleted.
**types**<br/>boolean | Indicates if all Type Elements should be deleted.
**services**<br/>boolean | Indicates if all Service Elements should be deleted.
**tags**<br/>boolean | Indicates if all Tag Elements should be deleted.
**snapshots**<br/>boolean | Indicates if all Flow snapshots should be deleted.
**states**<br/>boolean | Indicates if all Flow States should be deleted.


## Users

> User JSON:

```json
{
  "id": "{id}",
  "firstName": "Paul",
  "lastName": "Smith",
  "email": "paul.smith@mycompany.com",
  "username": "paul.smith@mycompany.manywho.com",
  "verified": true
}
```

*The User object provides basic information about Flow Builders and running users for the Tenant.*

Users on the Platform are identified via their email. As a result, the email address determines "who" the user is. The email address is the unique identifier across the entire platform. When running users access a Flow, a User is provisioned into the Tenant on-demand. In addition, Flow Builders are included in the User listing. As a single running user can login to multiple Services, a User entry will be provided for each Service being logged into. As a result, the username parameter is used to load an individual User record for a particular Service. Currently it is assumed that the username will be unique for each Service. Please contact the ManyWho team if this causes issues with User management.


### Get Users

> Example 200 OK Response

```json
[
  {
    "id": "914e2919-4c72-4b75-853e-84e060d49380",
    "firstName": "Paul",
    "lastName": "Smith",
    "email": "paul.smith@mycompany.com",
    "username": "paul.smith@mycompany.manywho.com",
    "verified": true
  },
  {
    "id": "4bb15de8-427c-4b8b-b853-bffafbc553a1",
    "firstName": "Etienne",
    "lastName": "Dubois",
    "email": "edubois@enduser.com",
    "username": null,
    "verified": true
  }
]
```

Used to get the list of Users. The User object provides basic information about Flow Builders and running users for the Tenant.

#### HTTP Request

`GET /api/admin/1/directory/{tenant_domain}/user`

#### Parameters

Key | Description
--- | -----------
**tenant_domain**<br/>string | The domain provided for the tenant. This is the domain part of any username used to login to the tenant. For example, for a username of: paul.smith@mycompany.manywho.com, the tenant_domain would be: @mycompany.manywho.com


### Get User

> Example 200 OK Response

```json
{
  "id": "914e2919-4c72-4b75-853e-84e060d49380",
  "firstName": "Paul",
  "lastName": "Smith",
  "email": "paul.smith@mycompany.com",
  "username": "paul.smith@mycompany.manywho.com",
  "verified": true
}
```

Used to get an individual User object for a Service or Flow Builder. The User object provides basic information about Flow Builders and running users for the Tenant.

#### HTTP Request

`GET /api/admin/1/directory/{tenant_domain}/user?username={username}`

#### Parameters

Key | Description
--- | -----------
**tenant_domain**<br/>string | The domain provided for the tenant. This is the domain part of any username used to login to the tenant. For example, for a username of: paul.smith@mycompany.manywho.com, the tenant_domain would be: @mycompany.manywho.com
**username**<br/>string | The username associated for the User record.


### Set User

> Example 200 OK Response

```json
{
  "id": "914e2919-4c72-4b75-853e-84e060d49380",
  "firstName": "Paul",
  "lastName": "Smith",
  "email": "paul.smith@mycompany.com",
  "username": "paul.smith@mycompany.manywho.com",
  "verified": true
}
```

Used to set an individual User object for a Service or Flow Builder. The User object provides basic information about Flow Builders and running users for the Tenant.

#### HTTP Request

`POST /api/admin/1/directory/{tenant_domain}/user`

#### Body

The raw JSON for the User.


### Delete User

> Success 204 No Content Response

Used to delete an individual User object for a Service or Flow Builder. This will not delete the User record entirely from the Platform as the User object is an aggregate object and a single User object can exist across multiple Tenants.

#### HTTP Request

`DELETE /api/admin/1/directory/{tenant_domain}/user?username={username}`

#### Parameters

Key | Description
--- | -----------
**tenant_domain**<br/>string | The domain provided for the tenant. This is the domain part of any username used to login to the tenant. For example, for a username of: paul.smith@mycompany.manywho.com, the tenant_domain would be: @mycompany.manywho.com
**username**<br/>string | The username associated for the User record.






























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
  "{id}",
  
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
