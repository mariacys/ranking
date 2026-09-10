# User Story 5: Price indicators in Advanced Search

**AS A** Ranking user

**I AM ABLE TO** filter the ranking using price indicators from Advanced Search

**SO I** can execute rankings focused on articles with the pricing situations I need to analyze

---

## Figma design
*To be defined*

## AppInsights metric
Use of price indicators in Advanced Search

## Snapshot testing
*To be defined*

## Feature Flag
NO

## Affect Highlights
NO

## Affect Sales
YES - the executed ranking changes according to the selected price indicators

---

## Context

Ranking users can already define the main execution criteria of a ranking from the sidebar and use Advanced Search for more specific conditions.

To support commercial analysis, users need to narrow down the ranking by pricing situations represented through price indicators. These indicators must behave like any other execution criterion of the sidebar: they must affect the ranking result, combine correctly with the rest of the selected filters, and be preserved in the user configuration and export summaries.

Additionally, if a price indicator is not allowed for a restricted role, it must not be available to that user.

---

## Acceptance Criteria

```gherkin
Scenario: Display price indicators section in Advanced Search
  Given the user opens "New Search"
  When the user expands "Advanced Search"
  Then a new filter section for price indicators is displayed
  And the section is part of the ranking execution criteria in the sidebar

Scenario: Show only applicable and authorized price indicators
  Given the user is configuring a ranking
  When the available price indicators are loaded
  Then only the indicators applicable to the current ranking context are displayed
  And any indicator restricted for the current user role is not displayed

Scenario: Select one or more price indicators
  Given the price indicators section is visible
  When the user selects one or more price indicators
  Then the selected values remain visible in Advanced Search until the user applies, clears, or changes the ranking context

Scenario: Execute ranking with selected price indicators
  Given the user has selected one or more price indicators
  When the user clicks "Apply"
  Then the ranking is executed
  And only articles matching at least one selected price indicator are returned

Scenario: Combine price indicators with the rest of the sidebar criteria
  Given the user has selected one or more price indicators
  And the user has also selected other filters in the sidebar
  When the user clicks "Apply"
  Then the ranking respects all selected sidebar criteria
  And the price indicators are combined with the rest of the execution filters

Scenario: No price indicator selected
  Given the price indicators section is visible
  When the user does not select any price indicator
  And the user clicks "Apply"
  Then the ranking is executed without applying any filter by price indicators

Scenario: Recalculate available selections when context changes
  Given the user has selected one or more price indicators
  When the user changes a higher-level ranking criterion that affects the available price indicators
  Then the list of available price indicators is recalculated
  And any selected indicator that is no longer valid is removed

Scenario: Clear Advanced Search resets price indicators
  Given the user has selected one or more price indicators
  When the user clicks "Clear"
  Then the selected price indicators are removed
  And the section returns to its default state

Scenario: Save and recover configurations with price indicators
  Given the user has executed a ranking with one or more price indicators selected
  When the user saves the configuration and later recovers it
  Then the same price indicators are restored in Advanced Search
  And the ranking is executed with those restored values

Scenario: Export ranking with price indicators applied
  Given the user has executed a ranking with one or more price indicators selected
  When the user exports the ranking to Excel or PDF
  Then the export contains the articles returned by that ranking
  And the filters summary includes the selected price indicators

Scenario: No articles match the selected price indicators
  Given the user has selected one or more price indicators
  When the user clicks "Apply" and no articles match the selected conditions
  Then the ranking shows the empty result state
```

---

## Notes

- Price indicators are execution filters of the sidebar, not quick filters over already loaded results
- Multiple selected price indicators use OR logic within the same filter
- The price indicators filter combines with the rest of the sidebar criteria in the standard ranking execution flow
- Restricted roles must never see price indicators that expose information they are not allowed to use
