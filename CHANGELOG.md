# Changelog

Notable changes to the ProxyJam API documentation. The format is based on
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

### Added

- The MCP server page moved to `/mcp-server` (its own tab); `/api/mcp` redirects there.
- MCP clients can sign in with a ProxyJam account (OAuth 2.1) at `https://proxyjam.com/mcp`, now the
  canonical MCP URL; spending is a separate opt-in on the consent screen. A new page, OAuth and agent
  registration (`/overview/oauth`), covers the endpoints, scopes, token lifetimes, revocation, and
  how an agent registers on its own and what a claim grants.
- API keys are also accepted as `Authorization: Bearer pj_…`.

### Changed

- API key links point at `app.proxyjam.com/apikey`: the dashboard has been the root of its own
  subdomain since frontend v0.1.6, and `/dashboard/apikey` survives there only as a redirect.

## 2026-06-13

### Added

- Initial public documentation: getting-started guides, concept pages (authentication, idempotency,
  errors), the full API reference, and the Python SDK guide.
