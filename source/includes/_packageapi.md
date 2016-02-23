# Package API


## Export Latest Version

#### HTTP Request

`GET /api/package/1/flow/{id}?nullPasswords={nullPasswords}`


## Export Specific Version

#### HTTP Request

`GET /api/package/1/flow/{id}/{version_id}?nullPasswords={nullPasswords}`


## Import

#### HTTP Request

`POST /api/package/1/flow/{id}/{version_id}?isActive={isActive}&isDefault={isDefault}&uriMapping[n][from]={from}&uriMapping[n][to]={to}`
