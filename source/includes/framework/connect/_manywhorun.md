## ManyWho Run

ManyWho also provides a number of features that you can access through the Run Service. These are features that help Flow Builders create more robust Flow applications:

1. **Execute Sub-Flows**: The ability to initialize, invoke and listen to changes in another Flow. This allows you to handle parallel Flow execution and create Flow "inboxes".
2. **Available Flows**: Exposes the list of Flows that are available to run.
3. **Sharing**: Exposes the sharing functionality to allow Flow Builders to configure how and when users can provide escalated access to Swimlanes.

For more information on Run functions, you can also reference the Run API documentation.

### Installing the ManyWho Run Service

#### Intro

To set up the ManyWho Run Service, please complete the following instructions. The ManyWho Run Service is part of the core platform.

##### Features

Name | Description
---- | -----------
**Logic** | You can execute Sub-Flows in your ManyWho Tenant.
**Listening** | Listen to Flow States in your ManyWho Tenant.
**Database** | Query Flows and Flow States in your ManyWho Tenant.

#### Configuration

When installing the Service, you should use the following settings:

**Connection Uri**

`https://flow.manywho.com/plugins/manywho/api/run/1`

**Configuration Values**

None

### Creating a Flow Listing

A Flow Listing allows running user(s) to view and run the Flows available in your ManyWho Tenant. This can be used in conjunction with the "Inbox" to allow your running user(s) to see a list of Flows available and also see a list of Flow States that may require action from them. In this example, we'll use the FlowOut feature to create an Inbox.

In order to complete the steps in this example, you will need to have a reasonable understanding of how to build Flows already. We'll assume you have some Flows already in your Tenant and you now wish to build an Inbox for managing them.

1. Create a new Object Value of Type Flow. Call it "State".
1. Create a new Flow for your Flow Listing (or re-use an existing one). This must be in the same Tenant.
1. In the Shared Elements tool, import the Flow Value you just created. Make sure the Flow Type and ManyWho Run Service are also imported.

Now that we have the basics needed for our Flow listing, we can create our Page for the listing:

1. Drag a Page onto your Flow.
1. Create a new Page Layout for this Page.
1. Drag a new Table component onto your Page Layout.
1. Bind that Table to the ManyWho Run Service and select the Flow Type and Binding to list your Flows in the Tenant.
1. Create a number of columns for your Table, you'll see we expose various pieces of information about the Flow.
1. Put the selected value into the Flow Value you created.
1. Save your Page Layout and Page.

As you can see the Flow listing is basically just like any other table of data in ManyWho. However, rather than querying data from, for example, Salesforce, you're querying the ManyWho database for Flows. As a result, you can create a filter on Developer Name to reduce the list just as you filter any other data from a Service.

At this stage, you will need to open the API tooling as we do not yet have point-and-click tooling for the FlowOut functionality:

1. Click on API in the Admin area of the tooling.
1. Use the `...map?filter=` endpoint to GET the list of Map Elements.
1. In the provided list, find your Inbox Map Element (the Page in your Flow). Grab the "id" property value.
1. Use the `...map/{id}` endpoint (pasting your id into the appropriate place) to GET the full Inbox Map Element.
1. Copy everything in the right pane into the left pane so we can make edits.

In order to allow the running user(s) to "join" a running Flow State (i.e. They click on a button to open a Flow that's running), we need to add the Outcome and configure the FlowOut. For more information on Outcomes, have a look at the MapElement in the Draw API documentation. Add the following JSON for your "outcomes" property:

```json
"outcomes": [
  {
    "developerName": "Run",
    "label": "Run",
    "pageActionType": "SAVE",
    "isBulkAction": false,
    "pageActionBindingType": "EDIT",
    "pageObjectBindingId": "{id}",
    "order": 0,
    "flowOut": {
      "valueElementFlowId": {
        "id": "{id}",
        "typeElementPropertyId": "{id}",
        "command": null
      }
    }
  }
]
```

Looking at the above metadata, you need to make some amendments to make this work. In order to allow running user(s) to Run a Flow, we need to tell the "Run" outcome where it's getting the Flow identifier from (so we know which Flow we're actually running). This will be the Flow the user selects in the Table. If you remember, we bound the Flows table to our Flow Value. That Flow Value will contain the selected Flow - which holds the unique identifier for the Flow in it's ID property. Here's how you get that information:

1. Use the `.../value?filter=` endpoint to get the list of values. Have a look at the ValueElement documentation in the Draw API for more details on this.
1. Find the Value with a "developerName" value of "Flow". Grab the "id" property value.
1. Use the `...value/{id}` endpoint (pasting your id into the appropriate place) to GET the full Value Element.
1. In the left pane, also paste the "id" property value into the "id" property in the "valueElementFlowId". I.e. here: `"valueElementFlowId"` -> `"id"`. This tells the FlowOut we're referencing your Flow Value for the information.
1. In the right pane again, find the "typeElementId" property for the "Flow" Value. We need to load the Type Element for Flow.
1. Use the`.../type/{id}` endpoint (pasting your typeElementId into the id placeholder) to GET the full Type Element.
1. In the Type definition, find the property with the "developerName" property called "ID". Grab the "id" property value for that property.
1. In the left pane, paste this property id into the "typeElementPropertyId" property in the "valueElementFlowId". I.e. here: `"valueElementFlowId"` -> `"typeElementPropertyId"`. This tells the FlowOut we're referencing the ID of the Flow Value, not the whole Flow Value.

That's it. The above instructions will ensure that this Outcome will pass the Flow identifier into the ManyWho platform so it knows which Flow to run. At this stage, we can simply save our MapElement by doing the following:

- Use the `.../map` endpoint to POST your amended JSON back to the Draw API. Have a look at the MapElement documentation in the Draw API for more information on this. Also, you might check out the *Creating an Inbox* documentation above as this would allow you to dynamically join running Flow States.

All of these changes will have been applied to your open Flow in the tooling, so you can simply Run/Publish the Flow to see the changes.

If you would like to "Place the Outcome with" the States table in your Page Layout, you can do these additional steps:

1. In the MapElement definition in the left pane, copy the value for the "pageElementId" property.
1. Use the `.../page/{id}` endpoint to load the PageElement associated with this MapElement.
1. In the right pane, find the "TABLE" component for the Flows. Grab the "id" property value.
1. In the left pane, paste the "id" property value into the "pageObjectBindingId" value. This tells the UI that the Outcome should be placed with the Flows Table.

Once you've completed these steps, save your MapElement changes as you did above using the `.../map` endpoint.

### Creating an "Inbox"

An Inbox allows running user(s) to access the list of Flow States (or Tasks) that they need to complete. It can also be used to simply show the status of various running Flow States in your Tenant. In this example, we'll use the FlowOut feature to create an Inbox.

In order to complete the steps in this example, you will need to have a reasonable understanding of how to build Flows already. We'll assume you have some Flows already in your Tenant and you now wish to build an Inbox for managing them.

1. Open the Flow you want to monitor from your Inbox.
1. Click on Publish.
1. Copy the Link to your Flow and paste it into NotePad.
1. In the Url, is the unique identifier for this flow. E.g.: https://flow.manywho.com/72dd7009-a144-46b4-b602-5fb5f03dc00a/play/default?flow-id=**68ac3ace-ae71-480c-a839-5d52782f0dfa**
1. Create a new String Value and paste in your Flow Id as the default value. Call it "FlowId: {name of your Flow}".
1. Create a new Object Value of Type State. Make sure you select "State" and not "$State" as the latter is the system Value. Call it "State".
1. Create a new Flow for your Inbox (or re-use and existing one). This must be in the same Tenant. Make sure you use the same Service as you did for the Sub-Flow for managing identity. If the Sub-Flow uses a different identity provider, this can cause issues.
1. In the Shared Elements tool, import the State Value you just created. Make sure the State Type and ManyWho Run Service are also imported.

Now that we have the basics needed for our inbox, we can create our Page for the inbox:

1. Drag a Page onto your Flow.
1. Create a new Page Layout for this Page.
1. Drag a new Table component onto your Page Layout.
1. Bind that Table to the ManyWho Run Service and select the State Type and Binding to list your States in the Tenant.
1. Create a number of columns for your Table, you'll see we expose various pieces of information about the Flow State.
1. Put the selected value into the State Value you created.
1. Save your Page Layout and Page.

As you can see the Inbox is basically just like any other table of data in ManyWho. However, rather than querying data from, for example, Salesforce, you're querying the ManyWho database for Flow States. As a result, you can create a filter on External Id to reduce the list just as you filter any other data from a Service.

At this stage, you will need to open the API tooling as we do not yet have point-and-click tooling for the FlowOut functionality:

1. Click on API in the Admin area of the tooling.
1. Use the `...map?filter=` endpoint to GET the list of Map Elements.
1. In the provided list, find your Inbox Map Element (the Page in your Flow). Grab the "id" property value.
1. Use the `...map/{id}` endpoint (pasting your id into the appropriate place) to GET the full Inbox Map Element.
1. Copy everything in the right pane into the left pane so we can make edits.

In order to allow the running user(s) to "join" a running Flow State (i.e. They click on a button to open a Flow that's running), we need to add the Outcome and configure the FlowOut. For more information on Outcomes, have a look at the MapElement in the Draw API documentation. Add the following JSON for your "outcomes" property:

```json
"outcomes": [
  {
    "developerName": "Join",
    "label": "Join",
    "pageActionType": "SAVE",
    "isBulkAction": false,
    "pageActionBindingType": "EDIT",
    "pageObjectBindingId": "{id}",
    "order": 0,
    "flowOut": {
      "valueElementStateId": {
        "id": "{id}",
        "typeElementPropertyId": "{id}",
        "command": null
      }
    }
  },
  {
    "developerName": "Start",
    "label": "Start",
    "pageActionType": "SAVE",
    "isBulkAction": false,
    "pageActionBindingType": "NEW",
    "pageObjectBindingId": "{id}",
    "order": 0,
    "flowOut": {
      "valueElementFlowId": {
        "id": "{id}",
        "typeElementPropertyId": "{id}",
        "command": null
      }
    }
  }
]
```

Looking at the above metadata, you need to make some amendments to make this work. In order to allow running user(s) to join a running Flow State, we need to tell the "Join" outcome where it's getting the Flow State identifier from (so we know which Flow State we're actually joining). This will be the State the user selects in the Table. If you remember, we bound the States table to our State Value. That State Value will contain the selected State - which holds the unique identifier for the State in it's ID property. Here's how you get that information:

1. Use the `.../value?filter=` endpoint to get the list of values. Have a look at the ValueElement documentation in the Draw API for more details on this.
1. Find the Value with a "developerName" value of "State". Grab the "id" property value.
1. Use the `...value/{id}` endpoint (pasting your id into the appropriate place) to GET the full Value Element.
1. In the left pane, also paste the "id" property value into the "id" property in the "valueElementStateId". I.e. here: `"valueElementStateId"` -> `"id"`. This tells the FlowOut we're referencing your State Value for the information.
1. In the right pane again, find the "typeElementId" property for the "State" Value. We need to load the Type Element for State.
1. Use the`.../type/{id}` endpoint (pasting your typeElementId into the id placeholder) to GET the full Type Element.
1. In the Type definition, find the property with the "developerName" property called "ID". Grab the "id" property value for that property.
1. In the left pane, paste this property id into the "typeElementPropertyId" property in the "valueElementStateId". I.e. here: `"valueElementStateId"` -> `"typeElementPropertyId"`. This tells the FlowOut we're referencing the ID of the State Value, not the whole State Value.

The above instructions will ensure that this Outcome will pass the Flow State identifier into the ManyWho platform so it knows which Flow State to join. Now we should configure the "Start" Outcome to start a new Flow so the running user(s) can kick off new Flows from our Inbox:

1. Use the `.../value?filter=` endpoint to get the list of values. Have a look at the ValueElement documentation in the Draw API for more details on this.
1. Find the Value with a "developerName" value of "FlowId: {name of your Flow}". Grab the "id" property value.
1. In the left pane, paste the "id" property value into the "id" property in the "valueElementFlowId". I.e. here: `"valueElementFlowId"` -> `"id"`. This tells the FlowOut we're referencing your specific Flow.

That's it. At this stage, we can simply save our MapElement by doing the following:

- Use the `.../map` endpoint to POST your amended JSON back to the Draw API. Have a look at the MapElement documentation in the Draw API for more information on this. Also, you might check out the *Creating a Flow Listing* documentation above as this would allow you to dynamically assign the Flow to Start rather than "hard-coding" the FlowId.

All of these changes will have been applied to your open Flow in the tooling, so you can simply Run/Publish the Flow to see the changes.

If you would like to "Place the Outcome with" the States table in your Page Layout, you can do these additional steps:

1. In the MapElement definition in the left pane, copy the value for the "pageElementId" property.
1. Use the `.../page/{id}` endpoint to load the PageElement associated with this MapElement.
1. In the right pane, find the "TABLE" component for the States. Grab the "id" property value.
1. In the left pane, for each of the Outcomes, paste the "id" property value into the "pageObjectBindingId" value. This tells the UI that the Outcome should be placed with the States Table.
1. For the "Start" Outcome, change the "isBulkAction" from `false` to `true`. This will ensure the Outcome appears at the top of the Table.

Once you've completed these steps, save your MapElement changes as you did above using the `.../map` endpoint.
