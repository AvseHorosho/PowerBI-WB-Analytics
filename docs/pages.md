# Report pages overview

This document describes the analytical purpose and logic of each key page in the Power BI report.
The report is designed to analyze Wildberries sales performance, Month-over-Month (MoM) dynamics,
profitability, logistics costs, and SKU-level drillthrough analysis.

---

## 01. Finance overview

**Purpose:**  
Provide a high-level financial snapshot of the business for the selected period.

**Key metrics:**
- Total revenue
- Gross profit
- ROI
- Core cost components (WB commission, logistics, cost of goods)

**Usage:**  
Used by management for quick assessment of overall financial performance and business health.
Supports fast identification of loss-making periods and margin pressure.

---

## 02. MoM Leaders (Realization)

**Purpose:**  
Identify products with the strongest Month-over-Month growth and decline based on realized sales.

**Logic:**
- Comparison of current month revenue vs previous month
- Absolute and relative MoM change
- Ranking of SKUs by growth and decline

**Usage:**  
Helps detect sales drivers and problem products.
Used for assortment decisions, promotions, and root-cause analysis of revenue drops.

---

## 03. Logistics & ROI by warehouse

**Purpose:**  
Analyze the impact of warehouse-level logistics costs on profitability.

**Key metrics:**
- Revenue by WB warehouse
- Logistics costs
- Gross profit
- ROI

**Usage:**  
Used to evaluate efficiency of regional logistics and identify warehouses generating losses.
Supports operational decisions on fulfillment strategy and warehouse prioritization.

---

## 04. Drillthrough: SKU

**Purpose:**  
Enable deep-dive analysis for a selected SKU.

**Drillthrough details:**
- Sales dynamics
- Costs structure
- Profitability metrics
- Related dimensions (category, warehouse, time)

**Usage:**  
Used by analysts and category managers to investigate anomalies, sharp MoM changes,
and SKU-level performance issues.

---

## Navigation logic

- Global slicers (time period, product, category) affect all pages
- Drillthrough is available from summary pages to SKU-level details
- Pages are designed to move from high-level overview → detailed analysis

---

## Notes

- All calculations are based on a clean semantic model
- MoM logic relies on a dedicated calendar with stable month keys
- The report is optimized for analytical transparency and auditability

