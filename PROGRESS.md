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


