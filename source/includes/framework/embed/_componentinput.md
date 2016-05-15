#### Input Component

##### Attributes

> Example JSON

```json
"attributes": {
  "dateTimeLocale": "en-us",
  "dateTimeFormat": "MM/DD/YYYY hh:mm:ss"
}
```

The following attributes can be added to the Input Component to further customize the user experience:

Key | Value | Description
--- | ----- | -----------
dateTimeLocale | {the local} | By default, the input field for DateTime Content Types, displayes using "en-us". Other locales are supported. For more information, please refer to the documentation here: [https://github.com/moment/moment/tree/develop/locale](https://github.com/moment/moment/tree/develop/locale)
dateTimeFormat  | {the format} | By default the date picker (only enabled with DateTime Content Types) does not display the time or allow users to specify a time, when selecting a date the time component will default to "now". More information on accepted dateTimeFormat strings can be found here: [http://momentjs.com/docs/#/displaying/format](http://momentjs.com/docs/#/displaying/format)
