# Claire de Binare - Docs Hub

This repository is the **Canonical Docs Hub** for the Claire de Binare project. It contains all architecture, governance, and design documentation.

## Quick Access

The primary entry point for all developers and agents is the Architecture Cockpit.

➡️ **[Go to Architecture Cockpit](./knowledge/ARCHITECTURE_COCKPIT.md)**

## Local Docs Sanity Checks

Run these commands to reproduce the docs workflow locally if GitHub Actions is blocked:

- `markdownlint 'docs/**/*.md' 'knowledge/**/*.md' README.md`
- `markdown-link-check 'docs/**/*.md' 'knowledge/**/*.md' README.md`

## Docs CI
.github/workflows/docs-ci.yml runs markdown linting and link checks when docs/knowledge sources change (logs, docs, or README updates).
