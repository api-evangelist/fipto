---
name: Pay a beneficiary from a Fipto wallet
description: Register and verify a payout counterparty, satisfy Verification of Payee and the Travel Rule, initiate the payout, and follow it to settlement.
api: openapi/fipto-customer-api-openapi.yml
operations: [listCompaniesByUser, listWallets, createBeneficiary, verifyBeneficiary, updateBeneficiaryTravelRule, listBeneficiaries, searchBeneficiaries, initiatePayout, getCompanyTransaction, searchTransactionsByCompanyId]
---

# Pay a beneficiary from a Fipto wallet

Base URL: `https://api.fipto.app` (production) or `https://api.demo.fipto.tech` (demo).
Auth: RSA HTTP message signature — see `authentication/fipto-authentication.yml`.

## Steps

1. **Resolve the company and the funding wallet.** `listCompaniesByUser`, then `listWallets`
   (`GET /companies/{company_id}/wallets`). Check the wallet holds the asset you intend to send.
2. **Create the beneficiary.** `createBeneficiary`
   (`POST /companies/{company_id}/beneficiaries`). A beneficiary is required before any payout — you
   cannot pay a raw IBAN or address inline. For fiat supply `account_number` and
   `account_number_type`; for digital supply the blockchain address. For many at once use
   `validateBatchBeneficiary` (validates a CSV) then `createBatchBeneficiaries`.
3. **Verify a euro beneficiary.** `verifyBeneficiary`
   (`POST /companies/{company_id}/beneficiaries/{beneficiary_id}/verify`) runs the SEPA Verification
   of Payee scheme and returns a VOP result code (`MTCH` and siblings). Run this before paying a new
   EUR counterparty.
4. **Complete Travel Rule data where required.** `updateBeneficiaryTravelRule`
   (`PATCH /companies/{company_id}/beneficiaries/{beneficiary_id}/wallet-details/travel-rule`).
   `travel_rule_status` is `completed` or `incomplete`; incomplete data will hold the transfer.
5. **Wait for the beneficiary to be usable.** Poll `searchBeneficiaries`
   (`GET /companies/{company_id}/beneficiaries/{beneficiary_id}`). Status is one of `active`,
   `pending`, `rejected`, `awaiting_approval`. Only `active` can be paid.
6. **Initiate the payout.** `initiatePayout`
   (`POST /companies/{company_id}/wallets/{wallet_id}/payouts`).
7. **Follow it to settlement.** `getCompanyTransaction`, or the `PAYOUT_COMPLETED` /
   `PAYOUT_REJECTED` webhook.

## Rules

- **There is no idempotency key.** Fipto accepts no `Idempotency-Key` header and no client-supplied
  reference on `initiatePayout`. **Never blind-retry a payout.** If a call times out, reconcile with
  `searchTransactionsByCompanyId` filtered by `wallet_id` and a `date_from` window before trying
  again.
- **A 2xx is not a settled payment.** Payout status can be `pending`, `submitted`, `in process`,
  `awaiting co-signer`, `awaiting approval`, `insufficient funds`, `rejected` or `completed`. Treat
  only `completed` as sent, and surface `awaiting co-signer` / `awaiting approval` to a human — those
  need a person in the Fipto platform.
- **Currency must match.** The beneficiary's currency must match the source wallet's currency; the
  API rejects the mismatch with `Beneficiary currency must match source wallet currency for payouts`.
  Convert first — see `fipto-convert-currency.md`.
- **Delegated access.** If you act as a PSD2 third party, the equivalent calls live under
  `/companies/{company_id}/aisp-pisp/` — `initiatePayoutAISPPISP`, `listBeneficiariesAISPPISP`,
  `getBeneficiaryAISPPISP`.
