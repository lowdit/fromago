# Changelog — fromago

Format : [Keep a Changelog](https://keepachangelog.com/fr/1.1.0/), versions
SemVer. Chaque entrée dit **quoi · où · migrer**. « Non publié » = ce que
reçoivent les sites qui suivent `main`. Politique :
`lowtech-dev-method/docs/TAGS-MODULES-HUGO.md`.

## Non publié

### Cassé

- **Retiré : `content/`** (`_index.md`, `404.md`, `offline.md`, `_redirects`). Hugo monte le contenu d'un
  thème chez chaque site qui l'importe : ces pages arrivaient chez tous les
  consommateurs (dont un `_redirects` « tout vers 404 »).
  Où : un site qui comptait sur l'accueil ou la page d'erreur du module.
  Migrer : écrire `content/_index.md` dans le site ; la page introuvable vient
  désormais du kit (`404.html`).
- **Retiré : restes de Higo jamais appelés** : `form/main copy`,
  `form/form-script`, `navigations/{tags,nav-translated,breadcrumb,paginator}`,
  `utils/isURL`, `_default/{list,single}.json`, `404.html`, et 37 feuilles CSS
  (`overgo/`, `base/`, `element/`, `object/` sauf `buttons` et `form`,
  `styles.css`, `fonts.css`, lightbox, night-owl).
  Où : un site qui les appelait par leur nom.
  Migrer : les copier dans le site ; la base CSS vient du kit (Overgo).
- **Retiré : `assets/js/`** (Frappe Charts, highlight, van11y, lightbox) : aucun gabarit ne les charge. 
  Où : un site qui faisait `resources.Get "js/…"` sur ces fichiers.
  Migrer : les copier dans `assets/js/` du site.
- **Retiré : shortcodes `gallery` et `section`** (restes de Higo, utilisés
  nulle part) et `simple-lightbox.min.js`.
  Où : un contenu qui écrit `{{< gallery >}}` ou `{{< section >}}`.
  Migrer : copier le shortcode dans le site (`layouts/_shortcodes/`).
- **Plus de copies de la marque dans fromago** (jetons, base, composants, vues,
  partials de coque) : elles sont servies par `lowdit-kit`.
  Où : un site qui charge fromago **sans** `lowdit-kit` ni minigo.
  Migrer : ajouter le kit en dernier dans la liste des thèmes,
  `theme = ["github.com/lowdit/fromago", "github.com/lowdit/lowdit-kit"]`
  (ou garder minigo, qui l'apporte).
- **Retiré** : `layouts/_default/baseof.html`, gabarit Overgo déjà masqué partout
  (minigo ou higo passent devant). La coque vient du gabarit de base de `lowdit-kit`.

- **Retiré** : `assets/js/mermaid.min.js`, copie : servi par `lowdit-kit`.

### Ajouté

- Modèle `inquiry` déclaré (`[params.lowdit.models.inquiry]`).
- Feuille du modèle `assets/css/views/inquiry.css`, venue de `lowdit-kit` (même
  chemin : transparent).
- `exampleSite` fonctionne sans minigo : `theme = ["github.com/lowdit/fromago", "github.com/lowdit/lowdit-kit"]`.

## v0.3.1

Dernière version distribuée avec des copies de la marque Brand. Historique antérieur : `git log`.
