#### Navigation Component

##### Attributes

None

##### Feature: Adding Additional Menus, Buttons, and Components

Additional React components can be added to the navigation bar adding the components property to the navigation setting in a custom player. This property takes an array of React components that will be rendered after any other items that are configured to be displayed in the navigation bar by your Flow.

```json
navigation: {
    isFixed: true;
    components: [
        React.DOM.li(null, React.DOM.a({ href: '#' }, 'My Custom Nav Item'))
    ]
}
```

<aside class="notice">
<b>Salesforce Service</b><br/>
The navigation bar is based on the Bootstrap 3 elements & styling. You can find more information on what elements the navigation bar supports and examples of using them here: [http://getbootstrap.com/components/#navbar](http://getbootstrap.com/components/#navbar)
</aside>

