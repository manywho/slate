## Salesforce

If you are an existing Salesforce customer, you may want to create a Developer Edition org to try out our platform. If you are not an existing Salesforce customer, you can get a free Developer Edition account to make the most of the ManyWho platform.

### Installing the Salesforce Service

To set up the Salesforce Service, please complete the following instructions.

#### Create a salesforce.com account

Go to http://developer.force.com and click on the Sign Up button on the top right of the page.

<aside class="notice">
<b>Note</b><br/>
Take a note of the website address being used by your account in salesforce. You should see something like 'https://na15.salesforce.com/'. Make a note of the first part that starts with 'na' or 'eu', etc. In this example, it's 'na15'. We'll need this information when setting up the Salesforce Service.
</aside>

#### Enable Social Features

##### Create a Custom Object for ManyWho

In order for ManyWho to leverage the social/feed capabilities of Salesforce (i.e. Chatter), you need to create a custom object. We use this to store the feed comments:

1. In the top right menu of your salesforce.com account, click on **Setup**
2. In the navigation bar on the left side, under the *Build* section, click on **Create**
3. In the sub-menu you have to go into *Objects* and then click **New**
4. On the screen for *New Custom Object*, complete the following (make sure this information is entered exactly as shown):
    - Label: ManyWhoFlow
    - Plural Label: ManyWhoFlows
5. Leave all of the other settings alone and click on the **Save** button.
6. In the *Custom Fields & Relationships* section, click on **New** to create a new field.
7. Select **URL** for the field type and click on **Next**
8. Provide the following for the field:
    - Field Label: JoinUri
    - Field Name: JoinUri
9. Click on Next.
10. Tick the box at the top of the **Visible** column to ensure this field is visible to all profiles.
11. Click on Next. Click on Save.

##### Add feed tracking to the ManyWhoFlow Custom Object

1. Under the *Build* section, click on **Customize**
2. In the displayed sub menu, scroll down and click on **Chatter**
3. In the displayed sub menu, click on **Feed Tracking**
4. On the *Feed Tracking* screen, select **ManyWhoFlow** in this list of objects (on the left beside the main setup menu)
5. Tick the box for **Enable Feed Tracking** at the top of the page area and click on the **Save** button

#### Enable Identity Features

We can set up salesforce.com so ManyWho users can login to their salesforce account without needing to use a complicated security token:

##### Basic Authentication

1. Under the *Administer* section, click on **Security Controls**
2. In the displayed sub menu, click on **Network Access**
3. On the *Network Access* screen, click on **New**
4. For the **Start IP Address** and **End IP Address** enter: *138.91.153.142*
5. Click on the **Save** button

Repeat the above steps, but this time use the IP address of: 54.164.117.86

##### OAuth2

1. Under the *Build* section, click on **Create**
2. In the displayed sub menu, click on **Apps**
3. In the *Connected Apps* section, click on **New**
4. You can enter anything for **Connected App Name** and **API Name**. We suggest naming it "ManyWho" for both.
5. Enter your email for the **Contact Email**
6. Tick the box for **Enable OAuth Settings**
7. For the **Callback URL**, enter: https://flow.manywho.com/api/run/1/oauth2
8. For the **Selected OAuth Scopes**, select **Full access (full)** and click on **Add**
9. Click on **Save** to create the *Connected App*

<aside class="notice">
<b>Note</b><br/>
Once the *Connected App* is created, view the details of the app. Make a note of the **Consumer Key** and **Consumer Secret**. We'll need this information when setting up the Salesforce Service.
</aside>

#### Configuring ManyWho

1. Login to ManyWho: https://manywho.com/log-in
2. Click on **Services** and click on **New**
3. For the **Name**, enter: Salesforce Service
4. For the **Connection Uri**, enter: https://salesforce.manywho.com/plugins/api/salesforce/1
5. Click on **Update**
6. For each of the options in the *Configuration* section, provide the values outlined in the table below. To do this:
    1. Click on the *asterix* button
    2. Enter the Value
    3. Press **ctrl-S** to save the Value
    4. Enter a name (suggested value in the table below)
    5. Click on the *green* button to save the Value
7. Once you have completed all of the required configuration options, click on **Update Actions & Types**

Name | Suggested Save Name | Required | Description
---- | ------------------- | -------- | -----------
AuthenticationUrl | Salesforce AuthenticationUrl | ✔ | For developer edition and production accounts, this is: https://login.salesforce.com  For sandboxes, this may be https://text.salesforce.com  If you're using your own domain, this would be the full url of your own domain.
Username | Salesforce Username | ✔ | Your username or the username of an API user account. This is needed for design time access.
Password | Salesforce Password | ✔ | Your password or the password of an API user account. This is needed for design time access.
ChatterBaseUrl | Salesforce ChatterBaseUrl | ✔ | This is the address of your Salesforce instance captured in the instructions above e.g. https://na30.salesforce.com
AdminEmail | Salesforce AdminEmail | ✔ | Likely your email address.
SecurityToken | Salesforce SecurityToken | ✘ | Your security token or the security token of an API user account. This can be needed for design time access.
Consumer Secret | Salesforce Consumer Secret | ✘ | If you wish to leverage OAuth2 authentication, this is the Consumer Secret value you captured in the instructions above.
Consumer Key | Salesforce Consumer key | ✘ | If you wish to leverage OAuth2 authentication, this is the Consumer Key value you captured in the instructions above.
Authentication Strategy | Salesforce Authentication Strategy | ✘ | This can have three possible values. **Standard** (or not provided/blank): Login to Salesforce using the active user, but use the stored username/password for functions that likely need high level privileges (such as querying the User table for Approval style Flows). **SuperUser**: Login using the stored credentials for everything. This is useful for public facing Flows that need access to Salesforce data. **ActiveUser**: Login using the active user session only.
Default From Email | Salesforce Default From Email | ✘ | If you wish to send notification emails from ManyWho, this is usually the username of a valid email account e.g. mydemo@gmail.com
Email Username | Salesforce Email Username | ✘ | The email username of a valid email account e.g. mydemo@gmail.com
Email Password | Salesforce Email Password | ✘ | The email password of a valid email account.
Email SMTP | Salesforce Email SMTP | ✘ | The SMTP server details for a valid email host e.g. smtp.gmail.com

### Launching a Flow from a Workflow Rule

Using Salesforce Workflow Rules, you can easily kick off a ManyWho Flow. The Flow can involve users, execute business rules and/or run over a period of time. There are no limitations on the kinds of things your Flow can do:

- Create/update multiple related or unrelated records
- Send out emails and tasks to users
- Request for approvals
- Update other systems or databases
- Send a text message notification
- And the list goes on...

You decide what your Flow should do. Use Workflow Rules to kick things off.

#### Configuring your Flow

There's nothing specific about a Flow that can be launched using Workflow Rules, however, you should be aware of a couple of things:

- If the flow uses authentication from another Service, the Workflow Rule will not be able to authenticate without coding an authentication mechanism
- If the user triggering the Flow is not authorized, the Workflow Rule will not be able to execute the flow (though it can initialize it ready for another user to join) without coding a solution

Make sure your flow also contains two Values:

Value Name | Value Type | Access | Description
---------- | ---------- | ------ | -----------
SalesforceNotificationRecordId | String | Input or Input/Output | This Value will contain the unique record identifier for the object triggering the Workflow Rule in Salesforce (e.g. 04k20000000KzEE).
SalesforceNotificationObjectName | String | Input or Input/Output | This Value will contain the API name for the object triggering the Workflow Rule in Salesforce (e.g. MyObject__c).

#### Configuring your Workflow Rule

1. Login to Salesforce (https://login.salesforce.com).
2. Click on **Setup** and find the *Build* section in the setup tree.
3. Click on **Create -> Workflow & Approvals -> Workflow Rules**.
4. Click on the **New Rule** button.
5. Select the Object you want to have trigger your Flow and click on the **Next** button.
6. Enter a memorable name for **Rule Name**.
7. Select any *Evaluation Criteria* and create a *Rule Criteria* (if you don't need any rules, we suggest creating a *Rule Criteria* that will always be true: e.g. Lead: First Name not equal to <empty box>).
8. Click on the **Save & Next** button.
9. Click on the **Add Workflow Action** menu and select **New Outbound Message**.
10. Enter a memorable name for **Name** and the **Unique Name** should auto populate.
11. Configure the **Endpoint URL** using the documentation below this list (i.e. https://salesforce.manywho.com/plugins/api/salesforce/1/workflowrules/{tenantid}/{flowid}/{playername}).
12. For the **User to send** as, make sure you select a user that can authenticate correctly with your Flow (i.e. the user is able to launch the Flow if they ran it directly).
13. Tick the **Send Session ID** check box so the Flow can login correctly as that user.
14. In the *... fields to send* section, make sure the *Id* field is in the list of **Selected Fields**.
15. Click on the **Save** button.
16. In the *Workflow Rules Using This Outbound Message* section, click on the *Rule Name* of the Workflow Rule you just created.
17. Click on the **Activate** button to make this Workflow rule live for us.

In case you have not added the Salesforce Service to your security settings (this only needs to be done once for your Salesforce org):

1. In the setup tree, find the *Administer* section.
2. Click on **Security Controls -> Remote Site Settings**.
3. Click on the **New Remote Site** button.
4. Enter a memorable name for **Remote Site Name**.
5. For the **Remote Site URL**, provide: https://salesforce.manywho.com (or perhaps another location if you're using your own implementation of this Service code).
6. Click on the **Save** button.

And that's it. When a user creates or updates an Object in Salesforce, this Workflow Rule will send a request to ManyWho to start your Flow.

#### Endpoint URL Configuration

You can configure the Endpoint URL for the Workflow Rule in various ways depending on the activity you're doing:

```
POST plugins/api/salesforce/1/workflowrules/{tenantid}/{flowid}/{playername}
```

Where the parameters are as follows:

Property | Type | Description
-------- | ---- | -----------
tenantid | String: GUID	 | The unique identifier for your tenant. The easiest way to get this value is to run your Flow from the draw tool. In the URL, the tenant id is the first long identifier:<br/><br/>`e.g. https://flow.manywho.com/03acfe49-3469-442d-9126-c7952e43c661/play/default?flow-id=3e4baabc-91ac-400a-af7a-18bb4a0defca&flow-version-id=4dc51959-3094-4ebf-8fcb-dc926c554695`
flowid | String: GUID | The unique identifier for your Flow. The easiest way to get this value is to run your flow from the draw tool. In the URL, the flow id is the second long identifier:<br/><br/>`e.g. https://flow.manywho.com/03acfe49-3469-442d-9126-c7952e43c661/play/default?flow-id=3e4baabc-91ac-400a-af7a-18bb4a0defca&flow-version-id=4dc51959-3094-4ebf-8fcb-dc926c554695`
playername | String | The unique name for your Flow user interface. By default, the player name is 'default', however, if you have created your own user experience, you can also get this value from running the flow from the draw tool. In the URL, the player name is the value just after the word 'play':<br/><br/>`e.g. https://flow.manywho.com/03acfe49-3469-442d-9126-c7952e43c661/play/default?flow-id=3e4baabc-91ac-400a-af7a-18bb4a0defca&flow-version-id=4dc51959-3094-4ebf-8fcb-dc926c554695`

In addition to the above required settings, you can optionally provide the following query string parameters to help with debugging and testing:

Name | Value
---- | -----
mode | This is the mode under which you'd like the Flow to execute. If the value is blank, the Flow will execute as normal, however, you can also use the following:<br/><br/><ul><li>**DEBUG**: Tells the Service and engine to run the flow in DEBUG mode. This means you will recieve debug notification emails and can also view logging information.</li><li>**DEBUG_STEPTHROUGH**: Tells the Service to execute the Flow, but not allow it to run through without a user debugging step-by-step. In this situation, you will be provided with a URL to join the Flow for debugging as part of your notification email.</li></ul>
email | The email that the notifications from the Service should be sent to. The Flow notifications will always go to the current Author of the Flow.

**Example**
```
POST https://salesforce.manywho.com/plugins/api/salesforce/1/workflowrules/03acfe49-3469-442d-9126-c7952e43c661/3e4baabc-91ac-400a-af7a-18bb4a0defca/default?mode=DEBUG&email=me@mycompany.com
```

### Listening to Record updates

As part of an executing Flow, it can sometimes be useful to wait for a particular record to be updated. In addition, there can be rules to determine when to proceed in the Flow. For example:

- Create a Task and wait for the Status to be *Completed*
- Load an existing Opportunity and wait for the Status to be *Closed Won*
- And the list goes on...

This can also be needed at any point in your Flow - not just the start. Equally, you may need to listen to different records depending on the route the Flow executes.

#### Configuring your Flow

There's nothing specific about a Flow that can listen to Salesforce records. Listening can happen at any point, however, Listening is only supported in the following Elements:

- **Database Load**: Load a record from Salesforce and listen to any changes to it.
- **Database Save**: Save a new or updated record to Salesforce and listen to any further changes to it.
- **Message**: Based on a previously loaded record from Salesforce, listen to any changes to it.
- **Page**: Based on a previously loaded record from Salesforce, listen to any changes to it.

It's important to note that you can only listen to records at the point to register the "listener". Once the Flow proceeds to the next step, it is no longer listening to any further updates.

To add a listener to one of the above elements, you need to add the following JSON to the Map Element:

```
"listeners": [
    {
      "developerName": "Hello",
      "serviceElementId": "18211a13-71b9-4e21-8d32-299027f5ab13",
      "listenerType": "EDIT",
      "valueElementToReferenceForListeningId": {
        "id": "028493b1-cb65-4724-8094-5e0997f4e6e1",
      },
      "attributes": null
    }
  ]
``` 

Where the properties are as follows:

Property | Type | Description
-------- | ---- | -----------
developerName | String | A memorable name for this listener so you can identify it easily in your Flow model.
serviceElementId | String: GUID | The unique identifier for the Salesforce Service in your tenant. You can get this by querying the Service API (api/draw/1/element/service?filter=) and locating the "id" property of the Salesforce Service.
listenerType | String | Currently the Salesforce Service only supports EDIT. However, in future more listeners may be supported. EDIT encompasses CREATE also.
valueElementToReferenceForListeningId | String: GUID | The unique identifier for the object Value loaded from Salesforce. In order for the listener to work, you must have first populated an object Value from Salesforce. You can then use this at any time to listen to that object. You can get the list of Values in your tenant by querying the Value API (api/draw/1/element/value?filter=substringof(developername, 'the name of my value') and locating the "id" property of the appropriate Value.
attributes | Key/Value pairs | Additional attributes that can help the Service make decisions about how best to execute the listener. This allows developers to extend our metadata as needed.

#### Configuring your Workflow Rule

In order to make a listener work, the Salesforce Service does not "ping" your Salesforce API for changes, but rather it relies on Workflow Rules to notify ManyWho of any record changes in the system. This approach minimizes the impact of this functionality on your API usage and also gives you greater control over the configuration of the rules. Here's how you configure Workflow Rules to send listener notifications:

1. Login to Salesforce (https://login.salesforce.com).
2. Click on **Setup** and find the *Build* section in the setup tree.
3. Click on **Create -> Workflow & Approvals -> Workflow Rules**.
4. Click on the **New Rule** button.
5. Select the Object you want to have your Flows listen to and click on the **Next** button. You only need to configure one listener per Object, you don't need to configure a Workflow Rule for each Flow that needs to listen to records of this Object type (e.g. Lead).
6. Enter a memorable name for **Rule Name**.
7. Select any *Evaluation Criteri*a and create a *Rule Criteria* (if you don't want Salesforce handling the listening rules, we suggest creating a *Rule Criteria* that will always be true: e.g. Lead: First Name not equal to <empty box>). You can also create the listening rules in ManyWho.
8. Click on the **Save & Next** button.
9. Click on the **Add Workflow Action** menu and select **New Outbound Message**.
10. Enter a memorable name for **Name** and the **Unique Name** should auto populate.
11. Configure the **Endpoint URL** using the documentation below this list (i.e. https://salesforce.manywho.com/plugins/api/salesforce/1/workflowrules/listener/{tenantid}).
12. For the **User to send as**, make sure you select a user that can authenticate correctly with your Flow.
13. Tick the **Send Session ID** check box so the Flow can login correctly as that user.
14. In the *... fields to send* section, make sure the Id field is in the list of **Selected Fields**.
15. Click on the **Save** button.
16. In the *Workflow Rules Using This Outbound Message* section, click on the *Rule Name of the Workflow Rule* you just created.
17. Click on the **Activate** button to make this Workflow rule live for us.

In case you have not added the Salesforce Service to your security settings (this only needs to be done once for your Salesforce org):

1. In the setup tree, find the *Administer* section.
2. Click on **Security Controls -> Remote Site Settings**.
3. Click on the **New Remote Site** button.
4. Enter a memorable name for **Remote Site Name**.
5. For the **Remote Site URL**, provide: https://salesforce.manywho.com (or perhaps another location if you're using your own implementation of this Service code).
6. Click on the **Save** button.

And that's it. When a user updates an Object in Salesforce, this Workflow Rule send a notification to ManyWho and any Flows listening to the record will execute accordingly.

#### Endpoint URL Configuration

You can configure the Endpoint URL for the Workflow Rule in various ways depending on the activity you're doing:

```
POST plugins/api/salesforce/1/workflowrules/listener/{tenantid}
```

Where the parameters are as follows:

Property | Type | Description
-------- | ---- | -----------
tenantid | String: GUID | The unique identifier for your tenant. An easy way to get this identifier is to login to the build tool using your author credentials and copy the unique identifier at the top right of the screen.

In addition to the above required settings, you can optionally provide the following query string parameters to help with debugging and testing:

Name | Value
---- | -----
mode | This is the mode under which you'd like the Flow to execute. If the value is blank, the Flow will execute as normal, however, you can also use the following:<ul><li>**DEBUG**: Tells the Service and engine to run the flow in DEBUG mode. This means you will recieve debug notification emails and can also view logging information.</li><li>**DEBUG_STEPTHROUGH**: Tells the Service to execute the Flow, but not allow it to run through without a user debugging step-by-step. In this situation, you will be provided with a URL to join the Flow for debugging as part of your notification email.</li></ul>
email| The email that the notifications from the Service should be sent to. The Flow notifications will always go to the current Author of the Flow.

**Example**
```
POST https://salesforce.manywho.com/plugins/api/salesforce/1/workflowrules/listener/03acfe49-3469-442d-9126-c7952e43c661?mode=DEBUG&email=me@mycompany.com
```

### Executing SOQL Queries

Sometimes when creating a Flow, it can be useful to execute SOQL queries against Salesforce to get exactly the data you need. Though ManyWho does allow you to construct queries using the standard tooling, we don't support more complex queries - for example:

- Grouping and aggregate functions
- Complex AND/OR where clauses (often where you need lots of brackets to get the logic right)
- Queries that are just easier to understand in code

We'd obviously recommend you use the standard metadata approach as much as possible as it reduces hard coded dependencies.

#### Configuring your Flow

SOQL queries are supported in the following Elements:

- **Database Load**: Add complex queries to your standard database load operations
- **Page**: Add additional query support to your Table and Combobox lookups

Wherever you have an **ObjectDataRequest** object in your flow, you can add complex SOQL queries. To add SOQL support to your **ObjectDataRequest**, you need to use the **Command** property:

```json
  "objectDataRequest": {
    "typeElementId": "531b4fdb-6d8a-4b79-8f86-f6b5c400f931",
    "typeElementBindingId": "5958a64d-92ca-4d40-aea3-4925eb227540",
    "listFilter": null,
    "command": {
      "commandType": "SOQL",
      "properties": {
        "soql": "SELECT Asset_Image_View__c, Id, Availability_Date_Summary__c, Model__c, Latest_Lessee__c, Model_ID__c, Name, YOM__c FROM Asset__c WHERE (Availability_Date__c = NEXT_N_DAYS:365 OR Availability_Date__c <= TODAY) AND Model__c = 'flowkey___bf213c34-4008-41d4-85ad-09cb5cf2ddb0|30e8e681-699b-47d5-b47f-7bdd06aaa8b0___flowkey'"
      }
    }
  }
```

Where the properties are as follows:

Property | Type | Description
-------- | ---- | -----------
typeElementId | String: GUID | The unique identifier for the Type that will be used to hold the data in the query. You can get this by querying the Type API (api/draw/1/element/service?filter=) and locating the "id" property of the Salesforce Service.
typeElementBindingId | String: GUID | The unique identifier for the Type Binding that will be used to translate the results of the query lookup to the standard Type properties. If you load the Type, the Binding identifier appears in the "binding" section of the JSON document. If you are using a non-aggregate SOQL query, you can simply use the existing Salesforce binding. If you are performing aggregate functions, you need to create a separate Type and Type Binding (see section below).
commandType | String | Currently the Salesforce Service only supports "SOQL". Meaning that this is a SOQL command we are executing on the Service.
soql | String	 | The actual SOQL that should be executed on the Service. If you need to reference a Value in your flow, the notation is slightly different from the standard notation of {![My Value]}. The notation structure is as follows:<br/><br/>`flowkey___<the id of the value>bar<the type element property id>___flowkey`<br/><br/>If your value reference does not require a type element property id, you should substitute: `00000000-0000-0000-0000-000000000000`<br/><br/>**NOTE**: If your query returns a non-aggregate result, you simply need to include all the columns you'd like to have populated in your Value. It's also recommended when creating SOQL queries that you test them using the Salesforce developer tools to make sure they are correctly formatted.

#### Advanced Concepts: Aggregate Functions

If you are creating a SOQL query because you need to get aggregate information (e.g. a record count of grouped records, a maximum number of records, etc.) you need to create a Type for that aggregate result. We'll walk through an example to illustrate how that can be done here.

##### Construct the SOQL

Let's assume we want to get a summary list of aircraft that are available for leasing over the next year. We want to group the results by Model of aircraft and return that list with the count of how many we have in stock currently for lease. Here's the SOQL for that query:

```
SELECT Max(Model_Replica__c), Max(Asset_Type__c), Max(Name), Count(Id), Max(Asset_Image_View__c) FROM Asset__c WHERE (Availability_Date__c = NEXT_N_DAYS:365 OR Availability_Date__c <= TODAY) AND Asset_Type__c = 'Aircraft' GROUP BY Model__c
```

You can see in the query that we're using a number of aggregate functions and we're grouping by Model as expected. We now need to create a Type in ManyWho that will be used to map the result of this query to Values in our Flow. The Type defines the structure of our business objects as well as the mapping between the underlying database. As a result, we need to create a business object Type to represent this summary.

##### Create the Type

Looking at the above Query, we should create a Type for the associated fields/properties. We can do that in the Draw tool very simply:

1. Create a new Type called "Model Summary"
2. Create the following fields/properties for that Type based on the above query:
    - Model Replica (String)
    - Asset Type (String)
    - Name (String)
    - Count (Number)
    - Image (String) 
3. Save the Type.

##### Create the Type Binding

Now we need to create the Binding. We'll need to do that manually through the Build tooling.

1. Find your newly created Type using: api/draw/1/element/type?filter=substringof(developerName, 'Model Summary').
2. Find the "id" property for the Type and the use: api/draw/1/element/type/<id value> to load the full Type definition.
3. Copy the contents of the right pane into the left pane - we're going to edit the Type definition.
4. Find the section in the document for "bindings". This should be null currently.

You now need to create a binding for Salesforce with field bindings from your SOQL query. This will tell ManyWho how to get the data from the your SOQL query into your Flow.

1. Find your Salesforce Service using: api/draw/1/element/service?filter=
2. Find the "id" property for the Salesforce Service.

Let's have a look at how we'd configure the binding - here's an example here:

```
  "bindings": [
    {
      "developerName": "Salesforce.com Model Summary Binding",
      "developerSummary": "The binding to show a summary of grouped assets filtered by date range.",
      "databaseTableName": "Asset__c",
      "serviceElementId": "de48e684-2381-4f08-b2a6-a7e59ad0ee8b",
      "propertyBindings": [
        {
          "databaseFieldName": "expr0",
          "typeElementPropertyId": "<the id of the Model Replica property>",
        },
        {
          "databaseFieldName": "expr1",
          "typeElementPropertyId": "<the id of the Asset Type property>",
        },
        {
          "databaseFieldName": "expr2",
          "typeElementPropertyId": "<the id of the Name property>",
        },
        {
          "databaseFieldName": "expr3",
          "typeElementPropertyId": "<the id of the Count property>",
        },
        {
          "databaseFieldName": "expr4",
          "typeElementPropertyId": "<the id of the Image property>",
        }
      ],
    }
  ] 
```

Where the properties are as follows:

Property | Type | Description
-------- | ---- | -----------
developerName | String | A memorable name for this binding so you can identify it easily in your Flow model.
databaseTableName | String | The API name of one of the tables used in the SOQL query (if you have more than one table, just pick any of them).
serviceElementId | String: GUID | The unique identifier for the Salesforce Service in your tenant. You can get this by querying the Service API (api/draw/1/element/service?filter=) and locating the "id" property of the Salesforce Service.
propertyBindings | Array | Each field in your SOQL query needs a property binding if you want the Value to populate in your Flow.
databaseFieldName | String | In Salesforce, when you use aggregate functions, it returns a the column name as exprn. As a result, for each aggregate function in our query, we use expr0, then expr1, etc incrementing 'n' for each aggregate. This property must match the name of a column returned in your SOQL query. If you're unsure of the names, simply execute the SOQL in the Salesforce developer tooling and look at the column names in the return resultset - you need to match those.
typeElementPropertyId | String: GUID | In the "properties" section of your Type, you should have each property listed with an identifier. In order to match your SOQL field mapping with your friendly Type names, you need to match each property in your Type with the binding. You do this using the "id" of the property and associating it with each associated property binding.

#### Ready to Use

Once you have created the Type and the appropriate binding you can now use this Type like any other Type in your Flow.


### Write a custom Service in Apex

In this recipe, we show you how to write a new Service using Salesforce Apex. Why would you need to write code?

- The logic is just too complex or it's more appropriate for a developer to manage the logic.
- You want to leverage some existing code within your Flow. 
- You want Salesforce to perform a complex multi-object query.

This is certainly not an exhaustive list as all projects vary. However, there can be situations where you need to enlist the support of your friendly neighborhood Apex developer.

#### Create the Common ManyWho API objects

We do not yet have a fully comprehensive set of our API objects in Salesforce Apex, however, we have many of the main ones. In order to make these objects available to you in your Salesforce org, download the SDK file here:

[ManyWho Apex API](https://drive.google.com/file/d/0BxOahH5Z4tUTX2NBcjY3aGlFLTg/view?usp=sharing)

To add this to your org, simply do the following:

1. Login to Salesforce (https://login.salesforce.com).
2. Click on **Setup** and find the *Build* section in the setup tree.
3. Click on **Develop -> Apex Classes**.
4. Click on the **New** button.
5. Copy the contents of the above file into the **Apex Class** tab.
6. Click on the **Save** button.

And that's it. You can now code up a Service directly in Apex. Let's do that now.

#### Tell ManyWho what the Service does

In order for Flow builders to leverage the Service, you need to provide a "describe" API endpoint. This informs the ManyWho platform as to what the Service can do - i.e. what functions it exposes for the Flow builder to leverage. Here's an example Apex class that describes a very basic call with a single input and single output:

```
@RestResource(urlMapping='/something/metadata')
global class SomethingDescribe {
 
    public static final String INPUT_MY_INPUT = 'An Input';
    public static final String OUTPUT_MY_OUTPUT = 'An Output';
 
    @HttpPost
    global static void doPost() {
        ManyWhoAPI.DescribeServiceActionResponseAPI describeServiceActionResponseAPI = null;
        ManyWhoAPI.DescribeServiceResponseAPI describeServiceResponseAPI = null;
        JSONGenerator jsonGenerator = null;
 
        // Create the describe response
        describeServiceResponseAPI = new ManyWhoAPI.DescribeServiceResponseAPI();
        describeServiceResponseAPI.actions = new List<ManyWhoAPI.DescribeServiceActionResponseAPI>();
 
        // Add a couple of configuration values that this service needs to function for all requests               
        describeServiceResponseAPI.configurationValues = new List<ManyWhoAPI.DescribeValueAPI>();
        describeServiceResponseAPI.configurationValues.add(new ManyWhoAPI.DescribeValueAPI('Hello', ManyWhoAPI.CONTENT_TYPE_STRING, true));
        describeServiceResponseAPI.configurationValues.add(new ManyWhoAPI.DescribeValueAPI('World', ManyWhoAPI.CONTENT_TYPE_STRING, true));
 
        // Create an action that authors and users can leverage
        describeServiceActionResponseAPI = new ManyWhoAPI.DescribeServiceActionResponseAPI();
        describeServiceActionResponseAPI.uriPart = 'dosomething';
        describeServiceActionResponseAPI.developerName = 'Do Something';
        describeServiceActionResponseAPI.developerSummary = 'Does something really cool';
        describeServiceActionResponseAPI.serviceInputs = new List<ManyWhoAPI.DescribeValueAPI>();
        describeServiceActionResponseAPI.serviceInputs.add(new ManyWhoAPI.DescribeValueAPI(INPUT_MY_INPUT, ManyWhoAPI.CONTENT_TYPE_STRING, true));
        describeServiceActionResponseAPI.serviceOutputs = new List<ManyWhoAPI.DescribeValueAPI>();
        describeServiceActionResponseAPI.serviceOutputs.add(new ManyWhoAPI.DescribeValueAPI(OUTPUT_MY_OUTPUT, ManyWhoAPI.CONTENT_TYPE_STRING, false));
 
        // Add the action to the describe
        describeServiceResponseAPI.actions = new List<ManyWhoAPI.DescribeServiceActionResponseAPI>();
        describeServiceResponseAPI.actions.add(describeServiceActionResponseAPI);
 
        // Tell ManyWho that this service provides logic only
        describeServiceResponseAPI.providesLogic = true;
         
        jsonGenerator = JSON.createGenerator(false);
        jsonGenerator.writeObject(describeServiceResponseAPI);
         
        // Return the describe to the caller
        RestContext.response.addHeader('Content-Type', 'application/json');
        RestContext.response.responseBody = Blob.valueOf(jsonGenerator.getAsString());
    }
}
```

It's important to note a few things about the above code:

- The root URL for your Service is /something and the describe endpoint is identified with the /metadata extension as per the RestResource attribute.
- The developerName constants are important as they'll be needed for the implementation of this Service. The describe API simply tells ManyWho "what" this Service does - it is not the actual implementation.
- The interface is provided as inputs/outputs which can also include List and Object types. This example simply shows "primitive" types for simplicity.

#### Create the code that actually does the work

In order for Flow users to leverage the Service, you need to provide an "invoke" API endpoint. This actually performs the operation at runtime - i.e. it's the actual implementation of what was described above. Here's an example Apex class that invokes a very basic call with a single input and single output (as per the "describe" above):

```
@RestResource(urlMapping='/something/dosomething')
global class SomethingInvokeDoSomething {
    @HttpPost
    global static void doPost() {
        ManyWhoAPI.ServiceResponseAPI serviceResponseAPI = null;
        ManyWhoAPI.ServiceRequestAPI serviceRequestAPI = null;
        JSONGenerator jsonGenerator = null;
        JSONParser jsonParser = null;
        String inputValue = null;
        // Get the JSON body in the request
        jsonParser = JSON.createParser(RestContext.request.requestBody.toString());
        // Parse out the service request object
        serviceRequestAPI = (ManyWhoAPI.ServiceRequestAPI)jsonParser.readValueAs(ManyWhoAPI.ServiceRequestAPI.class);
        // The user value passed into this invoke call
        inputValue = ManyWhoAPI.getContentValue(serviceRequestAPI.inputs, SomethingDescribe.INPUT_MY_INPUT, true);
 
        // Do something interesting here...
  
        // Create the response to send back to ManyWho
        serviceResponseAPI = new ManyWhoAPI.ServiceResponseAPI();
        serviceResponseAPI.token = serviceRequestAPI.token;
        serviceResponseAPI.tenantId = serviceRequestAPI.tenantId;
        serviceResponseAPI.invokeType = ManyWhoAPI.INVOKE_TYPE_FORWARD;
        serviceResponseAPI.outputs = new List<ManyWhoAPI.EngineValueAPI>();
        serviceResponseAPI.outputs.add(new ManyWhoAPI.EngineValueAPI(SomethingDescribe.OUTPUT_MY_OUTPUT, ManyWhoAPI.CONTENT_TYPE_STRING, 'World!!'));
        // Generate the service response json
        jsonGenerator = JSON.createGenerator(false);
        jsonGenerator.writeObject(serviceResponseAPI);
  
        // Return the describe to the caller
        RestContext.response.addHeader('Content-Type', 'application/json');
        RestContext.response.responseBody = Blob.valueOf(jsonGenerator.getAsString());
    }
}
```

It's important to note a few things about the above code:

- The RestResource attribute matches the root URL for the Service, plus the uriPart property provided in your describe. This class will handle the implementation for the 'dosomething'.
- We've used the constants in the describe class to make sure the developerName properties match. If these are changed you can also break running users.

#### Create a Public Site to host your API

If you already have a Public Site, you don't need to do these steps again (assuming you want to re-use the public site):

1. Login to Salesforce (https://login.salesforce.com).
2. Click on **Setup** and find the *Build* section in the setup tree.
3. Click on **Develop -> Sites**.
4. Click on the **New** button.
5. Enter a memorable name for the **Site Label**. The **Site Name** should populate correctly based on that label.
6. Do not provide a **Default Web Address**.
7. For the **Active Site Home Page**, select UnderConstruction for now.
8. Tick the **Require Secure Connections (HTTPS)** checkbox.
9. Click on the **Save** button.
10. You will be prompted to provide a subdomain for your site.
11. Enter a memorable name and click on the **Save** button.
12. On the *Sites* page, find your site listed and click on the **Activate** link.
13. For the same site, click on the *Site Label* for your site. Make a note of the *Site URL*.
14. Click on the **Public Access Settings** button.
15. Scroll down the page to the *Enabled Apex Class Access* section.
16. Click on the **Edit** button for that section.
17. Click on each of the classes you created for your Service and **Add** them to the list of **Enabled Apex Classes**.
18. Click on the **Save** button.

Those steps will have created a public site at the address provided for the Site URL noted in step 13. Your Service will be available at:

```
https://<your subdomain>-developer-edition.<your pod>.force.com/services/apexrest/<your root service address>
```

To test the Service is configured correctly, you can use one of many available tools to send a JSON POST request to the service. Try sending the following JSON in the post to check the basic service is available:

**Example**
```
POST https://<your subdomain>-developer-edition.<your pod>.force.com/services/apexrest/<your root service address>/<your uri part for the service>
```
```json
{
  "joinPlayerUri":"Hello",
  "playerUri":"World",
  "uri":"http://manywho.com"
}
```
 
Assuming that returns a JSON response with no errors, you should be able to now install the Service in ManyWho.

#### Installing your Service in ManyWho

1. Login to the draw tool using your authoring credentials.
2. Click on the **Services** option in the menu bar.
3. Click on the **Create New** button.
4. Provide a memorable name for **Name**.
5. For the **Service URL**, provide your root Service address (without the "metadata" or "uriPart" at the end).
6. Click **Next** to enter in additional configuration settings and finish as usual.

