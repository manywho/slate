### Creating a Custom Component
A UI component consists of at least one React component and potentially some optional CSS.

```javascript
var myComponent = React.createClass({

    render: function () {

        var model = manywho.model.getContainer(this.props.id, this.props.flowKey);
        var classes = manywho.styling.getClasses(this.props.parentId, this.props.id, 'component_name', this.props.flowKey);
        var children = manywho.model.getChildren(this.props.id, this.props.flowKey);

        return React.DOM.div({ className: classes.join(' '), id: this.props.id }, [
            React.DOM.p(null, 'My Component!'),
            manywho.component.getChildComponents(children, this.props.id, this.props.flowKey)      
        ]);

    }

});

manywho.component.register('component_name', myComponent);

manywho.styling.registerContainer('component_name', function (item, container) {      
    return [];
});
```

#### Id, ParentId & FlowKey
To ensure that each component can address it's model it is important to pass **this.props.id** into **component.getChildComponents** at this point the UI framework will take care of setting **this.props.id** to the relevant id.

**this.props.flowKey** is used to identify the flow that this component belongs too, this exists to support running multiple flows on the same page simultaneously. You won't need to do administer flowKey however it is important that it is passed into the relevant functions (e.g. getContainer, getClasses, getChildren, getChildComponents, etc).

#### render (required)
- model.GetContainer: returns the model object for the container that was fetched from ManyWho
- styling.getClasses: returns classes that may have been defined by the parent container that should be applied to this container / component
- model.getChildren: returns the child model objects for this container
- component.getChildComponents: returns the React components for the various child containers / components for this container

#### manywho.component.Register (required)
Register the component with the framework, this will ensure that you're component will be rendered.

#### manywho.styling.registerContainer (optional)
Register styling information that should be applied to any child components when they are being rendered. This should return either an empty array or an array of class names.
**item** will be the model of the child being rendered and **container** will be the model of the container that contains **item**. An example of this being used can be found
here: https://github.com/manywho/ManyWho_HTML5_Players2/blob/master/runtime/js/components/horizontal.js#L54
