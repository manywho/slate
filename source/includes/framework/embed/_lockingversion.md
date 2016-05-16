### Locking the UI Assets

In some cases you may want to "freeze" the version of ManyWho CSS and JavaScript for the HTML5 player, which normally, is updated regularly for you.

<aside class="notice">
<b>To Lock Or Not To Lock</b><br/>
We recommend if you do any customization of the UI framework that you lock the assets and manage version / updates manually. This gives you the option to do additional testing based on your customizations. If you are only changing the initialization options, it can be easier to allow ManyWho to push regular updates to you.
</aside>

You can do this by creating a custom player and pasting in the following HTML:

```html
<!DOCTYPE html>
<html lang="en" xmlns="http://www.w3.org/1999/xhtml" class="manywho" style="height: 100%;">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no">
    <title>ManyWho</title>
</head>
<body style="height: 100%;">
    <div id="manywho">
        <div id="loader" style="width: 100%; height: 100%; background: black; opacity: 0.3;">
            <div style="position: absolute; width: 100%; top: 50%; left: 0; margin-top: -4em; text-align: center; color: white;">
                <p style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; font-size: 2em">Initializing</p>
            </div>
        </div>
    </div>
    <!-- Paste vendor assets here-->
    <script>
        var manywho = {
            cdnUrl: 'https://assets.manywho.com',
            initialize: function () {
                var queryParameters = manywho.utils.parseQueryString(window.location.search.substring(1));
                manywho.settings.initialize({
                    adminTenantId: ManyWhoConstants.MANYWHO_ADMIN_TENANT_ID,
                    playerUrl: [ location.protocol, '//', location.host, location.pathname ].join(''),
                    joinUrl: [ location.protocol, '//', location.host, location.pathname ].join('')
                });
                var options = {
                    authentication: {
                        sessionId: queryParameters['session-token'],
                        sessionUrl: queryParameters['session-url']
                    },
                    navigationElementId: queryParameters['navigation-element-id'],
                    mode: queryParameters['mode'],
                    reportingMode: queryParameters['reporting-mode'],
                    trackLocation: false,
                    replaceUrl: true,
                    collaboration: {
                        isEnabled: false
                    },
                    autoFocusInput: true,
                    inputs: null,
                    annotations: null,
                    collapsible: true,
                    navigation: {
                        isFixed: true
                    },
                    callbacks: []
                };
                var tenantId = queryParameters['tenant-id'];
                if (!tenantId) {
                    tenantId = window.location.pathname
                                .split('/')
                                .filter(function (path) {
                                    return path && path.length > 0;
                                })[0];
                }
                manywho.engine.initialize(
                    tenantId,
                    queryParameters['flow-id'],
                    queryParameters['flow-version-id'],
                    'main',
                    queryParameters['join'],
                    queryParameters['authorization'],
                    options,
                    queryParameters['initialization']
                );
            }
        };
    </script>
    <script src="https://flow.manywho.com/js/constants"></script>
     
    <!-- Paste versioned assets here -->
    <link rel="stylesheet" href="https://assets.manywho.com/css/themes/mw-paper.css">
    <script>
        (function (manywho, window, $) {
            function appendScript(url, onLoad) {
                var script = document.createElement("script");
                script.type = "text/javascript";
                script.onload = onLoad;
                script.src = url;
                document.head.appendChild(script);
            }
            function appendStylesheet(url, id) {
                var compiledStyles = document.createElement("link");
                compiledStyles.rel = "stylesheet";
                compiledStyles.href = url;
                compiledStyles.id = id;
                document.head.appendChild(compiledStyles);
            }
            manywho.loader = {
                initialize: function(callback, cdnUrl, customResources) {
                    var scripts = [];
                    if (customResources)
                    {
                        customResources.forEach(function(url) {
                            if (url.match('\.css$')) {
                                appendStylesheet(url);
                            }
                            else if (url.match('\.js$')) {
                                scripts.push(url);
                            }
                        });
                    }
                    var loadedScriptCount = 0;
                    if (scripts.length > 0) {
                        scripts.forEach(function(url, index, scripts) {
             
                            appendScript(url, function() {
             
                                loadedScriptCount++;
                               if (loadedScriptCount == scripts.length) {
             
                                    callback();
             
                                }
             
                            });
             
                        });
                     
                    }
                    else {
                         
                        callback();
                         
                    }
                }
            }
            manywho.loader.initialize(manywho.initialize, manywho.cdnUrl, manywho.customResources);
        }(manywho, window, jQuery));
    </script>
</body>
</html>
```

In addition to the above HTML, you need to do the following:

- Replace <!-- Paste vendor assets here --> with the script tags from Vendor Assets.
- Replace <!-- Paste versioned assets here--> with the script & link tags from Versioned Assets.

The assets references can be found here: [UI - Change Log](https://developers.manywho.com/display/MA/UI+-+Change+Log)