---
title: Usages numériques sur le terrain
type: form
description: |-
  Enquête de terrain auprès des habitant·es et des acteurs locaux sur leurs usages du numérique.

  Aucune donnée nominative n'est collectée : les réponses servent à illustrer une démarche de démonstration.

form:
  - title: Votre contexte
    questions:
      - label: Dans quel territoire vivez-vous ou intervenez-vous ?
        name: territory
        type: text
        placeholder: Ville, quartier, vallée...
      - label: Vous répondez en tant que...
        name: profile
        type: radio
        element:
          - label: Habitant·e
          - label: Association
          - label: Collectivité
          - label: Entreprise locale
          - label: Autre
      - label: Comment vous connectez-vous le plus souvent ?
        name: connection
        type: radio
        element:
          - label: Fibre ou câble
          - label: Réseau mobile
          - label: Lieu public partagé
          - label: Je ne me connecte pas
  - title: Vos usages au quotidien
    questions:
      - label: À quelle fréquence utilisez-vous des services en ligne (démarches, achats, informations) ?
        name: frequency
        type: radio
        element:
          - label: Tous les jours
          - label: Chaque semaine
          - label: De temps en temps
          - label: Jamais
      - label: Quel usage vous paraît le plus utile au quotidien ?
        name: main-use
        type: text
        placeholder: Ex. santé, transport, administration, formation
      - label: Quelles difficultés rencontrez-vous ?
        name: obstacles
        type: textarea
        placeholder: Connexion, matériel, accompagnement, langue, confiance...
      - label: Vous sentez-vous à l'aise avec les outils numériques ?
        name: confidence
        type: radio
        element:
          - label: Pas du tout
          - label: Un peu
          - label: Plutôt à l'aise
          - label: Très à l'aise
  - title: Vos attentes pour demain
    questions:
      - label: Quelle priorité faudrait-il financer en premier ?
        name: priority
        type: radio
        element:
          - label: Accès et connexion
          - label: Matériel
          - label: Accompagnement humain
          - label: Formation
      - label: Quelle amélioration souhaiteriez-vous sur votre territoire ?
        name: wish
        type: textarea
        placeholder: Décrivez librement...
      - label: Votre adresse mail, si vous acceptez d'être recontacté·e
        name: email
        type: email
        placeholder: camille.martin@exemple.fr
        help: "(Facultatif — utilisé uniquement dans le cadre de cette enquête)"
---
