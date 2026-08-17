---
name: Collect a stablecoin payment with a Fipto payment link
description: Create a hosted checkout link, send it to the payer, and handle completion, underpayment and overpayment.
api: openapi/fipto-customer-api-openapi.yml
operations: [listCompaniesByUser, createPaymentLinks, getPaymentLink, listPaymentLinks, updatePaymentLink]
---

# Collect a stablecoin payment with a Fipto payment link

Base URL: `https://api.fipto.app` (production) or `https://api.demo.fipto.tech` (demo).
Auth: RSA HTTP message signature — see `authentication/fipto-authentication.yml`.

A payment link is a **Fipto-hosted** checkout page. Fipto runs the payer flow and converts the
received stablecoin to euros into your Fipto wallet. You do not render anything.

## Steps

1. **Resolve the company.** `listCompaniesByUser`.
2. **Create the link.** `createPaymentLinks`
   (`POST /companies/{company_id}/payment-links`).
3. **Send or redirect the payer** to the returned URL.
4. **Track it.** `getPaymentLink`
   (`GET /companies/{company_id}/payment-links/{payment_link_id}`), or list and filter with
   `listPaymentLinks`, which supports `statuses`, `expired`, `processed` and `refunded` filters.
5. **Amend if needed.** `updatePaymentLink`
   (`PATCH /companies/{company_id}/payment-links/{payment_link_id}`).
6. **Settle on the webhook.** `PAYMENT_LINK_COMPLETED` fires when the link is paid.

## Rules

- **Four statuses, and two of them are not failures.** `pending`, `completed`, `underpaid`,
  `overpaid`. On-chain payers routinely send the wrong amount; `underpaid` and `overpaid` are
  first-class outcomes your handler must resolve, not exceptions. Fipto documents the resolution
  paths at <https://docs.fipto.com/docs/edge-case-management>.
- **Deduplicate by `event_id`.** Webhook retries will re-deliver `PAYMENT_LINK_COMPLETED`.
- **Verify the webhook signature** against Fipto's published environment public key before acting on
  a completion — this is a money event on a public URL.
