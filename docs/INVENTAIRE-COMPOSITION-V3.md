# Inventaire — vague 3 composition CSS (Fromago)

> **Date :** 2026-11-13 · Réf. [`MIGRATION-UNIVERS-CSS.md`](../../lowdit-brand/docs/MIGRATION-UNIVERS-CSS.md).

## Layouts écran (exampleSite minigo+fromago)

| Fichier | Compositions | Métier |
| --- | --- | --- |
| `_partials/form/main.html` | `.wrapper[data-width=wide]`, `.stack`, `.doc-body` | `single-container`, champs legacy |
| `contact/single.html` | `.wrapper[data-width=reading]` | formulaire contact démo |
| `_default/single.html` | `.wrapper` + `.doc-body` (héritage Overgo) | `section-header`, `grid` legacy |

## Hors scope

- `fromago` baseof Overgo (`fg-wrapper`, utilitaires) : migration partielle — exampleSite passe surtout par minigo + layouts form/contact.
- Vague 4 : formulaires `form-radio`, `btn` → contrat `lowdit-field` / `minigo-btn`.

## Vérifications

```bash
hs test fromago
```
