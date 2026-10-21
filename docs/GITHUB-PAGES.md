# GitHub Pages — Fromago

- **Démo publiée (org, vérifiée 2026-10-21)** : [`https://lowdit.github.io/fromago/fr/`](https://lowdit.github.io/fromago/fr/) (racine redirige vers `/fr/`)
- **Source Hugo** : `exampleSite/` (`.github/hugo-site-dir`)
- **Build** : `./scripts/hugo-pages-build.sh "https://lowdit.github.io/fromago/"` (CI : `.github/workflows/gh-pages.yml`, Hugo **0.167.0** extended)
- **Activation** : Settings → Pages → GitHub Actions

Config prod : `exampleSite/config/production/hugo.toml` (modules Fromago + Minigo).
