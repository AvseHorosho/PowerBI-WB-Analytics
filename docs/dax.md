# DAX logic overview

This document describes the key DAX calculation logic used in the Power BI report.
The focus is not on full formulas, but on analytical intent, calculation patterns,
and design decisions behind the measures.

The report heavily relies on Month-over-Month (MoM) analysis, ranking logic,
and stable context handling for drillthrough scenarios.

---

## Core calculation principles

The DAX logic in this project follows several core principles:

- measures are preferred over calculated columns
- explicit context control is used instead of implicit behavior
- calendar-driven logic is used for all time-based calculations
- calculations are designed to be reusable across pages

This approach was chosen to ensure predictable behavior and analytical transparency.

---

## Revenue measures

### Revenue (Current Month)

Base revenue measure calculated from realization data
under the current filter context.

Used as:
- primary KPI on Finance overview
- base value for MoM comparison
- input for ranking logic

Key challenge:
Ensuring correct aggregation when multiple dimensions
(SKU, warehouse, category) are applied simultaneously.

---

### Revenue (Previous Month)

Calculated using explicit reference to the previous month key
from the calendar dimension.

Design decision:
Previous month logic is handled through the calendar table,
not through DAX date shifting.

This avoids:
- complex DATEADD / SAMEPERIODLASTYEAR logic
- ambiguity when custom calendars are used
- performance issues on large datasets

---

## Month-over-Month (MoM) logic

### Absolute MoM change

Difference between current month revenue
and previous month revenue.

Used for:
- identifying growth and decline leaders
- ranking SKUs by impact on total revenue

Critical aspect:
MoM calculations remain stable regardless of slicer combinations,
including SKU-level and warehouse-level filters.

---

### Relative MoM change (%)

Calculated as percentage change relative to previous month.

Used for:
- trend interpretation
- contextual analysis of growth vs decline magnitude

Design note:
Percentage measures are never used for ranking,
only for interpretation.

---

## Ranking logic (Leaders analysis)

### Ranking by revenue delta

SKUs are ranked based on absolute MoM revenue change.

Key design choices:
- ranking is based on measures, not raw columns
- filters are preserved except for ranking dimension
- ties are handled consistently

This logic enables:
- accurate identification of top growth drivers
- detection of SKUs causing the largest revenue drop

This was one of the most sensitive parts of the model,
as incorrect context handling easily leads to misleading leaders.

---

## Cost and profitability measures

### Cost components

Separate measures are used for:
- WB commission
- logistics costs
- cost of goods

These are aggregated independently and combined
only at the final profit calculation stage.

This allows:
- clear audit of cost structure
- flexible reuse across pages
- correct drillthrough behavior

---

### Gross profit and ROI

Gross profit is calculated as revenue minus all cost components.

ROI is calculated as a ratio measure based on gross profit
and total costs.

Design decision:
ROI is calculated strictly as a measure,
never as a pre-aggregated value,
to avoid distortion under filters.

---

## Logistics & warehouse analysis

Warehouse-level calculations reuse the same base measures
used in financial pages.

Important aspect:
No warehouse-specific logic is hardcoded in measures.
All warehouse analysis is driven by the warehouse dimension
and filter context.

This ensures:
- consistency between pages
- scalability for new warehouses
- correctness of ROI comparison

---

## Drillthrough behavior

All drillthrough pages rely on:
- shared dimensions
- inherited filter context
- the same base measures as summary pages

No special drillthrough-only measures are created.

This guarantees:
- consistency between overview and detail
- trust in numbers when navigating deeper
- reduced maintenance complexity

---

## Key challenges addressed

During development, the most challenging areas were:

- stabilizing MoM calculations across multiple slicers
- preventing incorrect leaders due to context leakage
- ensuring that drillthrough pages exactly match summary values
- balancing DAX simplicity with analytical correctness

These challenges were resolved through:
- explicit calendar logic
- careful use of context-preserving functions
- avoidance of bi-directional relationships
- strict separation of base measures and derived measures

---

## Summary

The DAX logic in this project is designed to be:
- transparent
- stable
- business-oriented
- scalable

The focus is on analytical correctness rather than formula complexity,
making the model suitable for real-world decision-making scenarios.

