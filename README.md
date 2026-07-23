# Budget vs. Actuals Variance Dashboard

A dynamic FP&A reporting dashboard built in Excel, using Power Query to automate data preparation and refresh. Budgeted figures are compared against actual results, with dollar and percentage variances surfaced for review.

The design objective was a reporting pack that updates on one click as each month of actuals arrives, rather than one that has to be rebuilt or manually re-pointed every period.

---

## Repository contents

| File | Description |
|---|---|
| `Budget vs Actuals_Startingfile.xlsx` | The dashboard. Contains the Power Query transformations, consolidated data model and reporting front end |
| `Presentation - FP&A Variance Analysis Final.pptx` | Supporting deck walking through the build and output |
| `LICENSE` | MIT |

---

## Method

**1. Data preparation.** Two source datasets — budget and actuals — are defined as named ranges and loaded into Power Query, keeping the transformation layer separate from the source data.

**2. Unpivoting.** Both datasets arrive wide, with dates spread across columns. Power Query unpivots them into long format, with a single date column. This removes the dependency on a fixed column structure, which is what normally breaks a reporting template when a new period is added.

**3. Consolidation.** A scenario column tags each row as Budget or Actual, and the two queries are appended into a single table. Adding a month of actuals to the source and refreshing is sufficient to update the entire dashboard.

**4. Reporting layer.** The front end is driven by `SUMIFS`, `FILTER`, `LET`, `XLOOKUP` and `IFERROR` against the consolidated table, with gross profit, net income and variance calculated on top. Reporting periods are controlled by dynamic date ranges rather than hardcoded references.

---

## Capabilities

- **One-click refresh.** New actuals flow through the query chain to the dashboard without manual data manipulation.
- **Variance analysis.** Both absolute and percentage variance are reported, identifying where performance ran ahead of or behind plan.
- **Decision support.** Revenue, cost and net income are broken out so performance can be traced to the driver rather than read only at the total.
- **Reusable structure.** The query and reporting logic are not specific to this dataset, and can be repointed to a different business, chart of accounts or reporting calendar without a rebuild.
- **Executive presentation.** Donut charts, variance indicators and consistent formatting present the output in a form suitable for review rather than as a raw data extract.

---

## Note on the approach

The value in this build sits in the transformation layer rather than the visuals. Placing the unpivot and append steps in Power Query means the reporting front end never has to accommodate a changing column structure — which is the failure point in most manually maintained variance packs, and the reason they tend to require rework each period.
