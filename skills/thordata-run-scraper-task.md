---
name: Run a Thordata Web Scraper task and collect the results
description: >-
  Launch a pre-built site scraper (Amazon, LinkedIn, TikTok, Zillow, Crunchbase and more) as an
  asynchronous task, poll it to completion and download the structured JSON or CSV. Use for
  structured extraction from a supported site rather than raw page collection.
api: openapi/thordata-scraper-api-openapi.yml
operations:
  - runScraperTask
  - getScraperTaskStatus
  - listScraperTasks
  - downloadScraperTaskResult
generated: '2026-08-11'
method: generated
---

# Run a Thordata Web Scraper task

This is the only asynchronous flow in the platform: launch, poll, download.

## What you need

**All three credentials.** The builder endpoint is the one place Thordata requires the scraper token
*and* the public pair together:

- `Authorization: Bearer <scraperToken>`
- `token: <publicToken>`
- `key: <publicKey>`

## Step 1 — launch

`runScraperTask` — `POST https://scraperapi.thordata.com/builder`, form-encoded:

- `spider_name` — the target site key, e.g. `amazon.com`
- `spider_id` — the scraper key, e.g. `amazon_product_by-url`
- `spider_parameters` — a **JSON-encoded string** containing an array of per-input objects, e.g.
  `[{"url":"https://www.amazon.com/dp/B0...","zip_code":"94107"}]`
- `spider_errors` — `true` to include per-input errors in the result set
- `file_name` — output name; `{{TasksID}}` is a supported template

Per-site parameter references are published under
`https://doc.thordata.com/doc/scraping/web-scraper-api/parameter-description/` — there is one page
per supported site.

For video or audio collection use `runVideoScraperTask` — `POST /video_builder` — which adds
`common_settings`, a JSON string carrying `resolution` (e.g. `<=360p`), `video_codec` (`vp9`,
`h264`), `audio_format` (`opus`, `mp3`, `aac`), `bitrate` (e.g. `<=320`) and `selected_only`.

## Step 2 — wait

Prefer **webhooks** over polling. Configure them in the dashboard integrations panel; Thordata will
POST on `In Progress`, `Task Success` and `Task Failure`. The payload is your own JSON template with
`{{ }}` variables — `resource.jsonUrl` and `resource.csvUrl` carry the download links, and
`Webhook-Dispatch-Id` carries the task id for de-duplication. **There is no signature on the
webhook**, so verify by other means and treat the body as untrusted; note also that the published
payload echoes the account `apiKey` inside `resource`.

If you must poll, call `getScraperTaskStatus` — `POST` `/tasks-status` on
`https://openapi.thordata.com/api/web-scraper-api` with `tasks_ids`, using only the `token` and
`key` headers (no bearer). Back off between polls; there is no published rate limit.

`listScraperTasks` — `POST /tasks-list` with `page` and `size` — returns `count` and `list` if you
need to reconcile history.

## Step 3 — download

`downloadScraperTaskResult` — `POST /tasks-download` with `tasks_id` and `type`, where `type` is one
of `json`, `csv`, `video`, `subtitle`, `audio`. Result objects are served from Tencent Cloud COS,
not from a thordata.com host.

## Rules

- **No idempotency key.** A retried `/builder` call creates a **second task** and a second charge.
  Record the returned task id before retrying anything.
- Only successful collection is billed; failed tasks are not.
- `proxy_type` integers mean different products on different endpoints — do not carry a value across
  from the proxy endpoints (see `data-model/thordata-data-model.yml`).
- To schedule recurring runs, use the dashboard Timer page with a standard 5-field cron expression
  (`0 8 * * 1-5` = weekdays at 08:00). Scheduled runs emit the same webhook events.

## Docs

- https://doc.thordata.com/doc/scraping/web-scraper-api/getting-started-guide
- https://doc.thordata.com/doc/scraping/web-scraper-api/integrations/webhook-integration
- https://doc.thordata.com/doc/scraping/web-scraper-api/scheduler
