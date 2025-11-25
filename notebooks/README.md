Jupyter notebooks should be saved here. 

project ultimate description
(all variables described with renamed variables!)

ROAD PUMP PRODUCTION FAILURE ANALYSIS
    - Identifying Risk Factors for Rod Pump Failure
    - Predicting well production and optimizing new well location

BACKGROUND:
    - Sucker rod pumps are a type of aritificial lift system used in oil wells. They operate by converting rotary motion from motor at surface into reciprocating motion that drives a piston down the well, lifting fluids to the surface.

    MAIN COMPONENTS:
        1. Pumpjack
            - visible above-ground drive for the well pump, connected to downhole pump by a series of interconnected sucker rods
        2. Sucker Rods
            - Steel rods, typically between 7 and 9 meters in length, used to join together the surface and downhole components of the pump.
        3. Plunger
            - The part of the pump that moves up and down to create the pumping action
        4. Barrels, Valves, and Hold-downs
            - These components are part of the pump's internal mechanism that helps in the movement of fluids
    REASONS FOR FAILURE:
        1. Wear and Tear: 
            - Continuous operation can lead to wear and tear of the rods, tubing and other components
        2. Corrosion:
            - Exposure to harsh chemicals and fluids can cause corrosion, leading to failure
        3. Gas Interference:
            - Gas brought into the pump can take up space in the compression chamber, reducing efficiency
        4. Mechanical Failures:
            - Issues like rod buckling, tubing failures, and improper alignment can cause the pump to fail


PROBLEM:
    - What production and mechanical parameters are the leading predictors for rod pump failure/downtime?
    - What is best design to mitigate failures in different conditions?

CLEANED DATA VARIABLES DESCRIPTION ***
    1. rod_uid
        - Description: Bottom Hole Assembly Lifetime Rod Identifier
    2. uwi
        - Description: Well Identifier with dashes (anonymized)
    3. well_name
        -  Description: Well Name (anonymized)
    4. well_id
        - Description: Well Identifier without dashes (anonymized)
    5. bha_tubing_id
        - Description: Bottom Hole Assembly Lifetime Tubing Identifier
    6. bha_lifetime_start
        - Description: Bottom Hole Assembly Lifetime Start
    7. bha_lifetime_end
        - Description: Bottom Hole Assembly Lifetime End
    8. bha_lifetime_id
        - Description: Bottom Hole Assembly Lifetime Identifier
    9. failure_type
        - Description: General type of failure recorded
    10. (null)

ADDITIONAL VARIABLES WITH DESCRIPTION
    11. h2s_conc
        - Hydrogen Sulfide Concentration in parts per million.
    12. PrimarySetpoint
        - Setpoints used to control the pump's operational parameters.
    13. secondary_setpoint
        - Description: Secondary setpoints used for additional control over the pump's operation.
    14. stroke_len
        - Description: Length of the stroke in the pumping mechanism.
    15. gross_stroke_len
        - Description: Total gross stroke length, considering all operational factors.
    16. fillage
        - Description: Efficiency or completeness of the pump fillage per stroke.
    17. yesterday_avg_spm
        - Description: Average number of strokes per minute recorded the previous day.
    18. bha_config
        -  Description: Configuration of the Bottom Hole Assembly.
    19. chemgroup1_any
        -  Description: Indicates if any chemical treatments from Group 1 were applied to the well.
    20. chemgroup1_all
        - Description: Indicates if all chemical treatments from Group 1 were applied to the well.
    21. chemgroup2_any
        - Description: Indicates if any chemical treatments from Group 2 were applied to the well.
    22. chemgroup2_all
        - Description: Indicates if all chemical treatments from Group 2 were applied to the well.
    23. chemgroup3_any
        - Description: Indicates if any chemical treatments from Group 3 were applied to the well.
    24. chemgroup3_all
        - Description: Indicates if all chemical treatments from Group 3 were applied to the well.
    25. max_unguided_dls
        - Description: Maximum unguided dog leg severity encountered in the wellbore.
    26. dls_high_in_hole
        - Description: Dog leg severity located high in the well hole.
    27. gas_anchor_len
        - Description: Length of the gas anchor used in the well.
    28. max_incline
        - Description: Maximum inclination recorded in the wellbore survey.
    29. wellbore_category
        - Description: Categorical classification of the wellbore based on its characteristics.
    30. manual_scale
        - Description: Manual scale used in measurements or adjustments.
    31. packer_vs_tac
        - Description: Comparison or status between the packer and tubing anchor catcher.
    32. avg_press_flowline
        - Description: Average pressure in the flowline.
    33. avg_press_tubing
        - Description: Average pressure in the tubing.
    34. avg_press_casing
        - Description: Average pressure in the casing.
    35. avg_diff_press
        - Description: Average differential pressure across the pump.
    36. avg_oil_vol
        - Description: Average volume of oil produced.
    37. avg_water_vol
        - Description: Average volume of water produced.
    38. avg_liquid_vol
        - Description: Average volume of all liquids produced.
    39. avg_watersg
        - Description: Average specific gravity of the water produced.
    40. rod_sinker_type
        - Description: Type of sinker rod used in the pump.
    41. rod_has_guides
        - Description: Indicates whether the rod string is equipped with guides.
    42. rod_make
        - Description: Manufacturer or make of the rod.
    43. rod_apigrade
        - Description: API grade of the rod.
    44. route
        - Description: Path or route of the data or material flow.
    45. overall_max_sideload
        - Description: Maximum sideload recorded overall.
    46. shallow_max_sideload
        - Description: Maximum sideload recorded in the shallower sections of the well.
    47. max_unguided_sideload
        - Description: Maximum unguided sideload recorded.
    48. dsand_dgas_type
        - Description: Type of downhole sand and gas handling equipment used.
    49. chrome_len
        - Description: Length of the chrome section in the assembly.
    50. enduralloy_len
        - Description: Length of the Enduralloy™-coated sections.
    51. poly_len
        - Description: Length of the polymeric sections.
    52. nip_set_depth
        - Description: Set depth of the nipple in the wellbore.
    53. pump_bore
        - Description: Diameter of the pump bore.
    54. gas_anchor_od
        - Description: Outer diameter of the gas anchor.
    
GUIDELINE??

Data Cleaning: 
    Address missing values and anomalies. This may involve imputation techniques you've already reviewed.
Exploratory Data Analysis (EDA): 
    Further explore the data to understand the distribution of key variables and their relationships, especially those related to failure types and operational conditions.
Feature Engineering: 
    Create new features that might help in predicting failures, such as operational time lengths or ratios of different pressures.
Predictive Modeling: 
    Develop machine learning models to predict failures. This involves splitting the data into training and test sets, choosing appropriate models (e.g., decision trees, logistic regression), and tuning them.
Validation and Testing: 
    Assess the model's performance using appropriate metrics such as accuracy, precision, recall, and F1-score.


FILE PATH
## WARNING
-   you need to run the files in this exact order.

**data_cleaning.ipynb**
IMPORT
***pip install numpy pandas matplotlib seaborn scipy***
# Data Cleaning Notebook
    This notebook cleans and preprocesses the rod pump dataset, including:
    - Column renaming
    - Missing value imputation
    - Log transformations for skewed distributions
    - Outlier removal using MAD
    - Final output saved to `rod_cleaned_final.csv`

**EDA.ipynb**
IMPORT
***pip install pandas seaborn matplotlib***
# Exploratory Data Analysis (EDA)
    This notebook performs exploratory analysis on the cleaned dataset:
    - Distribution plots for numeric, categorical, and boolean variables
    - Correlation heatmaps
    - Pairwise relationships
    - Relationships between `bha_lifetime_log` and input features

**feature_selection.ipynb**
IMPORT
***pip install pandas scikit-learn matplotlib seaborn***
# Feature Selection for Failure Prediction
    This notebook selects the most informative features for predicting rod pump failure using:
    - Random Forest feature importance
    - Lasso Regression (L1 regularization)
    - Recursive Feature Elimination (RFE)

    The output will guide feature selection for downstream modeling.

**updated_analysis.ipynb**
IMPORT
***pip install pandas numpy matplotlib seaborn scikit-learn***
    Based on its content and your workflow, this notebook appears to train classification models (e.g., Logistic Regression, Random Forest) using selected features from feature_selection.ipynb.

**updated2_analysis.ipynb**
IMPORT
***pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn***
    # ✅ Updated2 Analysis – Classification with Feature Engineering
    This notebook trains and evaluates classification models (Logistic Regression and Random Forest) using engineered features. We address class imbalance using SMOTE and evaluate model performance using precision, recall, F1-score, and confusion matrices.


**EDA_Modeling_Final.ipynb**
IMPORT
***pip install numpy pandas matplotlib seaborn scikit-learn tqdm***

