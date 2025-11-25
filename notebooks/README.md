# Notebooks – Rod Pump Failure Analysis

This folder contains the Jupyter notebooks and key figures used for the **Rod Pump Failure Analysis** project. The goal of these notebooks is to:

- Clean and preprocess the rod pump dataset  
- Explore relationships between operational / mechanical / production features and failures  
- Select important features for modeling  
- Train and evaluate machine learning models for failure prediction and pump lifetime  
- Visualize model performance and uncertainty  

> Note: The original well-level dataset from ConocoPhillips is **not** included in this public repository.  
> These notebooks assume access to a similarly structured dataset.

---

## Background (Short)

Sucker rod pumps are a common artificial lift system in oil wells. They use a surface **pumpjack** connected to a string of **sucker rods** to drive a downhole **plunger**, lifting fluids to the surface.

Common failure drivers include:

- **Wear and tear** of rods, tubing, and moving parts  
- **Corrosion** due to harsh fluids  
- **Gas interference**, reducing effective pumping  
- **Mechanical issues** such as rod buckling, tubing failure, or misalignment  

The central questions we study in these notebooks are:

- Which **production and mechanical parameters** are the strongest predictors of rod pump failure / downtime?  
- How can pump **design and operating conditions** be adjusted to reduce failure risk?

---

## Cleaned Dataset – Key Variables (Summary)

In the original project, the cleaned dataset (e.g. `rod_cleaned_final.csv`, not included here) contained:

- **Identifiers**
  - `rod_uid` – BHA (Bottom Hole Assembly) lifetime rod identifier  
  - `uwi`, `well_id`, `well_name` – anonymized well identifiers  
  - `bha_lifetime_start`, `bha_lifetime_end`, `bha_lifetime_id`  

- **Targets**
  - `failure_type` – general failure category (later mapped to a binary failure / non-failure target)  
  - `bha_lifetime_log` – log-transformed lifetime of the BHA  

- **Operational & Mechanical Features (examples)**
  - `h2s_conc` – H₂S concentration (ppm)  
  - `primary_setpoint`, `secondary_setpoint` – control setpoints  
  - `stroke_len`, `gross_stroke_len`, `fillage`, `yesterday_avg_spm`  
  - `bha_config`, `rod_sinker_type`, `rod_has_guides`, `rod_make`, `rod_apigrade`  
  - `gas_anchor_len`, `gas_anchor_od`, `max_incline`, `max_unguided_dls`, `dls_high_in_hole`  
  - `overall_max_sideload`, `shallow_max_sideload`, `max_unguided_sideload`  
  - `chrome_len`, `enduralloy_len`, `poly_len`, `nip_set_depth`, `pump_bore`  

- **Production & Pressure Features**
  - `avg_press_flowline`, `avg_press_tubing`, `avg_press_casing`, `avg_diff_press`  
  - `avg_oil_vol`, `avg_water_vol`, `avg_liquid_vol`, `avg_watersg`  

These variables are used throughout the notebooks for cleaning, EDA, feature selection, and modeling.

---

## Recommended Notebook Order (Core Workflow)

If you have a dataset with the same schema as the original project, run the notebooks in this order:

1. **`data_cleaning.ipynb`**  
   - Cleans and preprocesses the raw dataset  
   - Tasks:
     - Column renaming  
     - Handling missing values and anomalies  
     - Log transformations of skewed variables  
     - Outlier removal (e.g., MAD-based)  
     - Saves a cleaned dataset such as `rod_cleaned_final.csv` (not included here)

2. **`EDA.ipynb`**  
   - Exploratory Data Analysis on the cleaned dataset  
   - Includes:
     - Distributions for numeric, categorical, and boolean variables  
     - Correlation heatmaps  
     - Pairwise relationships  
     - Relationships between `bha_lifetime_log` / failure indicators and inputs  

3. **`feature_selection.ipynb`**  
   - Identifies the most informative predictors for failure / lifetime modeling  
   - Methods:
     - Random Forest feature importance  
     - Lasso (L1-regularized) regression  
     - Recursive Feature Elimination (RFE)  
   - Outputs ranked feature sets for downstream models.

4. **`updated_analysis.ipynb`** (legacy / reference)  
   - Earlier version of the classification pipeline.  
   - Kept for comparison and to show model evolution.

5. **`updated2_analysis.ipynb`**  
   - Main **binary classification** notebook (failure vs. non-failure).  
   - Steps:
     - Train/test split  
     - Class imbalance handling (e.g., SMOTE)  
     - Training Logistic Regression and Random Forest models  
     - Evaluation:
       - Accuracy, precision, recall, F1-score  
       - Confusion matrices (e.g., `confusingmatrix4nine.png`)  

6. **`EDA_Modeling_Final.ipynb`**  
   - Final, polished end-to-end workflow combining:
     - Key EDA plots  
     - Selected features from `feature_selection.ipynb`  
     - Best-performing models and hyperparameters  
     - Uncertainty analysis:
       - Bootstrapped accuracy (`bootstrapped_accuracy_rf.png`)  
       - Monte Carlo-style evaluation (`monte_carlo_accuracy_rf.jpg`)  
       - Additional uncertainty visualizations (`uncertainty_visualization.png`)  

7. **`final_code.ipynb`**  
   - Consolidated code-first version of the modeling pipeline.  
   - Good starting point if converting notebooks into a pure Python module.

---

## Other Notebooks & Artifacts

- `analysis.ipynb` – Additional exploration and scratch work  
- `data_clean_no_transform.ipynb` – Cleaning version without log transforms  
- `extendedLife.ipynb` – Extended lifetime / production analysis  
- `dataVisualizationUdated.ipynb` – Alternative / extra visualizations  
- `rodPumpFailureIdentification.ipynb` – Focused work on failure identification logic  
- `Modeling_Findings_Summary.md` – Written summary of key modeling results  
- `bootstrapped_accuracy_rf.png`, `monte_carlo_accuracy_rf.jpg`, `uncertainty_visualization.png` – Core model performance & uncertainty figures  

---

## Environment Notes (Quick)

Most notebooks assume the dependencies listed in the root-level `requirements.txt`. Roughly:

- `numpy`, `pandas`  
- `matplotlib`, `seaborn`  
- `scikit-learn`, `imbalanced-learn`  
- `tqdm`, `scipy` (where relevant)

See the root `README.md` for a full environment setup guide using **UV** or `pip`.
