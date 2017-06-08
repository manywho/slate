# Notifications

The notifications API allows you to view any notifications sent to your or inside your tenant.

## List tenant notifications

This endpoint will list all the notifications that have been sent from inside a tenant.

#### HTTP Request

`GET /api/notifications/1`

## List currently logged-in user's notifications

This endpoint will list all the notifications that have been sent to the user, across all tenants

#### HTTP Request

`GET /api/notifications/1/{id}`

## Get single notification

This endpoint will get a single notification

Key | Description
--- | -----------
**id**<br/>string | The ID of the notification
