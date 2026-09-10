# User Story 5: New price indicators in Advanced Search

**AS A** Ranking user

**I AM ABLE TO** use four new price indicators in Advanced Search

**SO I** can execute rankings using specific price-based conditions

---

## Figma design
*To be defined*

## AppInsights metric
Use of the new price indicators in Advanced Search

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

To support commercial analysis, the list of available indicators in Advanced Search must include four new price indicators:
- PVP Base
- PVP Red Label
- PVP Blue Label
- PVP Spain

These indicators must behave as numeric filters. When the user selects one of them, the available conditions must be numeric operators and the entered value must be numeric, allow integers or decimals with one or two decimal places, accept comma or dot as decimal separator, and be interpreted in euros without requiring any currency selection.

---

## Acceptance Criteria

```gherkin
Scenario: Show the 4 new price indicators in Advanced Search
  Given the user opens "New Search"
  When the user expands "Advanced Search"
  Then the list of possible indicators includes:
    - PVP Base
    - PVP Red Label
    - PVP Blue Label
    - PVP Spain

Scenario: Show numeric conditions for the new price indicators
  Given the user is adding a condition in Advanced Search
  When the user selects one of these indicators:
    - PVP Base
    - PVP Red Label
    - PVP Blue Label
    - PVP Spain
  Then the available conditions are numeric conditions
  And the user can select operators such as equal to or greater than

Scenario: Accept numeric values with two decimal places
  Given the user has selected one of the 4 new price indicators
  When the user enters the comparison value
  Then the value must be numeric
  And the value allows an integer format or a decimal format with one or two decimal places
  And the value accepts comma or dot as decimal separator

Scenario: Reject non-numeric values
  Given the user has selected one of the 4 new price indicators
  When the user enters a non-numeric value
  Then the condition cannot be applied
  And a validation message is displayed indicating that a valid numeric value must be entered

Scenario: Execute ranking with a new price indicator condition
  Given the user has defined a condition using one of the 4 new price indicators
  When the user clicks "Apply"
  Then the ranking is executed with that condition
  And only articles matching that numeric condition are returned

Scenario: Combine a new price indicator with the rest of the sidebar criteria
  Given the user has defined a condition using one of the 4 new price indicators
  And the user has also selected other filters in the sidebar
  When the user clicks "Apply"
  Then the ranking respects all selected sidebar criteria
  And the price indicator condition is combined with the rest of the execution filters

Scenario: Clear sidebar resets the new price indicators
  Given the user has defined a condition using one of the 4 new price indicators
  When the user clicks the sidebar "Clear" action
  Then the selected indicator, condition, and numeric value are removed
  And the section returns to its default state

Scenario: Save and recover configurations with the new price indicators
  Given the user has executed a ranking with a condition using one of the 4 new price indicators
  When the user saves the configuration and later recovers it
  Then the same indicator, numeric condition, and value are restored in Advanced Search
  And the ranking is executed with those restored values

Scenario: Export to Excel with a new price indicator applied
  Given the user has executed a ranking with a condition using one of the 4 new price indicators
  When the user exports the ranking to Excel
  Then the export contains the articles returned by that ranking
  And the Excel includes the selected indicator, condition, and value in the filters summary sheet

Scenario: Export to PDF with a new price indicator applied
  Given the user has executed a ranking with a condition using one of the 4 new price indicators
  When the user exports the ranking to PDF
  Then the export contains the articles returned by that ranking

Scenario: Interpret the entered value as euros
  Given the user has selected one of the 4 new price indicators
  When the user enters a numeric value
  Then the value is interpreted as an amount in euros
  And no currency selection is required
```

---

## Notes

- The new indicators are available in the list of indicators that can be used in Advanced Search
- These four indicators use numeric conditions and numeric input values
- The numeric value accepts integers and decimal values with one or two decimal places
- The numeric value accepts comma or dot as decimal separator
- Currency does not affect the behavior because these prices are always expressed in euros
- Advanced Search conditions are execution filters of the sidebar, not quick filters over already loaded results
