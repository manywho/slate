## Box Service

Box is a content management platform. Our box service integrates with their platform and allows access files in your box account as well as other more advanced features.

### Installing the Box Service

<aside class="notice">
<b>Note</b><br/>
Setting up folder listeners involves using the API tool. It is recommended to familiarise yourself with the API tool before progressing if you want to use that functionality.
</aside>

##### Connection Url & Values

```
https://services.manywho.com/api/box/2
```

Set the **SSO URL** to: http://box.myapp.com

<aside class="notice">
<b>Note</b><br/>
Box service supports single sign on (SSO). To use this feature a configuration value with a valid sso url must be defined.
</aside>

##### Types

Name | Description
---- | -----------
File | A representation of a file object on box
Folder | A representation of a folder object on box
Shared Link | A http link to the box file
Shared Link Access | The access restriction on a shared link. Can be either collaborators, company or open
Shared Link Permissions | Defines if a shared link can be downloaded or previewed.
View | A html representation of document file.

##### Actions

Name | Endpoint | Description
---- | -------- | -----------
File: Comment | file/comment | Adds a comment to a file
File: Copy | file/copy | Copies a file to a new folder with an optional new name
File: Share | file/share | Shares creates a Shared Link for a file.
File: View | file/view | Creates a View for a file
File: Move | file/move | Moves a file to a new folder with an optional new name
Folder: Create | folder/create | Creates a new folder

##### Action Inputs and outputs

###### File: Comment
**Inputs**

Name | Type | Mandatory | Description
---- | ---- | --------- | -----------
Source | File | File | Yes | The file to comment on
Message | String | Yes | The comments message

###### File: Copy
**Inputs**

Name | Type | Mandatory | Description
---- | ---- | --------- | -----------
Source | File | File | Yes | The file to copy
Destination
Folder | Folder | No | The destination folder
Name | String | No | The new Filename
 
###### File: Share
**Inputs**

Name | Type | Mandatory | Description
---- | ---- | --------- | -----------
Source | File | File | Yes | The file to share
Unshare | Date | Date | No | When the shared link expires
Access | Shared Link Access | No | Defines the access restriction on a shared link. Can be either collaborators, company or open
Permissions | Shared Link Permissions | No | Defines if a the shared link can be downloaded or previewed.

**Outputs**

Name | Type | Description
---- | ---- | -----------
Shared Link | Shared Link | The new link

###### File: View
**Inputs**

Name | Type | Mandatory | Description
---- | ---- | --------- | -----------
Source | File | File | Yes | The file to share
Unshare | Date | Date | No | When the shared link expires
Access | Shared Link Access | No | Defines the access restriction on a shared link. Can be either collaborators, company or open
Permissions | Shared Link Permissions | No | Defines if a the shared link can be downloaded or previewed.

**Outputs**

Name | Type | Description
---- | ---- | -----------
Shared Link | Shared Link | The new link

###### File: Move
**Inputs**

Name | Type | Mandatory | Description
---- | ---- | --------- | -----------
Source | File | File | Yes | The file to copy
Destination | Folder | Folder | No | The destination folder
Name | String | No | The new Filename

###### Folder: Create
**Inputs**

Name | Type | Mandatory | Description
---- | ---- | --------- | -----------
Parent | Folder | Folder | No | The folder in which to create the new folder. If undefined the folder will be created at root
Name | String | Yes | The Name of the new folder

**Outputs**

Name | Type | Description
---- | ---- | -----------
Folder | Folder | The new Folder
