# ProxyJam API Docs

Source for the [ProxyJam API documentation](https://docs.proxyjam.com), built with
[Mintlify](https://mintlify.com).

[![Docs](https://img.shields.io/badge/docs-docs.proxyjam.com-0066FF.svg)](https://docs.proxyjam.com)
[![Checks](https://github.com/getproxyjam/docs/actions/workflows/ci.yml/badge.svg)](https://github.com/getproxyjam/docs/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## Contents

- [Prerequisites](#prerequisites)
- [Local development](#local-development)
- [Project structure](#project-structure)
- [Editing and adding pages](#editing-and-adding-pages)
- [Validating your changes](#validating-your-changes)
- [Deployment](#deployment)
- [Contributing](#contributing)
- [Security](#security)
- [License](#license)

## Prerequisites

- [Node.js](https://nodejs.org) **v20.17.0+**
- The Mintlify CLI:
  ```bash
  npm i -g mint
  ```

## Local development

Run a live preview from the repository root (where `docs.json` lives):

```bash
mint dev
```

The site opens at `http://localhost:3000` and hot-reloads as you edit. If your local preview drifts
from production, update the CLI with `mint update`.

## Project structure

```
.
├── docs.json     # Mintlify configuration: theme, navigation, API settings
├── overview/     # Getting-started and concept guides (.mdx)
├── api/          # API reference pages (.mdx), grouped by area (orders, wallet, …)
└── images/       # Logos and other assets
```

`docs.json` is the single source of configuration: site name and theme, color palette, the
navigation tree, and the API defaults (base server `https://api.proxyjam.com/public/v1` and
`X-API-Key` authentication) shared by every reference page.

## Editing and adding pages

Every page is an `.mdx` file that starts with frontmatter:

```mdx
---
title: "List orders"
description: "Retrieve your orders, most recent first."
---
```

API reference pages add an `api` field describing the operation. The server and authentication are
inherited from `docs.json`, so the playground works without repeating them:

```mdx
---
title: "List orders"
description: "Retrieve your orders, most recent first."
api: "GET /orders"
---
```

After creating a page, add its path (without the `.mdx` extension, e.g. `api/orders/list-orders`)
to the `navigation` tree in `docs.json` so it appears in the sidebar. Pages that aren't listed in
the navigation won't show up in the rendered site.

> **Provider neutrality:** this documentation is public. Describe mobile proxies as
> "mobile rotating" — never name the upstream infrastructure provider in any page.

## Validating your changes

```bash
mint broken-links     # report broken internal links
mint validate         # strict build check — fails on warnings or errors
```

`mint broken-links` accepts extra flags for deeper checks, for example
`mint broken-links --check-anchors --check-redirects`. CI runs `mint broken-links` on every push and
pull request to `main`.

## Deployment

Once changes are merged to `main`, Mintlify publishes the site to
[docs.proxyjam.com](https://docs.proxyjam.com) automatically. No manual deploy step is required.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full workflow. Small fixes (typos, broken links,
clarifications) are very welcome.

## Security

To report a vulnerability in the API or platform, follow [SECURITY.md](SECURITY.md) — please don't
open a public issue.

## License

[MIT](LICENSE) © getproxyjam
