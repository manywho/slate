## Debugging the HTML5 Player Locally

When creating custom components you may need to debug the existing HTML5 player code in its un-compiled format:

```javascript
manywho.settings.initialize({
    adminTenantId: 'da497693-4d02-45db-bc08-8ea16d2ccbdf',
    playerUrl: [ location.protocol, '//', location.host, location.pathname ].join(''),
    joinUrl: [location.protocol, '//', location.host, location.pathname].join(''),
    platform: {
        uri: 'https://flow.manywho.com'
    }
});
```

1. Clone the HTML5 PLayers2 repo: https://github.com/manywho/ManyWho_HTML5_Players2
2. open `runtime\default.html` and edit `manywho.settings.initialize`
3. Open a the command line, cd into the repro directory and run gulp refresh
4. You can debug a production flow by adding the tenant-id, flow-id & flow-version-id query parameters in the browser (join query parameter is also supported) e.g. `http://localhost:3000?tenant-id=mytenantid&flow-id=myflowid&flow-version-id=myflowversionid`
