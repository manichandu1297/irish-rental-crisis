# 📅 Project Progress Log

## Day 1 — 08 March 2026
**Phase:** Project Setup & Planning  

**What I did:**
- Read and understood the full project scope
- Defined aim, objectives, stakeholders, and deliverables
- Researched available Irish rental datasets — RTB, CSO PxStat, Data.gov.ie
- Created GitHub repository with README and Python .gitignore

**Key decisions made:**
- Chose RTB/CSO as primary data sources — official, credible, publicly available
- Defined 7 project phases from data collection through to RAG chatbot
- Selected real-world Irish data only — no synthetic or Kaggle datasets

**Outcome:** Project foundation established. Repository live on GitHub.

## Day 2 — 09 March 2026
**Phase:** 1 — Data Collection (Core Rent Datasets)

**What I did:**
- Navigated CSO PxStat and understood the RTB dataset catalogue
- Downloaded RIQ02 — RTB quarterly rent index (2015–2025)
- Downloaded RIA02 — RTB annual rent index (2008–2024)
- Ran full inspection on both datasets — shape, nulls, duplicates, date range, categorical value counts
- Built and documented Notebook 01 in Google Colab

**Key decisions made:**
- Skipped RIH02 (half-yearly) — adds no value over RIQ02 which is more granular
- Filtered RIQ02 to 2015 onwards to stay within CSO 1M cell download limit
- Confirmed 73% nulls in RIQ02 are structural — RTB only reports rent where enough tenancies exist
- Dropped STATISTIC Label and UNIT columns — single value, no analytical use
- Added Dublin rent trend plots as sense checks against published RTB figures

**Outcome:** Two core rent datasets loaded, inspected, and sense-checked. Notebook 01 structure established.

## Day 3 — 12 March 2026
**Phase:** 1 — Data Collection (Complete)

**What I did:**
- Finalised and documented Notebook 01 — Data Collection & Ingestion
- Downloaded remaining 6 datasets — HAP10, TRS17, TRS18, TRS21, TRS22, FY001
- Ran full inspection on all 8 datasets — shape, nulls, duplicates, value counts
- Confirmed all datasets are structurally sound and ready for cleaning

**Key decisions made:**
- Filled HAP10 nulls with 0 — confirmed as HAP scheme rollout gap in 2015/2016
- Skipped employment by county — not published at county level on CSO PxStat
- Kept TRS datasets despite 2019 only — last pre-COVID stable baseline year
- Used Census years 2011, 2016, 2022 for population

**Outcome:** All 8 datasets collected and inspected. Notebook 01 complete and pushed to GitHub.

## Day 4 — 13 March 2026
**Phase:** 2 — Data Cleaning & Combining

**What I did:**
- Created Notebook 02 — Data Cleaning & Combining in Google Colab
- Cleaned RIQ02 and RIA02 — dropped redundant columns, renamed VALUE, removed structural nulls
- Extracted Year and Quarter number from Quarter string in RIQ02
- Cleaned HAP10 — filled 47 nulls with 0, split LEA column into Area and County

**Key decisions made:**
- Dropped structural nulls from RIQ02 and RIA02 — these are expected gaps, not data errors
- Split LEA column into Area and County across HAP10, TRS18, TRS22 — format was "Area, County"
- Kept only Median Total Gross Income from TRS17/18 — more informative than rental income alone

**Outcome:** Core rent datasets cleaned. HAP10 and LEA datasets restructured and ready.

---

## Day 5 — 14 March 2026
**Phase:** 2 — Data Cleaning & Combining

**What I did:**
- Cleaned TRS17, TRS18, TRS21, TRS22 — filtered to relevant statistics only
- Stripped council suffixes from county names in TRS17 and TRS21
- Fixed truncated county names — Limerick and Waterford were cut short after suffix removal
- Averaged Cork and Galway city/county entries to get one value per county
- Cleaned FY001 — filtered to Both sexes, dropped State row, kept 26 counties × 3 census years

**Key decisions made:**
- Kept Median Rent % and 30% threshold from TRS21/22 — direct affordability measures
- Averaged Cork and Galway — CSO reports city and county separately but FY001 treats them as one
- Used 2022 census population only — most recent, closest to rent data timeframe

**Outcome:** All 8 datasets fully cleaned and standardised. Zero nulls across all datasets confirmed.

---

## Day 6 — 15 March 2026
**Phase:** 2 — Data Cleaning & Combining (Complete)

**What I did:**
- Built county level context dataset — joined TRS17, TRS21, and FY001 population on County
- Split Dublin population equally across 4 sub-councils — FY001 only has one Dublin entry
- Built LEA level context dataset — joined HAP10, TRS18, TRS22 on LEA
- Validated both context datasets — zero nulls, correct row counts, clean column names
- Exported all 4 clean datasets to /content/

**Key decisions made:**
- Split Dublin population equally across Dublin City, Dún Laoghaire-Rathdown, Fingal, South Dublin
- Kept 29 county entries in county context — preserves Dublin sub-council granularity
- Exported 2 rent files and 2 context files separately — different granularities should not be merged

**Outcome:** 4 clean datasets exported — rent_quarterly_clean.csv (210,865 rows), rent_annual_clean.csv (109,380 rows), context_county_clean.csv (29 rows), context_lea_clean.csv (1,328 rows). Notebook 02 complete.

---

## Day 7 — 19 March 2026
**Phase:** 3 — EDA & Statistical Analysis

**What I did:**
- Built Notebook 03 — EDA & Statistical Analysis in Google Colab
- Analysed national rent trends from 2008 to 2025 — quarterly and annual views
- Explored county level rankings, Dublin premium, and commuter belt patterns
- Analysed rent by property type and bedroom count including cost per bedroom
- Calculated rent growth % by county since 2015 and since 2008
- Investigated COVID impact — which counties dropped most and recovered fastest
- Identified seasonal patterns across Q1–Q4
- Ran affordability analysis using context datasets — 30% stress threshold by county
- Analysed HAP demand growth 2015–2022 at national, county, and LEA level
- Built correlation matrix across all county level features

**Key decisions made:**
- Used top 15 only for growth and COVID drop charts — full list was unreadable
- Labelled only top 5 and bottom 5 points on scatter plots — avoids overlap
- Removed plt.savefig() — no need to save plots to disk
- Fixed YoY % change chart — 2022 bar was near-invisible, added value labels and minimum bar height
- Switched HAP 2015 vs 2022 chart to show value labels on small 2015 bars

**Key findings:**
- National average rent grew ~70% from 2015 to 2025
- Dublin is ~40% above the national average and the gap keeps widening
- Q3 (Jul–Sep) is consistently the most expensive quarter
- HAP demand grew every year without exception — state support is accelerating
- Location and population are the strongest correlators with rent level
- COVID caused a short dip in 2020 — all locations exceeded pre-COVID levels by 2022

**Outcome:** Notebook 03 complete with 31 plots and key findings summary. Ready for feature engineering.
---

## Day 8 — 21 March 2026
**Phase:** 4 — Feature Engineering & Preprocessing

**What I did:**
- Created Notebook 04 — Feature Engineering & Preprocessing in Google Colab
- Dropped Quarter column — redundant since Year and Q_Num already extracted
- Checked Value distribution — confirmed right skew, applied IQR capping and log transform
- Engineered Is_Dublin binary flag — EDA confirmed Dublin is a clear outlier
- Engineered Rent_Era grouping — Pre_Crisis, Peak, COVID, Post_COVID based on EDA findings
- Applied target encoding to Location — replaced with mean rent per location
- Applied one-hot encoding to PropertyType
- Applied ordinal encoding to Bedrooms and Rent_Era

**Key decisions made:**
- Used target encoding for Location instead of label encoding — label encoding assigns arbitrary alphabetical numbers which mean nothing to the model
- Dropped 79,728 aggregate rows where PropertyType = All property types and Bedrooms = All bedrooms — these are summary averages not real listings
- Dropped Is_Commuter — low correlation with target, arbitrary county boundary definition
- Bedroom mapping required fixing — actual values in data used different names than expected

**Outcome:** Encoding complete. Aggregate rows dropped. Dataset reduced from 210,865 to 131,137 clean rows. Feature set partially built.



