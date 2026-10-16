---
title: Digital Accessibility
type: form
description: |-
  I'd like to share some information with you for a survey on digital accessibility.

  Your answers stay anonymous and are used only to illustrate a demo process.

form:
  - title: First, tell us about yourself
    questions:
      - label: Your Name
        name: name
        type: text
        placeholder: First Name Last Name
        help: "(You can answer anonymously: leave this field empty)"
      - label: Your sector, if applicable
        name: sector
        type: text
        placeholder: Sector name
        help: "(Give the name of the sector)"
      - label: What position do you hold?
        name: jobtitle
        type: text
        placeholder: Job title
      - label: Your areas of activity
        name: countries
        type: text
        placeholder: City, region, country
        help: "(Enter places separated by commas)"
  - title: The challenges of digital accessibility
    questions:
      - label: How much do you know about digital accessibility?
        name: estimated-knowledge-accessibility
        type: radio
        help: "(e.g. Taking the various disabilities into account in your activities, knowledge of the laws that apply in your context, impacts on beneficiaries...)"
        element:
          - label: none
          - label: reduced
          - label: medium
          - label: important
          - label: total
      - label: In your opinion, how do you take digital accessibility into account in your projects?
        name: estimated-action-accessibility
        type: radio
        help: "(e.g. A process is in place for writing, designing or checking compliance)"
        element:
          - label: none
          - label: reduced
          - label: medium
          - label: important
          - label: total
      - label: Is digital accessibility an issue for your current sector or activities?
        name: mission-issue-present
        type: radio
        help: "(e.g. Requests on the subject, legal constraints...)"
        element:
          - label: "Oui"
          - label: "Non"
      - label: Will digital accessibility be a major issue in your future activities?
        name: mission-issue-futur
        type: radio
        help: "(e.g. Donor requirements for offers)"
        element:
          - label: "Oui"
          - label: "Non"
  - title: Digital experiences (quick personal feedback)
    questions:
      - label: If I say digital, what is the first word that comes to mind?
        name: first-word
        type: text
        placeholder: 1 word
        help: "(Positive or negative)"
      - label: In your opinion, what is the biggest obstacle to starting a digital accessibility process?
        name: first-block
        type: text
        placeholder: Administration, knowledge, large platforms
        help: "(Internal, external, human, material...)"
      - label: In your opinion, what action should be taken to start addressing digital inclusion?
        name: first-win
        type: textarea
        placeholder: Train, bring stakeholders together...
        help: "(The essential first step)"
      - label: Of these 3 actions, which do you think is the most fundamental internally?
        name: idea-internal
        type: radio
        element:
          - label: Internal culture
          - label: Training
          - label: Compliance
        help: "(For you or your team)"
      - label: Of these 3 actions, which do you think is the most fundamental externally?
        name: idea-external
        type: radio
        element:
          - label: Internal culture
          - label: Training
          - label: Compliance
        help: "(For your beneficiaries or partners)"
---
