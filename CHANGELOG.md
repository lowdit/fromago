# Changelog — fromago

Format : [Keep a Changelog](https://keepachangelog.com/fr/1.1.0/), versions
SemVer. Chaque entrée dit **quoi · où · migrer**. « Non publié » = ce que
reçoivent les sites qui suivent `main`. Politique :
`lowtech-dev-method/docs/TAGS-MODULES-HUGO.md`.

## Non publié

### Cassé

- **Plus de copies de la marque dans fromago** (jetons, base, composants, vues,
  partials de coque) : elles sont servies par `lowdit-kit`.
  Où : un site qui charge fromago **sans** `lowdit-kit` ni minigo.
  Migrer : ajouter le kit en dernier dans la liste des thèmes,
  `theme = ["github.com/lowdit/fromago", "github.com/lowdit/lowdit-kit"]`
  (ou garder minigo, qui l'apporte).
- **Retiré** : `layouts/_default/baseof.html`, gabarit Overgo déjà masqué partout
  (minigo ou higo passent devant). La coque vient du gabarit de base de `lowdit-kit`.

### Ajouté

- `exampleSite` fonctionne sans minigo : `theme = ["github.com/lowdit/fromago", "github.com/lowdit/lowdit-kit"]`.

## v0.3.1

Dernière version distribuée avec des copies de la marque Brand. Historique antérieur : `git log`.
