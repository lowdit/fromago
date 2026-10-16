---
tags:
  - "revue"
  - "fromago"
---
# Revue — Fromago : enquêtes, workflow PR, alignement lowtech

> Revue du **2026-10-16** (Hugo 0.167). Périmètre : `fromago` (thème enquêtes), le
> workflow `interviews.yml`, la mécanique « form → public-action-trigger → PR →
> content », et l'alignement avec les autres modules Lowdit (`repogo`, `resugo`,
> `sligo`). Faits **vérifiés par lecture du code et builds** (fromago seul, puis
> `["minigo","fromago"]`).

---

## 0. État réel : Fromago est déjà un module Lowdit (minigo requis)

Le socle de fromago **dépend de minigo** :

```
fromago/layouts/_default/baseof.html:6   {{ partial "lowdit/design-system.html" . }}
                                         + lowdit/favicon.html, diagrams.html,
                                           view-body-class.html, view-styles.html, logo.html
```

Conséquence **vérifiée** : `hugo --theme fromago` **échoue** —

```
ERROR … content/partnership/_index.md failed: baseof.html:6:5:
  partial "lowdit/design-system.html" not found
```

Donc :
- **`--theme "fromago"` (README, §Installation) est obsolète / cassé.** Il faut
  `theme = ["minigo","fromago"]`.
- Le `index.html` / `_default/list.html` de fromago (listes de debug
  `hugo.IsServer`) sont **dormants** : avec `["minigo","fromago"]`, le **1er thème
  est prioritaire**, donc `minigo/layouts/index.html` gagne pour l'accueil. Ces
  templates n'ont de sens **que** si fromago passe devant (`["fromago","minigo"]`)
  — configuration qui, elle, casse minigo ailleurs.

> Modèle à deux sites (rappel) : site **formulaires** (`--contentDir form`) qui
> sert les questionnaires, et site **rapport** (`content/`) qui reçoit les
> réponses. Les deux doivent tourner avec `["minigo","fromago"]`.

## 1. Accueil « affiche toutes les pages »

Deux sources possibles, selon le montage :

1. **`fromago/layouts/index.html`** (lignes 9-31) : sous `hugo.IsServer`, il
   liste `{{ range .Pages }}` = **toutes les pages de premier niveau**, sans
   filtrer les `sitemapExclude`. En prod il n'affiche que `i18n "home-message"`
   (« …Les formulaires ne sont pas accessibles depuis cette page. »). C'est un
   **template de debug**, masqué en prod — mais **dormant** sous minigo.
2. **`minigo/layouts/index.html`** : pour `siteProfile = "inquiry"` (ni
   `cv`/`publisher`/`presentations`/`library`/`hub`), rend le titre/contenu puis
   **`site.Sections`** (grille de cartes). En exempleSite cela inclut
   `installation`, `digitala11y`, `partnership`, `satisfaction-service`,
   `usages-terrain`, **`styleguide`**, `categories`, `tags`.

Le masquage en prod **est volontaire** (`home-message`). L'« accueil = toutes les
pages » vient donc soit du **template de debug** (si fromago passe devant), soit
de la **grille de sections** de minigo (cas exempleSite/`["minigo","fromago"]`).

## 2. « Installation » cassée

`exampleSite/content/installation/_index.md` déclare **`layout: product`**.

- `product` n'existe, dans l'écosystème, que via **minigo** :
  `minigo/layouts/section/installation.html` → `_partials/product/layout.html`
  (et `_default/single.product.html` pour les **pages simples**).
- **Fromago ne fournit aucun template `product`.** Sans le `section/installation`
  de minigo, `layout: product` retombe sur `_default/list.html` → dev : liste de
  toutes les pages ; prod : « Vous n'avez pas accès à la liste des questionnaires ».
- Vérifié : en `["minigo","fromago"]`, `/fr/installation/` rend bien la page
  produit (h1 « Installation », pas d'accès refusé). Le bug n'apparaît **que si
  minigo ne couvre pas `layout: product`**.

→ Correctif appliqué : template `product` côté fromago (§6), qui délègue à
minigo s'il est présent, sinon rend un gabarit autonome.

## 3. Modèle de données des réponses

- Clé = `slugpath = anchorize(lower .Page.Title)` (le **titre** de l'enquête).
- Fichier = `content/interviews/<slugpath>/<slugname>-<date>.md`.

Conséquences :
- **N réponses par enquête** : oui (plusieurs fichiers dans le dossier).
- **N enquêtes par site** : oui (une page `type: form` chacune).
- **Pas de dimension « organisme »** : la clé est le **titre**. Renommer une
  enquête **orpheline** les réponses ; deux titres identiques **fusionnent** le
  dossier. Pour « plusieurs enquêtes par organisme », ajouter une clé explicite
  (`slug: "<org>/<enquete>"`) et clé = **section**, pas titre.

## 4. Revue de `interviews.yml`

Deux copies **divergentes** :
- `fromago/.github/workflows/interviews.yml` — `base: master`, `yq` + `awk` de re-quoting.
- `fromago/exampleSite/.github/workflows/interviews.yml` — `base: content`, JSON inline.

### Élevé — sécurité (entrée **publique** via `repository_dispatch`)
1. **Injection shell** : `${{ github.event.client_payload.data.* }}` interpolé
   dans les blocs `run:` (payload d'un endpoint public) → exécution de commande.
2. **Path traversal** via **`slugname`** : utilisé tel quel dans le nom de
   fichier, **sans validation** (seul `slugpath` est contrôlé).
3. `echo '${{ toJson(...) }}'` : une apostrophe dans une valeur **casse le
   quoting** → injection.
4. **Aucun `permissions:`** → création de PR impossible (défaut read-only) ou trop
   large.

### Moyen — fiabilité
5. `awk` de re-quoting fragile (`-F': '` casse sur les valeurs contenant `: `) et
   inutile (`yq` produit déjà du YAML valide).
6. `body:` référence `steps.preprocess.outputs.interviews` **jamais défini**.
7. `base: master` (racine) vs `base: content` (exampleSite) → divergence.
8. `date=$(date +%s)` (epoch) vs `data.date` (YYYY-MM-DD) → noms incohérents.
9. `actions/checkout@v3` obsolète.
10. Écrasement silencieux si même `slugname`+`date`.

## 5. Alignement « logique lowtech » — verdict

| Critère | repogo | resugo | sligo | **fromago** |
|---|---|---|---|---|
| `theme = ["minigo","<module>"]` (minigo 1er) | `["repogo","minigo"]` | ✅ | ✅ | ✅ |
| `params.lowdit.siteProfile`/`view` | `publisher` | `cv-vitrine` | `deck-studio` | `inquiry` ✅ |
| `config/production` (modules GitHub) | ✅ | ✅ | ✅ | ✅ |
| dépend d'un `index`/`list` propre au thème | non | non | non | **oui (debug, dormant)** |
| dépend de partials minigo dans `baseof` | oui | oui | oui | **oui** ✅ |
| docs du module | `VISION`, `PDF`, … | `CHALLENGE-EXPORT-ATS` | `ARCHITECTURE`, `AI-INTENT` | **`MINIGO-STACK` (mince)** |

**Verdict** : fromago est **déjà dans la logique lowtech** par sa config
(`view: inquiry`, `config/production`, `baseof` minigo) et ses partials de
formulaire. Ce qui **décroche**, c'est l'**héritage du thème autonome** :

- `layouts/index.html` + `layouts/_default/list.html` : restes de debug
  (« toutes les pages ») issus de l'ancien thème standalone — désormais sans
  objet puisque minigo est obligatoire.
- `layout: product` non couvert côté fromago.
- README qui **prescrit une commande cassée** (`--theme fromago`).
- Docs du module plus pauvres que celles de ses pairs.

## 6. Correctifs appliqués (2026-10-16)

| # | Point | Correctif | Fichier(s) |
|---|---|---|---|
| 1 | `layout: product` non couvert | nouveau template **section** `product` : délègue à `partials/product/layout.html` (minigo) si présent, sinon rendu local (`h1` + contenu + sommaire des sous-pages) | `fromago/layouts/_default/list.product.html` |
| 2 | Sommaire de debug de l'accueil | **supprimé** `layouts/index.html` et `layouts/_default/list.html` (listings `hugo.IsServer` « toutes les pages ») : l'accueil et les listes sont désormais gouvernés par **minigo** | `fromago/layouts/index.html`, `fromago/layouts/_default/list.html` (retirés) |
| 2b | Panneau **debug** dupliqué (fromago + sligo) | **centralisé dans minigo** : `_partials/debug/{debug,debugprint,debuglist,debuglist-element}.html` + assets (`css/debug.css`, `css/checka11y.css`, `js/debug.js`, `js/debug/*`) + include dans `baseof` (`HUGO_ENV=dev`). Version retenue : `debugprint.html` **corrigée** (`.Language.Locale` au lieu de `LanguageCode` déprécié). Retiré de fromago. | `minigo/layouts/_partials/debug/*`, `minigo/assets/…`, `minigo/layouts/_default/baseof.html` |
| 3 | Sécurité `interviews.yml` | payload via `env:` (aucune interpolation dans `run:`), validation stricte `slugpath`+`slugname`+`realpath`, `permissions:` explicites, suppression du `awk`, `body` corrigé, `checkout@v4`, `create-pull-request@v6`, date = `data.date` (fallback `%F`) | `.github/workflows/interviews.yml` + `exampleSite/.github/workflows/interviews.yml` |
| 4 | README — commande cassée | `--theme "fromago"` remplacé par `theme = ["minigo","fromago"]` + section « Deux sites » et « Workflow PR » | `fromago/README.md` |

## 7. Reste à décider (arbitrage humain)

- ~~Supprimer `layouts/index.html` / `_default/list.html`~~ → **fait** ;
  ~~centraliser le debug dans minigo~~ → **fait**.
- ~~Sligo : retirer le même doublon debug~~ → **fait** (partials + assets +
  include `baseof` retirés ; build dev/prod OK, debug servi par minigo). Seul
  reste un `debug` vestigial dans la classe `<body>` de son `baseof` mort.
- **`list.product.html`** (nouveau, dans fromago) : à **déplacer vers minigo**
  (comme le debug) si l'on veut une vue `product` générique partagée ?
- **Unifier** les deux copies de `interviews.yml` (une seule source) et fixer la
  branche cible (`content`).
- **Modèle de données** : ajouter `slug`/`org` (clé explicite) pour le
  multi-enquêtes par organisme.
- **Richesse documentaire** : aligner fromago sur ses pairs (`ARCHITECTURE.md`,
  `VISION.md`).
- Migrer les éventuels consommateurs encore en `--theme "fromago"`.
