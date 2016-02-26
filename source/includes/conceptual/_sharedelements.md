## Shared Elements

### Flows
A Flow is an implementation of a process on the ManyWho platform. It will contain 1 or more [Map Elements](http://google.com)
and [Outcomes](http://google.com) that determines what happens and in what order.

#### Flow URL's
When you run a Flow a url is generated that you can use to share your Flow, for example:

https://flow.manywho.com/ba986a91-a39c-46db-91fd-14aa0545546f/play/default?flow-id=4003a819-e167-417f-a48e-fa7456d284d1&flow-version-id=d240fd97-4c96-4cfe-9cf6-f70eac0a97c2&navigation-element-id=b4d908e9-36fa-43a9-ab5f-f9af71d72fbf

This breaks down to:

| URL Part | Description | Optional |
|---|---|---|
| https://flow.manywho.com/ | Platform | No |
| ba986a91-a39c-46db-91fd-14aa0545546f | Tenant Id | No |
| play | Tell ManyWho that we are running a flow | No |
| default | The name of the player being used to run your Flow | No |
| flow-id=4003a819-e167-417f-a48e-fa7456d284d1 | The Id of the Flow to run | No |
| flow-version-id=d240fd97-4c96-4cfe-9cf6-f70eac0a97c2 | The version Id of the Flow to run | Yes |
| navigation-element-id=b4d908e9-36fa-43a9-ab5f-f9af71d72fbf | The Id of the navigation element to include in the Flow | Yes |

#### Activating & Versioning
When you run a Flow it will include a version ID `flow-version-id`. Each time you run a Flow all the elements in the Flow are "snapshotted" to a specific version.

Activating a Flow performs the same snapshotting as running a Flow however it also sets this latest version as the **default** version.
The default version will be run when you open a Flow via a url that doesn't contain a version ID e.g. https://flow.manywho.com/<tenant-id>/default/play/<flow-id>

If you don't specify the version ID in your url then you can consider activating a Flow the same as "Go Live" button.

#### Shared Elements
Values, Types, Page Layouts, Services & Tags are shared and can be used in multiple Flows.

When you activate a Flow a snapshot of the shared elements is taken, after this any changes made to the shared elements won't affect the activated version of the Flow.

### Services
Services allow you to interact with the world outside of your Flow. Services add a variety of functionality when added to your flow, including:

| Functionality | Description |
|---|---|
| Database | Saving, Loading & Deleting data |
| Actions | Perform one or more operations in the 3rd party service i.e. send a text message |
| Authorization | Gate your flows using Username & Password or OAuth2 |
| Files | Upload & Download Files |
| Voting | |

<aside class="notice">
Services are implemented outside of ManyWho, available services can be found here:
More information on creating your own Service can be found here:
</aside>

### Types
Types allow you define the "shape" of a complex value by defining what properties (which can be thought of sub-values) are available.

Types can be thought of as Interfaces if you are familiar with programming.

<aside class="notice">
Types on their own don't do anything. To use a Type you will need to create an Object Value.
</aside>

### Values
Values are used to hold your data while a Flow is running e.g. load customer info from Salesforce into a Value, edit the Value in your Flow, save the Value back to Salesforce.

Values are split into 3 basic categories:

#### Primitive
Primitive Values hold simple content only, including:

| Type | Description |
|---|---|
| String | Basic Text |
| Number | Digits 0-9 |
| DateTime | |
| Password | |
| Content | Rich Text i.e. formatting, images, etc |

#### Objects
Object values are values that are linked to a specific Type. When a value is an Object of a specific Type then the value will have all the properties of that Type.

#### Lists
Lists can hold 1 or more values of a specific type e.g. String, Number, Object, etc.

<aside class="notice">
Values that are created as a List are still a single Value. Although they can contain multiple "values" i.e. "list item1", "list item2", "list item3", it will still have a single ID and Name.
</aside>

### Pages

### Players
A Player is the "renderer" for your Flows that is used to display an executing Flow to the end user. By default Flows will be displayed using the "default" HTML5 Player, this will display your Flows in a browser and supports all the functionality provided by the ManyWho platform.

You can edit this player and / or create new HTML5 based players in ManyWho by selecting the **Players** menu option.

More information on the default HTML5 player and the UI framework in general can be found [here](#ui-framework) 
