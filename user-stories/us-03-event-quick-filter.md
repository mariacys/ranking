# User Story 3: Event Quick Filter

**AS A** user with a selected event

**I AM ABLE TO** use a quick filter for the event status and tags in Ranking

**SO I** can easily find articles based on their status within the selected event

---

## Figma design
[RANKCOMDA-16857 | Gestión de eventos](https://www.figma.com/design/Wa9pAKyRg3A1kLQOOBdnoC/branch/nTypHVTE5KenwQaAD3klXX/Ranking-%7C-Product-card---grid?node-id=5441-26137&t=fXsolz03rQbbxKPn-0)

## AppInsights metric
*To be defined*

## Snapshot testing
*To be defined*

## Feature Flag
The feature flag for all the Event Management Functionality

## Affect Highlights
YES - use of this Quick Filter

## Affect Sales
*To be defined*

---

## Context

During the preparation of a commercial event, articles displayed in Ranking can have different event statuses depending on the user role and the stage of the event workflow.

A buyer selects which of their items are candidates for a specific event, first creating a draft list. Management reviews these candidates and can approve or reject them. Management can also include new candidates for the event.

- A buyer can see which of their own articles have candidate, approved, or rejected status (only see their own articles)
- A director can see which articles are candidate, which are approved, or rejected, of any buyer, but they cannot see which articles have draft status
- For a buyer, only their own articles can be considered eligible to be added as a candidate
- For a director, any article can be considered eligible to be added as a candidate
- A director can add new candidate articles, reject a candidate, approve a candidate, or remove an article from the event
- A buyer can only add new candidates

To help users identify and work with the relevant articles more efficiently, Ranking must provide a quick filter that allows them to filter the current article list by event status and event tags.

---

## Acceptance Criteria

```gherkin
Scenario: Display event quick filter when event is selected
  Given an executed ranking
  When the user selects an event using the Event Management icon
  Then a new quick filter for the event is displayed in the quick filters bar
  And the quick filter is always positioned in the last position

Scenario: Remove event quick filter when exiting event management
  Given the user has selected an event and the event quick filter is visible
  When the user selects the "Exit event management" option
  Then the event quick filter is removed from the quick filters bar

Scenario: Display main filter tabs - event name and "No event"
  Given the event quick filter is visible
  When the user opens the event quick filter
  Then two main tabs are displayed:
    - The event name (e.g., "Black Friday") - for articles included in the event
    - "No [event name]" (e.g., "No Black Friday") - for articles not included in the event
  And an "Accept" button is displayed below the tabs

Scenario: Show "More event options" when event tab is selected
  Given the event quick filter is open
  When the user clicks on the event tab (e.g., "Black Friday")
  Then a "More [event name] options" section is enabled
  And the user can click to expand it

Scenario: Display event statuses and tags in More options section
  Given the event quick filter is open
  And the user has selected the event tab
  And the user clicks on "More [event name] options"
  Then the system shows the statuses applicable to the user role:
    - For buyer: Candidatos (Candidates), Aprobados (Approved), Rechazados (Rejected)
    - For director: Candidatos (Candidates), Aprobados (Approved), Rechazados (Rejected)
  And only statuses and tags present in the articles currently displayed on screen are shown
  And the system shows the event tags present in the articles:
    - Sin tag (With no tag)
    - Exp. TF / PPSS (Exposición en tienda física - Expose in physical stores)
    - Prioritario (Priority)

Scenario: Filter articles not included in the event
  Given the event quick filter is open
  When the user selects the "No [event name]" tab (e.g., "No Black Friday")
  And the user clicks the "Accept" button
  Then only articles that do not have any event status are displayed
  And the filter respects all other quick filters already applied to the ranking

Scenario: Filter articles in event with any status and tag
  Given the event quick filter is open
  And the user has selected the event tab (e.g., "Black Friday")
  And the user has not expanded "More [event name] options" OR has expanded it but selected nothing
  When the user clicks the "Accept" button
  Then only articles that have an event status are displayed
  And articles are shown regardless of their specific status or tags within the event
  And the filter respects all other quick filters already applied to the ranking

Scenario: Filter articles by selected statuses only
  Given the event quick filter is open
  And the user has selected the event tab
  And the user has selected one or more statuses from the status section
  And the user has not selected any tags
  When the user clicks the "Accept" button
  Then only articles that have one of the selected statuses are displayed
  And articles are shown regardless of their tags within the event

Scenario: Filter articles by selected tags only
  Given the event quick filter is open
  And the user has selected the event tab
  And the user has not selected any statuses
  And the user has selected one or more tags from the tags section
  When the user clicks the "Accept" button
  Then only articles that have one of the selected tags are displayed
  And articles are shown regardless of their status within the event

Scenario: Filter articles by selected statuses AND tags
  Given the event quick filter is open
  And the user has selected the event tab
  And the user has selected one or more statuses from the status section
  And the user has selected one or more tags from the tags section
  When the user clicks the "Accept" button
  Then only articles that have one of the selected statuses AND one of the selected tags are displayed
  And all other quick filters already applied remain active

Scenario: Display "No articles" message when filter returns no results
  Given the event quick filter is open
  And the user has applied filters
  When the user clicks the "Accept" button and no articles match the filter conditions
  Then a "No articles" message is displayed

Scenario: Recalculate filter options when ranking changes
  Given a ranking with an event selected
  When the user applies new quick filter conditions OR executes a new ranking
  Then the values displayed for statuses and tags in the event quick filter are recalculated
  And only statuses and tags present in the updated article list are shown

Scenario: Disable event tab when no articles in event
  Given an executed ranking with an event selected
  When none of the articles in the ranking are associated with the selected event
  Then the event tab (e.g., "Black Friday") is disabled

Scenario: Disable "No event" tab when all articles in event
  Given an executed ranking with an event selected
  When all articles in the ranking are associated with the selected event
  Then the "No [event name]" tab is disabled

Scenario: Clear event quick filter
  Given an event is selected
  And the user has applied the event quick filter
  When the user clears the event quick filter by clicking the X icon
  Then the article list is restored according to the other active filters
  And the quick filter is reset to its default state

Scenario: Export to Excel with event quick filter applied
  Given a ranking with an event selected and an event quick filter applied
  When the user exports the ranking to Excel
  Then the Excel contains only the articles currently displayed on screen
  And the Filters Summary page includes a new section for the event (e.g., "Black Friday")
  And the section shows the applied filter condition

Scenario: Export to PDF with event quick filter applied
  Given a ranking with an event selected and an event quick filter applied
  When the user exports the ranking to PDF
  Then the PDF contains only the articles currently displayed on screen
  And the Filters Summary page includes a new section for the event (e.g., "Black Friday")
  And the section shows the applied filter condition
```
