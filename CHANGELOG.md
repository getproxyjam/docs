# Changelog

Notable changes to the ProxyJam API documentation. The format is based on
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

### Added

- MCP clients can sign in with a ProxyJam account (OAuth 2.1) at `https://proxyjam.com/mcp`, now the
  canonical MCP URL; spending is a separate opt-in on the consent screen. A new page, OAuth and agent
  registration (`/overview/oauth`), covers the endpoints, scopes, token lifetimes, revocation, and
  how an agent registers on its own and what a claim grants.
- API keys are also accepted as `Authorization: Bearer pj_…`.
- `payment_url` on `GET /orders` and `GET /orders/{order_id}`: set while an order is `waiting_payment`
  for any external payment method (card, crypto, SBP, Telegram Stars), `null` otherwise.

### Changed

- On the OAuth consent screen, an app ProxyJam has not verified (anything but claude.ai and ChatGPT, including apps on your own computer) gets orders with proxy logins and passwords as a separate unticked *Show my orders and proxies* box, ticked and locked by *Allow spending from my wallet*, and is named by where access goes.
- Order `status` documents the real values — `new`, `waiting_payment`, `paid`, `provisioning_failed`,
  `provisioned`, `cancelled`, `refunded`, `expired` — in place of the old `pending`, `pending_payment`,
  `active` and `failed`. An unpaid order becomes `expired` when its payment window closes; a payment
  that arrives after that may be credited to the account balance, depending on the payment method (see
  Payment methods), and the order stays `expired`.
- The MCP server page moved to `/mcp-server` (its own tab); `/api/mcp` redirects there.
- API key links point at `app.proxyjam.com/apikey`: the dashboard has been the root of its own
  subdomain since frontend v0.1.6, and `/dashboard/apikey` survives there only as a redirect.

## 2026-06-13

### Added

- Initial public documentation: getting-started guides, concept pages (authentication, idempotency,
  errors), the full API reference, and the Python SDK guide.
