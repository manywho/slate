## Component State, Local State and Remote State
When working with custom components there are 3 types of state that you should be aware of:

### Component State
This is the regular React component state which can be accessed by this.state. Documentation about React component state can be found here: https://facebook.github.io/react/docs/getting-started.html

### Local State
This is the ManyWho flow state that currently exists in your browser session. The flow state contains a snapshot of the current state (values, selections, etc) of the flow.

```javascript
var state = manywho.state.getComponent(this.props.id, this.props.flowKey);
```

### Remote State
This is the same as the local state however it exists in the ManyWho cloud. The only important distinction is that the local state may be "out of sync" with the remote state periodically i.e. a user running a flow enters some values into some inputs on a page, these values only exist in the local state until the UI informs ManyWho to sync (usually via an outcome on the page).

### Which state should I use in my components?
Component state should be used when you need to track changes that only affect the UI and don't need to be synced to the flow e.g. dropdown toggling, switching between tabs.

Local State should be used when you do care about syncing changes back to ManyWho e.g. values entered into an input. Generally when rendering a component you will want to check if the state has a value to be displayed then fallback to the model to get a value, then in the components event handler call manywho.state.setComponent to put the updated value into the local state.

Remote state is taken care of for you, if you want your component to trigger events in the flow e.g. this combobox should sync with the remote state when the value changes as other components will update based on the selected value in the combobox, then you should call manywho.component.handleEvent in your components change handler(s).
