# Contributing to Ichava Documentation

This repo is the canonical source of long-form documentation for the [Ichava Laravel icon ecosystem](https://github.com/ichava/core). Pure markdown, no static-site builder yet, just `docs/*.md` files browseable on GitHub.

## What lives here

- `docs/`, topic files (architecture, configuration, environment, security, etc.)
- `README.md`, landing page + topic index

## What does NOT live here

- Code (everything is in [`ichava/core`](https://github.com/ichava/core), [`ichava/browser`](https://github.com/ichava/browser), and the icon-pack repos)
- Issues for those packages, file them at the relevant package's tracker (`ichava/core/issues`, etc.)
- Bugs *in the docs themselves* (typos, broken links, missing sections), file them here

## How to contribute

1. Fork the repo.
2. Edit a `docs/*.md` file with your change.
3. Use **CommonMark** (no MkDocs/VitePress directives yet), links between docs are relative (`[next](other-doc.md)`); links to code use absolute `https://github.com/ichava/core/blob/main/...` URLs.
4. Open a PR. Small typo fixes get merged fast.

## Style guide

- Sentence case for headings (`## Configuration`, not `## CONFIGURATION`).
- One H1 per file (the doc title); skip levels not allowed.
- Use **fenced code blocks with language tags** (`` ```bash ``, `` ```php ``, `` ```blade ``).
- Cross-link generously between docs, readers land here from package READMEs and need easy navigation.
- No emoji in headings (acceptable in body when meaningful).

## Reporting docs issues

Use the [issue tracker](https://github.com/ichava/documentation/issues). For urgent corrections to misleading content, just open a PR, far easier than going through the issue queue.
