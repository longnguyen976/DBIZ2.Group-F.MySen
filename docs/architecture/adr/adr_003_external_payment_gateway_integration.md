# ADR-003: Integrate external payment gateways (VNPay/MoMo) via webhook callbacks

| Field | Value |
|---|---|
| Status | Accepted |
| Date | Lesson 4 |

**Context.** Visitors need to purchase park admission e-tickets digitally (`UC-02`) using popular Vietnamese cashless methods. Handling raw bank card data or building direct banking integrations introduces severe PCI-DSS compliance overhead and security risks beyond project scope.

**Decision.** Delegate all monetary transactions to external payment gateways (VNPay and MoMo). The Ticketing Service generates a signed payment URL, redirects the user, and updates order status to `PAID` only upon receiving a verified server-to-server IPN/webhook callback before issuing the QR e-ticket.

**Consequences.** MySen stores zero sensitive card or e-wallet credentials. Order fulfillment remains reliable even if the visitor closes their browser mid-redirect, though the Ticketing Service must handle idempotent webhook retries and expired payment timeouts gracefully.