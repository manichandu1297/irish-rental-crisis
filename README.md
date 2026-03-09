# 🏠 Irish Rental Crisis — Analysis & Prediction Platform

> An end-to-end data platform analysing Ireland's rental crisis, predicting future rent prices using machine learning, and delivering insights through an interactive dashboard and AI-powered chatbot.

---

## 📌 Project Overview

Ireland is experiencing one of the most severe rental crises in its history. Rents have increased over **60% in the past decade**, leaving renters, policymakers, and businesses without reliable, data-driven tools to understand pricing trends, identify affordable areas, or query housing policy.

This project builds a complete data platform that:
- Analyses historical rental trends across all Irish counties (2007–2025)
- Identifies the key drivers of rent increases by area
- Predicts future rental prices using machine learning
- Delivers actionable insights through an interactive Power BI dashboard
- Provides an AI-powered chatbot for querying Irish housing policy documents

**All data is sourced from official Irish public datasets — RTB, CSO, Data.gov.ie.**

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

## 🏗️ Project Architecture

```
Phase 1 — Data Collection & Cleaning
Phase 2 — SQL Database Design (PostgreSQL)
Phase 3 — Exploratory Data Analysis & Statistical Analysis
Phase 4 — Machine Learning (Rent Price Prediction)
Phase 5 — Power BI Dashboard (4 pages)
Phase 6 — Streamlit Web App (4 pages, deployed)
Phase 7 — RAG Chatbot (LangChain + ChromaDB on Irish housing PDFs)
```

---

## 📁 Repository Structure

```
irish-rental-crisis/
├── data/
│   ├── raw/                  # Original downloaded datasets (not tracked in Git)
│   ├── processed/            # Cleaned, merged master dataset
│   └── documents/            # PDFs for RAG chatbot (not tracked in Git)
├── notebooks/
│   ├── 01_data_collection.ipynb
│   ├── 02_data_cleaning.ipynb
│   ├── 03_eda_analysis.ipynb
│   ├── 04_feature_engineering.ipynb
│   └── 05_ml_model.ipynb
├── sql/
│   ├── schema.sql            # PostgreSQL schema definition
│   ├── load_data.sql         # Data loading scripts
│   └── analysis_queries.sql  # 15+ validated analytical queries
├── models/
│   ├── rent_predictor.pkl    # Trained XGBoost / Random Forest model
│   └── label_encoders.pkl    # Encoded categorical features
├── dashboard/
│   └── rental_dashboard.pbix # Power BI dashboard file
├── app/
│   ├── main.py               # Streamlit entry point
│   └── pages/
│       ├── 01_rent_predictor.py
│       ├── 02_area_explorer.py
│       ├── 03_affordability.py
│       └── 04_chatbot.py
├── rag/
│   ├── ingest.py             # PDF ingestion & chunking
│   ├── retriever.py          # RAG retrieval logic
│   └── vectorstore/          # ChromaDB vector store (not tracked in Git)
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
| Machine Learning | Scikit-learn, XGBoost, Joblib |
| BI Dashboard | Power BI Desktop |
| Web App | Streamlit, Streamlit Cloud |
| RAG Chatbot | LangChain, ChromaDB, OpenAI API |
| Version Control | Git, GitHub |

---

## 🤖 Machine Learning Model

- **Target variable:** Median rent (€) by county, property type, and number of bedrooms
- **Algorithms:** XGBoost (primary), Random Forest (benchmark)
- **Features:** Location, property type, bedrooms, year, quarter, population density, employment rate, housing completions, transport proximity
- **Success criteria:** R² ≥ 0.80, MAE within 10% of median rent

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

## 📈 Key Insights (Updated as Project Progresses)

> *(This section will be populated as analysis is completed)*

---

## 🚀 How to Run

### 1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/irish-rental-crisis.git
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
streamlit
langchain
chromadb
openai
```

---

## 📌 Project Status

| Phase | Status |
|---|---|
| Phase 1 — Data Collection & Cleaning | 🔄 In Progress |
| Phase 2 — SQL Database Design | ⏳ Pending |
| Phase 3 — EDA & Statistical Analysis | ⏳ Pending |
| Phase 4 — Machine Learning | ⏳ Pending |
| Phase 5 — Power BI Dashboard | ⏳ Pending |
| Phase 6 — Streamlit App | ⏳ Pending |
| Phase 7 — RAG Chatbot | ⏳ Pending |

---

## 👤 Author

**Mani Chandu**
MSc Data Analytics | Based in Ireland
[LinkedIn](#) | [GitHub](#)

> Built as a portfolio project demonstrating end-to-end data engineering, analysis, machine learning, and AI capabilities using real Irish public data.

---

## 📄 Licence

This project uses publicly available data from RTB, CSO, and Data.gov.ie.
All analysis and code is original work. Data sources are credited throughout.
