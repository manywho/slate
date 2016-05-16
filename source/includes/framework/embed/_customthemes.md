### Custom Themes

The HTML5 player includes support for the various Bootswatch themes (available here: [http://bootswatch.com](http://bootswatch.com)), where the Paper theme is the default. You can change the theme at any time by running the following in the javascript console ('yeti' can be replaced with any Bootswatch theme name). Or you can add this line of JavaScript to your Player code within the initialization block.

```javascript
manywho.theming.apply('yeti');
```

#### Creating A New Theme

You can also use a custom theme that you have created instead of the included Bootswatch themes. Below are some steps outlining this process:

1. Namespace your theme's css to .mw-bs, the easiest way to do this is to wrap it in a LESS file e.g. `.mw-bs { @import (less) "mytheme.css"; }`
1. Upload your namespaced css to a publicly available url
1. Create a custom player in your tenant that is a copy of the default player
1. Add the following snippet of javascript to the top of the initialize function in your custom player (just before manywho.settings.initialize): `manywho.theming.custom('theme css url goes here');`

<aside class="notice">
<b>Bootstrap 3</b><br/>
Custom themes need to be Bootstrap 3 compatible.
</aside>
