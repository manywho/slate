## Page Element

> Example Request:

```json
{
  "label": "Incident Page",
  "pageContainers": null,
  "pageComponents": null,
  "pageConditions": null,
  "stopConditionsOnFirstTrue": false,
  "attributes": {
    "key1": "attribute1",
    "key2": "attribute2"
  },
  "tags": null,
  "updateByName": false,
  "elementType": "PAGE_LAYOUT",
  "developerName": "Incident Page",
  "developerSummary": "My page for gathering Incident information",
  "id": "{id}"
}
```

*The Page Element object provides the structure of your pages or screens.*

The purpose of the Page Element is to allow Flow builders to lay out the structure of the pages the users will interact with as part of the Flow application. The Page Element is extremely extensible and allows developers to create their own Components and Containers as needed to give users the best possible experience using your Flow application. The base properties of the Page Element are outlined here.

#### Page Element

Key | Description
--- | -----------
**id**<br/>string | A unique identifier field assigned by the platform. This value should not be included for new Page Elements.
**elementType**<br/>string | A unique element type for the Page Element. Valid values are:<ul><li>**PAGE_LAYOUT**: Page Layout Element.</li></ul>
**developerName**<br/>string | The name for the Page Element. This is typically a helpful name to remind builders of the purpose of the Page Element.
**developerSummary**<br/>string | The summary for the Page Element. This is typically additional information that will help explain the purpose of the Page Element.
**label**<br/>string | The label for the Page Element. This will appear to the running user(s).
**pageContainers**<br/>array | The configuration of the Page Containers that set the layout of the Page Components. See Page Containers below for details.
**pageComponents**<br/>array | The configuration of the Page Components that provide and gather information from and to the running user(s). See Page Components below for details.
**pageConditions**<br/>array | The configuration of the Page Conditions that set out various business rules for how the Page Layout is rendered to the running user(s). See Page Conditions below for details.
**stopConditionsOnFirstTrue**<br/>boolean | Indicates to the engine that the platform should stop evaluating the array of pageConditions as soon as one of them evaluates to true.
**attributes**<br/>object | Key/value pairs that provide additional information for the Page Layout to be rendered. Builders should refer to the documentation of the UI code being used.
**tags**<br/>array | The configuration of the tags associated with the Page Element. See PageTags for details.
**updateByName**<br/>boolean | When working with Page Element objects through the modeling API, this setting should be set to true if you do not have a unique identifier for a Page Element but wish to update any Page Element in the system that has this same name. This key is typically only used when scripting updates to Flows as part of a migration tool.

##### Page Containers

> Example pageContainers JSON:

```json
  [
    {
      "containerType": "VERTICAL_FLOW",
      "developerName": "My Vertical Container",
      "label": "",
      "pageContainers": null,
      "order": 0,
      "attributes": {
        "key1": "attribute1",
        "key2": "attribute2"
      },
      "tags": null
    }
  ]
```

A Page Container is used to determine the scaffolding of your Page. Page Containers allow Flow builders to set out the relative position of Page Components on the Page. In comparison with HTML5, a Page Container would be equivalent to a 'div' tag. As a result, Page Containers do not have any value or input, they are simply used to determine the layout or scaffolding aspects of the Page.

The type of Page Container is determined by the containerType property and developers looking to build custom Containers should use a unique containerType name to identify their Container implementation. The properties outlined below are the common attributes for typical Containers, however, if these do not suffice, developers should use the "attributes" to extend the attributes for their own specific needs. It's important to note that each of the properties below provides features and the engine does not have any understanding of one container type from another.

Key | Description
--- | -----------
**id**<br/>string | A unique identifier field assigned by the platform. This value should not be included for new Page Containers.
**containerType**<br/>string | The type of container that should be rendered. The containerType key can contain any value, however the default ManyWho UI code supports the following container types:<ul><li>**VERTICAL**: All child Page Components and Containers to this Container should be oriented vertically (e.g. in rows).</li><li>**HORIZONTAL**: All child Page Components and Containers to this Container should be oriented horizontally (e.g. in columns or shift to rows if there's not enough space).</li><li>**INLINE**: All child Page Components and Containers to this Container should be oriented inline (e.g. beside each other horizontally and "wrap" to the next line if there's not enough space).</li><li>**GROUP**: All child Page Containers to this Container should be grouped (e.g. each Container in this Container should appear as a tab).</li></ul>
**developerName**<br/>string | The name for the Page Container. This is typically a helpful name to remind builders of the purpose of the Page Container.
**label**<br/>string | The label for the Page Container. This will appear as a title heading to the running user(s).
**pageContainers**<br/>array | The array of nested Page Container objects associated with this parent Container.
**order**<br/>integer | The order in which the Page Container should be shown to running user(s) in relation to other Page Containers. The order must be greater than or equal to zero. If Page Containers have the same order, they will be rendered in random order.
**attributes**<br/>object | Key/value pairs that provide additional information for the Page Container to be rendered. Builders should refer to the documentation of the UI code being used.
**tags**<br/>array | The configuration of the tags associated with the Page Container. See PageTags for details.

##### Page Components

> Example pageComponents JSON:

```json
  [
   {
      "isEditable": true,
      "valueElementValueBindingReferenceId": {
        "id": "{id}",
        "typeElementPropertyId": "{id}",
        "command": ""
      },
      "valueElementDataBindingReferenceId": {
        "id": "{id}",
        "typeElementPropertyId": "{id}",
        "command": ""
      },
      "objectDataRequest": null,
      "fileDataRequest": null,
      "imageUri": null,
      "pageContainerDeveloperName": "R3",
      "developerName": "Assigned To",
      "componentType": "SELECT",
      "content": null,
      "label": "Assigned To",
      "columns": [
        {
          "typeElementPropertyId": "{id}",
          "isBound": false,
          "boundTypeElementPropertyId": "{id}",
          "label": "My Column",
          "isDisplayValue": true,
          "isEditable": false,
          "order": 0,
          "typeElementPropertyToDisplayId": "{id}",
          "componentType": null
        }
      ],
      "size": 0,
      "maxSize": 0,
      "height": 0,
      "width": 0,
      "isRequired": true,
      "isMultiSelect": false,
      "isSearchable": false,
      "hintValue": "Hint information",
      "helpInfo": "Help information",
      "order": 0,
      "attributes": {
        "key1": "attribute1",
        "key2": "attribute2"
      },
      "tags": null
    }
  ]
```

A Page Component is used to show or edit information on your Page. In comparison with HTML5, a Page Component would be equivalent to an 'input', 'textarea', or similar tag. As a result, Page Components typically do have a value or input, and are used to prompt the user for some form or input or to view a particular piece of information on the Page.

The type of Page Component is determined by the componentType property and developers looking to build custom Components should use a unique componentType name to identify their Component implementation. The properties outlined below are the common attributes for typical Components, however, if these do not suffice, developers should use the "attributes" to extend the attributes for their own specific needs. It's important to note that each of the properties below provides features and the engine does not have any understanding of one component type from another.

Key | Description
--- | -----------
**id**<br/>string | A unique identifier field assigned by the platform. This value should not be included for new Page Components.
**componentType**<br/>string | The type of component that should be rendered. The  componentType key can contain any value, however the default ManyWho UI code supports the following component types:<ul><li>**PRESENTATION**: Display formatted content to the running user(s) (typically HTML5).</li><li>**IMAGE**: Display a single image to the running user(s) (images can also be embedded in PRESENTATION markup).</li><li>**RICH_TEXT**: Collect formatted content from the running user(s) (typically an HTML5 editor).</li><li>**INPUT**: Collect string, date/time, numeric, password, etc data from the running user(s).</li><li>**RADIO**: Collect a single selection option from the running user(s), shown as radio buttons.</li><li>**CHECKBOX**: Collect a boolean or yes/no selection from the running user(s).</li><li>**SELECT**: Collect a single selection option from the running user(s), shown as a combobox.</li><li>**FILES**: Allow the running user(s) to upload/download and select from a list of files.</li><li>**TABLE**: Allow the running user(s) to edit, select, multi-select, search for data in a List or from a remote data source.</li></ul>
**content**<br/>string | The content that should be presented to the running user(s) as part of this Page Component. This property will be parsed if Value References are used in the content.
**isEditable**<br/>boolean | Indicates if the Page Component is editable by the running user(s).
**valueElementValueBindingReferenceId**<br/>object | The Value that should be used to store any data collected from the running user(s).
**valueElementDataBindingReferenceId**<br/>object | The Value that should be used to provide any data options that will be presented to the running user(s). For example, for a SELECT or RADIO Component, this would contain the list of options the running user(s) can select from.
**objectDataRequest**<br/>object | The ObjectDataRequest that should be used to asynchronously get the data options that will be presented to the running user(s). This is similar to the valueElementDataBindingReferenceId, however, the data is collected from the underlying Service asynchronously once the Page loads. The data collected is not stored in the Flow State.
**fileDataRequest**<br/>object | The FileDataRequest that should be used to asynchronously get the list of Files that will be presented to the running user(s). The file data is collected from the underlying Service asynchronously once the Page loads. The data collected is not stored in the Flow State.
**imageUri**<br/>string | The Uri of the image that should be presented to the running user(s) as part of this Page Component. This property will be parsed if Value References are used in the Uri.
**pageContainerId**<br/>string | The unique identifier for the Container that this Component should be placed into. This is the PageContainer.id property. This value is assigned by the platform.
**pageContainerDeveloperName**<br/>string | The unique name for the Container that this Component should be placed into. This is the PageContainer.developerName property. When creating a Page Element, you can use the developerName property of the Container to identify the placement of your Components.
**label**<br/>string | The label for the Page Component. This will appear as a title heading to the running user(s).
**columns**<br/>array | The array of columns associated with this Page Component. This property is typically used for rendering data or file tables. Each Column entry has the following keys:<br/><br/>**typeElementPropertyId** (string):<br/>The unique identifier of the Property in the Type of data being listed. This is property tells the platform which Property in the Type should be used to populate this column of data.<br/><br/>**isBound** (boolean):<br/>Indicates if this property is bound to the underlying<br/><br/>**boundTypeElementPropertyId** (string):<br/>If the valueElementValueBindingReferenceId is an Object of a different Type from the Type being listed, this property should be used. The value provided here should be the unique identifier of the Property in the Type for the valueElementValueBindingReferenceId Value. The platform will assign this column value into that Property.<br/><br/>**label** (string):<br/>The label for the column.<br/><br/>**isDisplayValue** (boolean):<br/>Indicates if this column should be displayed to the running user(s).<br/><br/>**isEditable** (boolean):<br/>Indicates if this column should be editable for running user(s).<br/><br/>**order** (integer):<br/>The order in which this column should appear in relation to other columns.<br/><br/>**typeElementPropertyToDisplayId** (string):<br/>If the Property in the Type is itself an Object, this property can be used to reference which Property in that Object Value will be displayed to the running user(s).
**size**<br/>integer | The number of characters that should be displayed for the Page Component.
**maxSize**<br/>integer | The maximum number of characters that can be entered by the running user(s) for this Page Component.
**height**<br/>integer | The number of characters high, or the number of pixels high the Page Component should be rendered.
**width**<br/>integer | The number of characters wide, or the number of pixels wide the Page Component should be rendered.
**isRequired**<br/>boolean | Indicates if the Page Component is required by the running user(s).
**isMultiSelect**<br/>boolean | Indicates if the Page Component allows multiple selection of options by the running user(s).
**isSearchable**<br/>boolean | Indicates if the Page Component is searchable by the running user(s).
**hintValue**<br/>string | The hint value for the Page Component. This will appear as a label inside of inputs to help the running user(s) as to what needs to be provided.
**helpInfo**<br/>string | The help information value for the Page Component. This will appear as help information for running user(s).
**order**<br/>integer | The order in which the Page Component should be shown to running user(s) in relation to other Page Components in the same Page Container. The order must be greater than or equal to zero. If Page Components have the same order, they will be rendered in random order.
**attributes**<br/>object | Key/value pairs that provide additional information for the Page Component to be rendered. Builders should refer to the documentation of the UI code being used.
**tags**<br/>array | The configuration of the tags associated with the Page Component. See PageTags for details.

##### Page Conditions

> Example pageConditions JSON:

```json
  [
    {
      "pageRules": [
        {
          "left": {
            "pageObjectReferenceId": "{id}",
            "typeElementPropertyId": "{id}",
            "pageObjectReferenceDeveloperName": null,
            "valueElementToReferenceId": {
              "id": "{id}",
              "typeElementPropertyId": "{id}",
              "command": null
            },
            "metadataType": "VALUE"
          },
          "criteriaType": "EQUAL",
          "right": {
            "pageObjectReferenceId": "{id}",
            "typeElementPropertyId": "{id}",
            "pageObjectReferenceDeveloperName": null,
            "valueElementToReferenceId": {
              "id": "{id}",
              "typeElementPropertyId": "{id}",
              "command": null
            },
            "metadataType": "VALUE"
          }
        }
      ],
      "comparisonType": "AND",
      "pageOperations": [
        {
          "assignment": null,
          "filter": null
        }
      ]
    }
  ]
```

Page Conditions are used to make your Pages dynamic. Based on a set of Page Rules, the Page Conditions can assign values to your Page Components but also change various properties on your Page Components and Containers such as: required, editable, visible. Page Components can also have data refreshed and objectDataRequest information dynamically assigned so you can, for example, change TABLE filters. This gives Flow builders the ability to provide single Pages that can provide the running user(s) with a very dynamic experience.

Key | Description
--- | -----------
**pageRules**<br/>array | The array of Page Rules that should be evaluated before performing any of the Page Operations. Each Page Rule represents an "if" statement (e.g. If x > y ...). If the Page Rule is true, "then" the associated Page Operations will be performed. Each Page Rule entry has the following keys:<br/><br/>**left** (object):<br/>The left Page Object Reference (see below for details) pointing to the Value Element, Page Component, or Page Container. In the expression 'x > y', this is 'x'.<br/><br/>**criteriaType** (string):<br/>The criteria under which the left and right Values should be compared. In the expression 'x > y', this is '>'. Valid values are:<ul><li>**EQUAL**: {left} is equal to {right}</li><li>**NOT_EQUAL**: {left} is not equal to {right}</li><li>**GREATER_THAN**: {left} is greater than {right}</li><li>**GREATER_THAN_OR_EQUAL**: {left} is greater than or equal to {right}</li><li>**LESS_THAN**: {left} is less than {right}</li><li>**LESS_THAN_OR_EQUAL**: {left} is less than or equal to {right}</li><li>**CONTAINS**: {left} contains the characters in {right}</li><li>**STARTS_WITH**: {left} starts with the characters in {right}</li><li>**ENDS_WITH**: {left} ends with the characters in {right}</li><li>**IS_EMPTY**: {left} is empty or null. When this criteria type is used, it must be compared with a {right} that is a ContentBoolean.</li></ul><br/>**right** (object):<br/>The right Page Object Reference (see below for details) pointing to the Value Element, Page Component, or Page Container. In the expression 'x > y', this is 'y'.
**comparisonType**<br/>string | The way in which the Rules should be compared. Valid values are:<ul><li>**AND**: Compare each Rule entry using an AND. This means that all Rules in the comparison must be true for this outcome to be selected.</li><li>**OR**: Compare each Rule entry using an OR. This means that any of the Rules in the comparison must be true for this outcome to be selected.</li></ul>
**pageOperations**<br/>array | The array of Page Operations that should be performed if the Page Rules evaluate to true. Each Page Operation entry has the following keys:<br/><br/>**assignment** (object):<br/>The configuration of the Assignment that should be performed. See Page Operation Assignment below for details.<br/><br/>**filter** (object):<br/>The configuration of the Filter that should be performed. See Page Operation Filter below for details.

##### Page Operation Assignment

> Example assignment JSON:

```json
  {
    "assignee": {
      "pageObjectReferenceId": "{id}",
      "typeElementPropertyId": "{id}",
      "pageObjectReferenceDeveloperName": "Financial Amount",
      "valueElementToReferenceId": {
        "id": "{id}",
        "typeElementPropertyId": "{id}",
        "command": null
      },
      "metadataType": "METADATA.EDITABLE"
    },
    "assignor": {
      "pageObjectReferenceId": "{id}",
      "typeElementPropertyId": "{id}",
      "pageObjectReferenceDeveloperName": null,
      "valueElementToReferenceId": {
        "id": "{id}",
        "typeElementPropertyId": "{id}",
        "command": null
      },
      "metadataType": "VALUE"
    }
  }
```

The Assignment object should be used when a value or piece of metadata for a Component or
Container needs to be changed. For example, a Page Component should be set as 'required' under a specific set of conditions. Or a Page Container should no longer be visible under another set of conditions.

Key | Description
--- | -----------
**assignee**<br/>object | The Page Object Reference (see below for details) pointing to the Value Element, Page Component, or Page Container being assigned. This is the object that will be altered as part of this assignment.
**assignor**<br/>object | The Page Object Reference (see below for details) pointing to the Value Element, Page Component, or Page Container being referenced for the assignment. This is the object that will be used to source the value that will be used as part of this assignment.

##### Page Operation Filter

> Example filter JSON:

```json
  {
    "assignee": {
      "pageObjectReferenceId": "{id}",
      "typeElementPropertyId": "{id}",
      "pageObjectReferenceDeveloperName": "Financial Amount",
      "valueElementToReferenceId": {
        "id": "{id}",
        "typeElementPropertyId": "{id}",
        "command": null
      },
      "metadataType": "METADATA.EDITABLE"
    },
    "assignor": {
      "pageObjectReferenceId": "{id}",
      "typeElementPropertyId": "{id}",
      "pageObjectReferenceDeveloperName": null,
      "valueElementToReferenceId": {
        "id": "{id}",
        "typeElementPropertyId": "{id}",
        "command": null
      },
      "metadataType": "VALUE"
    }
  }
```

The Filter object should be used when applying filters based on conditions. For example, the list of options in a combobox should be limited based on a checkbox being checked. The Filter object can be applied to Lists as well as ObjectDataRequests.

Key | Description
--- | -----------
**pageComponentId**<br/>string | The unique identifier for the Page Component to be filtered. This Page Component must be bound to a List (via the valueElementDataBindingReferenceId property) or to an ObjectDataRequest. **pageComponentDeveloperName**<br/>string | If a unique identifier has not yet been assigned to the Page Component, the developerName property can be referenced in place of the pageComponentId.
**columnTypeElementPropertyId**<br/>string | This property should only be used when filtering List bound Page Components. This property should be the unique identifier of the Property of the Type that is being filtered.
**criteriaType**<br/>string | This property should only be used when filtering List bound Page Components. Valid values are:<ul><li>**EQUAL**: {left} is equal to {right}</li><li>**NOT_EQUAL**: {left} is not equal to {right}</li><li>**GREATER_THAN**: {left} is greater than {right}</li><li>**GREATER_THAN_OR_EQUAL**: {left} is greater than or equal to {right}</li><li>**LESS_THAN**: {left} is less than {right}</li><li>**LESS_THAN_OR_EQUAL**: {left} is less than or equal to {right}</li><li>**CONTAINS**: {left} contains the characters in {right}</li><li>**STARTS_WITH**: {left} starts with the characters in {right}</li><li>**ENDS_WITH**: {left} ends with the characters in {right}</li><li>**IS_EMPTY**: {left} is empty or null. When this criteria type is used, it must be compared with a {right} that is a ContentBoolean.</li></ul><br/>
**filterValue**<br/>object | This property should only be used when filtering List bound Page Components. This property should be the unique identifier of the Property of the Type that is being filtered. The Page Object Reference (see below for details) pointing to the Value Element or Page Component containing the value to filter the List by.
**objectDataRequest**<br/>object | The configuration of the data request to be performed. See ObjectDataRequest for details.

##### Page Object Reference

> Example JSON:

```json
  {
    "pageObjectReferenceId": "{id}",
    "pageObjectReferenceDeveloperName": null,
    "typeElementPropertyId": "{id}",
    "valueElementToReferenceId": {
      "id": "{id}",
      "typeElementPropertyId": "{id}",
      "command": null
    },
    "metadataType": "VALUE"
  }
```

The Page Object Reference is a general purpose object for referencing data and metadata on the Page. It can be configured to reference data that is not formally stored into the Flow State and also Value Elements that are.

Key | Description
--- | -----------
**pageObjectReferenceId**<br/>string | The unique identifier of the Page Component or Page Container being referenced.
**pageObjectReferenceDeveloperName**<br/>string | If a unique identifier has not yet been assigned to the Page Component, the developerName property can be referenced in place of the pageObjectReferenceId.
**typeElementPropertyId**<br/>string | The unique identifier for the Property of the Type being referenced in the Page Component. This property is only needed for Page Components where the data binding (via the valueElementDataBindingReferenceId property) or ObjectDataRequest properties are being used.
**valueElementToReferenceId**<br/>object | The ValueElementId pointing to the Value Element being referenced.
**metadataType**<br/>string | The metadata of the Page Component or Page Container being referenced. Valid values are:<ul><li>**VALUE**: The value of the component or ValueElementId being referenced.</li><li>**METADATA.VISIBLE**: The visibility status of the Page Component or Container.</li><li>**METADATA.REQUIRED**: The required status of the Page Component or Container.</li><li>**METADATA.ENABLED**: The enabled status of the Page Component or Container.</li></ul><br/>


### Create/Update Page Elements

> Example 200 OK Response

```json
{
  "dateCreated": "0001-01-01T00:00:00Z",
  "dateModified": "0001-01-01T00:00:00Z",
  "whoCreated": null,
  "whoModified": null,
  "whoOwner": null,
  "label": "Incident Form",
  "pageContainers": [
    {
      "containerType": "VERTICAL_FLOW",
      "developerName": "Root",
      "label": "",
      "pageContainers": [
        {
          "containerType": "VERTICAL_FLOW",
          "developerName": "Intro",
          "label": "",
          "pageContainers": null,
          "order": 0,
          "attributes": null,
          "tags": null
        },
        {
          "containerType": "GROUP",
          "developerName": "Tabs",
          "label": "",
          "pageContainers": [
            {
              "containerType": "VERTICAL_FLOW",
              "developerName": "Actions",
              "label": "Actions",
              "pageContainers": null,
              "order": 0,
              "attributes": null,
              "tags": null
            },
            {
              "containerType": "VERTICAL_FLOW",
              "developerName": "Basic Details",
              "label": "Basic Details",
              "pageContainers": [
                {
                  "containerType": "VERTICAL_FLOW",
                  "developerName": "R1",
                  "label": "",
                  "pageContainers": null,
                  "order": 0,
                  "attributes": null,
                  "tags": null
                },
                {
                  "containerType": "INLINE_FLOW",
                  "developerName": "R2",
                  "label": "",
                  "pageContainers": null,
                  "order": 1,
                  "attributes": null,
                  "tags": null
                },
                {
                  "containerType": "INLINE_FLOW",
                  "developerName": "R3",
                  "label": "",
                  "pageContainers": null,
                  "order": 2,
                  "attributes": null,
                  "tags": null
                },
                {
                  "containerType": "VERTICAL_FLOW",
                  "developerName": "R4",
                  "label": "",
                  "pageContainers": null,
                  "order": 3,
                  "attributes": null,
                  "tags": null
                }
              ],
              "order": 1,
              "attributes": null,
              "tags": null
            }
          ],
          "order": 1,
          "attributes": null,
          "tags": null
        }
      ],
      "order": 0,
      "attributes": null,
      "tags": null
    }
  ],
  "pageComponents": [
    {
      "isEditable": false,
      "valueElementValueBindingReferenceId": null,
      "valueElementDataBindingReferenceId": null,
      "objectDataRequest": null,
      "fileDataRequest": null,
      "imageUri": null,
      "pageContainerDeveloperName": "Intro",
      "developerName": "Draft Incident",
      "componentType": "PRESENTATION",
      "content": "<h1>Incident Form</h1>\n<p>Please review the details of the submitted incident.</p>",
      "label": "",
      "columns": null,
      "size": 0,
      "maxSize": 0,
      "height": 0,
      "width": 0,
      "isRequired": false,
      "isMultiSelect": false,
      "isSearchable": false,
      "hintValue": "",
      "helpInfo": "",
      "order": 0,
      "attributes": null,
      "tags": null
    },
    {
      "isEditable": true,
      "valueElementValueBindingReferenceId": {
        "id": "4a513306-df8e-4c56-9eae-e71732df7489",
        "typeElementPropertyId": "69d0d073-1cf6-4cfe-9cdc-edaa4e68dabc",
        "command": ""
      },
      "valueElementDataBindingReferenceId": null,
      "objectDataRequest": null,
      "fileDataRequest": null,
      "imageUri": null,
      "pageContainerDeveloperName": "Actions",
      "developerName": "Details of Immediate Action",
      "componentType": "TEXTAREA",
      "content": null,
      "label": "Details of immediate action taken / needed to correct the error",
      "columns": null,
      "size": 0,
      "maxSize": 2000,
      "height": 5,
      "width": 150,
      "isRequired": true,
      "isMultiSelect": false,
      "isSearchable": false,
      "hintValue": "",
      "helpInfo": "",
      "order": 0,
      "attributes": null,
      "tags": null
    },
    {
      "isEditable": false,
      "valueElementValueBindingReferenceId": {
        "id": "4a513306-df8e-4c56-9eae-e71732df7489",
        "typeElementPropertyId": "222cb6d5-d3dd-41a4-8bc8-c970d0eb5ff9",
        "command": ""
      },
      "valueElementDataBindingReferenceId": null,
      "objectDataRequest": null,
      "fileDataRequest": null,
      "imageUri": null,
      "pageContainerDeveloperName": "Actions",
      "developerName": "Financial Amount",
      "componentType": "INPUT",
      "content": null,
      "label": "Financial Impact (GBP)",
      "columns": null,
      "size": 15,
      "maxSize": 255,
      "height": 0,
      "width": 0,
      "isRequired": false,
      "isMultiSelect": false,
      "isSearchable": false,
      "hintValue": "",
      "helpInfo": "",
      "order": 1,
      "attributes": null,
      "tags": null
    },
    {
      "isEditable": false,
      "valueElementValueBindingReferenceId": {
        "id": "4a513306-df8e-4c56-9eae-e71732df7489",
        "typeElementPropertyId": "ab82e602-bb92-4609-9f1d-35e71cde7669",
        "command": ""
      },
      "valueElementDataBindingReferenceId": null,
      "objectDataRequest": null,
      "fileDataRequest": null,
      "imageUri": null,
      "pageContainerDeveloperName": "Actions",
      "developerName": "Details of Financial Impact",
      "componentType": "TEXTAREA",
      "content": null,
      "label": "Details of financial impact",
      "columns": null,
      "size": 0,
      "maxSize": 2000,
      "height": 5,
      "width": 150,
      "isRequired": false,
      "isMultiSelect": false,
      "isSearchable": false,
      "hintValue": "Include the financial impact calculation and analysis of price impact where appropriate",
      "helpInfo": "",
      "order": 2,
      "attributes": null,
      "tags": null
    },
    {
      "isEditable": true,
      "valueElementValueBindingReferenceId": {
        "id": "e213c070-b272-4d21-afce-00cb672e5fd1",
        "typeElementPropertyId": null,
        "command": ""
      },
      "valueElementDataBindingReferenceId": null,
      "objectDataRequest": null,
      "fileDataRequest": null,
      "imageUri": null,
      "pageContainerDeveloperName": "R1",
      "developerName": "Summary of Incident",
      "componentType": "INPUT",
      "content": null,
      "label": "Summary of Incident",
      "columns": null,
      "size": 50,
      "maxSize": 255,
      "height": 0,
      "width": 0,
      "isRequired": true,
      "isMultiSelect": false,
      "isSearchable": false,
      "hintValue": "",
      "helpInfo": "",
      "order": 0,
      "attributes": null,
      "tags": null
    },
    {
      "isEditable": false,
      "valueElementValueBindingReferenceId": {
        "id": "03dc41dd-1c6b-4b33-bf61-cbd1d0778fff",
        "typeElementPropertyId": "6e1d4d49-ab0d-4475-9488-cf4a71d36beb",
        "command": ""
      },
      "valueElementDataBindingReferenceId": null,
      "objectDataRequest": null,
      "fileDataRequest": null,
      "imageUri": null,
      "pageContainerDeveloperName": "R2",
      "developerName": "Raised By",
      "componentType": "INPUT",
      "content": null,
      "label": "Raised By",
      "columns": null,
      "size": 35,
      "maxSize": 255,
      "height": 0,
      "width": 0,
      "isRequired": false,
      "isMultiSelect": false,
      "isSearchable": false,
      "hintValue": "",
      "helpInfo": "",
      "order": 0,
      "attributes": null,
      "tags": null
    },
    {
      "isEditable": false,
      "valueElementValueBindingReferenceId": {
        "id": "4a513306-df8e-4c56-9eae-e71732df7489",
        "typeElementPropertyId": "6188b05f-6154-4f35-bf8a-26dfc44ed861",
        "command": ""
      },
      "valueElementDataBindingReferenceId": null,
      "objectDataRequest": null,
      "fileDataRequest": null,
      "imageUri": null,
      "pageContainerDeveloperName": "R2",
      "developerName": "ID",
      "componentType": "INPUT",
      "content": null,
      "label": "ID",
      "columns": null,
      "size": 25,
      "maxSize": 255,
      "height": 0,
      "width": 0,
      "isRequired": false,
      "isMultiSelect": false,
      "isSearchable": false,
      "hintValue": "",
      "helpInfo": "",
      "order": 1,
      "attributes": null,
      "tags": null
    },
    {
      "isEditable": true,
      "valueElementValueBindingReferenceId": {
        "id": "a8c39a6d-a285-406a-a3f3-fe89c3c5befe",
        "typeElementPropertyId": null,
        "command": ""
      },
      "valueElementDataBindingReferenceId": {
        "id": "1d930ab0-7cf6-48dc-ab4c-3793b35c235a",
        "typeElementPropertyId": null,
        "command": ""
      },
      "objectDataRequest": null,
      "fileDataRequest": null,
      "imageUri": null,
      "pageContainerDeveloperName": "R2",
      "developerName": "Complaint",
      "componentType": "SELECT",
      "content": null,
      "label": "Complaint",
      "columns": [
        {
          "typeElementPropertyId": "9db3173a-7773-4638-88f9-1c69a448f459",
          "isBound": false,
          "boundTypeElementPropertyId": null,
          "label": "",
          "isDisplayValue": true,
          "isEditable": false,
          "order": 0,
          "typeElementPropertyToDisplayId": null,
          "componentType": null
        }
      ],
      "size": 0,
      "maxSize": 0,
      "height": 0,
      "width": 0,
      "isRequired": true,
      "isMultiSelect": false,
      "isSearchable": false,
      "hintValue": "",
      "helpInfo": "",
      "order": 2,
      "attributes": null,
      "tags": null
    },
    {
      "isEditable": true,
      "valueElementValueBindingReferenceId": {
        "id": "1b227d1b-d638-4a4d-95d6-cc2e306eed49",
        "typeElementPropertyId": null,
        "command": ""
      },
      "valueElementDataBindingReferenceId": null,
      "objectDataRequest": {
        "typeElementBindingId": "74388a56-1dc9-46c5-8763-461df61672b4",
        "typeElementId": "bf8ffc5a-73b3-4954-acf1-a9c6fcf96a11",
        "listFilter": null,
        "command": null,
        "typeElementDeveloperName": null
      },
      "fileDataRequest": null,
      "imageUri": null,
      "pageContainerDeveloperName": "R3",
      "developerName": "Assigned To",
      "componentType": "SELECT",
      "content": null,
      "label": "Assigned To",
      "columns": [
        {
          "typeElementPropertyId": "4b244d1e-716e-46d3-a10e-0db81892d4b4",
          "isBound": false,
          "boundTypeElementPropertyId": null,
          "label": "",
          "isDisplayValue": true,
          "isEditable": false,
          "order": 0,
          "typeElementPropertyToDisplayId": null,
          "componentType": null
        }
      ],
      "size": 0,
      "maxSize": 0,
      "height": 0,
      "width": 0,
      "isRequired": true,
      "isMultiSelect": false,
      "isSearchable": false,
      "hintValue": "",
      "helpInfo": "",
      "order": 0,
      "attributes": null,
      "tags": null
    },
    {
      "isEditable": true,
      "valueElementValueBindingReferenceId": {
        "id": "4a513306-df8e-4c56-9eae-e71732df7489",
        "typeElementPropertyId": "ba597d87-63bd-4afe-b9d4-c23395a34590",
        "command": ""
      },
      "valueElementDataBindingReferenceId": null,
      "objectDataRequest": null,
      "fileDataRequest": null,
      "imageUri": null,
      "pageContainerDeveloperName": "R3",
      "developerName": "Date of Event",
      "componentType": "INPUT",
      "content": null,
      "label": "Date of Event",
      "columns": null,
      "size": 35,
      "maxSize": 255,
      "height": 0,
      "width": 0,
      "isRequired": true,
      "isMultiSelect": false,
      "isSearchable": false,
      "hintValue": "",
      "helpInfo": "",
      "order": 1,
      "attributes": null,
      "tags": null
    },
    {
      "isEditable": true,
      "valueElementValueBindingReferenceId": {
        "id": "4a513306-df8e-4c56-9eae-e71732df7489",
        "typeElementPropertyId": "eca4ca88-085d-4bb6-8f73-99ab20327b35",
        "command": ""
      },
      "valueElementDataBindingReferenceId": null,
      "objectDataRequest": null,
      "fileDataRequest": null,
      "imageUri": null,
      "pageContainerDeveloperName": "R4",
      "developerName": "Is Breach",
      "componentType": "CHECKBOX",
      "content": null,
      "label": "Does this event represent a breach?",
      "columns": null,
      "size": 0,
      "maxSize": 0,
      "height": 0,
      "width": 0,
      "isRequired": false,
      "isMultiSelect": false,
      "isSearchable": false,
      "hintValue": "",
      "helpInfo": "",
      "order": 0,
      "attributes": null,
      "tags": null
    },
    {
      "isEditable": true,
      "valueElementValueBindingReferenceId": {
        "id": "9524218b-7b32-45cc-a04b-65489fbc1b69",
        "typeElementPropertyId": null,
        "command": ""
      },
      "valueElementDataBindingReferenceId": {
        "id": "ffa04819-944c-44c1-8f38-f95cec34869d",
        "typeElementPropertyId": null,
        "command": ""
      },
      "objectDataRequest": null,
      "fileDataRequest": null,
      "imageUri": null,
      "pageContainerDeveloperName": "R4",
      "developerName": "Breach Type",
      "componentType": "SELECT",
      "content": null,
      "label": "Breach Type",
      "columns": [
        {
          "typeElementPropertyId": "9db3173a-7773-4638-88f9-1c69a448f459",
          "isBound": false,
          "boundTypeElementPropertyId": null,
          "label": "",
          "isDisplayValue": true,
          "isEditable": false,
          "order": 0,
          "typeElementPropertyToDisplayId": null,
          "componentType": null
        }
      ],
      "size": 0,
      "maxSize": 0,
      "height": 0,
      "width": 0,
      "isRequired": true,
      "isMultiSelect": false,
      "isSearchable": false,
      "hintValue": "",
      "helpInfo": "",
      "order": 1,
      "attributes": null,
      "tags": null
    }
  ],
  "pageConditions": [
    {
      "pageRules": [
        {
          "left": {
            "pageObjectReferenceId": null,
            "typeElementPropertyId": null,
            "pageObjectReferenceDeveloperName": "",
            "valueElementToReferenceId": {
              "id": "db4b0557-e199-4909-b319-5db5058d7694",
              "typeElementPropertyId": null,
              "command": ""
            },
            "metadataType": "VALUE"
          },
          "criteriaType": "EQUAL",
          "right": {
            "pageObjectReferenceId": null,
            "typeElementPropertyId": null,
            "pageObjectReferenceDeveloperName": "",
            "valueElementToReferenceId": {
              "id": "be1bc78e-fd57-40ec-9a86-a815de2a9e28",
              "typeElementPropertyId": null,
              "command": ""
            },
            "metadataType": "VALUE"
          }
        }
      ],
      "comparisonType": "AND",
      "pageOperations": [
        {
          "assignment": {
            "assignee": {
              "pageObjectReferenceId": null,
              "typeElementPropertyId": null,
              "pageObjectReferenceDeveloperName": "Financial Amount",
              "valueElementToReferenceId": null,
              "metadataType": "METADATA.EDITABLE"
            },
            "assignor": {
              "pageObjectReferenceId": null,
              "typeElementPropertyId": null,
              "pageObjectReferenceDeveloperName": "",
              "valueElementToReferenceId": {
                "id": "be1bc78e-fd57-40ec-9a86-a815de2a9e28",
                "typeElementPropertyId": null,
                "command": ""
              },
              "metadataType": "VALUE"
            }
          },
          "filter": null
        },
        {
          "assignment": {
            "assignee": {
              "pageObjectReferenceId": null,
              "typeElementPropertyId": null,
              "pageObjectReferenceDeveloperName": "Details of Financial Impact",
              "valueElementToReferenceId": null,
              "metadataType": "METADATA.EDITABLE"
            },
            "assignor": {
              "pageObjectReferenceId": null,
              "typeElementPropertyId": null,
              "pageObjectReferenceDeveloperName": "",
              "valueElementToReferenceId": {
                "id": "be1bc78e-fd57-40ec-9a86-a815de2a9e28",
                "typeElementPropertyId": null,
                "command": ""
              },
              "metadataType": "VALUE"
            }
          },
          "filter": null
        }
      ]
    }
  ],
  "stopConditionsOnFirstTrue": false,
  "attributes": null,
  "tags": null,
  "updateByName": false,
  "elementType": "PAGE_LAYOUT",
  "id": "ed206576-c91c-426c-988b-76dd14752da7",
  "developerName": "Incident Form",
  "developerSummary": ""
}
```

Used to create new Page Element objects or update existing ones. The Page Element object provides the structure of your pages or screens.

#### HTTP Request

`POST /api/draw/1/element/page`

#### Body

The raw JSON for the Page Element.

<aside class="notice">
<b>Create vs Update</b><br/>
If the "id" property is included in the request, the platform will update the Element with the matching unique identifier. If the "updateByName" property is set to true, the platform will update the Element with the matching "developerName" property.
</aside>


### Import Page Element

Used to import an existing Page Element object into a Flow. The Page Element object provides the structure of your pages or screens.

#### HTTP Request

`POST /api/draw/1/element/flow/{flow_id}/page/{id}`

#### Parameters

Key | Description
--- | -----------
**flow_id**<br/>string | Unique identifier for the Flow
**id**<br/>string | The unique identifier for the Page Element


### Remove Page Element

Used to remove an existing Page Element object from a Flow. This is not the same as deleting the Page Element as it will still exist in the Tenant, but just not referenced in the Flow. The Page Element object stores data collected in the Flow State.

#### HTTP Request

`DELETE /api/draw/1/element/flow/{flow_id}/page/{id}`

#### Parameters

Key | Description
--- | -----------
**flow_id**<br/>string | Unique identifier for the Flow
**id**<br/>string | The unique identifier for the Page Element


### Query Page Elements

> Example 200 OK Response

```json
[
  {
    "dateCreated": "0001-01-01T00:00:00Z",
    "dateModified": "0001-01-01T00:00:00Z",
    "whoCreated": null,
    "whoModified": null,
    "whoOwner": null,
    "label": "Incident Form",
    "pageContainers": null,
    "pageComponents": null,
    "pageConditions": null,
    "stopConditionsOnFirstTrue": false,
    "attributes": null,
    "tags": null,
    "updateByName": false,
    "elementType": "PAGE_LAYOUT",
    "id": "ed206576-c91c-426c-988b-76dd14752da7",
    "developerName": "Incident Form",
    "developerSummary": ""
  }
]
```

Used to filter existing Page Element objects. The Page Element object provides the structure of your pages or screens.

#### HTTP Request

`GET /api/draw/1/element/page?filter={filter}`

#### Parameters

Key | Description
--- | -----------
**filter**<br/>string | The filter for querying Page Elements

<aside class="notice">
<b>Filter</b><br/>
The filter can take the following formats:
<ul><li><b>developerName eq '{developer_name}'</b>: Filter the list of Elements where the "developerName" property exactly matches the provided developer name (case insensitive)</li><li><b>substringof(developerName, '{developer_name}')</b>: Filter the list of Elements where the "developerName" property partially matches the provided developer name (case insensitive)</li></ul>
</aside>

### Get Page Element

> Example 200 OK Response

```json
{
  "dateCreated": "0001-01-01T00:00:00Z",
  "dateModified": "0001-01-01T00:00:00Z",
  "whoCreated": null,
  "whoModified": null,
  "whoOwner": null,
  "label": "Incident Form",
  "pageContainers": [ { pageContainers } ],
  "pageComponents": [ { pageComponents } ],
  "pageConditions": [ { pageConditions } ],
  "stopConditionsOnFirstTrue": false,
  "attributes": null,
  "tags": null,
  "updateByName": false,
  "elementType": "PAGE_LAYOUT",
  "id": "ed206576-c91c-426c-988b-76dd14752da7",
  "developerName": "Incident Form",
  "developerSummary": ""
}
```

Used to get an existing Page Element object. The Page Element object provides the structure of your pages or screens.

#### HTTP Request

`GET /api/draw/1/element/page/{id}`

#### Parameters

Key | Description
--- | -----------
**id**<br/>string | The unique identifier for the Page Element


### Delete Page Element

> Success 204 No Content Response

Used to delete an existing Page Element object. The Page Element object provides the structure of your pages or screens.

#### HTTP Request

`DELETE /api/draw/1/element/page/{id}`

#### Parameters

Key | Description
--- | -----------
**id**<br/>string | The unique identifier for the Page Element