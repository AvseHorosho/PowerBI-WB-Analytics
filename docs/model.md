# Data model overview

This document describes the semantic data model used in the Power BI report.
The model is designed to support financial analysis, Month-over-Month (MoM) comparison,
logistics efficiency evaluation, and SKU-level drillthrough scenarios.

---

## Model architecture

The model follows a clean star-schema approach with a clear separation between
fact tables and dimension tables.

Core principles:
- single source of truth for transactional data
- explicit relationships to avoid ambiguity
- calendar-driven time intelligence
- scalable structure for drillthrough and ranking logic

---

## Fact tables

### fact_sales (realization)

Primary fact table containing transactional sales and realization data.

Key attributes:
- date / YearMonth
- SKU identifiers
- warehouse identifier
- revenue metrics
- cost components

Used for:
- revenue calculations
- MoM comparison logic
- ranking of growth and decline leaders

---

## Dimension tables

### dim_calendar

Central calendar table used for all time-based analysis.

Key features:
- Year
- Month
- YearMonth key
- PreviousMonth key (for stable MoM logic)

Purpose:
- consistent time filtering across all pages
- simplified MoM calculations
- avoidance of complex DAX time-shift logic

---

### dim_product

Product dimension providing SKU-level attributes.

Key attributes:
- SKU (nm_id)
- supplier article
- product category

Purpose:
- grouping and filtering of SKUs
- drillthrough navigation
- aggregation at different product hierarchy levels

---

### dim_warehouse

Warehouse dimension representing Wildberries fulfillment locations.

Key attributes:
- warehouse name
- regional grouping

Purpose:
- logistics and ROI analysis
- warehouse-level profitability comparison

---

## Relationships

Relationship design principles:
- one-to-many relationships from dimensions to fact
- single-direction filtering
- avoidance of bi-directional relationships where possible

This design ensures:
- predictable filter propagation
- stable MoM calculations
- correct drillthrough behavior

---

## Time intelligence logic

Month-over-Month analysis is based on:
- YearMonth numeric key
- explicit reference to previous month key
- comparison of aggregated measures

This approach avoids:
- ambiguous date context
- performance-heavy DAX constructs
- dependency on complex built-in time intelligence

---

## Drillthrough support

The model is optimized for drillthrough scenarios:
- dimensions shared across summary and detail pages
- preserved filter context
- stable navigation from high-level KPIs to SKU-level details

---

## Model benefits

The chosen architecture provides:
- analytical transparency
- predictable calculation behavior
- performance stability
- ease of extension for additional metrics or periods

