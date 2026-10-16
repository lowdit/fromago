---
title: Satisfaction du service en ligne
type: form
description: |-
  Enquête courte après une démarche en ligne (exampleSite Fromago).
  Durée estimée : 3 minutes. Les réponses alimentent une démo interne uniquement et restent anonymes.

form:
  - title: Votre démarche
    questions:
      - label: Quelle démarche avez-vous effectuée ?
        name: procedure
        type: text
        placeholder: Ex. demande d'acte, inscription...
      - label: Sur quel appareil avez-vous réalisé cette démarche ?
        name: device
        type: radio
        element:
          - label: Ordinateur
          - label: Téléphone
          - label: Tablette
      - label: Aviez-vous déjà réalisé cette démarche auparavant ?
        name: first-time
        type: radio
        element:
          - label: Oui
          - label: Non
  - title: Votre ressenti
    questions:
      - label: Globalement, cette démarche était...
        name: rating
        type: radio
        element:
          - label: Très facile
          - label: Plutôt facile
          - label: Mitigé
          - label: Difficile
      - label: Les informations fournies étaient-elles claires ?
        name: clarity
        type: radio
        element:
          - label: Très claires
          - label: Plutôt claires
          - label: Peu claires
          - label: Pas claires du tout
      - label: Avez-vous trouvé facilement ce que vous cherchiez ?
        name: findability
        type: radio
        element:
          - label: Oui
          - label: Non
      - label: Qu'est-ce qui vous a aidé ou bloqué ?
        name: feedback
        type: textarea
        placeholder: Décrivez en quelques phrases...
  - title: Suites et contact
    questions:
      - label: Votre demande a-t-elle abouti ?
        name: outcome
        type: radio
        element:
          - label: Oui, entièrement
          - label: Partiellement
          - label: Non
      - label: Que faudrait-il améliorer en priorité ?
        name: improvement
        type: text
        placeholder: Une seule proposition suffit
      - label: Votre adresse mail, si vous acceptez d'être recontacté·e
        name: email
        type: email
        placeholder: camille.martin@exemple.fr
        help: "(Facultatif — utilisé uniquement pour vous répondre sur cette démarche)"
---
