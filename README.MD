# 🛍️ H&M Global Retail Store Analytics Dashboard  

An interactive **business intelligence dashboard** built with **SQL** and **Tableau**, analyzing **4,000+ H&M stores worldwide**.  
This project combines **data engineering, geospatial queries, and visual storytelling** to uncover insights in **store formats, operations, and clustering trends**.  

---

## 📊 Project Overview  
This dashboard supports data-driven retail strategy across three key areas:  

- 📌 **Store Format Penetration** → Analyze Flagship, Standard, and Outlet distribution across markets  
- ⏰ **Weekend Operational Efficiency** → Open–close duration parsing to highlight extended shopping behavior  
- 📍 **Proximity-Based Store Clustering** → Geospatial insights on store density in top global hubs  

---

## ⚙️ Tech Stack  
- **SQL (MySQL Workbench)**  
  - Relational modeling & normalization (3NF)  
  - Geospatial queries → `ST_Distance_Sphere`  
  - Time-based calculations → `STR_TO_DATE`, `TIMEDIFF`  

- **Tableau (Desktop & Public)**  
  - Symbol maps, filters, parameters  
  - Interactive storytelling & annotations  

- **Data Source**  
  - [H&M Stores Dataset – Kaggle](https://www.kaggle.com/datasets/shivamb/hm-stores-dataset)  
  - [H&M Retail Store Analytics Tableau] (https://github.com/Han-Nguyen162/H-M-Retail-Store-Analytics/releases/tag/release-2025-08)

---

## 🧠 Key Business Insights  
- **Format Strategy**  
  - Flagship stores dominate **Japan, France, Korea** → brand-immersive experiences  
  - Standard & Outlet stores cluster in **developing regions** → cost-focused expansion  

- **Weekend Operations**  
  - **Madina, Mecca, Taif** average **28–29 weekend hours**, vs global ~22 → cultural/religious demand, staffing opportunities  

- **Store Clustering**  
  - **London, Tokyo, Paris** → **100+ store pairs within 10km**, enabling hyperlocal campaigns, shared resources, or consolidation  

---

## 📂 Repository Structure  
```bash
H-M-Global-Store-Dashboard/
├── sql/
│   ├── store_format_penetration.sql
│   ├── weekend_hours_actual.sql
│   └── store_clustering_query.sql
├── data/
│   ├── storeformatpenetration.csv
│   ├── openhours.csv
│   └── storeclustering_LL.csv
├── H&M_Dashboard.twbx
├── README.md
└── LICENSE
