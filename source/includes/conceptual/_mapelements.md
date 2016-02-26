## Map Elements
Map Elements are the individual steps in your Flow that perform various actions e.g. displaying a form, saving & loading data, creating an item in Salesforce, etc.

You can edit an existing Map Element in your Flow by double-clicking on it in the Flow editor. The Map Element Config panel will then slide in from the right of the screen.

You can add a new Map Element into your Flow by dragging & dropping a Map Element from the palette sidebar on the left.

### Step
![Step](images/step.jpg)

Steps should be used when you want to display rich text content including:

- Images
- Videos
- Lists
- Links
- Tables
- Formatted Text (headings, bold, italics, alignment, etc)

Outcomes will be displayed as buttons below your content.

### Page
![Page](images/page.jpg)

Pages will display the content of a previously created Page Layout.

Page Layouts allow you to define complex layouts and can contain components to accept user input.

In the Map Element Config panel you can select to use and existing Page Layout from the dropdown, **Edit** the selected Page Layout, or create a **New** Page Layout.
Clicking either the **Edit** or **New** buttons will open the Page Layout in the Page Layout editor tab.


### Operator
![Operator](images/operator.jpg)

Operators allow you to manipulate Values when your Flow is running by defining one or more operations. For example you could set a date/time Value to now, or assign an object Value's property.

You can add an operation by clicking the **New** button under the **Operations** tab. Existing operations can be edited or deleted by clicking the relevant buttons next to the relevant operation.

#### Configuring an Operation

- Select a value that you want to operate on (**Value**)
- Select what type of operation you want to perform (**Operation**)
    - Set Equal To
    - Empty: Remove any existing content or items
    - Create New
    - Update: Add an item to a List or update an existing item in the List
    - Remove: Remove an item from a List
- Select what command to use (**Command**)
    - Value Of
    - Length Of: Use the length of a List as the value
    - First Record From: Use the first item of a List as the value
    - Last Record From: Use the last item of a List as the value
- Select the Value that you want to get the value from (**Reference**)

For example:

- Value: My Value
- Operation: Set Equal To
- Command: Value Of
- Reference: My Other Value

Can be read as "My Value = My Other Value" or "Set My Value to be equal to My Other Value"

#### Ordering
Each operation can be given a specific Order value (from 0 to infinity). This number will determine the order in which the operations will be run. Operations with the same order will be execute simultaneously.

### Decision
![Decision](images/decision.jpg)

Decisions allow you to execute an outcome based of one or more conditions in your flow.


### Message
![Message](images/message.jpg)

Messages allow you to interact with systems outside of ManyWho via Services (more information on services can be found here: ). For example sending a text message using the Twilio service.

You can define one or more Actions on a single Message Element. You can add an Action by clicking the New button under the General tab. Existing Actions can be edited or deleted by clicking the relevant buttons next to the relevant operation.

#### Anatomy of a Message Action
##### Inputs
A Message Action can define zero or more inputs that may or may not be required. Each Input will have a name and a type (String, Number, etc).

For example the "Send Text Message" Action in the Twilio Service has three Inputs: To, From & Message.

#### Outputs
A Message Action can define zero or more outputs. Like Inputs each Output will have a name and a type.

For example the "Send Text Message" Action in Twilio Service has one Output: Reply

#### Configuring an Action
- Select the Service that contains the Action that you want to execute
- Select the Action that you want to execute
- Click **Save**
- Give your Action a name
- For each Input for this Action select a Value to use as the Input (for non-required Inputs this is optional)
- For each Output for this Action select a Value that will hold the value returned by the service (this is optional)
- Click **Save**

#### Ordering
Each Action can be given a specific Order value (from 0 to infinity). This number will determine the order in which the Actions will be run. Actions with the same order will be grouped together and executed simultaneously.

For example if you four Actions, two with an order of 1 and two with an order of 2, the Actions with order 1 will execute first simultaneously. After they have both completed the other two Actions with an order of 2 will then execute simultaneously

### Load
Loads allow you to fetch data from an external source via a Service into a value (either a single item or a list of items). More information on Saving, Loading & Deleting can be found here:

### Save
Saves allow you to send data back to an external source via a Service. More information on Saving, Loading & Deleting can be found here:

### Delete
Deletes allow you to delete an item or multiple items from an external source via a Service. More information on Saving, Loading & Deleting can be found here:

### Swimlane
Swimlanes allow you to partition a section of your flow to use different authentication. For example you put a section of a flow into a Swimlane that only users in the Managers group have permissions to view. Users who aren't authorized to enter the Swimlane will see a message.

### Outcomes
Outcomes are the lines that connect the map elements together in your Flow and define the execution path through your Flow.

You can create an Outcome in your Flow by dragging and dropping from the source map element to the target map element (via the orange circular handle in the center of the source map element). A single map element can have any number of Outcomes going to and from it.

<aside class="notice">
A Flow won't be valid and will fail to run until you connect the Start element to another map element in your flow
</aside>

Step & Page Layout elements will display Outcomes as buttons that users running your Flow can click to determine which Outcome will be followed.
