#### Loading Custom Components and CSS

Below are some steps outlining the process for loading custom resources (CSS and JavaScript files) into the HTML5 Player, this is useful if you have created custom components:

1. Upload your resources to a publicly available url (this url will need to support CORS).
1. Create a custom player using the Player tool in the Admin area.
1. Alter the `manywho` object by adding a "customResources" property as shown below.

```javascript
var manywho = {
    cdnUrl: 'https://assets.manywho.com',
    customResources: [
        "https://mydomain.com/js/test.js"
    ],
    initialize: function () {
        // Your usual initialize code here...
    }
}
```

Any custom resource file loaded using the customResources property will be included into the player after the manywho resources have finished loading, this is desired when adding custom components for example. If you need your resources to load first then add them as script or link tags to the player directly.

<aside class="notice">
<b>Assets</b><br/>
You can use the Assets area to upload your files. Please note that files uploaded to your Assets repository are publicly accessible.
</aside>