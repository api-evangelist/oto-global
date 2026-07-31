---
name: Create an order and ship it with OTO
description: Authenticate, create an order, price it against carriers, create a shipment, print the AWB label, and track it.
api: openapi/oto-global-openapi.yml
operations: [refreshToken, createOrder, getDeliveryOptions, checkDeliveryFee, createShipment, printAWB, trackShipment]
generated: '2026-07-20'
method: generated
---

# Create an order and ship it with OTO

All calls hit `https://api.tryoto.com/rest/v2` (use `https://staging-api.tryoto.com/rest/v2` for testing).

1. **Get an access token** — `POST /refreshToken` with `{ "refresh_token": "<from OTO dashboard>" }`. Read `access_token` from the response (valid 1 hour). Send `Authorization: Bearer <access_token>` on every call below.
2. **Create the order** — `POST /createOrder` with recipient, items[], and pickup location. Capture the returned `orderId`.
3. **Choose a carrier** — `GET /getDeliveryOptions` and/or `POST /checkDeliveryFee` to compare rates across OTO's 450+ carriers.
4. **Create the shipment** — `POST /createShipment` with the `orderId` and chosen delivery company. On error, read `otoErrorCode` (e.g. `OTO1006` credit not enough, `OTO1001` invalid order id).
5. **Print the label** — `GET /print/{orderId}` (`printAWB`) to retrieve the AWB.
6. **Track it** — `POST /trackShipment` (or `POST /orderStatus`) for live status; or register the `orderStatus` webhook to receive pushes.

Conventions: errors return `{ success:false, otoErrorCode, otoErrorMessage }` (see errors/oto-global-error-codes.yml). No idempotency key is supported, so guard against duplicate createOrder calls yourself.
