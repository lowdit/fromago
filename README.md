# Fromago, ça donne faim ?

Vous rêvez de générer un formulaire d'enquête mais sans passer par de grandes plateformes ? Vous rêvez de récupérer les résultats dans un répertoire de contenu, qui va vous permettre de mettre à jour votre rapport ?

## Installation:

### Configure

**1.** Add the `{owner}/{repo}` value of the target repo (It can be a different repo).

Note: possible to define a target repo from the main `hugo.toml` files, or directly in a form page.

```
[params]
  targetrepo = "lowdit/fromago/"
```

**2.** Install Plugin on your git repo (on Github)

 * Form this page https://github.com/apps/public-action-trigger. Install the plugin on the target repo.

**3.** Grant Permission for Workflow

 * In your Github project, go to `Settings > Actions > General`. Scroll down to Workflow permissions.
 * `Read and write permissions`
 * `Allow GitHub Actions to create and approve pull requests`

## Launch

It's possible to store the form files in the same repo as the publishing website.

 1. Create another root folder called : `form`
 2. Add all your form files
 3. Launch a build command line as : `hugo serve --gc --contentDir "form"`

> **Thème.** Fromago **requiert Minigo** (son `baseof.html` appelle les partials
> `lowdit/design-system.html`, `lowdit/logo.html`, …). La commande historique
> `--theme "fromago"` **échoue**. Déclarez les deux thèmes, minigo en premier :
>
> ```toml
> theme = ["minigo", "fromago"]
> ```
>
> L'accueil et les listes sont alors rendus par Minigo (profil `inquiry`, cf.
> `[params.lowdit] siteProfile = "inquiry"` / `view = "inquiry"`) ; Fromago
> n'apporte que les vues de formulaire.

## Deux sites

| Site | Contenu | Rôle |
|------|---------|------|
| **Formulaires** | `--contentDir "form"` | sert les questionnaires (public) |
| **Rapport** | `content/` | reçoit les réponses, publie l'analyse |

Une enquête = un dossier de contenu avec `type: form` (ex. `content/enquete/_index.md`).
Le formulaire est rendu par `layouts/form/*` (`_partials/form/main.html`).

## Flux des réponses (automatisation)

À la soumission, le navigateur appelle **public-action-trigger**
(`https://publicactiontrigger.azurewebsites.net/api/dispatches/<targetrepo>`), ce
qui déclenche le workflow `.github/workflows/interviews.yml` (`repository_dispatch`
de type `interview`). Le workflow :

1. valide `slugpath` et `slugname` (anti-injection / anti-traversée) ;
2. écrit `content/interviews/<slugpath>/<slugname>-<date>.md` (front matter JSON) ;
3. ouvre une **Pull Request** à valider (branche `content` du site de rapport) ;
4. la fusion déclenche le déploiement du site de rapport.

> Sécurité : l'entrée étant **publique**, aucun champ du payload n'est interpolé
> directement dans un `run:` — tout passe par des variables d'environnement
> validées.

## Improvement

Rédiger un Readme potable

Insérer une options de formulaire à étape 
: https://css-tricks.com/how-to-create-multi-step-forms-with-vanilla-javascript-and-css/

Form Automation Tips for Happier User and Clients
: css-tricks.com/form-automation-tips-for-happier-user-and-clients/


