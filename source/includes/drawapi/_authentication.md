## Authenticating Flow Builders

> Authentication Request JSON:

```json
{
  "loginUrl": "https://flow.manywho.com/plugins/manywho/api/draw/1/authentication",
  "username": "paul.smith@mycompany.manywho.com",
  "password": "nottellin"
}
```

*Authenticate Flow Builders before using the Admin, Draw, Translate APIs.*

Once a Tenant and Flow Builder has been provisioned, you can authenticate against the Draw API. The returned token should be used in the standard HTTP Authorization header when performing any operations against the various APIs.

#### HTTP Request

`POST /api/draw/1/authentication`

#### Body

The raw JSON for the Tenant Registration Request:

Key | Description
--- | -----------
**loginUrl**<br/>string | This property should always be: https://flow.manywho.com/plugins/manywho/api/draw/1/authentication
**username**<br/>string | The username for the Flow Builder.
**password**<br/>string | The password for the Flow Builder.
