# Translate API

When building Flows on the Platform, all "content" is automatically separated from "logic". This means that all Flows are automatically ready for internationalization into other languages. The result being that you can write one Flow, but adjust the content accordingly for each Content Value Culture needed.

The Translate APIs allow builders to manage content translations for all Flows and Elements.


## Content Value Cultures

> Example Request:

```json
{
    "id": "{id}",
    "developerName": "My Culture",
    "developerSummary": "Support for my Culture",
    "brand": null,
    "language": "EN",
    "country": "UK",
    "variant": null
}
```

*The Content Value Culture object represents a language or brand supported by the Tenant.*

Content Value Cultures are used to specify the language/brand options that are available for the Tenant. By default all Tenants have a Content Value Culture for USA (English). However, for multi-national/language use-cases, others can be specified: E.g. Country: JP, Language: JP, Variant: (none). This follows the ISO conventions for language. However, the platform also supports a fourth variation on the standard ISO properties; this is Brand. As a result, Content Value Culture objects can also be used to specify white-labelling or single language variations on Flow content. 

#### Content Value Culture

Key | Description
--- | -----------
**id**<br/>string | A unique identifier field assigned by the platform. This value should not be included for new Content Value Cultures.
**developerName**<br/>string | The name for the Content Value Culture. This is typically a helpful name to remind builders of the purpose of the Content Value Culture.
**developerSummary**<br/>string | The summary for the Content Value Culture. This is typically additional information that will help explain the purpose of the Content Value Culture.
**brand**<br/>string | A value representing the Brand for this Content Value Culture.
**country**<br/>string | A value representing the Country for this Content Value Culture. This typically follows the ISO Internationalization conventions.
**language**<br/>string | A value representing the Language for this Content Value Culture. This typically follows the ISO Internationalization conventions.
**variant**<br/>string | A value representing the Variant for this Content Value Culture. This typically follows the ISO Internationalization contentions.


### Create/Update Content Value Culture

> Example 200 OK Response

```json
{
    "id": "709c586f-5112-41ab-8b68-9f796df7f708",
    "developerName": "Japanese",
    "developerSummary": "Support for Japanese",
    "brand": null,
    "language": "JP",
    "country": "JP",
    "variant": null
}
```

Used to create new Map Element objects or update existing ones. The Content Value Culture object represents a language or brand supported by the Tenant.

#### HTTP Request

`POST /api/translate/1/culture`

#### Body

The raw JSON for the Content Value Culture.

<aside class="notice">
<b>Create vs Update</b><br/>
If the "id" property is included in the request, the platform will update the Content Value Culture with the matching unique identifier.
</aside>


### Get Content Value Cultures

> Example 200 OK Response

```json
[
    {
        "id": "709c586f-5112-41ab-8b68-9f796df7f708",
        "developerName": "United States of America",
        "developerSummary": "Created by system",
        "brand": null,
        "language": "EN",
        "country": "USA",
        "variant": null
    }
]
```

Used to get existing Content Value Cultures. The Content Value Culture object represents a language or brand supported by the Tenant.

#### HTTP Request

`GET /api/translate/1/culture`


### Get Content Value Culture

> Example 200 OK Response

```json
{
    "id": "709c586f-5112-41ab-8b68-9f796df7f708",
    "developerName": "Japanese",
    "developerSummary": "Support for Japanese",
    "brand": null,
    "language": "JP",
    "country": "JP",
    "variant": null
}
```

Used to get an existing Content Value Culture. The Content Value Culture object represents a language or brand supported by the Tenant.

#### HTTP Request

`GET /api/translate/1/culture/{id}`

#### Parameters

Key | Description
--- | -----------
**id**<br/>string | Unique identifier for the Content Value Culture


### Delete Content Value Culture

> Success 204 No Content Response

Used to delete an existing Content Value Culture. The Content Value Culture object represents a language or brand supported by the Tenant.

#### HTTP Request

`DELETE /api/translate/1/culture/{id}`

#### Parameters

Key | Description
--- | -----------
**id**<br/>string | Unique identifier for the Content Value Culture


## Flow Translation

> Example Response:

```json
{
    "editingToken": "{id}",
    "id": "{id}",
    "developerName": "My Flow",
    "developerSummary": "A Flow that does a bunch of things.",
    "startMapElementId": "{id}",
    "navigationElements": [
        {
            "labelContentValueId": "{idA}",
            "navigationItems": [
                {
                    "locationMapElementId": "{id}",
                    "developerName": "Home",
                    "developerSummary": "",
                    "labelContentValueId": "{idB}",
                    "navigationItems": null
                },
                {
                    "locationMapElementId": "{id}",
                    "developerName": "Accounts",
                    "developerSummary": "",
                    "labelContentValueId": "{idC}",
                    "navigationItems": null
                }
            ],
            "id": "{id}",
            "elementType": "NAVIGATION",
            "developerName": "My Flow",
            "developerSummary": "",
            "contentValueDocument": {
                "translations": {
                    "<!-- Culture: United States of America -->": {
                        "contentValues": {
                            "{idA}": "My App",
                            "{idB}": "Home",
                            "{idC}": "Accounts"
                        }
                    }
                }
            }
        }
    ],
    "mapElements": [
        {
            "userContentContentValueId": "{idA}",
            "statusMessageContentValueId": "{idB}",
            "postUpdateMessageContentValueId": "{idC}",
            "notAuthorizedMessageContentValueId": "{idD}",
            "outcomes": [
                {
                    "developerName": "New",
                    "developerSummary": null,
                    "labelContentValueId": "{idE}",
                    "nextMapElementId": "{id}"
                }
            ],
            "id": "{id}",
            "elementType": "step",
            "developerName": "Home",
            "developerSummary": "",
            "contentValueDocument": {
                "translations": {
                    "<!-- Culture: United States of America -->": {
                        "contentValues": {
                            "{idA}": "<p>Welcome to my Accounts Flow.</p>",
                            "{idB}": null,
                            "{idC}": null,
                            "{idD}": null,
                            "{idC}": "New Account"
                        }
                    }
                }
            }
        }
    ],
    "pageElements": [
        {
            "labelContentValueId": "{idA}",
            "pageContainers": [
                {
                    "containerType": "VERTICAL_FLOW",
                    "developerName": "Root",
                    "labelContentValueId": "{idB}",
                    "pageContainers": null
                }
            ],
            "pageComponents": [
                {
                    "pageContainerDeveloperName": "Root",
                    "developerName": "Account Name",
                    "componentType": "INPUT",
                    "contentContentValueId": "{idC}",
                    "labelContentValueId": "{idD}",
                    "hintValueContentValueId": "{idE}",
                    "helpInfoContentValueId": "{idF}",
                    "columns": null
                }
            ],
            "id": "{id}",
            "elementType": "PAGE_LAYOUT",
            "developerName": "Account Detail",
            "developerSummary": "",
            "contentValueDocument": {
                "translations": {
                    "<!-- Culture: United States of America -->": {
                        "contentValues": {
                            "{idA}": "Account Detail",
                            "{idB}": "Details of Account",
                            "{idC}": null,
                            "{idD}": "Account Name",
                            "{idE}": "Enter account name",
                            "{idF}": "Some helpful info"
                        }
                    }
                }
            }
        }
    ],
    "valueElements": [
        {
            "contentType": "ContentString",
            "contentFormatContentValueId": null,
            "defaultContentValueContentValueId": "{idA}",
            "id": "{id}",
            "elementType": "VARIABLE",
            "developerName": "My Default Account Name",
            "developerSummary": "",
            "contentValueDocument": {
                "translations": {
                    "<!-- Culture: United States of America -->": {
                        "contentValues": {
                            "{idA}": "Account"
                        }
                    }
                }
            }
        }
    ]
}
```

*The Flow Translation object provides all of the content Elements and properties in a Flow that can be translated.*

The Flow Translation object provides every Element in the Flow that is available for translation. It therefore provides all of the content in the Flow, regardless of whether or not the Elements are shared (such as Value and Page Elements) or specific to the Flow (such as Map or Navigation Elements). The Flow Translation object also includes additional properties to help translators identify the purpose/location of the content being translated.

#### Flow Translation

Key | Description
--- | -----------
**id**<br/>string | A unique identifier field assigned by the platform for the Flow associated with this Flow Translation.
**editingToken**<br/>string | A unique identifier needed to perform any editing operations on a Flow or its contained Map, Group, or Navigation Elements.
**developerName**<br/>string | The name for the Flow associated with this Flow Translation. This is typically a helpful name to remind builders of the purpose of the Flow.
**developerSummary**<br/>string | The summary for the Flow associated with this Flow Translation. This is typically additional information that will help explain the purpose of the Flow.
**startMapElementId**<br/>string | The Map Element that should be used to start the Flow associated with this Flow Translation.
**navigationElements**<br/>string | The array of Navigation Element Translation objects associated with all of the Navigation Elements in the Flow.
**mapElements**<br/>string | The array of Map Element Translation objects associated with all of the Map Elements in the Flow.
**pageElements**<br/>string | The array of Page Element Translation objects associated with all of the Page Elements associated with the Flow.
**typeElements**<br/>string | The array of Type Element Translation objects associated with all of the Type Elements associated with the Flow.
**valueElements**<br/>string | The array of Value Element Translation objects associated with all of the Value Elements associated with the Flow.

#### Content Value Document

The Content Value Document provides all of the content for the Element. This is the content that needs to be translated for each of the provided entries. To add new translations, you must first add a new Content Value Culture to your Tenant. Once added, you can then provided content translations for that Culture.

Key | Description
--- | -----------
**translations**<br/>object | Contains the translations for each Content Value Culture supported by the Tenant. Each key in the object relates to the Content Value Culture identifier. For each of the Content Value Culture identifier keys is then a property for contentValues. The structure of this is as follows:<br/><br/>**{id}** (string):<br/>The unique identifier within the Element to be translated. This is associated with a label or piece of content in the structure of the Element. Looking within the Translation object, this will be paired with a property in the structure of the Element.<br/><br/>**{content}** (string):<br/>The content that will be shown to the user for the property and Content Value Culture. This is the content that should be translated.

### Query Flows for Translation

> Example 200 OK Response

```json
[
  {
    "dateCreated": "0001-01-00T00:00:00Z",
    "dateModified": "0001-01-00T00:00:00Z",
    "whoCreated": null,
    "whoModified": null,
    "whoOwner": null,
    "alertEmail": null,
    "isActive": false,
    "isDefault": false,
    "comment": null,
    "editingToken": "19299bca-8a07-4b35-97f4-4cca598856d9",
    "id": {
      "id": "b7e2a056-35dd-4973-b279-c85aeafb299c",
      "versionId": "b6292dc0-ce7a-47de-bed8-7dd15e219e98"
    },
    "developerName": "Course Registration Flow",
    "developerSummary": "This is a simple course registration flow.",
    "startMapElementId": "3a0498ad-bf4f-4bba-bd4c-6975cd5e1c2a",
    "allowJumping": false,
    "stateExpirationLength": 0,
    "authorization": {
      "serviceElementId": "6388c4d1-cdae-4cc5-bb3b-a7083b71c8df",
      "globalAuthenticationType": "ALL_USERS",
      "streamBehaviourType": "USE_EXISTING",
      "groups": null,
      "users": null,
      "locations": null
    }
  }
]
```

Used to filter existing Flow objects that are available for translation. The Flow Translation object provides all of the content Elements and properties in a Flow that can be translated.

#### HTTP Request

`GET /api/translate/1/flow?filter={filter}`

<aside class="notice">
<b>Filter</b><br/>
The filter can take the following formats:
<ul><li><b>developerName eq '{developer_name}'</b>: Filter the list of Flows where the "developerName" property exactly matches the provided developer name (case insensitive)</li><li><b>substringof(developerName, '{developer_name}')</b>: Filter the list of Flows where the "developerName" property partially matches the provided developer name (case insensitive)</li></ul>
</aside>


### Get Flow Translation

```json
{
    "editingToken": "d547172e-226a-4589-8208-500531fc76ce",
    "id": "67f95ea6-c7b0-40d2-b773-2abe275e6f8e",
    "developerName": "Course Registration App",
    "developerSummary": "This is the base app for my course registrations.",
    "startMapElementId": "62550650-7e26-4256-875f-e6c5f1cc3e01",
    "navigationElements": null,
    "mapElements": [
        {
            "userContentContentValueId": "0e84b98b-c9c9-4524-8540-c2e35970728f",
            "statusMessageContentValueId": "1c4e9f0a-854b-4d17-ae2d-9ee2f10e63bf",
            "postUpdateMessageContentValueId": "02e73da3-60f5-4455-a595-358c79f8ae8a",
            "notAuthorizedMessageContentValueId": "d43ef4f6-4eaa-4482-a717-aaa17c79f416",
            "outcomes": [
                {
                    "developerName": "Go",
                    "developerSummary": null,
                    "labelContentValueId": "fc7f5f31-bbda-4aa9-9616-cc3a1da98322",
                    "nextMapElementId": "85fcd2c6-41f3-4e40-ab38-de74d4097a9e"
                }
            ],
            "id": "62550650-7e26-4256-875f-e6c5f1cc3e01",
            "elementType": "START",
            "developerName": "Start",
            "developerSummary": "",
            "contentValueDocument": {
                "translations": {
                    "3ab44596-24eb-48a4-9cf6-480c332422ec": {
                        "contentValues": {
                            "1c4e9f0a-854b-4d17-ae2d-9ee2f10e63bf": null,
                            "d43ef4f6-4eaa-4482-a717-aaa17c79f416": null,
                            "02e73da3-60f5-4455-a595-358c79f8ae8a": null,
                            "0e84b98b-c9c9-4524-8540-c2e35970728f": null,
                            "fc7f5f31-bbda-4aa9-9616-cc3a1da98322": "Go"
                        }
                    }
                }
            }
        },
        {
            "userContentContentValueId": "6f017d91-cac2-426a-8b5b-333f9165cef7",
            "statusMessageContentValueId": "4250929c-6256-45a2-b9d5-4ee882a3c940",
            "postUpdateMessageContentValueId": "6caccd8a-f3cc-4d20-8133-7fb902ecbbe2",
            "notAuthorizedMessageContentValueId": "6eeefed3-8f32-405c-9a96-42fa4c403872",
            "outcomes": [
                {
                    "developerName": "New",
                    "developerSummary": null,
                    "labelContentValueId": "bfd17555-de0b-4919-b8b1-3468f9e827ff",
                    "nextMapElementId": "00000000-0000-0000-0000-000000000000"
                },
                {
                    "developerName": "Edit",
                    "developerSummary": null,
                    "labelContentValueId": "e2439aea-33bf-4364-b5c0-b32c9e4fa82e",
                    "nextMapElementId": "00000000-0000-0000-0000-000000000000"
                }
            ],
            "id": "85fcd2c6-41f3-4e40-ab38-de74d4097a9e",
            "elementType": "input",
            "developerName": "Course Registrations",
            "developerSummary": "",
            "contentValueDocument": {
                "translations": {
                    "3ab44596-24eb-48a4-9cf6-480c332422ec": {
                        "contentValues": {
                            "4250929c-6256-45a2-b9d5-4ee882a3c940": null,
                            "6eeefed3-8f32-405c-9a96-42fa4c403872": null,
                            "6caccd8a-f3cc-4d20-8133-7fb902ecbbe2": null,
                            "6f017d91-cac2-426a-8b5b-333f9165cef7": null,
                            "bfd17555-de0b-4919-b8b1-3468f9e827ff": "New Course Registration",
                            "e2439aea-33bf-4364-b5c0-b32c9e4fa82e": "Join"
                        }
                    }
                }
            }
        }
    ],
    "pageElements": [
        {
            "labelContentValueId": "7757d90f-2b85-4c86-b1be-85a75d2fb89e",
            "pageContainers": [
                {
                    "containerType": "VERTICAL_FLOW",
                    "developerName": "Root",
                    "labelContentValueId": "7939da52-beb7-4210-8217-1971a2b63588",
                    "pageContainers": null
                }
            ],
            "pageComponents": [
                {
                    "pageContainerDeveloperName": "Root",
                    "developerName": "My States",
                    "componentType": "TABLE",
                    "contentContentValueId": "b9f2b150-faab-429f-a5ff-86e7361143e9",
                    "labelContentValueId": "f9906716-d28b-42e4-a3d1-95b610b08691",
                    "hintValueContentValueId": "861be88f-54b7-466f-8b29-5c615d2f4684",
                    "helpInfoContentValueId": "d1ebeec3-c3c2-42d7-b213-9ef6deb47913",
                    "columns": [
                        {
                            "labelContentValueId": "dc73e253-15c4-41ad-aae3-63f52898a28c"
                        },
                        {
                            "labelContentValueId": "fd31b229-1214-4092-9808-bcf0326ba7ae"
                        },
                        {
                            "labelContentValueId": "8414e42e-2581-4e2b-bbca-964b6df69824"
                        },
                        {
                            "labelContentValueId": "d8f46d74-1a82-444a-a392-fb1a68d5264a"
                        }
                    ]
                },
                {
                    "pageContainerDeveloperName": "Root",
                    "developerName": "Intro",
                    "componentType": "PRESENTATION",
                    "contentContentValueId": "41226e95-6d18-43e9-a9f3-8d988fea7201",
                    "labelContentValueId": "9a25adc4-cd46-4d31-a03c-7059d82ed301",
                    "hintValueContentValueId": "8947bdf4-2ec6-45d6-99bf-48963d47b752",
                    "helpInfoContentValueId": "3ef081b1-9b81-467f-89b8-5ada78c357a6",
                    "columns": null
                }
            ],
            "id": "f308d950-a972-4d7a-9d8b-70f5bdfc3c2e",
            "elementType": "PAGE_LAYOUT",
            "developerName": "My Course Registrations",
            "developerSummary": "",
            "contentValueDocument": {
                "translations": {
                    "3ab44596-24eb-48a4-9cf6-480c332422ec": {
                        "contentValues": {
                            "7757d90f-2b85-4c86-b1be-85a75d2fb89e": "My Course Registrations",
                            "2123e514-b48a-4aa4-8bab-bcb7c11e1dee": "",
                            "48ab7fe7-2026-4958-9555-722b780bb919": "",
                            "036e20cc-0e6c-485b-a6c3-b923a072d562": "",
                            "d1f12d77-159f-4a19-86c4-001853e264ce": "",
                            "6030a4a7-4043-45b4-b6e7-9475e3c96acb": "<h1>Course Registrations</h1>\n<p>Below is the list of course registrations in flight:</p>",
                            "4f33f124-f246-417b-bd03-a392b7208bac": null,
                            "c0c4ccf8-f0d0-4b24-94a6-744280b44073": "",
                            "0c7d75ba-27c5-4d38-93de-8eebcf137ccb": "",
                            "19e90284-1232-49ea-be89-a3f1e1e5f45a": "",
                            "c85fbb1e-067d-4cc8-be94-d6f357eb2308": "",
                            "569396da-432b-4598-adf9-b8435ef74c3d": "<h1>Course Registrations</h1>\n<p>Below is the list of course registrations in flight:</p>",
                            "293afb8c-6ee9-4340-a5bb-ecf0bd4b924a": null,
                            "77b9bb54-0533-4deb-97ab-0567f7cd334e": "",
                            "7fc9ab7d-1e7f-47ac-b143-2f0000e64306": "",
                            "b9df8be6-1854-4b6f-9f78-9a4842107ad7": "",
                            "a6467ba2-298f-4c13-8425-f6d26bbcde47": "Owner First Name",
                            "22948405-265c-474b-9398-0f80a7efd26e": "Owner Last Name",
                            "01dbc0a3-d522-4321-af8b-9ee506046d6c": "Flow",
                            "8343eab8-3c63-4e60-9e7f-72535ab6e8c5": null,
                            "bc1672a8-7059-48ec-ba5e-0f740a8752e7": null,
                            "bd793247-f318-4a58-8fa0-74639f5bf5d9": "",
                            "8026eb1c-4e6c-4327-9305-211b21b8995a": "",
                            "c53c5ac0-203a-40a8-99b9-1f390f5ecc1f": "",
                            "a8e03c35-8e21-4ffb-bbc6-65b52b491fc1": "",
                            "734f8012-3742-4196-8388-c50e6d21fd2b": "<h1>Course Registrations</h1>\n<p>Below is the list of course registrations in flight:</p>",
                            "c07373f9-af7e-4024-a2e4-74b855942ee9": null,
                            "fadf2aed-7f42-4b74-a019-34443f194939": "",
                            "7daf53db-c888-4792-bf5e-0c18170cf6d9": "",
                            "8e06c115-ab06-41b9-b0c8-4635901033eb": "",
                            "9b2a3add-eeb8-454d-99b1-383045667349": "Owner First Name",
                            "52f2376e-e177-4e0e-b2bc-1d8e0b8ba106": "Owner Last Name",
                            "8c7aed9d-a9ae-4abe-8041-80ca6002ff84": "Flow",
                            "9d8348bb-a326-46c3-ba78-0ab824986299": null,
                            "1f2b0a90-cc2a-4bb6-a49b-f8818829332f": null,
                            "5e673572-9ebd-477c-9099-441f0ec4d0e6": "",
                            "13ffac75-4258-44c3-8981-037058273251": "",
                            "26bb76df-2202-429c-a370-a062486f8c93": "",
                            "c07d0288-ed7e-48f6-a22a-05f73f4664c4": "",
                            "810568c2-63b7-412e-8ef2-b76edfbaaf37": "Owner Last Name",
                            "c226232e-c525-4874-b633-ceedc7e43c21": "Owner First Name",
                            "2c1a9c67-d9b3-4480-a2cd-75a7ef39b198": "Flow",
                            "0d80e6a1-3715-4258-878f-ba20142e497b": null,
                            "b1d0b1bb-fc0d-45f9-80ea-21379d701692": null,
                            "8cb0ebbe-c383-4685-bcbb-ddf5aec9cebf": "",
                            "83aac573-46f1-4172-b53f-4a6201c039d1": "",
                            "d3ee863f-7cce-439d-a55e-ea20cca020e5": "",
                            "a0b89080-2927-4290-baa0-2add15712247": "<h1>Course Registrations</h1>\n<p>Below is the list of course registrations in flight:</p>",
                            "0dd1e674-e9a6-4566-8730-46bc286a7b44": null,
                            "cb6c8513-13ca-48fe-a448-47314c1c3f24": "",
                            "63d91f37-970e-4793-9095-40ff0f4d1891": "",
                            "dec4a473-59a1-4610-b0ee-6dbf8ff3dcbe": "",
                            "76b601ad-715c-4782-a106-531c0dea16e1": "",
                            "1ff82d3e-7897-4db3-8674-065708179cad": "<h1>Course Registrations</h1>\n<p>Below is the list of course registrations in flight:</p>",
                            "830a2527-3a22-4ddd-95ee-a1336c0dd576": null,
                            "dfaee25a-a3b0-44f9-a60a-b8dbd351b1a2": "",
                            "23a8f222-3658-4664-84dd-41d032b7ac55": "",
                            "fb915f8f-63d5-4228-9676-f2cd49823969": "",
                            "8f6375b6-5d48-445d-b676-d5df76df0339": "Owner",
                            "c58ae236-6383-4d37-87cc-d28be8a2250f": "Step",
                            "b1a95d4a-4de8-4c19-9338-693925a927a9": "Flow",
                            "348b8efe-e11e-478c-aabe-dbaba3fe22ec": null,
                            "4f89b8e5-1748-4c12-bc65-89058c95c892": null,
                            "82eabd90-3b19-4d3e-bfec-cdd3998a3ecf": "",
                            "32ad980e-a75b-49ce-861e-580b8e0d1186": "",
                            "7ec57ac0-8f0f-427f-bd61-4e770fdcd80f": "",
                            "53521a13-2ce1-440d-ac75-8f9b4137a723": "",
                            "82ecaf0f-10d6-4fe2-a7ea-52d6defcdb9d": "<h1>Course Registrations</h1>\n<p>Below is the list of course registrations in flight:</p>",
                            "3a90b14c-3b15-4fc0-b691-aba7dec8efc0": null,
                            "ae8e91a1-e2ea-44f7-92ba-67ada4dcd603": "",
                            "9f55591c-414e-42b4-b6e4-564834848dda": "",
                            "9666af0b-4161-4b26-ba81-39f7e50de7c5": "",
                            "95e5fbb6-aaf8-4cee-8b0e-986cd658d76d": "Owner",
                            "422fa040-c8a6-4372-9bbe-98bea0a26d3b": "Step",
                            "45511b20-8494-49fb-9023-051e0d0859f1": "Flow",
                            "9e5233e8-42bc-4bc6-bdfc-a7643cd04748": "Is Done",
                            "0b26933c-a498-4381-b5eb-2feeea5bbe2e": null,
                            "eb0798b5-e72b-4105-886c-48216fc7fce2": null,
                            "7939da52-beb7-4210-8217-1971a2b63588": "",
                            "3ef081b1-9b81-467f-89b8-5ada78c357a6": "",
                            "8947bdf4-2ec6-45d6-99bf-48963d47b752": "",
                            "9a25adc4-cd46-4d31-a03c-7059d82ed301": "",
                            "41226e95-6d18-43e9-a9f3-8d988fea7201": "<h1>Course Registrations Inbox</h1>\n<p>Below is the list of course registrations in flight:</p>",
                            "170fec92-22d1-4fd9-bd1a-8dec6ebade37": null,
                            "d1ebeec3-c3c2-42d7-b213-9ef6deb47913": "",
                            "861be88f-54b7-466f-8b29-5c615d2f4684": "",
                            "f9906716-d28b-42e4-a3d1-95b610b08691": "",
                            "fd31b229-1214-4092-9808-bcf0326ba7ae": "Owner",
                            "dc73e253-15c4-41ad-aae3-63f52898a28c": "Step",
                            "8414e42e-2581-4e2b-bbca-964b6df69824": "Flow",
                            "d8f46d74-1a82-444a-a392-fb1a68d5264a": "Is Done",
                            "b9f2b150-faab-429f-a5ff-86e7361143e9": null,
                            "336de50b-1dd7-46c6-a170-263e4ded0dc9": null
                        }
                    }
                }
            }
        }
    ],
    "valueElements": [
        {
            "contentType": "ContentPassword",
            "contentFormatContentValueId": null,
            "defaultContentValueContentValueId": "9adb70d4-be43-47e5-b39a-3994b7410544",
            "id": "24a4aae1-0dbc-4088-adf7-64f6f4ff680f",
            "elementType": "VARIABLE",
            "developerName": "Database Password",
            "developerSummary": "",
            "contentValueDocument": {
                "translations": {
                    "3ab44596-24eb-48a4-9cf6-480c332422ec": {
                        "contentValues": {
                            "9adb70d4-be43-47e5-b39a-3994b7410544": null
                        }
                    }
                }
            }
        }
        {
            "contentType": "ContentString",
            "contentFormatContentValueId": null,
            "defaultContentValueContentValueId": "9dcca5a5-4b7c-4215-b776-3958dc27781e",
            "id": "45bc7a26-3fce-4fcf-b9b5-b58252528617",
            "elementType": "VARIABLE",
            "developerName": "Database Authentication Url",
            "developerSummary": "",
            "contentValueDocument": {
                "translations": {
                    "3ab44596-24eb-48a4-9cf6-480c332422ec": {
                        "contentValues": {
                            "9dcca5a5-4b7c-4215-b776-3958dc27781e": "https://login.salesforce.com"
                        }
                    }
                }
            }
        },
        {
            "contentType": "ContentString",
            "contentFormatContentValueId": null,
            "defaultContentValueContentValueId": "40bc708b-139a-44a4-bdd0-46d6f4eb76a1",
            "id": "5779601d-1dea-45fd-9091-83a6885ee26c",
            "elementType": "VARIABLE",
            "developerName": "Database Username",
            "developerSummary": "",
            "contentValueDocument": {
                "translations": {
                    "3ab44596-24eb-48a4-9cf6-480c332422ec": {
                        "contentValues": {
                            "40bc708b-139a-44a4-bdd0-46d6f4eb76a1": "user@database.demo"
                        }
                    }
                }
            }
        },
        {
            "contentType": "ContentObject",
            "contentFormatContentValueId": null,
            "defaultContentValueContentValueId": "b847a788-7764-42db-b577-2605666cd30b",
            "id": "85919867-5f4d-4644-89b4-575389576d45",
            "elementType": "VARIABLE",
            "developerName": "My State",
            "developerSummary": "",
            "contentValueDocument": {
                "translations": {
                    "3ab44596-24eb-48a4-9cf6-480c332422ec": {
                        "contentValues": {
                            "b847a788-7764-42db-b577-2605666cd30b": null
                        }
                    }
                }
            }
        }
    ]
}
```

Used to get an existing Flow Translation. The Flow Translation object provides all of the content Elements and properties in a Flow that can be translated.

#### HTTP Request

`GET /api/translate/1/flow/{id}`

Key | Description
--- | -----------
**id**<br/>string | The unique identifier for the Flow associated with this Flow Translation.


## Page Element Translation

> Example Response:

```json
{
    "labelContentValueId": "{idA}",
    "pageContainers": [
        {
            "containerType": "VERTICAL_FLOW",
            "developerName": "Root",
            "labelContentValueId": "{idB}",
            "pageContainers": null
        }
    ],
    "pageComponents": [
        {
            "pageContainerDeveloperName": "Root",
            "developerName": "Account Name",
            "componentType": "INPUT",
            "contentContentValueId": "{idC}",
            "labelContentValueId": "{idD}",
            "hintValueContentValueId": "{idE}",
            "helpInfoContentValueId": "{idF}",
            "columns": null
        }
    ],
    "id": "{id}",
    "elementType": "PAGE_LAYOUT",
    "developerName": "Account Detail",
    "developerSummary": "",
    "contentValueDocument": {
        "translations": {
            "<!-- Culture: United States of America -->": {
                "contentValues": {
                    "{idA}": "Account Detail",
                    "{idB}": "Details of Account",
                    "{idC}": null,
                    "{idD}": "Account Name",
                    "{idE}": "Enter account name",
                    "{idF}": "Some helpful info"
                }
            }
        }
    }
}
```

*The Page Element Translation object provides all of the content properties in a Page Element that can be translated.*

The Page Element Translation object also includes additional properties to help translators identify the purpose/location of the content being translated.

#### Page Element Translation

Key | Description
--- | -----------
**labelContentValueId**<br/>string | A unique identifier for the Page Element label. This identifier matches with an identifier in the translations section.
**pageContainers**<br/>array | The array of Page Containers in the page. Each Page Container entry has the following keys:<br/><br/>**containerType** (string):<br/>The type of Page Container (see Page Element in the Draw API).<br/><br/>**developerName** (string):<br/>The developer name for the Page Container (see Page Element in the Draw API).<br/><br/>**labelContentValueId** (string):<br/>A unique identifier for the Page Container label property. This identifier matches with an identifier in the translations section.<br/><br/>**pageContainers** (string):<br/>The array of child Page Containers for this Page Container.
**pageComponents**<br/>array | The array of Page Components in the page. Each Page Component entry has the following keys:<br/><br/>**pageContainerDeveloperName** (string):<br/>The developer name for the Page Container in which the Page Component is placed (see Page Element in the Draw API).<br/><br/>**developerName** (string):<br/>The developer name for the Page Component (see Page Element in the Draw API).<br/><br/>**componentType** (string):<br/>The type of Page Component (see Page Element in the Draw API).<br/><br/>**contentContentValueId** (string):<br/>A unique identifier for the Page Component content property. This identifier matches with an identifier in the translations section.<br/><br/>**labelContentValueId** (string):<br/>A unique identifier for the Page Component label property. This identifier matches with an identifier in the translations section.<br/><br/>**hintValueContentValueId** (string):<br/>A unique identifier for the Page Component hint property. This identifier matches with an identifier in the translations section.<br/><br/>**helpInfoContentValueId** (string):<br/>A unique identifier for the Page Component helpInfo property. This identifier matches with an identifier in the translations section.
**id**<br/>string | The unique identifier for the Page Element associated with this Page Element Translation.
**elementType**<br/>string | The Element type for the Page Element associated with this Page Element Translation.
**developerName**<br/>string | The name for the Page Element associated with this Page Element Translation. This is typically a helpful name to remind builders of the purpose of the Flow.
**developerSummary**<br/>string | The summary for the Page Element associated with this Page Element Translation. This is typically additional information that will help explain the purpose of the Flow.
**contentValueDocument**<br/>object | See the Flow Translation Document section for details on this object.

### Get Page Element Translation

Used to get an existing Page Element Translation. The Page Element Translation object provides all of the content properties in a Page Element that can be translated.

#### HTTP Request

`GET /api/translate/1/element/page/{id}`

Key | Description
--- | -----------
**id**<br/>string | The unique identifier for the Page Element associated with this Page Element Translation.

### Update Page Element Translation

> Example 200 OK Response

```json
{
    "labelContentValueId": "e867f7b3-d4fb-44d1-a0d5-dee6b32b2e72",
    "pageContainers": [
        {
            "containerType": "VERTICAL_FLOW",
            "developerName": "Root",
            "labelContentValueId": "629746a7-6a80-4e8b-beda-86d5efd5449c",
            "pageContainers": null
        }
    ],
    "pageComponents": [
        {
            "pageContainerDeveloperName": "Root",
            "developerName": "Intro",
            "componentType": "PRESENTATION",
            "contentContentValueId": "7ee2e85a-782d-4239-8832-73f0b3a2b097",
            "labelContentValueId": "35b20e81-aec2-4579-963c-67ed2177fa71",
            "hintValueContentValueId": "e44fbccf-7dd1-4087-937b-7b2e03fc95e4",
            "helpInfoContentValueId": "44e4f2a3-ea7c-42c6-af81-10f393ed9b08",
            "columns": null
        },
        {
            "pageContainerDeveloperName": "Root",
            "developerName": "Tasks",
            "componentType": "TABLE",
            "contentContentValueId": "00d44f1f-5554-4199-b998-e7c3eedc1d91",
            "labelContentValueId": "ae648655-41ff-4cd5-b9c3-859b852c9807",
            "hintValueContentValueId": "53dfb219-92ad-4b49-8421-10557b518295",
            "helpInfoContentValueId": "cc56a4d5-469c-4a6f-ae55-edb3ac416ab6",
            "columns": [
                {
                    "labelContentValueId": "97e4d512-301a-41d4-a42e-2885b4108e3f"
                },
                {
                    "labelContentValueId": "0c40ca0d-9312-4d86-8bab-3489e0b5bd94"
                }
            ]
        }
    ],
    "id": "84a4a6d3-89a3-4a14-931b-b448d4a3c98a",
    "elementType": "PAGE_LAYOUT",
    "developerName": "Tasks",
    "developerSummary": "",
    "contentValueDocument": {
        "translations": {
            "8c7c8402-7dd3-44ef-8199-72d57e5a395b": {
                "contentValues": {
                    "e867f7b3-d4fb-44d1-a0d5-dee6b32b2e72": "Tasks",
                    "629746a7-6a80-4e8b-beda-86d5efd5449c": "",
                    "44e4f2a3-ea7c-42c6-af81-10f393ed9b08": "",
                    "e44fbccf-7dd1-4087-937b-7b2e03fc95e4": "",
                    "35b20e81-aec2-4579-963c-67ed2177fa71": "",
                    "7ee2e85a-782d-4239-8832-73f0b3a2b097": "<h1>My Tasks</h1>",
                    "ee7c1deb-41fd-4210-8986-a34f7fbcda8b": null,
                    "cc56a4d5-469c-4a6f-ae55-edb3ac416ab6": "",
                    "53dfb219-92ad-4b49-8421-10557b518295": "",
                    "ae648655-41ff-4cd5-b9c3-859b852c9807": "",
                    "97e4d512-301a-41d4-a42e-2885b4108e3f": "Subject",
                    "0c40ca0d-9312-4d86-8bab-3489e0b5bd94": "Due Date",
                    "00d44f1f-5554-4199-b998-e7c3eedc1d91": null,
                    "1f983609-3e67-49b1-83eb-728eb90b1252": null
                }
            }
        }
    }
}
```

Used to update a Page Element Translation. The Page Element Translation object provides all of the content properties in a Page Element that can be translated.

#### HTTP Request

`POST /api/translate/1/element/page`

#### Body

The raw JSON for the Page Element Translation.

## Value Element Translation

> Example Response:

```json
{
    "contentType": "ContentString",
    "contentFormatContentValueId": "{idA}",
    "defaultContentValueContentValueId": "{idB}",
    "id": "{id}",
    "elementType": "VARIABLE",
    "developerName": "Value",
    "developerSummary": "",
    "contentValueDocument": {
        "translations": {
            "<!-- Culture: United States of America -->": {
                "contentValues": {
                    "{idA}": null,
                    "{idB}": null
                }
            }
        }
    }
}
```

*The Value Element Translation object provides all of the content properties in a Value Element that can be translated.*

The Value Element Translation object also includes additional properties to help translators identify the purpose/location of the content being translated.

Key | Description
--- | -----------
**contentType**<br/>string | The content type represented by the Tag Element. Valid values are:<ul><li>**ContentString**: A string value</li><li>**ContentNumber**: A numeric value</li><li>**ContentPassword**: A hidden value</li><li>**ContentDateTime**: A date and time value</li><li>**ContentContent**: A rich content value</li><li>**ContentObject**: An object value</li><li>**ContentList**: A list value</li></ul>
**contentFormatContentValueId**<br/>string | The unique identitifer of the Content Value Document that contains the value of the Value element's content format
**defaultContentValueContentValueId**<br/>string | The unique identitifer of the Content Value Document that contains the value of the Value element's default value
**id**<br/>string | The unique identifier for the Value Element associated with this Value Element Translation.
**elementType**<br/>string | The Element type for the Value Element associated with this Value Element Translation.
**developerName**<br/>string | The name for the Value Element associated with this Value Element Translation. This is typically a helpful name to remind builders of the purpose of the Flow.
**developerSummary**<br/>string | The summary for the Value Element associated with this Value Element Translation. This is typically additional information that will help explain the purpose of the Flow.
**contentValueDocument**<br/>object | See the Flow Translation Document section for details on this object.

### Get Value Element Translation

Used to filter existing Value objects that are available for translation. The Value Translation object provides all of the properties in a Value that can be translated.

#### HTTP Request

> Example Response:

```json
{
    "contentType": "ContentString",
    "contentFormatContentValueId": "161f5ee2-4b91-43ad-a91e-d38c823f5fbd",
    "defaultContentValueContentValueId": "56e8259a-e723-48c3-bdb5-d8c1bc4a56cd",
    "id": "884f170a-f033-4c69-9c48-9ecf663a29d9",
    "elementType": "VARIABLE",
    "developerName": "Value Name",
    "developerSummary": "",
    "contentValueDocument": {
        "translations": {
            "ef6dc583-26b0-46ea-9623-1756695503a7": {
                "contentValues": {
                    "161f5ee2-4b91-43ad-a91e-d38c823f5fbd": "Content Format",
                    "56e8259a-e723-48c3-bdb5-d8c1bc4a56cd": "Default Value"
                }
            }
        }
    }
}
```

`GET /api/translate/1/element/value/{id}`

Key | Description
--- | -----------
**id**<br/>string | The unique identifier for the Value associated with this Value Translation.

### Update Value Element Translation

#### HTTP Request

> Example 200 OK Response

```json
{
    "contentType": "ContentString",
    "contentFormatContentValueId": "161f5ee2-4b91-43ad-a91e-d38c823f5fbd",
    "defaultContentValueContentValueId": "56e8259a-e723-48c3-bdb5-d8c1bc4a56cd",
    "id": "884f170a-f033-4c69-9c48-9ecf663a29d9",
    "elementType": "VARIABLE",
    "developerName": "Value Name",
    "developerSummary": "",
    "contentValueDocument": {
        "translations": {
            "ef6dc583-26b0-46ea-9623-1756695503a7": {
                "contentValues": {
                    "161f5ee2-4b91-43ad-a91e-d38c823f5fbd": "Content Format",
                    "56e8259a-e723-48c3-bdb5-d8c1bc4a56cd": "Default Value"
                }
            }
        }
    }
}
```

Used to update an existing Value Element translation.

`POST /api/translate/1/element/value`

#### Body

The raw JSON for the Value Element translation.


## Type Element Translation

### Get Type Element Translation

#### HTTP Request

`GET /api/translate/1/element/type/{id}`


### Update Type Element Translation

#### HTTP Request

`POST /api/translate/1/element/type`


## Map Element Translation

> Example response:

```json
{
    "userContentContentValueId": "{idA}",
    "statusMessageContentValueId": "{idB}",
    "postUpdateMessageContentValueId": "{idC}",
    "notAuthorizedMessageContentValueId": "{idD}",
    "outcomes": [
        {
            "developerName": "Outcome Name",
            "developerSummary": "Outcome Summary",
            "labelContentValueId": "{idE}",
            "nextMapElementId": "Id of the next Map Element"
        }
    ],
    "id": "Id of the Map Element",
    "elementType": "Map Element Type",
    "developerName": "Map Element Name",
    "developerSummary": "Map Element Summary",
    "contentValueDocument": {
        "translations": {
            "<!-- Culture: United States of America -->": {
                "contentValues": {
                    "{idE}": "Outcome Label",
                    "{idB}": null,
                    "{idC}": null,
                    "{idD}": null,
                    "{idA}": "<p>Content</p>"
                }
            }
        }
    }
}
```

*The Map Element Translation object provides all of the content properties in a Map Element that can be translated.*

The Map Element Translation object also includes additional properties to help translators identity the purpose/location of the content being translated.

Key | Description
--- | -----------
**userContentContentValueId**<br/>string | A unique identifier for the content inside Map Elements of type **Step**. This identifier matches with an identifier in the translations section.
**statusMessageContentValueId**<br/>string | A unique identifier for the content that should be shown to the user while waiting for a system step to complete. This identifier matches with an identifier in the translations section.
**postUpdateMessageContentValueId**<br/>string | A unique identifier for the content of the message that should be posted to the collaboration stream. This identifier matches with an identifier in the translations section.
**notAuthorizedMessageContentValueId**<br/>string | A unique identifier for the content that should be shown to the user if they are not authorized to take action on this Map Element. This identifier matches with an identifier in the translations section.
**outcomes**<br/>array | The array of Outcomes coming from the Map Element. Each Outcome entry has the following keys:<br/><br/>**developerName**(string):<br/>The developer name for the outcome object(see Outcome in the Draw API).<br/></br>**developerSummary**(string):<br/>The developerSummary of the outcome object(see Outcome in the Draw API).<br/><br/>**labelContentValueId**(string):<br/>A unique identifier for the Outcome label property. This identifier matches with an identifier in the translations section.<br/><br/>**nextMapElementId**(string):<br/>A unique identifier for the target Map Element of the Outcome(see Outcome in the Draw API).
**id**<br/>string | A unique identifier for the Map Element(see Map Element in the Draw API).
**elementType**<br/>string | The type of Map Element. Valid values are:<br/><br/><ul><li>step</li><li>input</li><li>decision</li><li>operator</li><li>message</li><li>database_delete</li><li>database_load</li><li>database_save</li>
**developerName**<br/>string | The developer name of the Map Element(see Map Element in the Draw API).
**developerSummary**<br/>string | The developer summary of the Map Element(see Map Element in the Draw API).
**contentValueDocument**<br/>object | See the Flow Translation Document section for details on this object.

### Get Map Element Translation

Used to filter existing Map Element objects that are available for translation. The Map Element Translation object provides all of the properties in a Map Element that can be translated.

#### HTTP Request

```json
{
    "userContentContentValueId": "fe6fceca-6498-46a2-8cf1-91a0792a9b8c",
    "statusMessageContentValueId": "e069447f-2244-4769-b0ba-4b94b75058f2",
    "postUpdateMessageContentValueId": "1ded70cc-7e00-4de4-b778-f0752ec22862",
    "notAuthorizedMessageContentValueId": "ed714ae2-79ad-4846-9e80-f44ea980f0a7",
    "outcomes": [
        {
            "developerName": "Outcome Name",
            "developerSummary": "Outcome Summary",
            "labelContentValueId": "34d6a14d-e578-400d-958a-94b2863596fe",
            "nextMapElementId": "9c07363f-51ee-48ba-a70e-1d7cc16625db"
        }
    ],
    "id": "5067025f-8ab8-43de-8293-875faf12f4c8",
    "elementType": "step",
    "developerName": "Map Element Name",
    "developerSummary": "Map Element Summary",
    "contentValueDocument": {
        "translations": {
            "e9f71cf1-b8d4-4acd-a16c-e51a8c328b60": {
                "contentValues": {
                    "34d6a14d-e578-400d-958a-94b2863596fe": "Outcome Label",
                    "e069447f-2244-4769-b0ba-4b94b75058f2": "Status message presented while waiting",
                    "ed714ae2-79ad-4846-9e80-f44ea980f0a7": "Message presented when not authorized",
                    "1ded70cc-7e00-4de4-b778-f0752ec22862": "Content added to the collaboration stream",
                    "fe6fceca-6498-46a2-8cf1-91a0792a9b8c": "<p>Content inside the step Map Element</p>"
                }
            }
        }
    }
}
```
`GET /api/translate/1/flow/{flow_id}/{editing_token}/element/map/{id}`

Key | Description
--- | -----------
**flow_id**<br/>string | The unique identifier of the Flow where the Map Element is present.
**editing_token**<br/>string | The unique identifier of the token used to validate changes to the Flow's Map Elements.
**id**<br/>string | The unique identifier of the Map Element associated with this Map Element Translation.

### Update Map Element Translation

#### HTTP Request

```json
{
    "userContentContentValueId": "fe6fceca-6498-46a2-8cf1-91a0792a9b8c",
    "statusMessageContentValueId": "e069447f-2244-4769-b0ba-4b94b75058f2",
    "postUpdateMessageContentValueId": "1ded70cc-7e00-4de4-b778-f0752ec22862",
    "notAuthorizedMessageContentValueId": "ed714ae2-79ad-4846-9e80-f44ea980f0a7",
    "outcomes": [
        {
            "developerName": "Outcome Name",
            "developerSummary": "Outcome Summary",
            "labelContentValueId": "34d6a14d-e578-400d-958a-94b2863596fe",
            "nextMapElementId": "9c07363f-51ee-48ba-a70e-1d7cc16625db"
        }
    ],
    "id": "5067025f-8ab8-43de-8293-875faf12f4c8",
    "elementType": "step",
    "developerName": "Map Element Name",
    "developerSummary": "Map Element Summary",
    "contentValueDocument": {
        "translations": {
            "e9f71cf1-b8d4-4acd-a16c-e51a8c328b60": {
                "contentValues": {
                    "34d6a14d-e578-400d-958a-94b2863596fe": "Outcome Label",
                    "e069447f-2244-4769-b0ba-4b94b75058f2": "Status message presented while waiting",
                    "ed714ae2-79ad-4846-9e80-f44ea980f0a7": "Message presented when not authorized",
                    "1ded70cc-7e00-4de4-b778-f0752ec22862": "Content added to the collaboration stream",
                    "fe6fceca-6498-46a2-8cf1-91a0792a9b8c": "<p>Content inside the step Map Element</p>"
                }
            }
        }
    }
}
```
`POST /api/translate/1/flow/{flow_id}/{editing_token}/element/map`

Key | Description
--- | -----------
**flow_id**<br/>string | The unique identifier of the Flow where the Map Element is present.
**editing_token**<br/>string | The unique identifier of the token used to validate changes to the Flow's Map Elements.

#### Body

The raw JSON for the Map Element translation.


## Navigation Element Translation

### Get Navigation Element Translation

#### HTTP Request

`GET /api/translate/1/flow/{flow_id}/{editing_token}/element/navigation/{id}`


### Update Navigation Element Translation

#### HTTP Request

`POST /api/translate/1/flow/{flow_id}/{editing_token}/element/navigation`
