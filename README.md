# Rod Pump Failure Analysis (NSC325 Final Project)

This repository contains my portion of an industry-collaborative project from **NSC 325: Inventors Program – Energy** at UT Austin. We applied supervised machine learning to predict **sucker rod pump failures** and analyze **well productivity** using operational, mechanical, and fluid-based well features.

The original dataset was provided by **ConocoPhillips** and includes more than 50 features for ~2,600 wells. Our goals were to:

- Identify risk factors associated with rod pump failures and downtime  
- Help minimize unplanned shutdowns and maintenance costs  
- Explore design and operating conditions that improve pump reliability and well performance  

> ⚠️ **Data Access Note**  
> Due to data-sharing agreements with ConocoPhillips, the original well-level datasets are **not included** in this public repository.  
> This repo focuses on the **modeling code, analysis workflow, and figures**, so the structure is reproducible on a similar dataset even though the raw CSVs are not available here.

---

## Repository Structure

```text
.
├── README.md                      # Project overview (this file)
├── requirements.txt               # Python dependencies
├── pyproject.toml                 # UV / project configuration
├── uv.lock                        # Lockfile for deterministic environments
├── confusingmatrix4nine.png       # Example confusion matrix figure
├── src/
│   └── nsc325_group1/
│       └── __init__.py            # Helper functions / notes for the project
└── notebooks/
    ├── README.md                  # Notebook documentation & variable descriptions
    ├── data_cleaning.ipynb        # STEP 1: Clean raw data, handle outliers, save cleaned CSV
    ├── EDA.ipynb                  # STEP 2: Univariate & bivariate EDA
    ├── feature_selection.ipynb    # STEP 3: Feature importance (RF, Lasso, RFE)
    ├── updated_analysis.ipynb     # Earlier modeling attempt (kept for reference)
    ├── updated2_analysis.ipynb    # STEP 4: Binary failure classifier + evaluation
    ├── EDA_Modeling_Final.ipynb   # STEP 5: Final end-to-end modeling & uncertainty
    ├── final_code.ipynb           # Consolidated core modeling pipeline
    ├── analysis.ipynb             # Additional exploration / scratch work
    ├── data_clean_no_transform.ipynb
    ├── extendedLife.ipynb         # Extended lifetime analysis
    ├── dataVisualizationUdated.ipynb
    ├── rodPumpFailureIdentification.ipynb
    ├── Modeling_Findings_Summary.md
    ├── bootstrapped_accuracy_rf.png
    ├── monte_carlo_accuracy_rf.jpg
    └── uncertainty_visualization.png
```

## Modeling Overview

We framed two main prediction problems:

### 1. Binary Classification – Failure vs. Non-Failure

- **Target:** consolidated `failure_type` into a binary indicator (failure / no-failure)  
- **Models:** Logistic Regression, Random Forest  
- **Techniques:**
  - Train/test split with cross-validation  
  - Class imbalance handling (e.g., SMOTE in `updated2_analysis.ipynb`)  
  - Evaluation using accuracy, precision, recall, F1-score, and confusion matrix  
  - Uncertainty assessment with bootstrapping and Monte Carlo simulations  

### 2. Regression – Pump Lifetime & Production

- **Target (in some notebooks):** `bha_lifetime_log` (log-transformed lifetime)  
- We explored how:
  - Mechanical design  
  - Pressure conditions  
  - Fluid volumes  

  relate to **pump lifetime** and **well production**.

**Key engineered / impactful features included:**

- Average tubing / casing / flowline pressures  
- Average oil, water, and liquid volumes  
- Gas anchor length and related geometric features  
- Specific gravity of produced water  
- Various rod / tubing configuration attributes  

---

## How to Run the Code Locally

Because the original well-level data is private, you won’t be able to reproduce the **exact** results without a similar dataset. However, you can still:

- Inspect the full modeling workflow  
- Adapt the pipeline to your own dataset with a similar schema  

### 1️⃣ Clone the Repository

```bash
cd ~/projects  # or wherever you keep projects
git clone https://github.com/nancy1404/rod-pump-failure.git
cd rod-pump-failure
```

### 2️⃣ Set Up a Python Environment

You can use either **UV** (recommended) or plain `pip`.

#### Option A – Using UV

If you have [UV](https://astral.sh/uv/) installed:

```bash
uv sync
```

This will create a virtual environment (e.g. `.venv/`) and install dependencies from `pyproject.toml` / `uv.lock`.

Activate the environment (typical Mac/Linux):

```bash
source .venv/bin/activate
```

#### Option B – Using pip

If you prefer a regular `pip` workflow:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
````

### 3️⃣ Open the Project in VS Code

From the repo root:

```bash
code .
````

- Install the **Python** and **Jupyter** extensions if prompted.  
- Select the `.venv` Python interpreter as the kernel for all notebooks.  

---

### 4️⃣ Run Notebooks in Order (Recommended Workflow)

If you have a dataset with the same structure as the original Conoco file, run the notebooks in this order:

1. `notebooks/data_cleaning.ipynb`  
2. `notebooks/EDA.ipynb`  
3. `notebooks/feature_selection.ipynb`  
4. `notebooks/updated2_analysis.ipynb`  
5. `notebooks/EDA_Modeling_Final.ipynb`  

Each notebook contains comments and markdown cells that describe the logic and decisions (e.g., transformations, model choices, thresholds).

---

## Developer Notes

- **Tech stack:** Python, pandas, NumPy, scikit-learn, matplotlib, seaborn, imbalanced-learn, tqdm  
- **Versioning:** `pyproject.toml` + `uv.lock` for reproducible environments  
- **Code organization:**
  - Exploratory work is kept in **notebooks**  
  - Reusable helpers live under `src/nsc325_group1/`  

If you’re a recruiter or collaborator and want more detail on my specific contributions (data cleaning, feature engineering, model selection, uncertainty analysis), feel free to reach out via GitHub or LinkedIn.

