---
name: Automate conversions and payouts on Fipto
description: Create trigger-action rules that convert or pay out automatically when funds arrive, and manage their lifecycle.
api: openapi/fipto-customer-api-openapi.yml
operations: [listCompaniesByUser, listWallets, listBeneficiaries, listAutomations, createAutomation, getAutomation, updateAutomation, deleteAutomation]
---

# Automate conversions and payouts on Fipto

Base URL: `https://api.fipto.app` (production) or `https://api.demo.fipto.tech` (demo).
Auth: RSA HTTP message signature — see `authentication/fipto-authentication.yml`.

An automation rule fires on a trigger event and performs a conversion or a payout without a further
API call. It replaces a polling loop.

## Steps

1. **Resolve the company, the source wallet, and the destination.** `listCompaniesByUser`,
   `listWallets`, and — for a payout rule — `listBeneficiaries`.
2. **Check what already exists.** `listAutomations`
   (`GET /companies/{company_id}/automations`). Only **one rule per trigger event per wallet** is
   allowed, so creating a second one on the same pair will be rejected.
3. **Create the rule.** `createAutomation` (`POST /companies/{company_id}/automations`).
   - `rule_type` is `conversion` or `payout`.
   - `trigger_event` is `payin_completed` or `conversion_completed`. A conversion rule can only be
     triggered by `payin_completed`.
   - `amount_mode` is `full` or `inherited`.
   - A conversion rule requires `destination_wallet_id`; a payout rule requires
     `destination_beneficiary_id`.
4. **Manage it.** `getAutomation`, `updateAutomation` (`PUT`), `deleteAutomation`.

## Rules

- **`createAutomation` requires 2FA verification.** This is stated in the contract itself. An
  unattended agent cannot create a rule on its own — a human must complete strong authentication.
  Plan for the handoff rather than retrying.
- **Eligibility is narrow.** The source wallet asset must be EUR, USD or a stablecoin, and a
  beneficiary that targets another Fipto wallet cannot be used for automation.
- **Deletion is terminal.** `Cannot update a deleted automation rule` and
  `This automation rule has already been deleted` are documented 400 responses — re-create instead of
  reviving.
- **Automations raise no webhook of their own.** Only the underlying payin/payout/payment-link events
  fire, so reconcile the result through the transaction list.
