# Contributing

Thanks for helping improve the ProxyJam API documentation.

This repository is the published, canonical home of the docs. We develop them upstream and mirror
changes here. Issues and pull requests are welcome — a maintainer reviews them and syncs accepted
changes upstream so they flow back on the next publish.

## Getting started

Install the [Mintlify CLI](https://mintlify.com) (Node.js v20.17.0+) and start a live preview:

```bash
npm i -g mint
mint dev
```

The preview runs at `http://localhost:3000` and reloads as you edit.

## Editing content

- Pages are `.mdx` files with `title` and `description` frontmatter.
- API reference pages add an `api` field (for example `api: "GET /orders"`); the server and
  `X-API-Key` auth come from `docs.json`.
- When you add a page, register its path in the `navigation` tree in `docs.json` — unlisted pages
  don't appear in the sidebar.
- Keep the writing concise and task-focused, and prefer runnable examples.

**Provider neutrality:** these docs are public. Refer to mobile proxies as "mobile rotating" and do
not name specific upstream infrastructure providers anywhere.

## Before opening a pull request

Run the same checks CI runs, plus a strict build:

```bash
mint broken-links
mint validate
```

Then open a pull request describing what you changed. Screenshots are helpful for visual changes.
