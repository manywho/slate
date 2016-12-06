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

`POST /api/admin/1/provisioning`

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

`POST /api/admin/1/directory/user/password?username={username}`

#### Parameters

Key | Description
--- | -----------
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
  "password":"nottellin"
}
```

#### HTTP Request

`POST /api/admin/1/directory/user/credential/{token}`

#### Parameters

Key | Description
--- | -----------
**token**<br/>string | The token that was provided to the user as part of the notification callback. The token is not provided in the email, but rather the token is provided after the user clicks on the notification email link. The token will either be parsed into the provided redirectUrl (if specified) or provided in the REST response from a GET request to the notification callback Url provided in the email.

#### Body

The raw JSON for the Password Request:

Key | Description
--- | -----------
**password**<br/>string | The new password to be applied to the Flow Builder account.
