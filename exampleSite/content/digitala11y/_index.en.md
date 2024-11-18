---
title: Digital Accessibility
type: form
description: |-
  I'd like to share some information with you for a survey on digital accessibility. 


form:
  - title: First, tell us about yourself
    questions:
      - label: Your Name
        name: name
        type: text
        placeholder: First Name Last Name
        help: "(You can answer anonymously: do not put anything in this field)"
      - label: Your sector, if applicable
        name: sector
        type: text
        placeholder: Sector name
        help: "(Give the name of the sector)"
      - label: What position do you hold?
        name: jobtitle
        type: text
        placeholder: Job title
      - label: Your countries of activity
        name: countries
        type: text
        placeholder: Uganda, Niger, Mali
        help: "(Enter country names separated by commas)"
  - title: The challenges of digital accessibility
    questions:
      - label: How much do you know about digital accessibility?
        name: estimated-knowledge-accessibility
        type: radio
        help: (e.g. Taking into account the various disabilities in your activities, knowledge of the laws that apply in your context, impacts on beneficiaries...)
        element:
          - label: none
          - label: reduced
          - label: medium
          - label: important
          - label: total
      - label: In your opinion, how do you take digital accessibility into account in your projects?
        name: estimated-action-accessibility
        type: radio
        element:
          - label: none
          - label: reduced
          - label: medium
          - label: large
          - label: total
        help: (e.g. A process is in place for writing, designing or checking compliance)
      - label: Is digital accessibility an issue for your current sector or activities?
        name: mission-issue-present
        type: radio
        element:
          - label: "oui"
          - label: "non"
        help: (Ex. Requests on the subject, legal constraints,...)
      - label: Will digital accessibility be a major issue in your future activities?
        name: mission-issue-futur
        type: radio
        element:
          - label: "oui"
          - label: "non"
        help: (e.g. Obligation of donors for offers)
  - title: Digital Experiences (Quick personal feedback)
    questions:
      - label: If I say digital, what's the first word that comes to mind?
        name: first-word
        type: text
        placeholder: 1 word
        help: (Positive or negative)
      - label: In your opinion, what is the biggest obstacle to implementing digital accessibility?
        name: first-block
        type: text
        placeholder: Administration, knowledge, GAFAM
        help: (Internal, external, human, material...)
      - label: What action do you think needs to be taken to start taking digital inclusion issues into account?
        name: first-win
        type: text
        placeholder: Train, bring together stakeholders
        help: (The essential first step)
      - label: Of these 3 actions, which do you think is the most fundamental internally?
        name: idea-internal
        type: radio
        placeholder: Internal culture, Training, Compliance
        element:
          - label: Internal culture
          - label: Training
          - label: Compliance
        help: (For you or your team)
      - label: Of these 3 actions, which do you think is the most fundamental externally?
        name: idea-external
        type: radio
        placeholder: Internal culture, Training, Compliance
        element:
          - label: Internal culture
          - label: Training
          - label: Compliance
        help: (For your beneficiaries or partners)
---
