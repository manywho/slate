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