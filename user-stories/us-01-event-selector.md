# User Story 1: Event selector

**AS A** user with an authorized role (buyer or director)

**I AM ABLE TO** see an event selector in Ranking when there is at least one open event available for my role

**SO I** can access and work on the relevant commercial event

---

## Figma design
[RANKCOMDA-16857 | Gestión de eventos](https://www.figma.com/design/Wa9pAKyRg3A1kLQOOBdnoC/branch/nTypHVTE5KenwQaAD3klXX/Ranking-%7C-Product-card---grid?node-id=5026-1175&p=f&t=quaKCC44iYa7rifo-0)

## AppInsights metric
Selected event by role and brand

## Snapshot testing
*To be defined*

## Feature Flag
YES - display or not the Event Management icon by role and brand

## Affect Highlights
YES - Event Management functionality

## Affect Sales
*To be defined*

---

## Context

Throughout the year, Inditex organizes specific, time-limited events where selected items are offered for sale. Examples include Black Friday and Singles' Day. These events are considered "open" when the items to be included can still be managed, or "closed" when they are locked.

Certain Ranking users want to view which events are currently open and select a specific event in order to perform actions on the associated items.

---

## Acceptance Criteria

### Scenario: Show Event Management icon

**Given:**
- A Ranking user
- The user is an authorized user to manage events
- At that moment there is at least one open event available for the user
- The executed ranking meets these conditions:
  - The Brand of the Ranking is not Tempe (The One - Event Management application does not consider Tempe as a brand)
  - The ranking is based on at least one active campaign (active campaign for the sale)
  - The Ranking is grouped by Comercial criteria, and not separated by campaign
  - The ranking is a MoQuCo view Ranking
  - The Ranking can be a Today or UY Ranking, a Ranking of a period, a Sales Channel Ranking, a custom Ranking (XS or XL), a Sales ranking, or a Total or by Invoice Ranking, from any brand, multisection or multiproduct or both

**When:**
- These conditions are met

**Then:**
- The Event Management Icon is displayed

**Note:** If any of these conditions are not met, the Management Icon is not displayed.

---

### Scenario: Show onboarding message on first visibility

**Given:**
- A Ranking user
- The Event Management Icon is visible for the first time to this user

**When:**
- The icon becomes visible

**Then:**
- An onboarding message is displayed (only first time, not on subsequent visits)

---

### Scenario: Event Management icon actions - Hover

**Given:**
- The Event Management Icon is displayed

**When:**
- The user hovers over the icon

**Then:**
- A tooltip is displayed with the text "Event management"

---

### Scenario: Event Management icon actions - Click (no event selected)

**Given:**
- The Event Management Icon is displayed
- No event is currently selected

**When:**
- The user clicks on the icon

**Then:**
- An event list is displayed with the opened events available for the user at that moment

---

### Scenario: Event Management icon actions - Click (event already selected)

**Given:**
- The Event Management Icon is displayed
- An event is already selected

**When:**
- The user clicks on the icon

**Then:**
- The event list is displayed with the currently selected event highlighted
- An option "Exit event management" is also displayed at the bottom of the list

---

### Scenario: Event Selector visual state - No event selected

**Given:**
- The Event Management Icon is displayed
- No event is selected

**When:**
- Viewing the icon

**Then:**
- The Event Selector icon is displayed in default state
- No blue dot is visible
- On hover: tooltip "Event management" is shown

---

### Scenario: Event Selector visual state - Event selected

**Given:**
- The Event Management Icon is displayed
- An event is selected

**When:**
- Viewing the icon

**Then:**
- The Event Selector icon displays a blue dot indicator
- The icon remains visible in the header of the Ranking
- On hover: tooltip displays the selected event name

---

### Scenario: Show Event list

**Given:**
- The Event Management Icon is displayed
- The user clicks on the icon

**When:**
- The event list is opened

**Then:**
- A list with the open events available to the current user is displayed

---

### Scenario: Select an event from the list

**Given:**
- The event list is displayed

**When:**
- The user clicks on an event from the list

**Then:**
- Multiselecting is not allowed (only one event at a time)
- The previous selected event is deselected (if there was a previous different selection)
- The event is selected
- The event list closes
- A visual indicator (blue dot) appears next to the Event Selector icon
- If the executed ranking has a view mode 'photo' or 'mosaic', the view mode switches to card view
- The view mode selector of the ranking toolbar is disabled (Temporary fix to ensure US consistency. In future US RANKCOMDA-16899, the toolbar will be redesigned)
- The event will remain selected until the user decides to exit the event or runs a Ranking that does not meet the conditions

---

### Scenario: Exit event management

**Given:**
- The event list is displayed
- An event is currently selected

**When:**
- The user clicks on the "Exit event management" option of the event list

**Then:**
- The event is deselected immediately
- The blue dot disappears from the Event Selector icon
- The event list closes

---

### Scenario: Close event list by clicking outside

**Given:**
- The event list is displayed

**When:**
- The user clicks outside the event list

**Then:**
- The event list closes

---

## Notes

- The Event Management icon visibility depends on user role, brand, and campaign configuration
- Only one event can be selected at a time
- The event remains selected across multiple ranking operations until explicitly exited
- The onboarding message appears only on the user's first encounter with the icon
