# Vancouver 311 Service Requests Dashboard

An end-to-end analytics pipeline built on the [City of Vancouver's Open Data Portal](https://opendata.vancouver.ca/explore/dataset/3-1-1-service-requests/), analyzing 10,000+ resident service requests to surface operational trends across Vancouver's city departments and neighbourhoods.

![Dashboard Screenshot](screenshots/dashboard.png)

---

## Business Questions

This project was designed to answer four operational questions a city analyst or public sector stakeholder might ask:

1. **What are residents calling about most?** — Identify the highest-volume request types to understand where city resources are most in demand
2. **How does request volume trend over time?** — Detect seasonal patterns and month-over-month changes in service demand
3. **Which neighbourhoods generate the most requests?** — Pinpoint geographic hotspots for service delivery
4. **Which departments take the longest to close requests?** — Identify potential bottlenecks in city service delivery

---

## Key Findings

- **Water infrastructure dominates requests** — Water Leak Cases are the single most common request type, with Water Meter Readings and Water Service Line Turn-Offs also in the top three. This points to aging water infrastructure as a key pressure point for the city
- **Request volume peaks in January–February** — A clear seasonal pattern emerges, likely driven by winter weather and cold-weather infrastructure stress
- **Downtown generates the highest request volume** — Followed by Kensington-Cedar Cottage and Grandview-Woodland
- **PDS Planning and PR Park Operations have the longest closure times** — Averaging over 100 days, significantly above other departments, suggesting resource or process constraints worth investigating

---

## Tech Stack

| Layer | Tool |
|---|---|
| Data Ingestion | Python (`requests`, `pandas`) |
| Data Cleaning | Python (`pandas`) in Jupyter Notebooks |
| Visualization | Microsoft Power BI Desktop |
| Version Control | Git / GitHub |
| Data Source | Vancouver Open Data Portal (Opendatasoft API) |

---

## Project Structure

```
vancouver-311-analytics/
│
├── data/
│   ├── raw_311.csv          # Raw API pull (gitignored)
│   └── clean_311.csv        # Cleaned, analysis-ready dataset
│
├── notebooks/
│   ├── 01_ingest.ipynb      # Pulls data from Vancouver Open Data API
│   └── 02_clean.ipynb       # Cleans, transforms, and exports CSV
│
├── powerbi/
│   └── vancouver_311.pbix   # Power BI report file
│
├── screenshots/
│   └── dashboard.png        # Dashboard preview
│
└── README.md
```

---

## How to Run This Project

### Prerequisites
- Python 3.x
- Jupyter Notebook (via VS Code or standalone)
- Microsoft Power BI Desktop

### Setup

1. Clone the repository:
```bash
git clone https://github.com/chestermew/vancouver-311-analytics.git
cd vancouver-311-analytics
```

2. Install dependencies:
```bash
pip install pandas requests jupyter
```

3. Run the notebooks in order:
   - `notebooks/01_ingest.ipynb` — fetches data from the Vancouver Open Data API
   - `notebooks/02_clean.ipynb` — cleans and exports `data/clean_311.csv`

4. Open `powerbi/vancouver_311.pbix` in Power BI Desktop and refresh the data source to point to your local `clean_311.csv`

---

## Data Notes

- **Source:** [City of Vancouver Open Data Portal — 3-1-1 Service Requests (2022–present)](https://opendata.vancouver.ca/explore/dataset/3-1-1-service-requests/)
- **Volume:** 10,000 records pulled via API (2022–2024)
- **Null local_area values:** ~8.6% of records have no neighbourhood — this is a known data quality issue documented by the City, where certain request types have address data withheld for privacy reasons
- **Open requests:** A small number of records have no close date, indicating requests still in progress at time of extraction. These are retained in the dataset and flagged via the `is_closed` field
- **Obsolete request types:** Call types prefixed with `ZZ – OLD` refer to deprecated categories and have been excluded from visuals

---

## License

Data sourced under the [City of Vancouver Open Data Licence](https://opendata.vancouver.ca/pages/licence/).
