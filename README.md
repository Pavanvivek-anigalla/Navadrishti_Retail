# How to Run This Project

### Step 1: Download the Project

- Click the green **Code** button on this GitHub repo and select **Download ZIP**
- Extract the ZIP file on your local machine

### Step 2: Download the Dataset

- Download the source data from [University of Leipzig - Abt-Buy Dataset]  https://dbs.uni-leipzig.de/files/datasets/Abt-Buy.zip
- Extract it -- you need these 3 CSV files:

| File | Description |
|---|---|
| `Abt.csv` | ABT Electronics product catalog |
| `Buy.csv` | Buy.com product catalog |
| `abt_buy_perfectMapping.csv` | Ground-truth product mappings |

### Step 3: Open Snowflake and Create a Workspace

1. Log in to your **Snowflake account** (you need `ACCOUNTADMIN` role or equivalent)
2. Make sure you have a warehouse running (default: `COMPUTE_WH`)
3. Go to **Projects > Workspaces** in Snowsight
4. Create a **new Workspace**

### Step 4: Upload All Project Files to the Workspace

1. In the Workspace, click the **"+"** button or use the upload option
2. Upload the entire project folder structure:
   - `Untitled.sql`
   - `Navadrishti APP/` folder (contains `Navadrishti.py`, `snowflake.yml`, `pyproject.toml`, `.streamlit/config.toml`)
   - `cortex_project/` folder (contains all `.yaml` agent and semantic view files)
   - `docs/` folder (optional -- for reference only)
3. Also upload the 3 CSV dataset files (`Abt.csv`, `Buy.csv`, `abt_buy_perfectMapping.csv`)

### Step 5: Run the Backend SQL Pipeline

This sets up the entire database, tables, matching logic, and analytics views.

1. Open **`Untitled.sql`** in the Workspace
2. Make sure the warehouse is set to `COMPUTE_WH` (or your preferred warehouse)
3. **Run all the SQL statements** in order (top to bottom)

This will:
- Create the `NAVADRISHTI_DB` database and `RETAIL_INTELLIGENCE` schema
- Create base tables (`ABT_PRODUCTS`, `BUY_PRODUCTS`, `PRODUCT_MAPPING`)
- Create a stage (`RETAIL_STAGE`) and file format for CSV loading
- **Note:** You need to upload the 3 CSV files to the `RETAIL_STAGE` stage (via Snowsight: go to **Data > Databases > NAVADRISHTI_DB > RETAIL_INTELLIGENCE > Stages > RETAIL_STAGE** and upload the files there)
- Load the CSV data into the tables
- Run the product matching pipeline (exact model matching, fuzzy Jaro-Winkler matching, manufacturer filtering)
- Create analytics views (`PRICING_INTELLIGENCE`, `PRICING_RECOMMENDATIONS`, `MARKET_INTELLIGENCE`)

### Step 6: Deploy the Cortex AI Components

Deploy the semantic view and AI agents from the `cortex_project/` folder:

1. In the Workspace, navigate to the `cortex_project/` folder
This deploys:

RETAIL_INTELLIGENCE_VIEW -- Semantic View (connects 5 tables with 9 verified queries)
PRODUCT_MATCHING -- Cortex Agent for product matching queries
PRICING_INTELLIGENCE -- Cortex Agent for pricing analysis
MARKET_INTELLIGENCE -- Cortex Agent for market trend queries
### Step 7: Run the Streamlit App (Navadrishti.py)
Navigate to the Navadrishti APP/ folder in the Workspace
Open Navadrishti.py
Deploy and run the Streamlit app
