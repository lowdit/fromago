# Fromago, ça donne faim ?

Vous rêvez de générer un formulaire d'enquête mais sans passer par de grandes plateformes ? Vous rêvez de récupérer les résultats dans un répertoire de contenu, qui va vous permettre de mettre à jour votre rapport ?

## Actions :

 1. Rédiger un Readme potable
 2. Insérer une options de formulaire à étape : https://css-tricks.com/how-to-create-multi-step-forms-with-vanilla-javascript-and-css/

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
 * `Allow GitHub Actions to create and approve pull requests`

## Launch

It's possible to store the form files in the same repo as the publishing website.

 1. Create onther root folder called : `form`
 2. Add all your form files
 3. Launch a build command line as : `hugo serve --gc --contentDir "form" --theme "fromago"`


