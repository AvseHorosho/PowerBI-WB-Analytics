# PowerBI-WB-Analytics

Wildberries analytics project built in Power BI.
## Business Context

This project represents an analytical Power BI report built for a Wildberries (WB) marketplace seller.
The primary goal is to analyze financial performance, identify revenue drivers and losses, and detect inefficient products and logistics operations.

The report is designed to support business decisions in the following areas:
- profitability control
- operational efficiency
- SKU-level performance monitoring
- warehouse and logistics optimization


## Data Sources & Model

The report is built on transactional Wildberries sales and realization data for the period:
**December 2021 – May 2022**.

Key data layers:
- sales and realization facts
- commissions and logistics costs
- product attributes (SKU, supplier article)
- warehouse and regional dimensions
- calendar dimension with Month-over-Month logic

The semantic model follows a clean star-schema approach with:
- centralized fact tables
- role-playing calendars for MoM and drillthrough scenarios
- explicit relationships to avoid ambiguity in time-based calculations

The model is optimized for analytical queries and drillthrough navigation.


## Key Analytical Features

- **Financial overview**
  - revenue, gross profit, ROI
  - core cost components (WB commission, logistics, cost of goods)

- **Month-over-Month (MoM) analysis**
  - identification of growth and decline leaders
  - comparison with previous periods
  - ranking of SKUs by revenue delta

- **SKU drillthrough**
  - detailed product-level analysis
  - transition from summary KPIs to individual SKU performance

- **Logistics & warehouse efficiency**
  - profitability and ROI by warehouse
  - detection of unprofitable logistics directions
  - support for warehouse-level optimization decisions


## Navigation & User Experience

The report is structured for different business roles:
- executives (high-level financial overview)
- analysts (MoM dynamics and comparisons)
- category and product managers (SKU drillthrough)

Interactive features include:
- synchronized slicers
- cross-filtering between visuals
- drillthrough navigation from summary pages to detailed views

Screenshots of key report pages and their analytical purpose are provided in the `docs/screenshots` section.


## Power BI Report Access

Due to GitHub file size limitations, PBIX files are not stored directly in this repository.

The full Power BI report can be accessed here:
- **Google Drive (PBIX files):**
  https://drive.google.com/drive/folders/1zoEV2jGBrZNeaEx8QKa3gH0N4XxLiHag

The report is also published to **Power BI Service (private workspace)** for interactive viewing.

## Project scope
- Month-over-Month (MoM) sales analysis
- Leaders of growth and decline
- Drillthrough analysis by SKU
- Clean semantic model and DAX measures

## Screenshots

See key report pages here: [docs/screenshots](docs/screenshots)

Preview:
- Finance overview: ![Finance](docs/screenshots/01_finance_overview.jpg)
- MoM leaders: ![MoM](docs/screenshots/02_mom_leaders.jpg)
- Logistics ROI by warehouse: ![Logistics ROI](docs/screenshots/03_logistics_roi_by_warehouse.jpg)
- Drillthrough SKU: ![Drillthrough SKU](docs/screenshots/04_drillthrough_sku.jpg)

## Tech stack
- Power BI Desktop
- DAX
- Power Query (M)
- Data modeling

## Repository structure
- `pbix/` — Power BI report files
- `docs/` — business & technical documentation
- `screenshots/` — report screenshots

## Notes
PBIX files are intended to be opened locally in Power BI Desktop.
