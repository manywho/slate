### Adding Custom CSS Classes to Components & Containers

Page Components & Containers rendered using the HTML5 player uses standard CSS for their styling. You can customize the look & feel of Page Components & Containers by overriding their default styling using custom styles (either inline in a custom player or in a separate stylesheet).

Occasionally it may be required to add custom classes to a Page Component or Container, for example, if you have existing styles that you want to implement. You can do this by adding the following piece of javascript to your HTML5 player:

```javascript
// Add 'my-class' to presentation components
manywho.styling.registerComponent('presentation', 'my-class');
 
// Adds 'my-class-1' & 'my-class-2' to the vertical container
manywho.styling.registerComponent('vertical_flow', ['my-class-1', 'my-class-2']);
 
// Adds 'my-class' to input components
manywho.styling.registerComponent('input', function(item, container) {
    return 'my-class';
});
```
