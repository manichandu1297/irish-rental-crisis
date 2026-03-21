# 🏠 Irish Rental Crisis — Analysis & Prediction Platform

> An end-to-end data platform analysing Ireland's rental crisis, predicting rent prices using machine learning, forecasting future trends, and delivering insights through an interactive dashboard and AI-powered chatbot.

---

## 📌 Project Overview

Ireland is experiencing one of the most severe rental crises in its history. Rents have increased over **60% in the past decade**, leaving renters, policymakers, and businesses without reliable, data-driven tools to understand pricing trends, identify affordable areas, or query housing policy.

This project builds a complete data platform that:
- Analyses historical rental trends across all Irish counties (2008–2025)
- Identifies the key drivers of rent increases by area
- Predicts monthly rent using a Random Forest model (R² = 0.978, MAE = €54)
- Forecasts future rent trends using Facebook Prophet
- Delivers actionable insights through an interactive Power BI dashboard
- Provides an AI-powered chatbot for querying Irish housing policy documents

**All data is sourced from official Irish public datasets — RTB and CSO PxStat.**

---

## 🎯 Target Stakeholders

| Stakeholder | Use Case |
|---|---|
| Renters | Find affordable areas, understand rent trends |
| Immigrants & Newcomers | Navigate the rental market with data |
| RTB / Dept. of Housing | Evidence-based policy decisions |
| Local Councils | Monitor housing pressure by area |
| Property Investors | Identify emerging rental markets |
| Researchers | Access clean, structured Irish rental data |

---

## 📊 Data Sources

| Source | Dataset | Coverage |
|--------|---------|----------|
| RTB / CSO PxStat | RIQ02 — Quarterly Rent Index | 2015–2025 |
| RTB / CSO PxStat | RIA02 — Annual Rent Index | 2008–2024 |
| CSO PxStat | HAP10 — HAP Properties by Local Electoral Area | 2015–2022 |
| CSO PxStat | TRS17 — Median Landlord Income by Local Authority | 2019 |
| CSO PxStat | TRS18 — Median Landlord Income by Local Electoral Area | 2019 |
| CSO PxStat | TRS21 — Rent as % of Disposable Income by Local Authority | 2019 |
| CSO PxStat | TRS22 — Rent as % of Disposable Income by Local Electoral Area | 2019 |
| CSO PxStat | FY001 — Population by County | Census 2011, 2016, 2022 |

---

## 🏗️ Project Architecture

```
Phase 1 — Data Collection & Ingestion
Phase 2 — Data Cleaning & Combining
Phase 3 — EDA & Statistical Analysis
Phase 4 — Feature Engineering & Preprocessing
Phase 5 — SQL Warehouse & Business Queries
Phase 6 — Machine Learning (Rent Prediction)
Phase 7 — Time Series Forecasting
Phase 8 — Power BI Dashboard
Phase 9 — Streamlit Web App
Phase 10 — RAG Chatbot
```

---

## 📁 Repository Structure

```
irish-rental-crisis/
├── data/
│   ├── raw/                          # Original downloaded datasets (not tracked in Git)
│   ├── processed/                    # Cleaned, combined datasets
│   └── documents/                    # PDFs for RAG chatbot (not tracked in Git)
├── notebooks/
│   ├── 01_data_collection.ipynb      # Load and inspect all 8 raw datasets
│   ├── 02_data_cleaning.ipynb        # Clean, standardise, combine, export 4 clean CSVs
│   ├── 03_eda_analysis.ipynb         # 31 plots, 12 sections, key rental crisis insights
│   ├── 04_feature_engineering.ipynb  # Encode, scale, engineer features, export model-ready dataset
│   ├── 05_sql_warehouse.ipynb        # PostgreSQL schema, 4 views, 12 business queries
│   ├── 06_ml_model.ipynb             # Linear Regression, Random Forest, XGBoost — RF wins
│   └── 07_forecasting.ipynb          # Prophet + ARIMA rent forecasting 2025–2027
├── models/
│   └── rent_predictor.pkl            # Trained Random Forest model (R² = 0.978)
├── dashboard/
│   └── rental_dashboard.pbix         # Power BI dashboard file
├── app/
│   ├── main.py                       # Streamlit entry point
│   └── pages/
│       ├── 01_rent_predictor.py
│       ├── 02_area_explorer.py
│       ├── 03_affordability.py
│       └── 04_chatbot.py
├── rag/
│   ├── ingest.py                     # PDF ingestion & chunking
│   ├── retriever.py                  # RAG retrieval logic
│   └── vectorstore/                  # ChromaDB vector store (not tracked in Git)
├── requirements.txt
└── README.md
```

---

## 🔧 Technology Stack

| Layer | Tools |
|---|---|
| Data Processing | Python, Pandas, NumPy |
| Visualisation | Matplotlib, Seaborn, Plotly |
| Database | PostgreSQL, SQLAlchemy |
| Machine Learning | Scikit-learn, XGBoost, Random Forest, Joblib |
| Forecasting | Facebook Prophet, ARIMA |
| BI Dashboard | Power BI Desktop |
| Web App | Streamlit, Streamlit Cloud |
| RAG Chatbot | LangChain, ChromaDB, OpenAI API |
| Version Control | Git, GitHub |

---

## 🤖 Machine Learning Model

- **Task:** Predict monthly rent (€) given location, property type, bedrooms, and time period
- **Best model:** Random Forest — R² = 0.978, MAE = €54
- **Algorithms compared:** Linear Regression (baseline), Random Forest, XGBoost
- **Key features:** Location (target encoded), Year, Property Type, Bedrooms, Dublin flag
- **Target variable:** Log-transformed monthly rent, converted back to euros for evaluation
- **Success criteria:** R² ≥ 0.80, MAE within 10% of median rent — both achieved

---

## 📈 Time Series Forecasting

- **Models:** Facebook Prophet (primary), ARIMA (benchmark)
- **Coverage:** National average + top 5 counties by rent level
- **Forecast horizon:** 2025–2027
- **Input data:** RTB annual rent index back to 2008 — 16 years of history
- **Output:** Predicted rent with confidence intervals

---

## 💬 RAG Chatbot

An AI chatbot powered by **LangChain + ChromaDB** trained on official Irish housing policy documents:
- RTB Annual Reports (2019–2023)
- Housing for All — Government Plan
- Daft.ie Rental Reports
- RTB Rent Pressure Zone guidelines

Ask it questions like:
> *"What are the current Rent Pressure Zone rules in Dublin?"*
> *"What does Housing for All say about social housing targets?"*

**Success criteria:** Correctly answers 8/10 test queries with cited source documents.

---

## 📈 Key Insights

- National average rent grew **70%+ from 2015 to 2025**
- Dublin rents are **~40% above the national average** — and the gap is still widening
- **Q3 (Jul–Sep)** is consistently the most expensive quarter — academic calendar effect
- **HAP properties grew every year** from 2015 to 2022 — state support demand is accelerating
- Counties above the **30% housing stress threshold**: Dublin City, Dún Laoghaire-Rathdown, Fingal, South Dublin
- **Location alone explains 73% of rent variation** in the Random Forest model
- COVID caused a short dip in 2020 — **every location exceeded pre-COVID rent levels by 2022**

---

## 🚀 How to Run

### 1. Clone the repository
```bash
git clone https://github.com/manichandu1297/irish-rental-crisis.git
cd irish-rental-crisis
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Run the Streamlit app locally
```bash
streamlit run app/main.py
```

### 4. View the deployed app
> 🔗 [Live App on Streamlit Cloud](#) *(link added after deployment)*

---

## 📋 Requirements

```
pandas
numpy
matplotlib
seaborn
plotly
scikit-learn
xgboost
joblib
sqlalchemy
psycopg2-binary
prophet
statsmodels
streamlit
langchain
chromadb
openai
```

---

## 📌 Project Status

| Phase | Status |
|---|---|
| Phase 1 — Data Collection & Ingestion | ✅ Complete |
| Phase 2 — Data Cleaning & Combining | ✅ Complete |
| Phase 3 — EDA & Statistical Analysis | 🔄 In Progress |
| Phase 4 — Feature Engineering & Preprocessing | ⏳ Pending |
| Phase 5 — SQL Warehouse & Business Queries | ⏳ Pending |
| Phase 6 — Machine Learning (Rent Prediction) | ⏳ Pending |
| Phase 7 — Time Series Forecasting | ⏳ Pending |
| Phase 8 — Power BI Dashboard | ⏳ Pending |
| Phase 9 — Streamlit App | ⏳ Pending |
| Phase 10 — RAG Chatbot | ⏳ Pending |

---

## 👤 Author

**Mani Chandu**
MSc Data Analytics | Based in Ireland
[LinkedIn](#) | [GitHub](#)

> Built as a portfolio project demonstrating end-to-end data engineering, analysis, machine learning, forecasting, and AI capabilities using real Irish public data.

---

## 📄 Licence

This project uses publicly available data from RTB and CSO PxStat.
All analysis and code is original work. Data sources are credited throughout.
