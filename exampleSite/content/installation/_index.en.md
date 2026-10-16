---
title: Installation
description: Install Fromago locally, from a GitHub fork, or as a Hugo module — a ready multilingual site (fr / en).
layout: product
weight: 1
---

**Fromago** is the **survey** engine of the Lowdit ecosystem: accessible, static forms, reassuring copy, exports for analysis. This page walks through installation.

## Requirements

| Tool | Version | When |
| --- | --- | --- |
| [Hugo](https://gohugo.io/) (extended) | ≥ 0.128 | Always |
| [Go](https://go.dev/) | ≥ 1.21 | Only for Hugo modules |
| Git | — | Clone / fork |

## Quick start

```bash
git clone https://github.com/lowdit/fromago
cd fromago/exampleSite
hugo server
```

→ demo at <http://localhost:1313/fr/> (the site is **multilingual**: the root redirects to the default language).

## Straight from GitHub (fork — nothing to install)

1. **Fork** [`lowdit/fromago`](https://github.com/lowdit/fromago).
2. In the fork: **Settings → Pages → Source: GitHub Actions**.
3. The workflow builds `exampleSite/` and publishes the demo.
4. Your content goes in `exampleSite/content/**/_index.md` (add `.en.md` for English).

## Locally (cloned repo)

```bash
git clone https://github.com/lowdit/fromago
cd fromago/exampleSite
hugo server        # http://localhost:1313/fr/
hugo               # build into public/
```

## In your own site (Hugo module)

```toml
# hugo.toml
theme = ["minigo", "fromago"]

defaultContentLanguage = "fr"
defaultContentLanguageInSubdir = true

[params.lowdit]
  siteProfile = "inquiry"
  view = "inquiry"
```

## Multilingual — always mind the language prefix

The site lives under `/fr/` and `/en/`. Rules to follow:

- **Content**: suffix translations (`.en.md`) or use language folders.
- **Links**: let Hugo build URLs (`{{ .RelPermalink }}`); menu `url` values are prefixed via `relLangURL`.
- **Hand-written absolute paths**: always go through `relLangURL` / `relURL`.

## Forms: demo mode

An `exampleSite` must **not** leave submittable forms online.

```toml
[params.lowdit]
  formsDemo = true   # frozen fields + “demo” banner, nothing is sent
```

For a **closed** survey (no longer valid): `formclosed = true` in front matter → the questionnaire stays visible but inert, with the matching notice.

## Deployment (GitHub Pages)

- By default the workflow builds **`exampleSite/`** (`.github/hugo-site-dir`).
- For a root site: put `content/` + `hugo.toml` at the root and set `.` in `.github/hugo-site-dir`.

## Vues and engines

Vue **inquiry** (Fromago): trust, narrow measure, forms. See `lowdit-brand/brand/VUES-PREMIUM.md`.
