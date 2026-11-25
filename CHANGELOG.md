# Changelog

Notable changes to the ProxyJam API documentation. The format is based on
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

### Added

- Per-route rate limits on the routes that reach the payment provider or the upstream pool, and on
  webhook create/update and password change, listed in one table under Rate limits
  (`/overview/errors#rate-limits`) and on each endpoint page. An IP-counted limit counts an IPv6
  caller by its `/64`.
- At most 10 API keys per account; an 11th answers `409 CONFLICT`.
- Password reset and verification emails are capped per account (one a minute, five a day); a capped
  request gets the usual answer and sends nothing.
- MCP: `429 slow_down` after 30 unrecognised API keys from one address in 10 minutes.
- MCP clients can sign in with a ProxyJam account (OAuth 2.1) at `https://proxyjam.com/mcp`, now the
  canonical MCP URL; spending is a separate opt-in on the consent screen. A new page, OAuth and agent
  registration (`/overview/oauth`), covers the endpoints, scopes, token lifetimes, revocation, and
  how an agent registers on its own and what a claim grants.
- API keys are also accepted as `Authorization: Bearer pj_…`.
- `payment_url` on `GET /orders` and `GET /orders/{order_id}`: set while an order is `waiting_payment`
  for any external payment method (card, crypto, SBP, Telegram Stars), `null` otherwise.

### Changed

- On the OAuth consent screen, an app ProxyJam has not verified (anything but claude.ai and ChatGPT,
  including apps on your own computer) gets orders with proxy logins and passwords as a separate
  unticked *Show my orders and proxies* box, ticked and locked by *Allow spending from my wallet*,
  and is named by where access goes, or as "An app on this computer" for a loopback redirect or a
  native app's private-use scheme. This applies from the next sign-in; existing connections keep
  the scopes they were granted.
- Order `status` documents the real values — `new`, `waiting_payment`, `paid`, `provisioning_failed`,
  `provisioned`, `cancelled`, `refunded`, `expired` — in place of the old `pending`, `pending_payment`,
  `active` and `failed`. An unpaid order becomes `expired` when its payment window closes; a payment
  that arrives after that may be credited to the account balance, depending on the payment method (see
  Payment methods), and the order stays `expired`.
- The MCP server page moved to `/mcp-server` (its own tab); `/api/mcp` redirects there.
- API key links point at `app.proxyjam.com/apikey`: the dashboard has been the root of its own
  subdomain since frontend v0.1.6, and `/dashboard/apikey` survives there only as a redirect.
- Prose says IP allowlist instead of whitelist ("Update IP allowlist", IP-allowlist authentication).
  The endpoint `PUT /orders/{order_id}/whitelist`, the `whitelisted_ips` field, the MCP tool
  `set_proxy_whitelist` and the page address `/api/orders/proxy-whitelist` are unchanged.
- Change proxy signature describes the signature as the device and operating system the proxy
  presents.

## 2026-06-13

### Added

- Initial public documentation: getting-started guides, concept pages (authentication, idempotency,
  errors), the full API reference, and the Python SDK guide.
