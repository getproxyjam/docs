# Changelog

Notable changes to the ProxyJam API documentation. The format is based on
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

### Changed

- Rate limits are documented per identity class — a bearer token, a recognised API key, or the
  caller's address — replacing the single flat 100/60 with a burst of 10. The identification order
  is corrected: a bearer token now takes precedence over an `X-API-Key`. Per-route limits are
  listed rather than illustrated with one example, `X-RateLimit-Limit` is described as the steady
  rate rather than the bucket's capacity, and a `503` is documented as load shedding that carries
  `Retry-After`, not only as an unreachable dependency.
- API key links point at `app.proxyjam.com/apikey`: the dashboard has been the root of its own
  subdomain since frontend v0.1.6, and `/dashboard/apikey` survives there only as a redirect.

## 2026-06-13

### Added

- Initial public documentation: getting-started guides, concept pages (authentication, idempotency,
  errors), the full API reference, and the Python SDK guide.
