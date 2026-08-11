---
name: Fetch a blocked or JavaScript-heavy page with the Thordata Universal Scraping API
description: >-
  Retrieve any URL through Thordata's unblocking layer with optional JavaScript rendering,
  geo-targeting, resource blocking and custom headers or cookies, returning HTML or a PNG
  screenshot. Use when a plain HTTP fetch is blocked, geo-fenced or client-side rendered.
api: openapi/thordata-universal-api-openapi.yml
operations:
  - scrapeUrl
generated: '2026-08-11'
method: generated
---

# Fetch a blocked or JavaScript-heavy page

## What you need

A **scraper token** (`THORDATA_SCRAPER_TOKEN`). The same token works for the SERP API.

## Call

`scrapeUrl` — `POST https://universalapi.thordata.com/request`
(`https://webunlocker.thordata.com/request` is a documented alias for the same contract).

Headers: `Authorization: Bearer <scraperToken>`, `Content-Type: application/x-www-form-urlencoded`.

Body fields:

- `url` — **required**. The target URL.
- `js_render` — `True` or `False`. Set `True` for SPAs and dynamically loaded content. Recommended.
- `type` — `html` (default) or `png` for a screenshot.
- `country` — proxy country code (`us`, `de`, …) for geo-targeted collection.
- `block_resources` — comma-separated resource types to skip (`image`, `script`, `css`). Cuts
  collection time on heavy pages.
- `clean_content` — comma-separated content to strip from the body (`js`, `css`). Use this to reduce
  tokens before handing the result to a model.
- `wait` — fixed wait in milliseconds. **Maximum 100000.**
- `wait_for` — CSS selector to await. **Overrides `wait`.** Maximum 30 seconds; content is returned
  automatically on timeout rather than erroring.
- `headers` — a **JSON-encoded string**, not a nested object:
  `[{"name":"User-Agent","value":"Mozilla/5.0"}]`
- `cookies` — same shape: `[{"name":"session","value":"abc"}]`

## Reading the response

On success you get the page body directly — `text/html` or `image/png` — not a JSON envelope. On
failure you get `{code, msg, data}`. Resolve status by precedence: body `code` when present and not
200, otherwise the HTTP status.

`300` means the request was accepted but nothing could be collected. It is **retryable and not
billed** — usually worth one retry with `js_render=True` and a longer `wait`.

## Rules

- **Only a 200 is billed.** 300, 400, 401, 429 and 5xx are free.
- **No idempotency key.** A retried success is charged again.
- **No rate-limit headers and no published limit.** 429 means concurrency was exceeded; back off
  exponentially. 402 is also a rate-limit condition in Thordata's own SDKs even though it is absent
  from the published response-code table.
- Prefer `wait_for` over `wait` — it returns as soon as the selector lands instead of always paying
  the full delay.
- If you need Markdown rather than HTML, the API has no Markdown output. Convert client-side (the
  official LangChain pack does exactly this in `thordata_fetch_markdown`).

## Docs

- https://doc.thordata.com/doc/scraping/universal-scraping-api/send-your-first-request
- https://doc.thordata.com/doc/scraping/web-unlocker/query-parameters
- https://doc.thordata.com/doc/scraping/universal-scraping-api/response-codes
