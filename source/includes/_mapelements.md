## Map Element

> Example Request:

```json
{
  "id": null,
  "developerName": "My Map Element",
  "developerSummary": "An example Map Element configuration",
  "x": 250,
  "y": 350,
  "groupElementId": "{id}",
  "pageElementId": "{id}",
  "dataActions": null,
  "listeners": null,
  "messageActions": null,
  "navigationOverrides": null,
  "operations": null,
  "outcomes": null,
  "viewMessageAction": null,
  "vote": null,
  "clearNavigationOverrides": false,
  "postUpdateToStream": false,
  "postUpdateWhenType": "not sure what this is",
  "postUpdateMessage": "The Flow has progressed to this step",
  "statusMessage": "The Flow is currently busy doing some work",
  "notAuthorizedMessage": "You are not authenticated for the swimlane",
  "userContent": "This is my content",
  "updateByName": false
}
```

*The Map Element object represents any node or Element in your Flow diagram.*

Map Elements are used to set out the actions and journey of your Flow. Each Map Element performs an action - which may be to present the user with information, collect information, or perform logical actions such as inserting records into a database, executing business rules, or sending messages to a 3rd party application. There's a lot of functionality packed into Map Elements, and that has been separated out in the sections below. The base properties of the Map Element are outlined here.

#### Map Element

Key | Description
--- | -----------
**id**<br/>string | A unique identifier field assigned by the platform. This value should not be included for new Map Elements.
**elementType**<br/>string | A unique element type for the Map Element. Valid values are:<ul><li>**START**: Start Element.</li><li>**STEP**: Step Element.</li><li>**INPUT**: Page Element.</li><li>**DECISION**: Decision Element.</li><li>**OPERATOR**: Operator Element.</li><li>**MESSAGE**: Message Element.</li><li>**DATABASE_SAVE**: Database Save Element.</li><li>**DATABASE_LOAD**: Database Load Element.</li><li>**DATABASE_DELETE**: Database Delete Element.</li></ul>
**developerName**<br/>string | The name for the Map Element. This is typically a helpful name to remind builders of the purpose of the Map Element.
**developerSummary**<br/>string | The summary for the Map Element. This is typically additional information that will help explain the purpose of the Map Element.
**x**<br/>integer | The X coordinate of the Map Element in the Flow diagram. If the Map Element is contained inside a Group Element, this the X coordinate in relation to the Group Element.
**y**<br/>integer | The Y coordinate of the Map Element in the Flow diagram. If the Map Element is contained inside a Group Element, this the Y coordinate in relation to the Group Element.
**groupElementId**<br/>string | The unique identifier for the Group Element that holds this Map Element. This identifier is only required for Map Elements that are in a Group Element. E.g. if a Map Element is in a Swimlane, this will be the unique identifier of the Swimlane Group Element that is in charge of restricting access to this step in the Flow.
**pageElementId**<br/>string | The unique identifier for the Page Element that is associated with this Map Element. This identifier is only required for Map Elements that will render a Page Layout. E.g. if a Map Element is a Page, this will be the unique identifier of the Page Layout that should be shown to the user at this step in the Flow.
**clearNavigationOverrides**<br/>boolean | If any Navigation Overrides have been applied to the Navigation of the running Flow, this step should clear all of the overrides.
**postUpdateToStream**<br/>boolean | If the Flow is associated with a Stream (E.g. a social feed in Chatter), this boolean indicates that the Map Element should automatically post to the stream when reached.
**postUpdateWhenType**<br/>string | If the postUpdateToStream key is set to true, this value tells the platform when to perform the actual update. Valid values are:<ul><li>**ON_LOAD**: Post the update to the stream when the Map Element loads.</li><li>**ON_EXIT**: Post the update to the stream when the Map Element is finished (i.e. by clicking on an Outcome that moves the Flow to the next step).</li></ul>
**postUpdateMessage**<br/>string | If the postUpdateToStream key is set to true, this is the content of the message that will be posted to the stream.
**statusMessage**<br/>string | If the Flow is currently in a "WAIT" state as a result of a Message Action, this is the message that will be shown to the users while waiting. The status message can be overwritten by the Service at runtime.
**notAuthorizedMessage**<br/>string | If the running user(s) of the Flow does not have access to a particular section of the Flow (E.g. due to a Swimlane), this is the message that will be shown to the users who are not authorized to view the content or take action on a Map Element step.
**userContent**<br/>string | The content that should be displayed to the running user(s) of the Flow. This key is only used for Step Map Elements and is a quick way of building out content in a Flow without needing to build a Page Layout.
**updateByName**<br/>boolean | When working with Map Element objects through the modeling API, this setting should be set to true if you do not have a unique identifier for a Map Element but wish to update any Map Element in the system that has this same name. This key is typically only used when scripting updates to Flows as part of a migration tool.
**viewMessageAction**<br/>string | (reserved for future development)

##### Data Actions

> Example dataActions JSON:

```json
  [
    {
      "developerName": "Save My Account",
      "crudOperationType": "SAVE",
      "isSmartSave": true,
      "order": 0,
      "valueElementToReferenceId": {
        "id": "{id}",
        "typeElementPropertyId": "{id}",
        "command": null
      },
      "valueElementToApplyId": {
        "id": "{id}",
        "typeElementPropertyId": "{id}",
        "command": null
      },
      "objectDataRequest": {
        "typeElementId": "{id}",
        "typeElementBindingId": "{id}",
        "listFilter": {
          "filterId": {
            "id": "{id}",
            "typeElementPropertyId": "{id}",
            "command": null
          },
          "comparisonType": "AND",
          "where": [
            {
              "columnTypeElementPropertyId": "{id}",
              "criteriaType": "EQUAL",
              "valueElementToReferenceId": {
                "id": "{id}",
                "typeElementPropertyId": "{id}",
                "command": null
              }
            }
          ],
          "orderByTypeElementPropertyId": "{id}",
          "orderByDirectionType": "DESC",
          "limit": 250,
          "filterByProvidedObjects": false
        },
        "command": {
          "commandType": null,
          "properties": {
            "key1": "value1",
            "key2": "value2"
          }
        }
      }
    }
  ]
```

A Data Action is used to perform create, read, update, or delete (CRUD) type operations on a Service. There are a number of features that make data actions particularly powerful:

1. You do not need to manage INSERT vs UPDATE operations. We automatically track the objects in your Flow and know if it is a new object to be inserted or an update to an existing object. This is done using our "SAVE" operation. We do not separate INSERT and UPDATE.
2. You can configure filters using our common metadata. This means you do not need to understand the query language of the underlying Service, you can create queries using a standard notation and we automatically translate this notation into SQL (RDBMS), SOQL (Salesforce), ZOQL (Zuora), etc.
3. The Data Action automatically knows where the data needs to go. There is no need to map fields into the database as this is already configured in the Type. In addition, a number of Services also support "smart save" which does a smart merge of data collected/changed in the Flow with data already stored in the Service.
4. If you need advanced data management capabilities such as summary roll-ups or joined tables, you can configure this using "commands" (as supported by the underlying Service implementation).

<aside class="notice">
<b>Data Actions Support</b><br/>
Map Elements that support Data Actions are:
<ul>
<li>Database Save</li>
<li>Database Load</li>
<li>Database Delete</li>
</ul>
</aside>

Key | Description
--- | -----------
**developerName**<br/>string | The name for the Data Action. This is typically a helpful name to remind builders of the purpose of the Data Action.
**crudOperationType**<br/>string | This is the type of operation being performed. Valid values are:<ul><li>**SAVE**: Save the data in the referenced Value back to the Service. This is an create or update operation in CRUD.</li><li>**LOAD**: Load data from the Service into the referenced Value. This is a read operation in CRUD.</li><li>**DELETE**: Delete the data stored in the reference Value from the Service. This data action can only be performed in the Value was first loaded from the Service.</li></ul>
**isSmartSave**<br/>boolean | Indicates if the data should saved using tracked changes in the data. Smart save must be supported in the underlying Service as the platform will only send changed data back to the Service rather than the complete Object or List.
**order**<br/>integer | The order in which the Data Action should be performed in relation to other Data Actions. The order must be greater than or equal to zero. If Data Actions have the same order, they will be performed in parallel to improve Flow performance.
**valueElementToReferenceId**<br/>object | The ValueElementId pointing to the Object or List Value that should be saved or deleted. This property is only needed for SAVE or DELETE operations or for LOAD operations where filterByProvidedObjects is true. E.g. which Object or List Value are you saving or deleting from the Service.
**valueElementToApplyId**<br/>object | The ValueElementId pointing to the Object or List Value that should be changed as a result of the Data Action. This property is only needed for SAVE or LOAD operations. E.g. which Object or List Value should be populated as a result of executing the save or load on the Service. When objects are saved, we send back the resulting data as it can often include additional information due to formula fields, triggers, etc.
**objectDataRequest**<br/>object | The configuration of the data operation being performed. See ObjectDataRequest for details.

##### Listeners

> Example listeners JSON:

```json
  [
    {
      "developerName": "My Listener",
      "serviceElementId": "{id}",
      "listenerType": null,
      "valueElementToReferenceForListeningId": {
        "id": "{id}",
        "typeElementPropertyId": "{id}",
        "command": null
      },
      "attributes": {
        "key1": "attribute1",
        "key2": "attribute2"
      }
    }
  ]
```

A Listener is used to listen to events on Objects stored or managed by a Service. When an event occurs (e.g. a record is updated) in the underlying application (e.g. Salesforce), the platform will trigger the executing Flow of the event so it can take appropriate action.

Listeners work as follows:

1. You send the Service the Objects you want to listen to (referencing the appropriate Value). In addition, you specify the type of event you're interested in (e.g. record created).
2. The Service will notify the platform when that event has happened on the associated Object(s). This will populate the referenced Value with the latest data from the Service.
3. You specify the Outcomes (with Comparisons/Rules) under which you "accept" the event and the path the Flow should follow. If those Comparisons/Rules are met, the Flow will proceed to the next MapElement in the Flow as defined by the matching Outcome. If not, the Flow will continue to wait until the appropriate event occurs.

<aside class="notice">
<b>Listeners Support</b><br/>
Map Elements that support Listeners are:
<ul>
<li>Page</li>
<li>Message</li>
<li>Database Save</li>
<li>Database Load</li>
</ul>
</aside>

Key | Description
--- | -----------
**developerName**<br/>string | The name for the Listener. This is typically a helpful name to remind builders of the purpose of the Listener.
**serviceElementId**<br/>string | The unique identifier for the Service that will be listening for events on the provided Objects.
**listenerType**<br/>string | The type of events being listened for. The value depends on the implementation of the Service. Builders should refer to the documentation of the Service being used. E.g. "UPDATE" might listen for update events on a record in Salesforce.
**valueElementToReferenceForListeningId**<br/>object | The Object or List Value that contains information about the data the Service should be listening to. E.g. This might reference a Value containing a particular "Account". The Value being referenced typically must have been loaded from/saved to the Service before it can be listened to.
**attributes**<br/>object | Key/value pairs that provide additional information for the listener to be registered. Builders should refer to the documentation of the Service being used.

##### Message Actions

> Example messageActions JSON:

```json
  [
    {
      "developerName": "Send Message",
      "serviceElementId": "{id}",
      "uriPart": null,
      "inputs": [
        {
          "developerName": "Hello",
          "contentType": "ContentString",
          "typeElementId": "{id}",
          "valueElementToReferenceId": {
            "id": "{id}",
            "typeElementPropertyId": "{id}",
            "command": null
          },
          "order": 0
        }
      ],
      "outputs": [
        {
          "developerName": "World",
          "contentType": "ContentString",
          "typeElementId": "{id}",
          "valueElementToApplyId": {
            "id": "{id}",
            "typeElementPropertyId": "{id}",
            "command": null
          },
          "order": 0
        }
      ],
      "attributes": {
        "key1": "attribute1",
        "key2": "attribute2"
      },
      "order": 0
    }
  ]
```

A Message Action is used to perform general API operations on a Service. There are a number of features that make Message Actions particularly powerful:

* **Multiple inputs/multiple outputs**: When executing a Message Action, the Service can specify multiple inputs and multiple outputs post processing. E.g. you might have a Service that moves a file from one folder to another (in Box.com). For this you'd specify the file that needs to be moved and the location you'd like to move it from and to (these would be the inputs). The outputs might be the file with revised information regarding its location and permissions.
* **They can "wait"**: When executing a Message Action, it can sometimes take some time to complete the request. Alternatively, the request may need to wait for a response. E.g. if you are sending a text message via Twilio.com and you want to have the Flow wait for the response before proceeding. Other Services may be used precisely to cause the Flow to wait, e.g. our Timer Service that allows you to stop or wait the flow for a timer interval or until a specific date. A "wait" can be created by building Comparison/Rules (e.g. the rules under which the Flow will proceed down a particular path). The Flow will only follow an Outcome until the Rules are satisfied.

It's important to note that Message Actions are described in the Service definition. The purpose of the Message Actions is to map Values in the Flow to the inputs and outputs specified by the Service.

<aside class="notice">
<b>Message Actions Support</b><br/>
Map Elements that support Message Actions are:
<ul>
<li>Page</li>
<li>Message</li>
</ul>
</aside>

Key | Description
--- | -----------
**developerName**<br/>string | The name for the Message Action. This is typically a helpful name to remind builders of the purpose of the Message Action.
**serviceElementId**<br/>string | The unique identifier for the Service that this Message Action will be executed against.
**uriPart**<br/>string | The URI part of the Message Action supported by the Service. This property identifies which action will be executed against the Service.
**inputs**<br/>array | The array of inputs associated with the action (as provided by the Service). Each Input entry maps a Value in the Flow to an input requested by the Service. Each Input entry has the following keys:<br/><br/>**developerName** (string):<br/>The name of the Input as provided by the definition of the Service.<br/><br/>**contentType** (string):<br/>The content type of the Input as provided by the Service. Valid values are:<ul><li>**ContentString**: A string value</li><li>**ContentNumber**: A numeric value</li><li>**ContentPassword**: A hidden value</li><li>**ContentDateTime**: A date and time value</li><li>**ContentContent**: A rich content value</li><li>**ContentObject**: An object value</li><li>**ContentList**: A list value</li></ul><br/>**typeElementId** (string):<br/>The Type of the Object or List value being provided.<br/><br/>**valueElementToReferenceId** (object):<br/>The ValueElementId pointing to the Value to be mapped to the Input entry.<br/><br/>**order** (integer):<br/>The order in which this Input should appear when listed in any tooling user interface.
**outputs**<br/>array | The array of outputs associated with the action (as provided by the Service). Each Output entry maps an output from the Service to a Value in the Flow. Each Output entry has the following keys:<br/><br/>**developerName** (string):<br/>The name of the Output as provided by the definition of the Service.<br/><br/>**contentType** (string):<br/>The content type of the Output as provided by the Service. Valid values are:<ul><li>**ContentString**: A string value</li><li>**ContentNumber**: A numeric value</li><li>**ContentPassword**: A hidden value</li><li>**ContentDateTime**: A date and time value</li><li>**ContentContent**: A rich content value</li><li>**ContentObject**: An object value</li><li>**ContentList**: A list value</li></ul><br/>**typeElementId** (string):<br/>The Type of the Object or List value being provided.<br/><br/>**valueElementToApplyId** (object):<br/>The ValueElementId pointing to the Value to be mapped to the Output entry.<br/><br/>**order** (integer):<br/>The order in which this Output should appear when listed in any tooling user interface.
**attributes**<br/>object | Key/value pairs that provide additional information for the Message Action to be executed. Builders should refer to the documentation of the Service being used.
**order**<br/>integer | The order in which the Message Action should be performed in relation to other Message Actions. The order must be greater than or equal to zero. If Message Actions have the same order, they will be performed in parallel to improve Flow performance.

##### Navigation Overrides

> Example navigationOverrides JSON:

```json
  [
    {
      "navigationElementId": "{id}",
      "navigationItemId": "{id}",
      "locationMapElementId": "{id}",
      "isEnabled": false,
      "isVisible": true
    }
  ]
```

A Navigation Override is used to alter the functionality of Navigation in your Flow. As running users go through a Flow, it is often useful to alter how the Navigation works. As a result, when the user gets to a particular Map Element, you can execute changes to the Navigation. These changes will persist until altered by another Map Element. This can be useful in a variety of use-cases:

* Certain parts of the Navigation should only be functional once a certain portion of the Flow has been completed. You can either disable or only make visible these parts of the Navigation when ready. For example, you might want to disable Navigation steps 3-5 until step 2 in your Flow has been completed.
* You want the Navigation to remember where the user was in a particular section of your Flow. For example, the user might be going through a sequence of diagnostic steps under a "Diagnose" Navigation Item. If the user then clicks on an "FAQ" navigation item to answer a quick question, by default when they click back on "Diagnose" it will restart the diagnostic section. If each Map Element in the "Diagnose" section overrides the navigation to point to that particular Map Element, when the user clicks on the "Diagnose" navigation item, it will take them to that particular Map Element, not back to the start.

<aside class="notice">
<b>Navigation Overrides Support</b><br/>
All Map Elements support Navigation Overrides.
</aside>

Key | Description
--- | -----------
**navigationElementId**<br/>string | The unique identifier for the Navigation Element being overridden.
**navigationItemId**<br/>string | The unique identifier for the specific Navigation Item within the Navigation Element that is being overridden.
**locationMapElementId**<br/>string | The unique identifier that the Navigation Item should now point to as part of this override. If this is null, it is assumed that the Navigation Item should continue to point to the location specified in the original Navigation Element.
**isEnabled**<br/>boolean | Indicates if the Navigation Item should be enabled. Disabling the Navigation Item prevents the running user(s) from moving to that location in the Flow via the Navigation.
**isVisible**<br/>boolean | Indicates if the Navigation Item should be visible. If this key is set to false, the running user(s) will no longer see the Navigation Item in the Navigation.

##### Operations

> Example operations JSON:

```json
  [
    {
      "valueElementToApplyId": {
        "id": "{id}",
        "typeElementPropertyId": "{id}",
        "command": null
      },
      "valueElementToReferenceId": {
        "id": "{id}",
        "typeElementPropertyId": "{id}",
        "command": null
      },
      "macroElementToExecuteId": "{id}",
      "order": 0
    }
  ]
```

An Operation is used to make a change to a Value or execute a Macro in your Flow. Each Operation can be ordered allowing builders to do Operations in a particular sequence - as individual commands performed on Values. Here are some examples of Operations:

* You want to assign the content of a Value so the user doesn't need to do it manually.
* You want to get the next Object from a List of Objects in your Flow.
* You want to execute a Macro that performs complex logic and business rules on Values in your Flow.

In mathematics, an Operation would be something like: x = 3

<aside class="notice">
<b>Operations Support</b><br/>
Map Elements that support Operations are:
<ul>
<li>Operator</li>
</ul>
</aside>

Key | Description
--- | -----------
**valueElementToApplyId**<br/>object | The ValueElementId pointing to the Value that will be changed. In mathematic expression of x = 3, this is x.
**valueElementToReferenceId**<br/>object | The ValueElementId pointing to the Value that will be referenced for the change. In mathematic expression of x = 3, this is 3.
**macroElementToExecuteId**<br/>object | The unique identifier for the Macro Element that should be executed as part of this Operation. If this key is populated, you cannot also use the Value keys above - you should do any Value changes in a separate Operation entry.
**order**<br/>integer | The order in which the Operation should be performed in relation to other Operations. The order must be greater than or equal to zero. If Operations have the same order, they will be applied in random order.

##### Outcomes

> Example outcomes JSON:

```json
  [
    {
      "id": null,
      "developerName": "Next",
      "developerSummary": null,
      "label": "Next",
      "nextMapElementId": "{id}",
      "pageActionType": "SAVE",
      "isBulkAction": false,
      "pageActionBindingType": "EDIT",
      "pageObjectBindingId": "{id}",
      "order": 0,
      "comparison": {
        "comparisonType": "AND",
        "rules": [
          {
            "leftValueElementToReferenceId": {
              "id": "{id}",
              "typeElementPropertyId": "{id}",
              "command": null
            },
            "criteriaType": "EQUAL_TO",
            "rightValueElementToReferenceId": {
              "id": "{id}",
              "typeElementPropertyId": "{id}",
              "command": null
            }
          }
        ],
        "comparisons": null,
        "order": 0
      },
      "flowOut": {
        "valueElementStateId": {
          "id": "{id}",
          "typeElementPropertyId": "{id}",
          "command": null
        },
        "valueElementFlowId": {
          "id": "{id}",
          "typeElementPropertyId": "{id}",
          "command": null
        },
        "flowId": {
          "id": "{id}",
          "versionId": "{id}"
        },
        "valueElementExternalIdentifierId": {
          "id": "{id}",
          "typeElementPropertyId": "{id}",
          "command": null
        }
      },
      "controlPoints": [
        {
          "x": 0,
          "y": 0
        }
      ]
    }
  ]
```

An Outcome is used to make move the running user(s) from one Map Element in the Flow to another or from one Map Element into another Flow. An outcome can represent a button the running user(s) can click, or it can represent a path the executing Flow should follow based on logical operations in the Flow. Outcomes can be combined with business rules (provided by Comparison/Rules) to determine the path of execution based on pre-determined logic.

<aside class="notice">
<b>Outcomes Support</b><br/>
All Map Elements support Outcomes. Map Elements that support Outcomes with Comparison/Rules are:
<ul>
<li>Page</li>
<li>Decision</li>
<li>Message</li>
</ul>
</aside>

<aside class="success">
<b>Pages, Decisions, and Messages</b><br/>
When using outcomes with Comparison/Rules, it's important to note a few things:
<ul>
<li><b>Decision</b>: The Outcomes are evaluated in real-time and an Outcome path is always selected or the Flow completes. Decisions do not have the ability to "wait", they are processed and the correct Outcome path is selected. If none of the Outcome Comparison/Rules evaluate to true, the Flow finishes.</li>
<li><b>Message</b>: The Outcomes are evaluated in real-time every time the Service responds with a status update. As a result, the Flow will continue to "wait" until one of the Outcome Comparision/Rules evaluates to true. A Flow can "wait" for as long as the State exists on the platform.</li>
<li><b>Page</b>: The Page effectively extends Message. As a result, Outcomes that have a blank "label" key can be used with Outcomes running users can click/select. For example, you may have a Page used for approving some data. The Page could also execute a Message Action with the Timer Service to "wait" 2 hours. If he Message Action returns before the running user(s) take action, the Flow will progress down the Outcome path configured to proceed when the Timer Service responds. This is useful for escalation use-cases.</li>
</ul>
</aside>

Key | Description
--- | -----------
**id**<br/>string | A unique identifier field assigned by the platform. This value should not be included for new Outcomes.
**developerName**<br/>string | The name for the Outcome. This is typically a helpful name to remind builders of the purpose of the Outcome.
**developerSummary**<br/>string | The summary for the Outcome. This is typically additional information that will help explain the purpose of the Outcome.
**label**<br/>string | The label for the Outcome. If the Outcome will appear as a button to the running user(s), a label is required.
**nextMapElementId**<br/>string | The unique identifier for the Map Element that this outcome should send the user to. If the flowOut key is used, this property is not required as the running user(s) will leave the current Flow and be sent into the Flow configured in the flowOut key.
**pageActionType**<br/>string | Determines if the data collected at this Map Element should be saved and the type of validation that should be applied when saving. Valid values are:<ul><li>**SAVE**: If the outcome is selected, save all of the data collected/changed back to the Flow State.</li><li>**NO_SAVE**: If the outcome is selected, do not save any of the data collected/changed. This is the equivalent of a "cancel".</li><li>**PARTIAL_SAVE**: If the outcome is selected, save any of the data collected/changed, but ignore any isRequired designations on fields. This allows the running user(s) to follow an outcome path without the running user(s) completing all of the required Page fields.</li></ul>
**isBulkAction**<br/>boolean | Indicates that this outcome should be treated as a "bulk" operation. This is not tied to any functionality in the platform, but rather indicates to UX developers that the outcome should not appear "inline" in tables, etc.
**pageActionBindingType**<br/>string | An arbitrary string value that indicates the type of button the Outcome represents. This indicates to UX designers how they should render the button to running users. For example, if this key is set to "DELETE", the UX designer might decide to give the Outcome button a red background and an 'x' icon.
**pageObjectBindingId**<br/>string | The unique identifier of the Page Component or Container in the Page Layout associated with this Map Element (as indicated by the pageElementId for the Map Element). If this key is provided, the Outcome will appear "with" the Page Component or Container. For example, if the Outcome is bound to a table Component, it would appear either with each record in the table (isBulkAction: false) or at the top of the table (isBulkAction: true).
**order**<br/>integer | The order in which the Outcome should be evaluated or shown to running user(s) in relation to other Outcomes. The order must be greater than or equal to zero. If Outcomes have the same order, they will be evaluated or rendered in random order. When Comparison/Rules are configured, the order is particularly important as it determines the order in which the rules are evaluated.
**comparison**<br/>object | The base Comparison object that should be used when evaluating Rules. The Comparison indicates how the array of Rules should be evaluated - e.g. this AND that, or, this OR that. All Rules within a Comparison object are evaluated according to the same comparisonType. However, Comparison objects and Rule objects can be nested to create a hierarchy of business rules. E.g. Expressions such as (x > y OR a <= b) AND c = d.<br/><br/>**comparisonType** (string):<br/>The way in which the Rules should be compared. Valid values are:<ul><li>**AND**: Compare each Rule entry using an AND. This means that all Rules in the comparison must be true for this outcome to be selected.</li><li>**OR**: Compare each Rule entry using an OR. This means that any of the Rules in the comparison must be true for this outcome to be selected.</li></ul><br/>**rules** (array):<br/>The array of Rule objects that should be evaluated for this Comparison object.<br/><br/>**leftValueElementToReferenceId** (object):<br/>The ValueElementId pointing to the Value that holds the "left" part of the rule. In the expression 'x > y', this is 'x'.<br/><br/>**criteriaType** (string):<br/>The criteria under which the left and right Values should be compared. In the expression 'x > y', this is '>'. Valid values are:<ul><li>**EQUAL**: {left} is equal to {right}</li><li>**NOT_EQUAL**: {left} is not equal to {right}</li><li>**GREATER_THAN**: {left} is greater than {right}</li><li>**GREATER_THAN_OR_EQUAL**: {left} is greater than or equal to {right}</li><li>**LESS_THAN**: {left} is less than {right}</li><li>**LESS_THAN_OR_EQUAL**: {left} is less than or equal to {right}</li><li>**CONTAINS**: {left} contains the characters in {right}</li><li>**STARTS_WITH**: {left} starts with the characters in {right}</li><li>**ENDS_WITH**: {left} ends with the characters in {right}</li><li>**IS_EMPTY**: {left} is empty or null. When this criteria type is used, it must be compared with a {right} that is a ContentBoolean.</li></ul><br/>**rightValueElementToReferenceId** (object):<br/>The ValueElementId pointing to the Value that holds the "right" part of the rule. In the expression 'x > y', this is 'y'.<br/><br/>**comparisons** (array):<br/>The array of nested Comparison objects associated with this parent Comparison.
**flowOut**<br/>object | The details of the Flow that this outcome should link to if the user clicks on the Outcome. The Flow Out configuration can only be used with Step and Page elements.<br/><br/>**valueElementStateId** (object):<br/>The ValueElementId pointing to the Value that holds the unique identifier for the State of a running Flow. If this object is configured, the other keys on this object are redundant.<br/><br/>**valueElementFlowId** (object):<br/>The ValueElementId pointing to the Value that holds the unique identifier for the Flow that should be started. The key should be used instead of the flowId key and allows dynamic assignments of a Flow.<br/><br/>**flowId** (object):<br/>The unique identifier for the Flow that should be started. This object contains an id and a versionId key for the Flow, however, only the id key is respected as versioned Flow links are not supported.<br/><br/>**valueElementExternalIdentifierId** (object):<br/>The ValueElementId pointing to the Value that should be assigned to the running Flow's external identifier. The external identifier can be used to load or filter Flow States.
**controlPoints**<br/>array | The array of control points (or "kinks") in the Outcome arrow as it appears in the Flow diagram. If there are no control points, it is assumed the arrow for the Outcome points directly from this Map Element to the next Map Element.<br/><br/>**x** (integer):<br/>The X coordinate of the control point in the Flow diagram.<br/><br/>**y** (integer):<br/>The Y coordinate of the control point in the Flow diagram.

##### Vote

> Example vote JSON:

```json
  {
    "voteType": null,
    "minimumCount": 0,
    "minimumPercent": 0,
    "attributes": {
      "key1": "attribute1",
      "key2": "attribute2"
    }
  }
```

The Vote object is used to configure voting or multi-user approval options on an Outcome. By configuring the Vote, you can determine if a set number of running users or a percentage of running users (within the authentication context of the Map Element) must click on a particular Outcome before the Flow will proceed down that path. For example, before the approval is accepted, more than two running users must click on the "Approve" outcome before the Flow will progress. A few details about this feature:

The implementation of the Vote algorithm is determined by the Service. Builders should refer to the documentation of the Service being used.
The first running user to click on an Outcome contained in a voting Map Element will force the platform to "lock" the Page from any further user inputs. Effectively the Map Element becomes read-only until the Vote is completed.

<aside class="notice">
<b>Vote Support</b><br/>
Map Elements that support Vote are:
<ul>
<li>Step</li>
<li>Page</li>
</ul>
</aside>

Key | Description
--- | -----------
**voteType**<br/>string | The type of Vote this object represents. The values for this key are arbitrary, however, if a Service supports Voting, we request that developers support two fundamental Voting approaches:<ul><li>**COUNT**: The Vote should be based on a fixed number of running users that click on the Outcome.</li><li>**PERCENT**: The Vote should be based on the percentage of running users that click on the Outcome. The percentage is calculated based on the authorization context of the Map Element at the time of execution.</li></ul>
**minimumCount**<br/>integer | A number representing the minimum number of running users that must click on any Outcome for the Flow to follow that path.
**minimumPercent**<br/>integer | A number representing the minimum percentage of running users that must click on any Outcome for the Flow to follow that path. 100% would be 100.
**attributes**<br/>object | Key/value pairs that provide additional information for the Vote to be executed. Builders should refer to the documentation of the Service being used.


### Create/Update Map Elements

> Example 200 OK Response

```json
{
  "dateCreated": "0001-01-01T00:00:00Z",
  "dateModified": "0001-01-01T00:00:00Z",
  "whoCreated": null,
  "whoModified": null,
  "whoOwner": null,
  "operations": null,
  "listeners": null,
  "viewMessageAction": null,
  "messageActions": null,
  "dataActions": null,
  "navigationOverrides": null,
  "vote": null,
  "clearNavigationOverrides": false,
  "postUpdateToStream": false,
  "userContent": null,
  "statusMessage": null,
  "postUpdateMessage": null,
  "notAuthorizedMessage": null,
  "postUpdateWhenType": "",
  "updateByName": false,
  "groupElementId": "7f31a72e-eb11-4378-b9f8-ba70d334b789",
  "x": 1190,
  "y": 150,
  "pageElementId": "ed206576-c91c-426c-988b-76dd14752da7",
  "outcomes": [
    {
      "id": "56b5872c-c1cd-45fc-9248-d1e588732b9e",
      "developerName": "Submit",
      "developerSummary": null,
      "label": "Submit",
      "nextMapElementId": "f66ae1c0-c9ae-4015-bf6d-8632afcf51ce",
      "pageActionType": "",
      "isBulkAction": false,
      "pageActionBindingType": "SAVE",
      "pageObjectBindingId": null,
      "order": 0,
      "comparison": null,
      "flowOut": null,
      "controlPoints": null,
      "nextMapElementDeveloperName": null
    }
  ],
  "id": "898fb039-d99f-4302-9e3c-f8b6f68a2fed",
  "elementType": "INPUT",
  "developerName": "Assess Incident",
  "developerSummary": ""
}
```

Used to create new Map Element objects or update existing ones. The Map Element object represents any node or Element in your Flow diagram.

#### HTTP Request

`POST /api/draw/1/{flow_id}/{editing_token}/map`

#### Parameters

Key | Description
--- | -----------
**flow_id**<br/>string | Unique identifier for the Flow containing the Map Element
**editing_token**<br/>string | The active Editing Token for the Flow being edited


#### Body

The raw JSON for the Map Element.

<aside class="notice">
<b>Create vs Update</b><br/>
If the "id" property is included in the request, the platform will update the Element with the matching unique identifier. If the "updateByName" property is set to true, the platform will update the Element with the matching "developerName" property.
</aside>


### Query Map Elements

> Example 200 OK Response

```json
[
  {
    "dateCreated": "0001-01-01T00:00:00Z",
    "dateModified": "0001-01-01T00:00:00Z",
    "whoCreated": null,
    "whoModified": null,
    "whoOwner": null,
    "operations": null,
    "listeners": null,
    "viewMessageAction": null,
    "messageActions": null,
    "dataActions": null,
    "navigationOverrides": null,
    "vote": null,
    "clearNavigationOverrides": false,
    "postUpdateToStream": false,
    "userContent": null,
    "statusMessage": null,
    "postUpdateMessage": null,
    "notAuthorizedMessage": null,
    "postUpdateWhenType": "",
    "updateByName": false,
    "groupElementId": "7f31a72e-eb11-4378-b9f8-ba70d334b789",
    "x": 1190,
    "y": 150,
    "pageElementId": "ed206576-c91c-426c-988b-76dd14752da7",
    "outcomes": [
      {
        "id": "56b5872c-c1cd-45fc-9248-d1e588732b9e",
        "developerName": "Submit",
        "developerSummary": null,
        "label": "Submit",
        "nextMapElementId": "f66ae1c0-c9ae-4015-bf6d-8632afcf51ce",
        "pageActionType": "",
        "isBulkAction": false,
        "pageActionBindingType": "SAVE",
        "pageObjectBindingId": null,
        "order": 0,
        "comparison": null,
        "flowOut": null,
        "controlPoints": null,
        "nextMapElementDeveloperName": null
      }
    ],
    "id": "898fb039-d99f-4302-9e3c-f8b6f68a2fed",
    "elementType": "INPUT",
    "developerName": "Assess Incident",
    "developerSummary": ""
  }
]
```

Used to filter existing Map Element objects. The Map Element object represents any node or Element in your Flow diagram.

#### HTTP Request

`GET /api/draw/1/{flow_id}/{editing_token}/map?filter={filter}`

#### Parameters

Key | Description
--- | -----------
**flow_id**<br/>string | Unique identifier for the Flow containing the Map Element
**editing_token**<br/>string | The active Editing Token for the Flow being edited
**filter**<br/>string | The filter for querying Map Elements


### Get Map Element

> Example 200 OK Response

```json
{
  "dateCreated": "0001-01-01T00:00:00Z",
  "dateModified": "0001-01-01T00:00:00Z",
  "whoCreated": null,
  "whoModified": null,
  "whoOwner": null,
  "operations": null,
  "listeners": null,
  "viewMessageAction": null,
  "messageActions": null,
  "dataActions": null,
  "navigationOverrides": null,
  "vote": null,
  "clearNavigationOverrides": false,
  "postUpdateToStream": false,
  "userContent": null,
  "statusMessage": null,
  "postUpdateMessage": null,
  "notAuthorizedMessage": null,
  "postUpdateWhenType": "",
  "updateByName": false,
  "groupElementId": "7f31a72e-eb11-4378-b9f8-ba70d334b789",
  "x": 1190,
  "y": 150,
  "pageElementId": "ed206576-c91c-426c-988b-76dd14752da7",
  "outcomes": [
    {
      "id": "56b5872c-c1cd-45fc-9248-d1e588732b9e",
      "developerName": "Submit",
      "developerSummary": null,
      "label": "Submit",
      "nextMapElementId": "f66ae1c0-c9ae-4015-bf6d-8632afcf51ce",
      "pageActionType": "",
      "isBulkAction": false,
      "pageActionBindingType": "SAVE",
      "pageObjectBindingId": null,
      "order": 0,
      "comparison": null,
      "flowOut": null,
      "controlPoints": null,
      "nextMapElementDeveloperName": null
    }
  ],
  "id": "898fb039-d99f-4302-9e3c-f8b6f68a2fed",
  "elementType": "INPUT",
  "developerName": "Assess Incident",
  "developerSummary": ""
}
```

Used to get an existing Map Element object. The Map Element object represents any node or Element in your Flow diagram.

#### HTTP Request

`GET /api/draw/1/{flow_id}/{editing_token}/map/{id}`

#### Parameters

Key | Description
--- | -----------
**flow_id**<br/>string | Unique identifier for the Flow containing the Map Element
**editing_token**<br/>string | The active Editing Token for the Flow being edited
**id**<br/>string | The unique identifier for the Map Element


### Delete Map Element

> Success 204 No Content Response

Used to delete an existing Map Element object. The Map Element object represents any node or Element in your Flow diagram.

#### HTTP Request

`DELETE /api/draw/1/{flow_id}/{editing_token}/map/{id}`

#### Parameters

Key | Description
--- | -----------
**flow_id**<br/>string | Unique identifier for the Flow containing the Map Element
**editing_token**<br/>string | The active Editing Token for the Flow being edited
**id**<br/>string | The unique identifier for the Map Element