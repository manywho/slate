### Localization

You can change the default text used throughout the player by configuring the localization object:

```javascript
manywho.settings.initialize({
    adminTenantId: ManyWhoConstants.MANYWHO_ADMIN_TENANT_ID,
    playerUrl: [ location.protocol, '//', location.host, location.pathname ].join(''),
    joinUrl: [ location.protocol, '//', location.host, location.pathname ].join(''),
    localization: {
        initializing: 'Init'
    }
});
```

<aside class="notice">
<b>Available Options</b><br/>
The localization object currently supports the following properties: initializing, executing, loading, navigating, syncing, joining, sending, returnToParent
</aside>

