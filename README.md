# Fipto

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Fipto is a Paris-based enterprise stablecoin payments and multi-currency accounts platform that lets businesses send and receive both fiat and stablecoin payments, hold multi-asset wallets with EUR and USD named accounts, convert between fiat and digital currencies, and automate treasury and reconciliation. It is licensed as a Payment Institution by France's ACPR (code 17908) and as a Crypto-Asset Service Provider by the AMF under MiCA (authorization A2026-009), and is ISO/IEC 27001:2022 certified. Fipto publishes a REST API (OpenAPI 3.0.3) covering wallets, beneficiaries, payouts, transactions, conversions, payment links, automation rules and an AISP/PISP access surface, plus signed webhooks and an open-source Model Context Protocol server for AI agents.

**Areas:** Company · Blockchain · Payments · Stablecoins · Banking · Treasury · Cross-Border Payments · Digital Currency · Fintech · Wallets

## Fipto on APIs.io

Everything profiled for Fipto is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/fipto/](https://apis.io/providers/fipto/)** — or go straight to one of the APIs or properties below.

### APIs (12)

- [Fipto AISP/PISP API](https://apis.io/apis/fipto/fipto-aisp-pisp-api/) — Endpoints for AISP/PISP.
- [Fipto Assets API](https://apis.io/apis/fipto/fipto-assets-api/) — Retrieve information about assets supported by Fipto.
- [Fipto Automations API](https://apis.io/apis/fipto/fipto-automations-api/) — The Automations API from Fipto — 2 operation(s) for automations.
- [Fipto Beneficiaries API](https://apis.io/apis/fipto/fipto-beneficiaries-api/) — Manage your beneficiaries to whitelist addresses for payout.
- [Fipto Companies API](https://apis.io/apis/fipto/fipto-companies-api/) — Manage information and settings of a company.
- [Fipto Conversions API](https://apis.io/apis/fipto/fipto-conversions-api/) — Manage conversions.
- [Fipto Internal Transfers API](https://apis.io/apis/fipto/fipto-internal-transfers-api/) — The Internal Transfers API from Fipto — 1 operation(s) for internal transfers.
- [Fipto Payin Simulation API](https://apis.io/apis/fipto/fipto-payin-simulation-api/) — The Payin Simulation API from Fipto — 1 operation(s) for payin simulation.
- [Fipto Payment links API](https://apis.io/apis/fipto/fipto-payment-links-api/) — Manage payment links.
- [Fipto Transactions API](https://apis.io/apis/fipto/fipto-transactions-api/) — Initiate payout and retrieve information about ongoing and completed transactions.
- [Fipto Travel Rule API](https://apis.io/apis/fipto/fipto-travel-rule-api/) — The Travel Rule API from Fipto — 1 operation(s) for travel rule.
- [Fipto Wallets API](https://apis.io/apis/fipto/fipto-wallets-api/) — Manage wallets and their related wallet details.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Fipto Webhooks](https://apis.io/asyncapis/fipto/fipto-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [fipto](https://apis.io/servers/fipto/fipto/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Fipto Agentic Access](https://apis.io/agentic-access/fipto/fipto-agentic-access/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Fipto Customer Api Overlay](https://apis.io/overlays/fipto/fipto-customer-api-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Fipto Authentication](https://apis.io/security/fipto/fipto-authentication/)
- [Fipto Domain Security](https://apis.io/security/fipto/fipto-domain-security/)
- [Fipto Trust Center](https://apis.io/security/fipto/fipto-trust-center/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Fipto Plans Pricing](https://apis.io/plans/fipto/fipto-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Fipto Rate Limits](https://apis.io/rate-limits/fipto/fipto-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://fipto.com)
- [Documentation](https://docs.fipto.com/docs/introduction)
- [Getting started](https://docs.fipto.com/docs/introduction)
- [API reference](https://docs.fipto.com/reference/getting-started)
- [Sign up](https://www.fipto.com/demo)
- [Support](https://www.fipto.com/contact)
- [Blog](https://www.fipto.com/company/blog)
- [Compliance](https://www.fipto.com/company/compliance)
- [Terms of service](https://www.fipto.com/legal/terms-and-conditions)
- [Privacy policy](https://www.fipto.com/legal/privacy)
- [Status](https://status.fipto.com/)

## API Evangelist rating

**Kin Score 48.6** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 71.7 |
| Contract quality | 52.6 |
| Contract governance | 18.2 |
| Operational transparency | 15.8 |
| Developer ergonomics | 58.9 |
| Access clarity | 50.0 |

**Agent readiness 32.1** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | mostly |

**Regulatory alignment 39.3** — Payments

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/fipto/](https://apis.io/providers/fipto/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Fipto: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/fipto/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
