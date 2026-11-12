# Election Results and Voter Behaviour: An Interactive D3.js Analysis of Indian Elections (1952–2024)
## Bharat Electoral Analytics Dashboard — ECI Statistical Observatory

An academic and portfolio-level Big Data Visualization (BDV) platform analyzing longitudinal Indian Lok Sabha General Election results, electoral competitiveness, gender participation convergence, and coalition politics from 1951–52 to 2024.

---

## 1. Overview & Objectives

The **Bharat Electoral Analytics Dashboard** provides an interactive web-based visualization system based on canonical Election Commission of India (ECI) statistical reports.

Key analytical dimensions:
- **Longitudinal Turnout Trajectories (1951–2024):** 18 Lok Sabha elections tracking total electors, votes polled, and turnout percentage.
- **Gender Convergence & Crossover:** Historical male vs. female turnout, visualizing the reversal from an 11.79 percentage-point female turnout deficit in 1971 to the historic female crossover in 2019 and parity in 2024.
- **Political Party & Alliance Performance:** Seat conversion vs. national vote share % with a prominent 272-seat majority benchmark.
- **Macro-Regional Political Alignment:** Analysis across 6 geographical zones (North, South, East, West, Central, Northeast India) comparing NDA, INDIA, and regional party formations.
- **State-Level Demographics & Geo-Spatial Cartography:** Interactive D3.js India choropleth map with verified GeoJSON boundaries (36 States & UTs) and toggleable India Tile Cartogram.
- **Empirical Findings & Data Explorer:** Live multi-variable filtering, row searching, column sorting, reconciliation audits, and direct CSV exports.

---

## 2. Project Architecture & Directory Structure

```
election bdv/
├── assets/
│   └── geojson/
│       ├── india_states.geojson    # Verified 36-State GeoJSON polygon boundaries
│       └── india.json              # TopoJSON archive
├── data/
│   ├── raw/                        # Canonical source CSV files
│   │   ├── national_series.csv     # 18 Lok Sabha general elections (1951-52 to 2024)
│   │   ├── party_performance.csv   # Party seats and vote shares
│   │   ├── regional_shifts.csv     # 6 Macro regions seat distributions & turnout
│   │   └── state_demographics.csv  # 36 States/UTs participation, demographics, margins
│   └── processed/                  # Normalized and seat-reconciled datasets (543 seats)
│       ├── national_series.csv
│       ├── party_performance.csv
│       ├── regional_shifts.csv
│       └── state_demographics.csv
├── notebooks/
│   ├── data_cleaning.ipynb         # Python & Pandas validation and reconciliation pipeline
│   └── data_analysis.ipynb         # Exploratory data analysis (EDA) & statistical visualizations
├── records/                        # Original source backup
├── src/
│   ├── css/
│   │   └── style.css               # Base stylesheet
│   └── js/
│       └── main.js                 # Shared frontend entry point
├── bharat_electoral_analytics_dashboard.html # Core production frontend
├── index.html                      # Web server & deployment entry point (synchronized)
├── package.json                    # Project configuration & npm scripts
├── .gitignore                      # Git ignore specifications
└── README.md                       # Comprehensive documentation
```

---

## 3. Dataset Schemas & Reconciliation Audit

### A. `national_series.csv` (18 Records, 1951–52 to 2024)
- `election_year`: ECI edition label (`1951-52`, `1957`, ..., `2024`).
- `electors`: Total registered electors on electoral rolls (97.98 Cr in 2024).
- `votes`: Total valid votes polled (64.64 Cr in 2024).
- `turnout_pct`: Overall voter participation percentage (peak: 67.40% in 2019; 66.10% in 2024).
- `male_turnout_pct` & `female_turnout_pct`: Gender-disaggregated turnout (`NA` preserved for 1951–1967 as ECI did not publish gender breakdowns prior to 1971).
- `winner`: Formation forming government.

### B. `party_performance.csv` (28 Major Parties & Blocs)
- `party`: Full name and party acronym.
- `alliance`: Coalition alignment (`NDA`, `INDIA`, `Unaligned`, `Mixed`).
- `seats_won`: Parliamentary seats won.
- `vote_share_pct`: National vote percentage.
- **Audit Note:** The supplied raw file listed 25 seats for `Others & Independents` (summing to 544). The official 2024 Lok Sabha total is 543 seats (Others = 24 seats). The dataset reconciliation pipeline accurately reconciled this sum to 543 seats.

### C. `regional_shifts.csv` (6 Macro-Geographical Zones)
- `region`: North (126 seats), South (131 seats), East (118 seats), West (103 seats), Central (40 seats), Northeast (25 seats).
- `total_seats`: Exactly 543 seats.
- `nda_seats`: 293 seats.
- `india_seats`: 234 seats.
- `other_seats`: 16 seats.
- `avg_turnout_pct`: Regional turnout percentage (peak: Northeast India at 77.12%).

### D. `state_demographics.csv` (All 36 States & Union Territories)
- `state_ut`: 28 States and 8 Union Territories.
- `seats`: State parliamentary seats (sum: 543).
- `turnout_pct`: Total voter turnout percentage.
- `female_turnout_pct` & `male_turnout_pct`: State-level gender participation rates.
- `youth_elector_share_pct`: Percentage of electors aged 18–29.
- `avg_victory_margin_pct`: Electoral competitiveness index (lowest: Chandigarh 0.56%, highest: Tripura 36.80%).

---

## 4. Visualizations & Analytical Features

1. **KPI Summary Cards:** Live updates for Turnout, Lok Sabha Seats scope, Elector counts, and Winning Coalition based on active filters.
2. **Historical Line Chart (D3.js):** 3-series trajectory (Overall, Male, Female turnout) spanning 18 elections with clickable year markers.
3. **Party Performance Bar Chart (D3.js):** Horizontal bar chart color-coded by alliance, switchable between Seats won and Vote Share %, with a prominent **272 Majority Benchmark** line.
4. **Interactive India Map (D3.js & GeoJSON):**
   - High-fidelity SVG boundary choropleth using `assets/geojson/india_states.geojson`.
   - Dual view toggle: Switch between **Geographic Boundaries** and **Proportional India Tile Cartogram**.
   - Metric switcher: Total Turnout, Female Turnout, Male Turnout, Youth Elector Share, and Victory Margin.
   - Click to select and focus state metrics across the entire dashboard.
5. **Regional Grouped Bar Chart (D3.js):** Alliance seat shares alongside average regional turnout diamonds.
6. **Dynamic Insights Generator:** Synthesizes empirical takeaways on gender parity, youth turnout, and regional coalition dynamics.
7. **Data Explorer & Audit Hub:** Search across records, sort columns, view seat reconciliation, and download raw or filtered CSVs.

---

## 5. Getting Started & Running Locally

### Option 1: Live Web Server (Recommended)
```bash
npm install
npm start
```
The application will be served at `http://localhost:3000` (or `http://localhost:5000`), serving [index.html](file:///d:/projects/election%20bdv/index.html) and [bharat_electoral_analytics_dashboard.html](file:///d:/projects/election%20bdv/bharat_electoral_analytics_dashboard.html).

### Option 2: Python Built-In HTTP Server
```bash
python -m http.server 8080
```
Open `http://localhost:8080` in your web browser.

### Option 3: Direct File Protocol (`file:///`)
Double-click [bharat_electoral_analytics_dashboard.html](file:///d:/projects/election%20bdv/bharat_electoral_analytics_dashboard.html). The dashboard has built-in offline fallbacks and zero-CORS tile cartogram geometry, ensuring that all charts and features render immediately even without a local web server.

---

## 6. Data Cleaning & Analysis Notebooks

To run the data cleaning and exploratory analysis pipelines:
```bash
jupyter notebook notebooks/data_cleaning.ipynb
jupyter notebook notebooks/data_analysis.ipynb
```

---

## 7. Deployment Instructions

### Deploy to Vercel
1. Install Vercel CLI: `npm i -g vercel`
2. Run `vercel` from the project root (`d:\projects\election bdv`).
3. Vercel automatically detects `index.html` and static assets.

### Deploy to GitHub Pages
1. Push the repository to GitHub.
2. Go to **Settings** > **Pages**.
3. Select the branch (e.g. `main`) and root folder `/`.
4. The dashboard will be live at `https://<username>.github.io/<repo-name>/`.
