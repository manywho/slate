## Email

You can use the Email Service to send Emails, using your current provider.


### Installing the Email Service


#### Intro

In order to install the Email Service, you first need some information about your email provider, the information needed is in the section configuration.

#### Configuration

When installing the Service, you should use the following settings:


**Connection Uri**

`https://services.manywho.com/api/email/1`


**Configuration Values**

Name | Type | Required | Description
---- | ---- | :------: | -----------
Host | String | ✔ | The host of your email provider (E.g. smtp.yourdomain.com).
Port | Numeric | ✔ | The port of your email provider (E.g. 587).
Username | String | ✔ | The username of your email provider ( E.g. admin@yourdomain.com)
Password | Password | ✔ | The password for your email provider.
Transport | String | ✔ | The transport for your email provider, it can be "plain", "ssl" or "tls".


#### Types

The following Types are available for this Service. The Database column indicates if the Type can be Saved, Loaded, or Deleted using the Service. The Listening column indicates if Objects of this Type can be listened to.

Name | Description | Database | Listening
---- | ----------- | :------: | :-------:
**Contact** | It contains a name and email address | ✘ | ✘

#### Actions

Some helpful summary information about the Actions that can be performed.


##### Send Email

Use this action to send emails.

**Inputs**

Name | Type | Required | Description
---- | ---- | :------: | -----------
**From** | Contact | ✔ | From which account is sent this email.
**To** | List of Contact | ✔ | List of contacts to be send in the to field.
**To (CC)** | List of Contact | ✘ | List of contacts to be added in the carbon copy field.
**To (BCC)** | List of Contact | ✘ | List of contacts to be added in the blind carbon copy field.
**Subject** | String | ✘ | Subject of the email.
**Body** | String | ✘ | Body (text) of the email.
**HTML Body** | String | ✘ | Body (html) of the email.
**Attachments** | List of $File | ✘ | The list of $Files to be attached to the email.

### Code

You can access the source code and developer details about implementation on GitHub.


**GitHub**

`https://github.com/manywho`
