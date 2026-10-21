---
title: Installation
description: Installer Fromago en local, depuis un fork GitHub, ou comme module Hugo — site multilingue prêt (fr / en).
layout: product
weight: 1
---

**Fromago** est le moteur d'**enquêtes** de l'écosystème Lowdit : formulaires accessibles et statiques, copy rassurante, exports pour l'analyse. Cette page couvre l'installation pas à pas.

## Prérequis

| Outil | Version | Quand |
| --- | --- | --- |
| [Hugo](https://gohugo.io/) (extended) | ≥ 0.128 | Toujours |
| [Go](https://go.dev/) | ≥ 1.21 | Seulement pour les modules Hugo |
| Git | — | Clone / fork |

## Démarrage rapide

```bash
git clone https://github.com/lowdit/fromago
cd fromago/exampleSite
hugo server
```

→ démo sur <http://localhost:1313/fr/> (le site est **multilingue** : la racine redirige vers la langue par défaut).

## Directement depuis GitHub (fork — rien à installer)

1. **Forker** [`lowdit/fromago`](https://github.com/lowdit/fromago).
2. Dans le fork : **Settings → Pages → Source : GitHub Actions**.
3. Le workflow construit `exampleSite/` et publie la démo.
4. Votre contenu : `exampleSite/content/**/_index.md` (+ `.en.md` pour l'anglais).

## En local (dépôt cloné)

```bash
git clone https://github.com/lowdit/fromago
cd fromago/exampleSite
hugo server        # http://localhost:1313/fr/
hugo               # build dans public/
```

## Dans votre propre site (module Hugo)

```toml
# hugo.toml
theme = ["minigo", "fromago"]

defaultContentLanguage = "fr"
defaultContentLanguageInSubdir = true

[params.lowdit]
  siteProfile = "inquiry"
  view = "inquiry"
```

## Multilingue — toujours penser au préfixe de langue

Le site vit sous `/fr/` et `/en/`. Règles à respecter :

- **Contenu** : suffixer les traductions (`.en.md`) ou utiliser des dossiers de langue.
- **Liens** : laisser Hugo générer les URLs (`{{ .RelPermalink }}`) ; côté menu, `url` est automatiquement préfixé par `relLangURL`.
- **Chemins absolus écrits à la main** : toujours passer par `relLangURL` / `relURL`, jamais `/ma-page/`.
- **Pas de menu principal** ici : l'accueil sert de sommaire (cartes de sections), toutes construites avec les URLs de langue.

## Structure d'un site

```
.
├── hugo.toml
├── content/
│   ├── _index.md          # accueil fr (/fr/)
│   ├── _index.en.md       # accueil en
│   ├── installation/
│   ├── digitala11y/_index.md
│   └── …                  # une enquête par dossier (type: form)
└── assets/css/site-overrides.css
```

## Formulaires : mode démonstration

Un `exampleSite` ne doit **pas** laisser de formulaires soumettables en ligne.

```toml
[params.lowdit]
  formsDemo = true   # champs figés + bandeau « démonstration », aucun envoi
```

Pour une enquête **clôturée** (plus valide) : `formclosed = true` dans le front matter → le questionnaire reste affiché mais inerte, avec la mention correspondante.

## Configuration (`params.lowdit`)

| Clé | Défaut | Rôle |
| --- | --- | --- |
| `view` | `inquiry` | Posture de la vue (confiance, formulaires) |
| `siteProfile` | `inquiry` | Accueil enquêtes |
| `formsDemo` | `false` | Figer les formulaires (démo) |
| `logo` / `faviconDir` | — | Marque du site |

## Déploiement GitHub Pages

**Démo org (live)** : [`https://lowdit.github.io/fromago/fr/`](https://lowdit.github.io/fromago/fr/) — détail dans `docs/GITHUB-PAGES.md`.

- Par défaut, le workflow construit **`exampleSite/`** (`.github/hugo-site-dir`).
- Pour un site à la racine : `content/` + `hugo.toml` à la racine et `.` dans `.github/hugo-site-dir`.

## Dépannage

| Symptôme | Cause | Correction |
| --- | --- | --- |
| Page 404 depuis le menu | URL sans préfixe de langue | laisser `relLangURL` construire le lien |
| Formulaire qui envoie | démo désactivée | `formsDemo = true` |
| `/` renvoie une redirection | `defaultContentLanguageInSubdir` | normal : viser `/fr/` ou `/en/` |

## Vues et moteurs

Vue **inquiry** (Fromago) : confiance, mesure étroite, formulaires. Voir `lowdit-brand/brand/VUES-PREMIUM.md`.
