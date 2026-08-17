---
name: Receive a payment into a Fipto wallet
description: Create a Fipto wallet, generate its receiving coordinates (IBAN or blockchain address), verify the deposit landed, and reconcile it from the webhook or the transaction list.
api: openapi/fipto-customer-api-openapi.yml
operations: [listCompaniesByUser, listAssets, createWalletByCompanyId, createWalletDetailsByWalletId, getWalletDetailsByWalletId, simulatePayin, searchTransactionsByCompanyId, getCompanyTransaction]
---

# Receive a payment into a Fipto wallet

Base URL: `https://api.fipto.app` (production) or `https://api.demo.fipto.tech` (demo).

## Before you start

Every request is signed. Build a `Signature` header per draft-cavage-http-signatures-12 with
`algorithm="hs2019"`, `keyId` = the UUID of your Fipto API user, over `(request-target) host date`
and — on bodied requests — `content-type digest`. `Date` must be RFC 1123 and less than a minute old.
`Digest` is `SHA-256=<base64 sha256 of the raw body>`. See `authentication/fipto-authentication.yml`.
There is no API key and no OAuth. Credentials are issued by Fipto during onboarding, not self-serve.

## Steps

1. **Resolve the company.** `listCompaniesByUser` (`GET /companies`). Almost every other path is
   scoped under `/companies/{company_id}/`, so hold this id.
2. **Check the asset is supported.** `listAssets`
   (`GET /companies/{company_id}/assets`). Do not assume an asset is enabled for your company — the
   set is per-company. USD specifically may need `requestUsdOnboarding` first.
3. **Create the wallet.** `createWalletByCompanyId`
   (`POST /companies/{company_id}/wallets`). A wallet is the balance container. It is **not** the
   thing money is sent to.
4. **Create the receiving coordinates.** `createWalletDetailsByWalletId`
   (`POST /companies/{company_id}/wallets/{wallet_id}/wallet-details`). This is the step integrations
   miss: `wallet_details` carries the IBAN for a fiat wallet or the blockchain address (and optional
   tag) for a digital one. A wallet with no wallet_details cannot receive anything.
5. **Read the coordinates back** with `getWalletDetailsByWalletId`, and hand `iban` or
   `address` (+ `tag`) to the payer. `getWalletDetailsPDF` returns a shareable account-details PDF.
6. **Test it on demo.** `simulatePayin`
   (`POST /companies/{company_id}/wallets/{wallet_id}/payin-simulation`) returns `204` and generates a
   payin on the demo environment only. Allow up to one minute for it to appear. By default it targets
   the first wallet_details created in the wallet.
7. **Reconcile.** Prefer the webhook: `PAYIN_CREATED` then `PAYIN_COMPLETED`, verified against
   Fipto's published per-environment RSA public key on the `Fipto-Signature` header. Otherwise poll
   `searchTransactionsByCompanyId` filtered by `wallet_id` and `transaction_types`, and read a single
   record with `getCompanyTransaction`.

## Rules

- **Deduplicate webhooks by `event_id`.** Fipto retries up to 10 times (2s → 900s, ~32 minutes total)
  whenever your endpoint does not answer 2XX within 5 seconds, so the same event will arrive twice.
- **Payin status is not binary.** `in transit`, `completed`, `returned`, and
  `waiting for travel rule information` are all real. The last one means the payment is held pending
  Travel Rule data — it is not a failure and not a success.
- **Pagination** is `page_number` (default 1) and `page_size` (default 100), with
  `meta.total_results` on the response. There are no cursors, so a busy transaction list can shift
  between pages.
- **Trace with `meta.request_id`** from the response body when contacting support. It is a body
  field, not a header.
