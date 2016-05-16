#### Rich Text / Content Component

##### Attributes

None

##### Feature: Add Image Upload Support

You can add image upload support to your Flow applications using the Rich Text editor. This is done by editing the meta-data for your component:

Open the Page Layout with your Rich Text / Content Component.
Click on Edit Page Metadata.
Copy the "id" property for the Page Layout.
Using the API tool (Admin), use the `.../page/{id}` endpoint (pasting your id into the appropriate place) to GET the full Page Element.
Copy the contents of the right pane into the left pane.
Use the `.../service?filter=` endpoint to get the list of available Service Elements.
Find the Service Element that will be used to store the uploaded file. Grab the "id" property for that Service Element.

Now that you have the necessary information for the base configuration, change the "fileDataRequest" property for your component to:

```json 
"fileDataRequest": {
    "serviceElementId": "{id of the service holding the files}",
    "resourcePath": null,
    "resourceFile": null
}
```

To provide image upload support for your running user(s), the file will be uploaded to the underlying Service. As a result, the Service must support file uploads. Use the `.../page` endpoint to POST your amended JSON back to the Draw API.

<aside class="notice">
<b>Salesforce Service</b><br/>
In case you are using the Salesforce Service to host the files, the resourcePath property must contain the following string: "ParentRecordId:{id of the record the file will be attached to}" E.g.: "ParentRecordId:{![Case].[Case Id]}"
</aside>
