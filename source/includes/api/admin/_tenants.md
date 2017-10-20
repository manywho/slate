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
      {
        "developerName": "Interal Network",
        "developerSummary": "Only allow access when inside the company firewall.",
        "startIPAddress": "195.3.5.56",
        "endIPAddress": "195.3.5.58"
      }
    ],
    "isPackagingRestrictedByIPRange": false,
    "authorizedPackagingIPRanges": null,
    "isDrawRestrictedByIPRange": false,
    "authorizedDrawIPRanges": null,
    "isRunRestrictedByIPRange": false,
    "authorizedRunIPRanges": null,
    "isServiceRestrictedByRemoteSites": true,
    "authorizedServiceRemoteSites": [
      {
        "developerName": "Salesforce Service",
        "developerSummary": "Only allow access to the production Salesforce Service.",
        "uri": "https://salesforce.manywho.com",
        "disableProtocolSecurity": false
      }
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
  },
  "tenantSettings": {
    "formatValues": true,
    "releaseCycle": "rolling"
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
**stateSettings**<br/>object | The settings for State persistence and storage. The State Settings object has the following keys:<br/><br/>**endpoint** (string):<br/>The Uri for the State persistence implementation. This endpoint must implement our Reporting API interface. More details on that can be found on GitHub here: https://github.com/manywho/reporting<br/><br/>**persistToDatabase** (boolean):<br/>(deprecated)
**tenantSettings**<br />object | The settings specific to the tenant. It has the following keys: <br /><br />**releaseCycle** (string): <br />The version of the platform your tenant's flow will run using - can be one of **rolling** for the latest version always, or **monthly** for a monthly-released, 1-month delayed version (based on **rolling**).

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
  "stateSettings": null
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

### Delete Tenant

> Success 204 No Content Response

<aside class="error">
<b>Careful!</b><br/>
Use this API with extreme caution. Though we do keep backups of Tenant, recovering from Tenant delete operations takes time and is chargeable. A request to delete Tenant does require verification via email before the actual delete is performed.
</aside>

#### HTTP Request

`DELETE /api/admin/1/tenant`

#### Body

There is not body in this request.


### Delete Tenant Data

> Success 204 No Content Response

```json
{
  "flows": true,
  "pages": true,
  "values": true,
  "types": true,
  "services": true,
  "tags": true,
  "snapshots": true,
  "states": true,
  "macros": true
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

#### Tenant Data Delete Request

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
**macros**<br/>boolean | Indicates if all Macros should be deleted.
