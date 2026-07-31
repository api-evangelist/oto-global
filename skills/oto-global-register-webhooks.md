---
name: Register OTO webhooks for order and wallet events
description: Authenticate and register/list/update/remove OTO webhooks to receive real-time order status, new order, shipment error, and wallet transaction pushes.
api: openapi/oto-global-openapi.yml
operations: [refreshToken, webhook, getWebhook, putWebhook, deleteWebhook]
generated: '2026-07-20'
method: generated
---

# Register OTO webhooks

Base URL `https://api.tryoto.com/rest/v2`. Authenticate first.

1. **Get an access token** — `POST /refreshToken` with your `refresh_token`; send `Authorization: Bearer <access_token>`.
2. **Register an endpoint** — `POST /webhook` with your HTTPS URL and a webhook `type`. Supported types: `orderStatus`, `newOrders`, `shipmentError`, `walletTransaction`.
3. **List registrations** — `GET /webhook` (`getWebhook`).
4. **Update / remove** — `PUT /webhook` (`putWebhook`) or `DELETE /webhook` (`deleteWebhook`).

Payload notes (asyncapi/oto-global-webhooks.yml): `orderStatus` carries `orderId`, `otoId`, `status`, and a `brandedTrackingURL`; all `timestamp` values are UTC. Verify and respond 2xx quickly, then process asynchronously.
