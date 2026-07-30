# User Story 4: Individual article status changes in event mode

**AS A** user with an authorized role (buyer or director)

**I AM ABLE TO** change the event status of individual articles

**SO I** can manage article statuses within the event

---

## Figma design
[RANKCOMDA-16857 | Gestión de eventos](https://www.figma.com/design/Wa9pAKyRg3A1kLQOOBdnoC/branch/nTypHVTE5KenwQaAD3klXX/Ranking-%7C-Product-card---grid?node-id=5413-162557&t=GN0se2ft63kVbprT-0)

## AppInsights metric
*To be defined*

## Snapshot testing
*To be defined*

## Feature Flag
The feature flag for all the Event Management Functionality + future flag for individual changes

## Affect Highlights
YES - use of the individual contextual menu for event status changes

## Affect Sales
*To be defined*

---

## Context

When a user has selected an event in Ranking, users can change the status of individual articles without bulk selection. This is achieved through a context menu (3 dots icon) on each article card, which displays available actions based on the user's role and the article's current event status.

The available actions vary by role and article state:
- A buyer can only propose their own articles (and only those without an event status label)
- A director can approve, reject, or remove articles from the event, with available actions depending on the article's current state

---

## Acceptance Criteria

```gherkin
Scenario: Display context menu when no articles are selected
  Given an event is selected
  When the user hovers over the 3 dots icon on an article card
  Then the context menu is displayed
  And the menu contains the existing navigation options:
    - Análisis Históricos
    - Página Web Oficial
  And only for editable items (depending on the user's role and article status) a new section "Gestión de evento" (Event Management) is displayed below the navigation options

Scenario: Context menu shows only navigation options when no event is selected
  Given no event is selected
  When the user hovers over the 3 dots icon on an article card
  Then the context menu is displayed
  And the menu contains only the existing navigation options:
    - Análisis Históricos
    - Página Web Oficial
  And the "Gestión de evento" section is not displayed

Scenario: Show actions for buyer
  Given a buyer has selected an event
  And an article belongs to the buyer
  And the article does not have an event status label
  When the user opens the context menu
  Then the "Gestión de evento" section displays only the option:
    - Proponer artículo (Propose article)

Scenario: Hide event management for buyer articles with status or not owned
  Given a buyer has selected an event
  When the user opens the context menu on an article
  Then if the article does not belong to the buyer OR the article has an event status label
  Then the "Gestión de evento" section is not displayed
  And only the navigation options are shown

Scenario: Show event management options for director - article without event status
  Given a director has selected an event
  And an article does not have an event status label
  When the user opens the context menu
  Then the "Gestión de evento" section displays only the option:
    - Proponer artículo (Propose article)

Scenario: Show event management options for director - Candidato status
  Given a director has selected an event
  And an article has the "Candidato" status label
  When the user opens the context menu
  Then the "Gestión de evento" section displays the options:
    - Aprobar (Approve)
    - Rechazar (Reject)
    - Eliminar (Remove from event)

Scenario: Show event management options for director - Rechazado status
  Given a director has selected an event
  And an article has the "Rechazado" status label
  When the user opens the context menu
  Then the "Gestión de evento" section displays the options:
    - Aprobar (Approve)
    - Eliminar (Remove from event)

Scenario: Show event management options for director - Aprobado status
  Given a director has selected an event
  And an article has the "Aprobado" status label
  When the user opens the context menu
  Then the "Gestión de evento" section displays the options:
    - Rechazar (Reject)
    - Eliminar (Remove from event)

Scenario: Execute 'Aprobar', 'Rechazar', 'Eliminar' actions on individual article
  Given the context menu is open
  And the user can see available event management options
  When the user clicks on one of these actions: 'Aprobar', 'Rechazar', 'Eliminar'
  Then the action is executed immediately
  And the context menu closes after the action
  And a confirmation message is displayed: "El estado del artículo [article name] ha sido cambiado"
  And the article status is updated in the ranking in real time
  And the article shows its new status label in the ranking
  Or the label is removed if the action is 'Eliminar'

Scenario: Execute 'Proponer artículo' action on individual article
  Given the context menu is open
  And the user can see the 'Proponer artículo' action
  When the user clicks on the 'Proponer artículo' action
  Then -----PENDING TO DEFINE
```

---

## Notes

- The action "Proponer artículo" execution flow is pending definition
- The context menu behavior ensures that individual actions are only available when no bulk selection is active (see US-06)
