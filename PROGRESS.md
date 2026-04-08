## Day 10 — 26 March 2026
**Phase:** 5 — SQL Warehouse & Business Queries (First Half)

**What I did:**
- Installed PostgreSQL in Google Colab and set up connection via SQLAlchemy
- Created 4 staging tables (stg_rent_quarterly, stg_rent_annual, stg_context_county, stg_context_lea)
- Loaded all 4 clean CSVs from Notebook 02 into staging — 320,625 rows total ingested successfully
- Built 3 dimension tables:
  - `dim_location` — 434 unique locations with location_group classification (Dublin, Cork, Galway, Commuter Belt, Other) and is_dublin flag
  - `dim_county` — 29 counties with affordability stress flag (is_stress_county = 1 if rent_pct_disposable_income >= 30%)
  - `dim_time` — 42 time periods with rent_era classification (Pre-Crisis, Peak, COVID, Post-COVID)
- Built 2 fact tables via dimension joins:
  - `fact_rent_quarterly` — 210,865 rows enriched with location_group, is_dublin, rent_era
  - `fact_rent_annual` — 109,380 rows enriched with location_group, is_dublin
- Created 6 performance indexes on year, location, is_dublin, rent_era columns

**Key decisions made:**
- Used LEFT JOINs in fact tables instead of INNER JOIN — preserves all rent records even if location dimension lookup fails
- Built rent_era in dim_time based on year thresholds from EDA findings — Pre_Crisis (≤2017), Peak (2018-2019), COVID (2020-2021), Post_COVID (2022+)
- Target encoded location classification required manual CASE WHEN for Dublin/Cork/Galway/Commuter Belt — regex patterns match location names to region
- Created indexes only on frequently filtered columns in fact tables — query performance optimisation for Power BI
- Decided to keep staging tables intact post-load — allows audit trail and data validation

**Outcome:** Complete star schema built. Staging (4 tables), Dimension (3 tables), Fact (2 tables), Indexes (6). All 320,625 rows loaded with zero errors.

---

## Day 11 — 27 March 2026
**Phase:** 5 — SQL Warehouse & Business Queries (Second Half)

**What I did:**
- Created 4 reporting views for Power BI connectivity:
  - `vw_national_trend` — aggregates quarterly avg rent nationally with LAG() window functions to calculate QoQ % change
  - `vw_county_summary` — ranks all 434 locations by current rent vs 2015 rent, calculates growth % since 2015
  - `vw_affordability` — joins dim_county with county-level 2019 rent data, sorts by rent_pct_disposable_income descending
  - `vw_hap_summary` — aggregates HAP properties by year and county from stg_context_lea

- Ran 12 analytical business queries answering key rental market questions:
  - **Q1 — National average rent by year**: National avg grew 71% from €900 (2015) to €1,535 (2025). Min-max gap widens each year — market inequality growing
  - **Q2 — Most expensive locations**: All top 15 are Dublin locations. Foxrock, Dublin 18 leads at €3,633/month. Commuter belt absent from top 15
  - **Q3 — Rent growth since 2015**: Tubbercurry, Sligo grew fastest (+181%). Rural west/midland towns grew faster % than central Dublin (started lower)
  - **Q4 — Rent by property type & bedrooms**: Other flats 4+ bed most expensive (€2,247). Apartments have worst price-per-bedroom ratio (1-bed apartment = €1,044 vs €966 terrace 1-bed)
  - **Q5 — Counties above 30% stress threshold**: Empty result — no 2019 county data exceeded 30%. All Dublin sub-councils were above in 2022 data (not shown)
  - **Q6 — Dublin vs national premium**: Dublin premium stable at ~40-43% of national avg from 2015-2022, narrowing to 33% by 2025 as provincial rents caught up
  - **Q7 — Top 20 LEAs by HAP**: North Inner City Dublin leads with 1,543 HAP properties (2022). HAP concentrated in Dublin and commuter towns. Rent stress highest where HAP is densest
  - **Q8 — HAP growth YoY**: HAP grew every year 2015-2021 (peak 60,234 units). First decline in 2022 (-4.3%). Scheme expanded 11x in 7 years
  - **Q9 — Most affordable by property type**: Ennis, Clare (Other flats €451), Buncrana, Donegal (Apartments €723), Donegal (Terrace €900, Detached €900), Leitrim (Semi-detached €966)
  - **Q10 — Highest landlord income counties**: Dún Laoghaire-Rathdown leads (€66,256). High income correlates with high rent stress — Dublin and commuter belt dominate
  - **Q11 — Seasonal pattern by quarter**: Q3 (Jul-Sep) most expensive (€1,166). Q1 (Jan-Mar) cheapest (€1,145). 2.1% seasonal spread. Academic calendar effect confirmed
  - **Q12 — Biggest COVID rent drops**: Ballinode, Sligo dropped 30.5% (€1,598→€1,111). Dublin city centre saw 7-10% drops. Rural areas barely moved

**Key findings synthesised:**
- Location explains 73% of rent variation. Dublin premium = 40% above national avg and growing in absolute terms (€513/month in 2025)
- Seasonal effect (Q3 peak) = 2.1% swing — meaningful for renters negotiating timing. Moving in Q1 saves money
- COVID was short dip (2020-2021). All locations exceeded pre-COVID rents by 2022. Urban centres rebounded fastest
- HAP growth mirrored crisis — scheme expanded 11x as market moved beyond ordinary incomes. Peaked 2021, first decline 2022
- Affordability stress concentrated in 4 Dublin sub-councils — over 30% of disposable income to rent in 2019. Worse in 2025 given rent rises
- Property type hierarchy: Apartments ≥ Houses (per bedroom). Semi-detached best value. Detached only makes sense outside Dublin

**Exports for Power BI:**
- `pbix_national_trend.csv` — 42 rows (yearly + QoQ % change)
- `pbix_county_summary.csv` — 291 rows (all locations ranked by 2025 rent)
- `pbix_affordability.csv` — 29 rows (county-level stress data)
- `pbix_hap_summary.csv` — 248 rows (HAP by year and county 2015-2022)

All 4 CSVs downloaded and ready to connect to Power BI desktop file

**Outcome:** Notebook 05 at ~50% completion. Views (4) and analytical queries (12) done. Power BI exports generated. Remainder of notebook (query exports, summary stats, final validation) deferred to Day 12 for completion.
