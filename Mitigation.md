# CII Readiness Check

## Information Architecture, Flow Chart & User Flow

---

## 1. Page Purpose

The **CII Readiness Check** page allows a client/admin user to:

1. Select a vessel and calculation year.
2. Select the calculation basis.
3. Calculate the vessel's CII performance using available voyage and fuel data.
4. Review the vessel's current CII performance.
5. Select one or multiple predefined mitigation scenarios.
6. Run a scenario analysis.
7. Compare the projected CII performance against the current baseline.
8. Understand CII rating, ETS savings, FuelEU status, and potential improvement.
9. Download the resulting CII report.

### Primary user question

> "How is this vessel performing against CII requirements, and what actions can improve its performance?"

---

# 2. Information Architecture

```text
CII Readiness Check
│
├── Page Header
│   ├── Title
│   ├── Description
│   └── Page Actions
│
├── Calculation Configuration
│   ├── Vessel
│   ├── Year
│   ├── Calculation Type
│   │   ├── Base
│   │   └── Actual
│   └── Calculate CII Score
│
├── Operational Data Summary
│   │
│   ├── Voyage History
│   │   ├── Voyages Considered
│   │   ├── Period
│   │   ├── Total Distance
│   │   └── Total Cargo
│   │
│   └── Fuel Details
│       ├── Fuel Types Used
│       └── Total Fuel Consumed
│
├── CII Performance
│   ├── Current Attained CII
│   ├── Required CII
│   ├── CII Rating
│   ├── Rating Year
│   ├── CII Rating Scale
│   └── Download Report
│
├── Mitigation Scenario Analysis
│   ├── Scenario Selection
│   │   ├── No Action (Baseline)
│   │   ├── Speed Reduction -1 kn
│   │   ├── Speed + Hull Clean
│   │   ├── Above + B20 Biofuel
│   │   ├── LNG Dual-Fuel Retrofit
│   │   └── Wind Assist (Rotor)
│   │
│   ├── Scenario Assumptions
│   │   ├── CII Reduction
│   │   └── Fuel Reduction
│   │
│   └── Run Scenario Analysis
│
└── Scenario Results vs Baseline
    ├── Baseline Result
    ├── Selected Scenario Result
    ├── New CII
    ├── Rating
    ├── ETS Saving
    └── FuelEU Status
```

---

# 3. Page Layout Hierarchy

The page should follow this visual hierarchy:

```text
┌─────────────────────────────────────────────────────────────┐
│ CII Verification - Actual Performance                      │
│ Calculated using actual voyage history and fuel data.      │
├─────────────────────────────────────────────────────────────┤
│ Vessel             Year              Calculation Type       │
│ [AB SERENA ▼]      [2026 ▼]         ○ Base  ○ Actual       │
│                                                   [Calculate]│
├─────────────────────────────────────────────────────────────┤
│ Voyage History                     Fuel Details             │
│ ┌─────────────────────┐             ┌─────────────────────┐ │
│ │ Voyages             │             │ Fuel types          │ │
│ │ Period              │             │ Total fuel          │ │
│ │ Distance            │             │                     │ │
│ │ Cargo               │             │                     │ │
│ └─────────────────────┘             └─────────────────────┘ │
├─────────────────────────────────────────────────────────────┤
│ CII Performance                                  [Download] │
│                                                             │
│ Current CII    Required CII        CII Rating Scale         │
│ 4.99 D         5.35                A → E                    │
├─────────────────────────────────────────────────────────────┤
│ Mitigation Scenario Analysis                                 │
│                                                             │
│ Select │ Scenario              │ CII │ Fuel │               │
│   □    │ No Action (Baseline)  │ 0%  │ 0%   │               │
│   □    │ Speed reduction -1 kn │ ~6% │ ~6%  │               │
│   □    │ Speed + hull clean    │ ~10%│ ~10% │               │
│   □    │ Above + B20 biofuel   │ ~10%│ ~10% │               │
│   □    │ LNG dual-fuel retrofit│ ~23%│ ~23% │               │
│   □    │ Wind assist (rotor)   │~5-8%│~5-8% │               │
│                                                             │
│                       [Run Scenario Analysis]                │
├─────────────────────────────────────────────────────────────┤
│ Scenario Results vs Baseline                                  │
│                                                             │
│ Scenario │ New CII │ Rating │ ETS Saving │ FuelEU Status    │
│ Baseline │ 4.99    │ D      │ €0         │ Non-Compliant    │
│ Selected │ 4.69    │ C      │ €49K       │ Non-Compliant    │
└─────────────────────────────────────────────────────────────┘
```

---

# 4. Calculation Configuration

## 4.1 Vessel

Required field.

Purpose:

* Determines which vessel's operational data is used.
* Determines vessel-specific CII requirements and characteristics.

Control:

* Searchable select/dropdown.

Example:

```text
Vessel
[ AB SERENA                         ▼ ]
```

---

## 4.2 Year

Required field.

Purpose:

* Determines the calculation/rating year.

Example:

```text
Year
[ 2026                             ▼ ]
```

---

## 4.3 Calculation Type

Two options:

```text
Calculation Type

○ Base
○ Actual
```

### Base

Used when calculating against the predefined/base dataset or reference calculation.

### Actual

Used when calculating using the vessel's actual voyage history and fuel consumption.

The selected calculation type must be clearly reflected in the page title/subtitle or calculation context.

---

# 5. Calculate CII Score

Primary action:

```text
[ Calculate CII Score ]
```

### Preconditions

The button should only execute when:

* Vessel is selected.
* Year is selected.
* Calculation Type is selected.
* Required voyage/fuel data is available.

### If data is missing

Display an informative validation state.

Example:

```text
Unable to calculate CII

Required voyage or fuel consumption data is missing
for the selected vessel and year.

[View Voyage History]
[View Fuel Data]
```

Do not show misleading CII results when the underlying data is incomplete.

---

# 6. Operational Data Summary

After successful calculation, show the source data used for the calculation.

## Voyage History

Display:

* Voyages Considered
* Period
* Total Distance
* Total Cargo

Example:

```text
Voyage History

Voyages considered    : 2
Period                 : 2024–2025
Total Distance         : 12,212 NM
Total Cargo            : 257,323 DWT
```

---

## Fuel Details

Display:

* Fuel Types Used
* Total Fuel Consumed

Example:

```text
Fuel Details

Fuel types used        : HFO, MGO
Total fuel consumed    : 233 MT
```

These cards are informational and provide transparency into the calculation.

---

# 7. CII Performance

This is the primary results section.

## 7.1 Current Attained CII

Example:

```text
Current (Attained) CII
4.99
D
```

This represents the vessel's calculated actual CII.

---

## 7.2 Required CII

Example:

```text
Required CII
5.35
```

This represents the required/reference CII threshold for the selected calculation year.

---

## 7.3 CII Rating

Possible ratings:

```text
A
B
C
D
E
```

The rating should be visually associated with the CII scale.

---

## 7.4 Rating Year

Display the year associated with the rating.

Example:

```text
Rating Year
2025
```

---

# 8. CII Rating Visualization

The rating scale should communicate:

```text
Better                                           Worse

A ───────────────────────────────────────────────
B ───────────────────────────────────────────────
C ───────────────────────────────────────────────
D ───────────────────────●───────────────────────
E ───────────────────────────────────────────────
```

The current CII value should be represented by a marker positioned against the appropriate range.

Example:

```text
CII Score (gCO₂e / dwt-nm)

Better                                      Worse

A     ─────────────────────────────────────
B     ─────────────────────────────────────
C     ─────────────────────────────────────
D     ────────────────────────●────────────
E     ─────────────────────────────────────

                         4.99
```

The visualization must clearly communicate that:

> Lower CII is better.

---

# 9. Download Report

Action:

```text
[ Download Report ]
```

Purpose:

* Export the calculated CII result.
* Include relevant calculation inputs and results.
* Include selected scenario analysis where applicable.

If no CII calculation has been completed, the report action should remain disabled or unavailable.

---

# 10. Mitigation Scenario Analysis

## Purpose

This section allows the user to simulate possible operational or technical improvements.

The scenarios are **predefined system templates**.

Users do not create new scenarios from this screen.

---

# 11. Default Scenario Templates

The system must provide the following scenarios:

| Select | Scenario               | CII Reduction | Fuel Reduction |
| ------ | ---------------------- | ------------: | -------------: |
| ☐      | No Action (Baseline)   |            0% |             0% |
| ☐      | Speed reduction -1 kn  |           ~6% |            ~6% |
| ☐      | Speed + hull clean     |          ~10% |           ~10% |
| ☐      | Above + B20 biofuel    |          ~10% |           ~10% |
| ☐      | LNG dual-fuel retrofit |          ~23% |           ~23% |
| ☐      | Wind assist (rotor)    |         ~5–8% |          ~5–8% |

These values represent **scenario assumptions/templates**, not final calculated results.

---

# 12. Scenario Selection Behavior

The user can select:

* One scenario
* Multiple scenarios

Example:

```text
☐ No Action (Baseline)
☑ Speed reduction -1 kn
☑ Speed + hull clean
☐ Above + B20 biofuel
☐ LNG dual-fuel retrofit
☐ Wind assist (rotor)
```

The selection state should be visually clear.

---

# 13. Important Scenario Logic

The scenarios are **cumulative mitigation strategies** where the scenario name indicates the intended combination.

For example:

```text
Speed reduction -1 kn
        ↓
Speed + hull clean
        ↓
Above + B20 biofuel
```

Therefore:

### Speed reduction -1 kn

Represents:

```text
Speed reduction
```

### Speed + hull clean

Represents:

```text
Speed reduction
+
Hull cleaning
```

### Above + B20 biofuel

Represents:

```text
Speed reduction
+
Hull cleaning
+
B20 biofuel
```

The system should avoid accidentally applying the same mitigation action twice.

The scenario calculation engine should interpret the selected scenario according to its predefined template/configuration.

---

# 14. Scenario Selection Examples

## Single Scenario

User selects:

```text
☑ Speed reduction -1 kn
```

System calculates:

```text
Baseline CII
4.99

Projected CII
4.69

Improvement
~6%
```

---

## Multiple Scenarios

User selects:

```text
☑ Speed reduction -1 kn
☑ Speed + hull clean
```

The system evaluates the selected scenario configuration and returns the applicable scenario result.

The UI should not simply add percentages blindly.

For example:

```text
6% + 10% ≠ automatically 16%
```

The backend/calculation engine should determine the final CII and fuel impact using the configured scenario rules.

---

# 15. Run Scenario Analysis

Primary action:

```text
[ Run Scenario Analysis ]
```

This action should only be enabled when:

* A valid CII baseline exists.
* At least one scenario is selected.

If no scenario is selected:

```text
Select at least one mitigation scenario
to run the analysis.
```

---

# 16. Scenario Analysis Processing Flow

```text
User selects scenario(s)
          │
          ▼
Validate baseline CII
          │
          ▼
Validate scenario selection
          │
          ▼
Load scenario assumptions
          │
          ▼
Apply scenario calculation
          │
          ▼
Calculate projected CII
          │
          ├── Calculate new rating
          │
          ├── Calculate fuel impact
          │
          ├── Calculate ETS savings
          │
          └── Determine FuelEU status
          │
          ▼
Update Scenario Results
          │
          ▼
Compare against baseline
```

---

# 17. Scenario Results vs Baseline

This section displays the result after the user runs the scenario analysis.

## Required columns

| Scenario                | New CII | Rating | ETS Saving (Annually) | FuelEU Status |
| ----------------------- | ------: | ------ | --------------------: | ------------- |
| Baseline (Current)      |    4.99 | D      |                    €0 | Non-Compliant |
| Speed Reduction (-1 kn) |    4.69 | C      |                  €49K | Non-Compliant |
| Hull Cleaning           |    4.49 | C      |                  €83K | Non-Compliant |
| B20 Biofuel             |    4.49 | C      |                  €83K | Compliant     |
| LNG Dual-Fuel Retrofit  |    3.84 | B      |                 €191K | Compliant     |

The exact calculated values must come from the calculation engine.

---

# 18. Baseline Row

The baseline should always be available after CII calculation.

Example:

```text
Baseline (Current)

New CII       4.99
Rating        D
ETS Saving    €0
FuelEU        Non-Compliant
```

The baseline acts as the comparison reference.

---

# 19. Scenario Result Logic

For each selected scenario, calculate:

```text
New CII
↓
New CII Rating
↓
Fuel Consumption Impact
↓
ETS Saving
↓
FuelEU Compliance
```

The user should be able to immediately understand:

> "What happens if I apply this mitigation strategy?"

---

# 20. Result States

## 20.1 Improved Rating

Example:

```text
Baseline
4.99 — D

Scenario
4.69 — C
```

Visually communicate that the rating improved.

---

## 20.2 No Rating Improvement

Example:

```text
Baseline
4.99 — D

Scenario
4.85 — D
```

The result should still show the CII improvement even if the rating remains unchanged.

---

## 20.3 FuelEU Compliant

Use a positive compliance status:

```text
Compliant
```

---

## 20.4 FuelEU Non-Compliant

Use:

```text
Non-Compliant
```

The status must not rely on color alone.

---

# 21. Empty State

Before CII calculation:

```text
CII Performance

No CII calculation available.

Select a vessel, year and calculation type,
then calculate the CII score.
```

Scenario analysis should remain unavailable until a valid baseline exists.

---

# 22. Scenario Analysis Empty State

After CII calculation but before selecting scenarios:

```text
Scenario Results vs Baseline

Select one or more mitigation scenarios
and run the analysis to view projected results.
```

---

# 23. Loading State

When calculating:

```text
Calculating CII...
```

When running scenario analysis:

```text
Running scenario analysis...
```

The primary action should be temporarily disabled to prevent duplicate calculations.

---

# 24. Error Handling

## CII Calculation Error

```text
Unable to calculate CII

The CII calculation could not be completed.
Please verify the voyage and fuel data and try again.

[Try Again]
```

---

## Scenario Calculation Error

```text
Unable to run scenario analysis

The selected scenario could not be calculated.
Please try again.

[Try Again]
```

---

## Missing Data

```text
Insufficient Data

There is not enough voyage or fuel data
to calculate the CII for the selected vessel/year.

[View Data]
```

---

# 25. User Flow

## Primary User Flow

```text
START
  │
  ▼
Open CII Readiness Check
  │
  ▼
Select Vessel
  │
  ▼
Select Year
  │
  ▼
Select Calculation Type
  │
  ▼
Click "Calculate CII Score"
  │
  ▼
Validate Required Data
  │
  ├── NO ──► Show Missing Data/Error
  │              │
  │              └──► User fixes data
  │                         │
  │                         └──► Calculate Again
  │
  └── YES
       │
       ▼
Calculate CII
       │
       ▼
Display Operational Data
       │
       ▼
Display CII Performance
       │
       ├──────────────► Download Report
       │
       ▼
Review Current CII
       │
       ▼
Review Mitigation Scenarios
       │
       ▼
Select One or Multiple Scenarios
       │
       ▼
Click "Run Scenario Analysis"
       │
       ▼
Validate Scenario Selection
       │
       ├── NO ──► Ask User to Select Scenario
       │
       └── YES
             │
             ▼
       Run Calculation
             │
             ▼
       Calculate Projected CII
             │
             ▼
       Calculate Rating
             │
             ▼
       Calculate ETS Savings
             │
             ▼
       Determine FuelEU Status
             │
             ▼
       Display Scenario Results
             │
             ▼
       Compare With Baseline
             │
             ▼
           END
```

---

# 26. Detailed User Journey

## Step 1 — Enter Page

User opens:

```text
CII Readiness Check
```

The page initially shows the calculation configuration.

---

## Step 2 — Configure Calculation

User selects:

```text
Vessel: AB SERENA
Year: 2026
Calculation Type: Actual
```

---

## Step 3 — Calculate

User clicks:

```text
Calculate CII Score
```

The system retrieves the required operational data and calculates the vessel's CII.

---

## Step 4 — Review Operational Data

User reviews:

```text
Voyage History
+
Fuel Details
```

This gives confidence that the correct data is being used.

---

## Step 5 — Review Current Performance

User sees:

```text
Current Attained CII: 4.99
Required CII: 5.35
Rating: D
```

The rating visualization provides additional context.

---

## Step 6 — Explore Mitigation Options

User reviews the available mitigation scenarios:

```text
No Action
Speed reduction -1 kn
Speed + hull clean
Above + B20 biofuel
LNG dual-fuel retrofit
Wind assist (rotor)
```

---

## Step 7 — Select Scenario

User selects one or multiple scenarios.

Example:

```text
☑ Speed reduction -1 kn
☑ Speed + hull clean
```

---

## Step 8 — Run Scenario

User clicks:

```text
Run Scenario Analysis
```

---

## Step 9 — Review Results

The system calculates and displays:

```text
Baseline
4.99 — D

Projected
4.49 — C
```

Along with:

```text
ETS Saving
FuelEU Status
```

---

## Step 10 — Compare and Decide

User compares the scenarios and determines which mitigation strategy provides the most appropriate balance between:

* CII improvement
* Rating improvement
* Fuel reduction
* ETS savings
* FuelEU compliance

---

## Step 11 — Export

User can click:

```text
Download Report
```

to export the CII calculation and scenario results.

---

# 27. Complete End-to-End Flow Chart

```text
                    ┌──────────────────────┐
                    │ CII Readiness Check  │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Select Vessel        │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Select Year          │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Select Calculation    │
                    │ Type                  │
                    │ Base / Actual         │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Calculate CII Score   │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Validate Data         │
                    └──────────┬───────────┘
                               │
                    ┌──────────┴──────────┐
                    │                     │
                  Invalid               Valid
                    │                     │
                    ▼                     ▼
              ┌───────────┐      ┌──────────────────┐
              │ Error /   │      │ Calculate CII    │
              │ Missing   │      └────────┬─────────┘
              │ Data      │               │
              └─────┬─────┘               ▼
                    │             ┌──────────────────┐
                    │             │ Operational Data │
                    │             │ Summary          │
                    │             └────────┬─────────┘
                    │                      │
                    │                      ▼
                    │             ┌──────────────────┐
                    │             │ CII Performance  │
                    │             │                  │
                    │             │ Attained CII     │
                    │             │ Required CII     │
                    │             │ Rating           │
                    │             └────────┬─────────┘
                    │                      │
                    │                      ▼
                    │             ┌──────────────────┐
                    │             │ Mitigation       │
                    │             │ Scenarios        │
                    │             └────────┬─────────┘
                    │                      │
                    │                      ▼
                    │             ┌──────────────────┐
                    │             │ Select one or    │
                    │             │ multiple         │
                    │             │ scenarios        │
                    │             └────────┬─────────┘
                    │                      │
                    │                      ▼
                    │             ┌──────────────────┐
                    │             │ Run Scenario     │
                    │             │ Analysis         │
                    │             └────────┬─────────┘
                    │                      │
                    │                      ▼
                    │             ┌──────────────────┐
                    │             │ Scenario Engine  │
                    │             └────────┬─────────┘
                    │                      │
                    │             ┌────────┼─────────┐
                    │             ▼        ▼         ▼
                    │          New CII   Rating   Savings
                    │             │        │         │
                    │             └────────┼─────────┘
                    │                      │
                    │                      ▼
                    │             ┌──────────────────┐
                    │             │ FuelEU Status    │
                    │             └────────┬─────────┘
                    │                      │
                    │                      ▼
                    │             ┌──────────────────┐
                    │             │ Scenario Results │
                    │             │ vs Baseline      │
                    │             └────────┬─────────┘
                    │                      │
                    │                      ▼
                    │             ┌──────────────────┐
                    │             │ Compare & Decide │
                    │             └────────┬─────────┘
                    │                      │
                    │                      ▼
                    │             ┌──────────────────┐
                    │             │ Download Report  │
                    │             └──────────────────┘
                    │
                    └──────────────► Retry
```

---

# 28. System Logic Summary

The implementation should follow this relationship:

```text
VESSEL
   +
YEAR
   +
CALCULATION TYPE
   │
   ▼
Operational Data
   │
   ├── Voyage Data
   └── Fuel Data
   │
   ▼
BASELINE CII
   │
   ├── Attained CII
   ├── Required CII
   └── Rating
   │
   ▼
MITIGATION SCENARIO SELECTION
   │
   ├── Speed Reduction
   ├── Hull Cleaning
   ├── B20 Biofuel
   ├── LNG Retrofit
   └── Wind Assist
   │
   ▼
SCENARIO CALCULATION
   │
   ├── Projected CII
   ├── Projected Rating
   ├── Fuel Impact
   ├── ETS Savings
   └── FuelEU Status
   │
   ▼
SCENARIO RESULTS VS BASELINE
```

---

# 29. Key UX Rules

### Rule 1 — Baseline first

Never allow scenario analysis without a valid baseline CII calculation.

### Rule 2 — Scenario templates are predefined

The six scenarios are system-defined templates:

```text
No Action (Baseline)
Speed reduction -1 kn
Speed + hull clean
Above + B20 biofuel
LNG dual-fuel retrofit
Wind assist (rotor)
```

### Rule 3 — User can select multiple scenarios

Checkboxes should be used rather than radio buttons.

### Rule 4 — Scenario assumptions are not final results

The `~6%`, `~10%`, `~23%` values are assumptions/templates.

The right-side result must show the actual calculated output.

### Rule 5 — Baseline remains the comparison reference

Every scenario result should be understood relative to:

```text
Current Baseline
```

### Rule 6 — Results should answer business questions

The result should clearly communicate:

```text
Did CII improve?
Did the rating improve?
How much can we save?
Are we FuelEU compliant?
```

### Rule 7 — No misleading percentage addition

When multiple scenarios are selected, the calculation engine must apply the predefined scenario rules rather than blindly adding reduction percentages.

### Rule 8 — Calculation transparency

The user should always be able to identify:

```text
What data was used?
What is the baseline?
What scenario was selected?
What assumptions were applied?
What is the resulting CII?
```

---

# 30. Final IA Summary

```text
CII READINESS CHECK
│
├── 01. Calculation Configuration
│   ├── Vessel
│   ├── Year
│   ├── Calculation Type
│   └── Calculate CII
│
├── 02. Operational Data
│   ├── Voyage History
│   └── Fuel Details
│
├── 03. CII Performance
│   ├── Attained CII
│   ├── Required CII
│   ├── CII Rating
│   ├── Rating Year
│   ├── Rating Scale
│   └── Download Report
│
├── 04. Mitigation Scenario Analysis
│   ├── No Action
│   ├── Speed Reduction -1 kn
│   ├── Speed + Hull Clean
│   ├── Above + B20 Biofuel
│   ├── LNG Dual-Fuel Retrofit
│   ├── Wind Assist (Rotor)
│   └── Run Scenario Analysis
│
└── 05. Scenario Results vs Baseline
    ├── Scenario
    ├── New CII
    ├── Rating
    ├── ETS Saving
    └── FuelEU Status
```

## Core Product Flow

**Configure → Calculate → Verify Data → Review Baseline → Select Mitigation → Run Analysis → Compare Results → Decide → Download Report**
