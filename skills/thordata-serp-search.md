---
name: Collect search engine results with the Thordata SERP API
description: >-
  Run a real-time search against Google, Bing, Yandex or DuckDuckGo through Thordata and get back
  parsed JSON or raw HTML, with geo and language targeting. Use when an agent needs live search
  results rather than a cached index.
api: openapi/thordata-scraper-api-openapi.yml
operations:
  - searchSerp
  - listCountries
generated: '2026-08-11'
method: generated
---

# Collect search engine results with the Thordata SERP API

## What you need

A **scraper token** (`THORDATA_SCRAPER_TOKEN`), from Dashboard > SERP API > API Playground > Token.
This is not the same credential as the `publicToken`/`publicKey` pair used by the account and task
endpoints — see `authentication/thordata-authentication.yml`.

## Step 1 — check the target country is supported (optional)

If you are geo-targeting, call `listCountries` on `https://openapi.thordata.com/api/locations` with
the `token` and `key` headers to confirm the country code is available for the product. Skip this
if you are searching without a country.

## Step 2 — run the search

Call `searchSerp` — `POST https://scraperapi.thordata.com/request`.

Send `Authorization: Bearer <scraperToken>` (or the token in a bare `token` header) and a
form-encoded body:

- `engine` — **required**. `google`, `bing`, `yandex`, `duckduckgo`.
- `q` — the query. Required for every engine **except** `yandex`.
- `text` — the query for `yandex` instead of `q`.
- `json` — `1` for parsed JSON, `0` for raw HTML. **Do not send `2` ("both")** — it is deprecated and
  the dashboard does not support it.
- `gl` — country code for localized results. `hl` — language code.
- `num` — result count. `start` — pagination offset. Both are passthroughs to the search engine, not
  Thordata pagination.
- `tbm` — result vertical. Use the published mapping: `images`/`isch` → `isch`, `news`/`nws` → `nws`,
  `shop`/`shopping` → `shop`, `videos`/`vid` → `vid`.
- `tbs` — time filter. Use the published mapping: `hour` → `qdr:h`, `day` → `qdr:d`, `week` → `qdr:w`,
  `month` → `qdr:m`, `year` → `qdr:y`.
- `render_js` — `True`/`False`. `no_cache` — `True`/`False`.

## Step 3 — read the result correctly

The response is a JSON envelope: `{code, msg, data}`. **Resolve status by precedence** — trust the
body `code` when it is present and not 200, otherwise fall back to the HTTP status.

| Code | Meaning | Retry? | Billed? |
|---|---|---|---|
| 200 | Success | no | **yes** |
| 300 | Accepted but nothing collected | yes | no |
| 400 | Bad parameters | no | no |
| 401 | Bad token | no | no |
| 403 | Target server refused | no | no |
| 429 / 402 | Rate or concurrency limit | yes, exponential backoff | no |
| 500 / 504 | Server or upstream timeout | yes, exponential backoff | no |

## Rules

- **Only a 200 is billed.** Retrying a 300, 429 or 5xx costs nothing, so a backoff loop is
  financially safe. A retried **200** is charged again.
- **There is no idempotency key.** Every call is a new billable collection. If you retry after a
  timeout where the response may have been delivered, you may pay twice.
- **There are no rate-limit headers.** No `RateLimit-*`, no `Retry-After`. Back off blind on 429 —
  exponential backoff is what Thordata's own SDKs implement.
- Thordata publishes **no numeric rate limit**, so do not assume a safe concurrency; ramp up.
- Use the SSL certificate Thordata publishes, or ignore SSL errors, per the configuration docs.

## Docs

- https://doc.thordata.com/doc/scraping/serp-api/send-your-first-request
- https://doc.thordata.com/doc/scraping/serp-api/query-parameters
- https://doc.thordata.com/doc/scraping/serp-api/response-codes
