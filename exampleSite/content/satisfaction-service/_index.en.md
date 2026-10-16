---
title: Online service satisfaction
type: form
description: |-
  Short survey after completing an online procedure (Fromago exampleSite).
  Estimated time: 3 minutes. Demo data only, and answers stay anonymous.

form:
  - title: Your procedure
    questions:
      - label: Which procedure did you complete?
        name: procedure
        type: text
        placeholder: e.g. certificate request, registration...
      - label: On which device did you complete this procedure?
        name: device
        type: radio
        element:
          - label: Computer
          - label: Phone
          - label: Tablet
      - label: Had you completed this procedure before?
        name: first-time
        type: radio
        element:
          - label: Oui
          - label: Non
  - title: Your experience
    questions:
      - label: Overall, this procedure was...
        name: rating
        type: radio
        element:
          - label: Very easy
          - label: Rather easy
          - label: Mixed
          - label: Difficult
      - label: Was the information provided clear?
        name: clarity
        type: radio
        element:
          - label: Very clear
          - label: Rather clear
          - label: Not very clear
          - label: Not clear at all
      - label: Did you easily find what you were looking for?
        name: findability
        type: radio
        element:
          - label: Oui
          - label: Non
      - label: What helped or blocked you?
        name: feedback
        type: textarea
        placeholder: A few sentences...
  - title: Follow-up and contact
    questions:
      - label: Did your request succeed?
        name: outcome
        type: radio
        element:
          - label: Yes, fully
          - label: Partially
          - label: No
      - label: What should be improved first?
        name: improvement
        type: text
        placeholder: One suggestion is enough
      - label: Your email address, if you agree to be contacted again
        name: email
        type: email
        placeholder: camille.martin@example.com
        help: "(Optional — used only to reply to you about this procedure)"
---
