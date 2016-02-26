### Creating Your First Flow
This tutorial will guide you through the process of creating a Flow on ManyWho. More specific details on what a Flow is can be found (here)[#flows],
for the purposes of this tutorial all you need to know is that a Flow is a series of steps that you have defined that users can execute through.

<aside class="notice">
This tutorial assumes that you have already registered with ManyWho and that you have logged in to the Draw tool: https://flow.manywho.com/draw
</aside>

#### Create a New flow
1. You can create a new Flow by selecting the **Flows** menu item then click the **New** button.
2. Decide how you will want users running your Flow to authenticate with the Flow. For example you may want to restrict access to your Flow to only users in a specific Salesforce group.
For now select **ManyWho Identity** and click **Next**
3. By default new Flows will be publically accessible and won't display a social feed (this can be changed at any time). Click **Save & Open** to open the Flow to edit.

#### Adding a Map Element to your Flow

IMAGE here

A Flow must contain 1 or more Map Elements that will define what the Flow will do. We are going to add a Step to the Flow that will display some text. You can add a Step by dragging & dropping the Step element from the toolbox bar onto the canvas.

After you drop the Step element onto the canvas the element configuration panel will slide in from the right of the Flow graph.

Give your Step a name and some content that you want it to display then hit the **Save** button.

#### Connecting the Start Element
For a Flow to be valid the Start Map Element must be connected to one Map Element via an (Outcome)[#outcome].

You can create an Outcome between Start and the new Step by dragging from the orange drag handle in the center of the Start element and dropping onto the Step. This will display the Outcome configuration panel, give your Outcome a name and label and hit the **Save** button.

#### Running the Flow
Now that you have created a Flow you can run it by clicking on the **Run** button in the toolbox bar, this will display the Run dialog, in here click the **Run** button and your Flow will open in a new tab.
