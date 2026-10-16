---
title: Digital practices on the ground
type: form
description: |-
  A field survey among local residents and stakeholders about their digital practices.

  No personal data is collected: answers are used only to illustrate a demo process.

form:
  - title: Your context
    questions:
      - label: In which area do you live or work?
        name: territory
        type: text
        placeholder: City, neighbourhood, valley...
      - label: You are answering as...
        name: profile
        type: radio
        element:
          - label: Resident
          - label: Association
          - label: Local authority
          - label: Local business
          - label: Other
      - label: How do you connect most often?
        name: connection
        type: radio
        element:
          - label: Fibre or cable
          - label: Mobile network
          - label: Shared public place
          - label: I do not connect
  - title: Your everyday practices
    questions:
      - label: How often do you use online services (procedures, shopping, information)?
        name: frequency
        type: radio
        element:
          - label: Every day
          - label: Every week
          - label: From time to time
          - label: Never
      - label: Which use seems most useful in daily life?
        name: main-use
        type: text
        placeholder: e.g. health, transport, administration, training
      - label: What difficulties do you face?
        name: obstacles
        type: textarea
        placeholder: Connection, equipment, support, language, trust...
      - label: Do you feel comfortable with digital tools?
        name: confidence
        type: radio
        element:
          - label: Not at all
          - label: A little
          - label: Fairly comfortable
          - label: Very comfortable
  - title: Your expectations for tomorrow
    questions:
      - label: Which priority should be funded first?
        name: priority
        type: radio
        element:
          - label: Access and connection
          - label: Equipment
          - label: Human support
          - label: Training
      - label: What improvement would you like in your area?
        name: wish
        type: textarea
        placeholder: Describe freely...
      - label: Your email address, if you agree to be contacted again
        name: email
        type: email
        placeholder: camille.martin@example.com
        help: "(Optional — used only within this survey)"
---
