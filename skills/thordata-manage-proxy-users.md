---
name: Provision and meter Thordata proxy sub-users
description: >-
  Create, cap, meter and delete proxy sub-users, whitelist IPs for password-free access, and read
  account traffic and wallet balances. Use when an agent has to hand out or reclaim proxy access
  and keep spend under control.
api: openapi/thordata-public-api-openapi.yml
operations:
  - listProxyUsers
  - createProxyUser
  - updateProxyUser
  - deleteProxyUser
  - getProxyUserUsage
  - listWhitelistedIps
  - addWhitelistedIp
  - deleteWhitelistedIp
  - getTrafficBalance
  - getWalletBalance
  - getAccountUsageStatistics
generated: '2026-08-11'
method: generated
---

# Provision and meter Thordata proxy sub-users

All operations here live on `https://openapi.thordata.com/api` and authenticate with the
**publicToken + publicKey** pair only — sent as the `token` and `key` headers. The scraper bearer
token is not used and will not work.

## Read the account first

- `getTrafficBalance` — `GET /account/traffic-balance` → `traffic_balance` in **KB**.
- `getWalletBalance` — `GET /account/wallet-balance` → `balance` in **USD**.
- `getAccountUsageStatistics` — `GET /account/usage-statistics` with `from_date` and `to_date`.
  **The range cannot exceed 180 days** — exceeding it returns code `10021`.

## Provision a sub-user

`createProxyUser` — `POST /proxy-users/create-user`:

- `username` — **required**, and globally unique. A collision returns code `10018`
  ("The username already exists"), so generate defensively.
- `password` — **required**.
- `proxy_type` — **required**. On *this* endpoint `1` = Residential, `2` = Unlimited.
- `status` — `"true"` or `"false"` (strings, not booleans).
- `traffic_limit` — cap in **MB**. `0` means unlimited; the minimum non-zero value is **100**.

Then `updateProxyUser` (`/proxy-users/update-user`) to change status or raise the cap, and
`deleteProxyUser` (`/proxy-users/delete-user`) to remove.

`listProxyUsers` — `GET /proxy-users/user-list` — returns `user_count`, `limit` and
`remaining_limit` (both **KB**) plus the users with their `usage_traffic`. Note the unit mismatch:
you **set** limits in MB and **read** usage in KB.

## Meter a sub-user

- `getProxyUserUsage` — `GET /proxy-users/usage-statistics` — daily, by `username` and date range.
- `getProxyUserUsageHourly` — `GET /proxy-users/usage-statistics-hour` — hourly.

## Whitelist an IP instead of shipping credentials

`addWhitelistedIp` — `POST /whitelisted-ips/add-ip` with `ip`, `proxy_type`, `status`. On the
whitelist endpoints `proxy_type` is `1` = Residential, `2` = Unlimited, **`9` = Mobile**.
`listWhitelistedIps` and `deleteWhitelistedIp` complete the set.

## Rules

- **`proxy_type` is overloaded and this is the most common integration bug on this API.** It is
  `{1: ISP, 2: Datacenter}` on `listProxies`, `{1: Residential, 2: Unlimited}` on the proxy-user
  endpoints, and `{1: Residential, 2: Unlimited, 9: Mobile}` on the whitelist endpoints. Never carry
  a value from one family to another.
- Error codes here are the five-digit Public API space (`10000` parameter error, `10011` too
  frequent — retryable with backoff, `10013` bad public token, `10014` bad public key), **not** the
  HTTP-shaped codes the scraping endpoints return.
- **No idempotency key.** A retried `create-user` either succeeds twice or trips `10018`; a retried
  `delete-user` is not guaranteed safe. Read `listProxyUsers` to confirm state rather than assuming.
- `traffic_limit` is the only spend control on a sub-user. Set it — an unlimited sub-user draws
  against the account traffic balance with nothing to stop it.

## Docs

- https://doc.thordata.com/doc/proxies/residential-proxies/user-and-pass-auth
- https://doc.thordata.com/doc/proxies/residential-proxies/whitelisted-ips
