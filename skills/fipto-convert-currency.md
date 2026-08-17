---
name: Convert between fiat and digital currency on Fipto
description: Discover tradable pairs, take a time-limited quote, confirm it, and read the resulting conversion.
api: openapi/fipto-customer-api-openapi.yml
operations: [listCompaniesByUser, listWallets, getPairs, createAQuote, confirmQuoteStatus, getConversion, searchTransactionsByCompanyId]
---

# Convert between fiat and digital currency on Fipto

Base URL: `https://api.fipto.app` (production) or `https://api.demo.fipto.tech` (demo).
Auth: RSA HTTP message signature — see `authentication/fipto-authentication.yml`.

Conversion on Fipto is **quote-then-confirm**, not a single call. A quote is priced and expires.

## Steps

1. **Resolve the company and both wallets.** `listCompaniesByUser`, then `listWallets`. You need a
   sell wallet and a buy wallet, and they must hold **different** assets.
2. **Check the pair is tradable.** `getPairs`
   (`GET /companies/{company_id}/pairs`) returns the conversion pairs configured for your company.
   Forbidden pairs fail later with `Manual flow required: pair is forbidden`.
3. **Create the quote.** `createAQuote` (`POST /companies/{company_id}/quotes`). Status starts at
   `submitted`.
4. **Confirm it before it expires.** `confirmQuoteStatus`
   (`PATCH /companies/{company_id}/quotes/{quote_id}/status`). Statuses run
   `submitted` → `pending` → `confirmed`.
5. **Read the conversion.** `getConversion`
   (`GET /companies/{company_id}/conversions/{conversion_id}`). Status is `confirmed`, `completed`,
   `returned` or `insufficient funds`. It also appears in `searchTransactionsByCompanyId`.

## Rules

- **Handle expiry as a normal path, not an error.** `Quote is expired`, `Quote already validated` and
  `Quote is not in submitted status` are documented 400 messages. On expiry, re-quote — do not retry
  the confirm.
- **`Manual flow required: …` means stop and escalate to a human.** It is returned when the amount is
  above the maximum or below the minimum EUR trading volume, when company trading limits are hit, or
  when the pair is forbidden. These are per-company commercial limits set by Fipto, not transient
  errors, and retrying will not clear them.
- **Errors are English sentences, not codes.** The 400 envelope is `{"data":{"message":"..."}}` and
  the spec pins the message text with regex patterns. Match on the documented strings in
  `errors/fipto-problem-types.yml`; there is no stable error code.
- **Decimals matter.** `Sell amount must have {n} decimals` is enforced per asset.
- **Automate it if it repeats.** A recurring convert-on-receipt can be expressed as an automation
  rule instead — see `fipto-automate-treasury.md`.
