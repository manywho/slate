## Available components

| Name | Description | Available In Page Layout Editor | Notes | Supported Attributes |
| --- | --- | --- | --- | --- |
| Content |	Richtext WYWIWYG editor | Yes | | |	 	 
| File Upload |	Allows the user to upload files | No | | <ul><li>isAutoUpload: true to upload immediately after selecting file(s)</li></ul> |
| Flip | Container that displays 2 children and animates between them |	No | Supports only 2 child items. Default width and height are 250px, you can override this by adding a custom style: .mw-flip.flip-container, .mw-flip.front, .mw-flip.back | |	 
| Group | Container that displays it's children in a set of tabs | Yes | | |	 	 
| Hidden | Does not display anything | No |	Useful for when you need a value to exist on a page for validation | |
| Horizontal | Container that displays its children horizontally | Yes | Based on a 12 column grid, children are divided equally | |	 
| IFrame |	Embedded browser window | No | Web content is loaded from the imageUri metadata property | |	 
| Image	| Displays an image | No | Image is displayed via the imageUri metadata property | |
| Inline | Container that displays its children horizontally inline | Yes |	Children are displayed side by side and will wrap | |
| Input | Accept input from a user | Yes | Supports: text, boolean, date, password, number | <ul><li>dateTimeFormat: format string for displaying datetimes</li></ul> |
| List | Bullet or numbered list | No | | <ul><li>ordered: true to display as a numbered list</li></ul> |
| Presentation | Displays richtext content | Yes | | |
| Radio | Mutually exclusive list selection | No | | <ul><li>multiselect: true to display a list of checkboxes</li></ul> |
| Select | Displays a combobox | Yes | | |
| Table | Displays a table | Yes | | <ul><li>borderless: true to remove the table-bordered style</li><li>striped: true to add the table-striped style</li><li>radio: true to display radio button selection in a prepended column</li><li>pagination: true to enable pagination on a table bound to a list</li><li>classes: string of class names that will be added to the table-container element</li><li>outcomes: icons to display outcomes as icons only</li></ul> |
| Textarea | Accept multiline text input from the user | Yes | | |	 	 
| Vertical | Container that displays its children vertically | Yes | | |
