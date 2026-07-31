---
name: Create and manage a return with OTO
description: Authenticate, create a return shipment, generate a customer return link, notify the customer, and check return status.
api: openapi/oto-global-openapi.yml
operations: [refreshToken, createReturnShipment, getReturnLink, triggerReturnSms, getReturnDetails]
generated: '2026-07-20'
method: generated
---

# Create and manage a return with OTO

Base URL `https://api.tryoto.com/rest/v2`. Authenticate first (see below).

1. **Get an access token** — `POST /refreshToken` with your `refresh_token`; use `Authorization: Bearer <access_token>`.
2. **Create the return** — `POST /createReturnShipment` referencing the original order. Handle `OTO1187` (items already returned).
3. **Get the customer return link** — `POST /getReturnLink` to produce a hosted self-service return URL.
4. **Notify the customer** — `POST /triggerReturnSms` to send the return SMS (localizable: en/ar/tr).
5. **Check status** — `POST /getReturnDetails` for the current return state; the `orderStatus` webhook also fires `Returned` transitions.

Errors follow the `{ success:false, otoErrorCode, otoErrorMessage }` envelope (errors/oto-global-error-codes.yml).
