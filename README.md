# Thordata

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

Web data collection infrastructure combining a global proxy network with four HTTP collection APIs. The proxy side spans residential, ISP, datacenter, mobile and high-bandwidth pools reached through a gateway with per-product ports, geo-targeting encoded in the username, and either Basic auth or IP whitelisting. The API side is a SERP API across Google, Bing, Yandex and DuckDuckGo; a Universal Scraping API and Web Unlocker for JavaScript-rendered and blocked pages; a Web Scraper API of pre-built extractors for Amazon, LinkedIn, TikTok, Zillow, Crunchbase and sixteen more sites, run as asynchronous tasks with cron scheduling and webhook callbacks; and a remote Scraping Browser driven over the Chrome DevTools Protocol from Puppeteer, Playwright or Selenium. A public management API covers account balances, proxy inventory, proxy sub-user provisioning with traffic caps, IP whitelisting and geo-targeting reference data. Thordata maintains a canonical cross-language SDK specification on GitHub that drives official Python, JavaScript, Go and Java clients, publishes an OpenAPI generated from it, ships an official LangChain tool pack and a Firecrawl-compatible layer, and serves a full markdown documentation index at llms.txt. Billing is prepaid and unusual in one respect that matters to automated consumers: only a 200 response is charged, so failed and empty collections cost nothing.

**Areas:** Proxy Network · Web Scraping · Data Extraction · SERP · Search data · Web unblocking · Residential Proxies · Mobile Proxies · ISP Proxies · Datacenter Proxies · Scraping Browser · Data-for-AI

## Thordata on APIs.io

Everything profiled for Thordata is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/thordata/](https://apis.io/providers/thordata/)** — or go straight to one of the APIs or properties below.

### APIs (11)

- [Thordata Locations API](https://apis.io/apis/thordata/thordata-locations-api/) — Geo-targeting reference data - the countries, states, cities and ASNs available for each proxy product. Read this before setting a country, state or city on…
- [Thordata Proxy IP Extract API](https://apis.io/apis/thordata/thordata-proxy-ip-extract-api/) — Pull a batch of proxy endpoints as host:port pairs for the residential or unlimited product, filtered by country, state, city, protocol and session time,…
- [Thordata Account API](https://apis.io/apis/thordata/thordata-account-api/) — Balances and usage statistics
- [Thordata Proxy API](https://apis.io/apis/thordata/thordata-proxy-api/) — Purchased proxy inventory
- [Thordata Proxy Users API](https://apis.io/apis/thordata/thordata-proxy-users-api/) — Proxy sub-user lifecycle and per-user usage
- [Thordata SERP API](https://apis.io/apis/thordata/thordata-serp-api-api/) — Real-time search engine results
- [Thordata Tasks API](https://apis.io/apis/thordata/thordata-tasks-api/) — Task lifecycle for the Web Scraper API
- [Thordata Web Scraper API](https://apis.io/apis/thordata/thordata-web-scraper-api-api/) — Pre-built site scrapers launched as asynchronous tasks
- [Thordata Whitelist API](https://apis.io/apis/thordata/thordata-whitelist-api/) — IP whitelisting for password-free proxy authentication
- [Thordata Public API](https://apis.io/apis/thordata/thordata-public-api-api/) — The Public API API from Thordata — 1 operation(s) for public api.
- [Thordata Universal API](https://apis.io/apis/thordata/thordata-universal-api-api/) — The Universal API API from Thordata — 1 operation(s) for universal api.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Thordata Web Scraper Webhooks](https://apis.io/asyncapis/thordata/thordata-web-scraper-webhooks/)

#### Collections (6)

Postman and Open Collection request collections.

- [Thordata Locations API](https://apis.io/collections/thordata/open-thordata-locations-api/)
- [Thordata Proxy IP Extract API](https://apis.io/collections/thordata/open-thordata-proxy-extract-api/)
- [Thordata Public API](https://apis.io/collections/thordata/open-thordata-public-api/)
- [Thordata Scraper API](https://apis.io/collections/thordata/open-thordata-scraper-api/)
- [Thordata Universal Scraping API / Web Unlocker](https://apis.io/collections/thordata/open-thordata-universal-api/)
- [Thordata Web Scraper API - Tasks](https://apis.io/collections/thordata/open-thordata-web-scraper-tasks/)

#### Overlays (6)

OpenAPI overlays, including conversational phrasing for each operation.

- [Thordata Locations Api Overlay](https://apis.io/overlays/thordata/thordata-locations-api-overlay/)
- [Thordata Proxy Extract Api Overlay](https://apis.io/overlays/thordata/thordata-proxy-extract-api-overlay/)
- [Thordata Public Api Overlay](https://apis.io/overlays/thordata/thordata-public-api-overlay/)
- [Thordata Scraper Api Overlay](https://apis.io/overlays/thordata/thordata-scraper-api-overlay/)
- [Thordata Universal Api Overlay](https://apis.io/overlays/thordata/thordata-universal-api-overlay/)
- [Thordata Web Scraper Tasks Overlay](https://apis.io/overlays/thordata/thordata-web-scraper-tasks-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Thordata Authentication](https://apis.io/security/thordata/thordata-authentication/)
- [Thordata Domain Security](https://apis.io/security/thordata/thordata-domain-security/)
- [Thordata Vulnerability Disclosure](https://apis.io/security/thordata/thordata-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Thordata Plans Pricing](https://apis.io/plans/thordata/thordata-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Thordata Rate Limits](https://apis.io/rate-limits/thordata/thordata-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.thordata.com/)
- [Documentation](https://doc.thordata.com/doc/overview)
- [Getting started](https://doc.thordata.com/doc/scraping/serp-api/quick-start-guide)
- [API reference](https://thordata.github.io/thordata-sdk-spec/)
- [Pricing](https://www.thordata.com/pricing)
- [Sign up](https://dashboard.thordata.com/register)
- [Support](https://www.thordata.com/contact-us)
- [Blog](https://www.thordata.com/blog)
- [Security](https://www.thordata.com/security-vulnerabilities-reward-program)
- [Terms of service](https://www.thordata.com/service-agreement)
- [Privacy policy](https://www.thordata.com/privacy-policy)
- [GitHub](https://github.com/Thordata)

## API Evangelist rating

**Kin Score 38.8** — thin · rubric 0.24.0 · scored 2026-10-17

| Facet | Score |
|---|---|
| Discoverability | 78.6 |
| Contract quality | 20.3 |
| Contract governance | 4.5 |
| Operational transparency | 36.8 |
| Developer ergonomics | 56.5 |
| Access clarity | 38.2 |

**Agent readiness 31.5** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
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

**Regulatory alignment 30.4** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/thordata/](https://apis.io/providers/thordata/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Thordata: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/thordata/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
