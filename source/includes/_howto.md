# How To

We've created this section to include answers to common questions. Please refer to the core API documentation for more in-depth information about various features, as this section does not give a complete picture of all the things you can do with the Platform.

## General

### Debugging a Flow

As with all things in technology, it often doesn't work the first time. When things don't work, there's nothing more frustrating than not know what's gone wrong. As a result, ManyWho has built-in debugging capabilities to help Flow Builders get detailed knowledge of what's happening on the service.
When running a Flow from the tooling, you will have noticed that we three buttons for running a Flow. If running in Debug or Debug Step-through, the platform will do the following:

- Populate the preCommitStateValues so you can see exactly what values are waiting in the engine to be committed. These are the changes that will be applied to the Values in your Flow State once the Map Element and Map Element Outcome have successfully completed and navigated the user to the next Element in the Flow.
- Populate the stateValues so you can see exactly what Values are currently being stored in the engine State.

However, in addition to the features of the debug options, the engine will also perform substantially more validation on the incoming requests to make sure the request is valid. Therefore, if you're building a new HTML5 Player or simply debugging your Flows, make sure you flip the mode to one of the 'debug' modes - it will save you a lot of time!

## Pages

### Creating Picklists

It's very easy to create re-usable PickList or ComboBox Page Components using the Platform. However, there are a few steps to do this to ensure your Flow applications are consistent:

1. You need to create a Type for the structure of your entries in the ComboBox. If you're used to HTML, this might contain a Label and a Value. But in reality, the Type can be as complicated as you like and hold as much data as you need to drive the rules and logic of your Flow.
1. You need to create a List Value to hold the data in your ComboBox.
1. You can optionally create an Object Value to hold the user selection.
1. You need to create the ComboBox Page Component that brings it all together.

<aside class="notice">
<b>Hint</b><br/>
Try creating a Type with two string properties: Label and Name. From there you can always add more properties. You can then also re-use this Type for all ComboBoxes you use for all Flows. You can also re-use your List for all Flows ensuring keep central lists of all picklists in one place.
</aside>

### Creating Dynamic Pages

To create Dynamic Pages, you should use what we call "Page Conditions". Have a look in the PageElement documentation under the Draw API for details on how PageConditions are configured. In our tooling, you can also use our point-and-click Page Conditions editor to easily configure new and existing logic in your Pages.

### Hiding Buttons

Referencing Creating Dynamic Pages, you cannot currently create Page Conditions for Outcomes. However, it is still possible to apply dynamic logic to Outcomes. The way you do this is to "place the outcome with" a Page Component and then apply the Page Conditions for hide/display to the Page Component. When the Page Component is hidden, the Outcome (button) will be hidden also.

### Creating Editable "Spreadsheets"

It can be helpful to allow users to "inline" edit data contained in a Table component. The following assumes you have a working knowledge of Flow building.

1. Create a new Type or use an existing Type, this will represent the columns of your Table.
1. Create a new List Value of the above Type.
1. Add some data to the List via the List editor. These entries will represent the rows in your Table.
1. Create a new Page and new Page Layout in your Flow.
1. Create a new Table Page Component referencing your List as the data source, and also the place to save the data.
1. Add the relevant columns you want to display to the running user(s). Tick the "Editable" box for all columns you want the user to be able to edit inline.
1. Save the Page Layout and Page.

That's it. You've now created an editable Table.

<aside class="notice">
<b>Data</b><br/>
It's important to note that you can make any Table editable - even if the data is sourced from a Service.
</aside>

### Adding Custom Components to your Pages

Currently some Page Components aren't available in the drag & drop Page Editor, however they are available in the UI framework. For example, have a look at our GitHub repository:

**Digital Signature Pad**: Allows you to draw your signature directly on the Page.

http://github.com/manywho/ui-signature-pad

**Box**: Includes the various UI components available from Box.com, such as the document Viewer.

http://github.com/manywho/ui-box

**QR Code Reader**: Add a QR Code scanner/reader to your Flow applications.

http://github.com/manywho/ui-qr-code

However, our UI framework also includes additional UI components are standard. Check out the Embed section and our UI Framework for details.

The simplest way to add a custom component is to do the following:

1. Find a component that's similar to the custom component in terms of features.
1. Drag that component into your Page Layout, providing as many of the configuration options as possible.
1. Click on the Edit Page Metadata button.
1. Find the component you just added in the JSON.
1. Change the "componentType" to the component type value provided in the documentation for the custom component.
1. Click to Edit the component again, and note that all settings are now available to change.

<aside class="notice">
<b>Note</b><br/>
You should reference the settings for the custom component on which settings can be used and are supported.
</aside>

### Searching Specific Database Columns

You can add column specific search capabilities by configuring your Page metadata as shown in the example JSON.

```json
"objectDataRequest": {
    "typeElementBindingId": null,
    "typeElementId": null,
    "listFilter": {
        "search": "Search For",
        "searchCriteria": [
            {
                "columnTypeElementEntryId": "{id of the property}"
            }
        ]
    },
    "command": null,
    "typeElementDeveloperName": null
}
```

<aside class="notice">
<b>Service</b><br/>
It's important to note that searching by specific database columns is based on the Service. Not all Services support this feature so you should make sure you check out any Service documentation if you're not getting the expected results. In addition, the search by column is not available for data that is bound to a List Value.
</aside>

## Navigation

### Changing the Navigation Menu Dynamically

Each Map Element in the Flow has the ability to override the standard Navigation menu. Have a look in the MapElement documentation under the Draw API for details on how NavigationOverrides are configured. You can disable or hide individual parts or the whole Navigation menu by adding an override to a specific map element. For example if you have a Step / Page in your Flow that you don't want to display the navigation on you would add an override like the following to the Map Element's metadata:

```json
"navigationOverrides": [
    {
        "isEnabled": true,
        "isVisible": false,
        "navigationElementId": "{id of the navigation to hide}",
        "navigationItemId": "{id of the navigation item to hide}" //  e.g. 00000000-0000-0000-0000-000000000000
        "locationMapElementId" "{id of the map element the navigation item points to}" // Omit if you are hiding / disabling the entire nav bar
    }
]
```

A couple of interesting features to mention:

1. Set the `navigationItemId` to an empty Guid (I.e. "00000000-0000-0000-0000-000000000000") to hide the entire Navigation menu from the running user(s). This is in addition to setting "isVisible" to `false`;
1. You can edit the Navigation Element metadata by using the Draw API with the API tool. Make sure you check out the NavigationElement documentation for details on this.
1. The NavigationOverride will continue to take affect for every subsequent Map Element that is navigated to until it has been cleared. You can clear navigation overrides by setting "clearNavigationOverrides" to true on a Map Element.
