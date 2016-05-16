### Embedding the HTML5 Player

The HTML5 player supports being embedded into existing pages without requiring the use of an IFrame (embedding using an IFrame is supported also). The HTML5 player's CSS is namespaced to the .mw-bs class so it will won't clash with any existing styles on your page. You can embed the player onto your page by copying and pasting the following:

```html
<div id="manywho">
    <div id="loader" style="width: 100%; height: 100%; background: black; opacity: 0.3;">
        <div style="position: absolute; width: 100%; top: 50%; left: 0; margin-top: -4em; text-align: center; color: white;">
            <p style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; font-size: 2em">Initializing</p>
        </div>
    </div>
</div>
<script src="https://assets.manywho.com/js/vendor/jquery.min.js"></script>
<script src="https://assets.manywho.com/js/vendor/bootstrap.min.js"></script>
<script src="https://assets.manywho.com/js/vendor/react.min.js"></script>
<script src="https://assets.manywho.com/js/vendor/socket.io-1.3.2.js"></script>
<script src="https://assets.manywho.com/js/vendor/chosen.jquery.min.js"></script>
<script src="https://assets.manywho.com/js/vendor/loglevel.min.js"></script>
<script src="https://assets.manywho.com/js/vendor/moment-with-locales.min.js"></script>
<script>
    var manywho = {
        cdnUrl: 'https://assets.manywho.com',
        initialize: function () {
            var queryParameters = manywho.utils.parseQueryString(window.location.search.substring(1));
            manywho.settings.initialize({
                adminTenantId: ManyWhoConstants.MANYWHO_ADMIN_TENANT_ID,
                playerUrl: [ location.protocol, '//', location.host, location.pathname ].join(''),
                joinUrl: [ location.protocol, '//', location.host, location.pathname ].join(''),
                platform: {
                    uri: 'https://flow.manywho.com'
                }
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
                }
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
<script src="https://assets.manywho.com/js/loader.min.js"></script>
```

<aside class="notice">
<b>Lock Assets</b><br/>
If you are embedding the HTML5 Player into another page (e.g. a Visualforce Page), we highly recommend that you lock your assets to a specific version.
</aside>