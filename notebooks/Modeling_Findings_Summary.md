
# 📝 Modeling Findings Summary  
**Rod Pump Failure Prediction — Phase 2 Results**

## 📌 Modeling Goal:
To identify the most important factors that predict whether a rod pump will **fail** or **not**, using real operational and production data.

---

## 🔧 1. Data Preparation
- We used the dataset `rod_cleaned_final.csv`, which contains **1977 rows** and **58 engineered features**.
- A new target variable called `failed` was created from the `failure_type` column:
  - `failed = 1` → pump failed (e.g., "Tubing", "Sucker Rod Pump", etc.)
  - `failed = 0` → no failure

## 🛠 2. Feature Engineering
We added several important features based on domain logic:
- `stroke_power` = stroke length × strokes per minute → movement capacity
- `oil_ratio` = avg oil / total liquid
- `water_ratio` = avg water / total liquid
- `pressure_efficiency` = flowline pressure – tubing pressure
- `stroke_len_sq` = square of stroke length (nonlinear effects)

These features were used alongside selected log-transformed and numeric features in modeling.

---

## 📊 3. Correlation Analysis
Top features positively correlated with failure (`failed = 1`) were:
- `avg_diff_press` (+0.19)
- `fillage_log` (+0.19)
- `oil_ratio` (+0.14)
- `stroke_power` (+0.10)
- `pressure_efficiency` (+0.08)

Top *negative* correlations (features that protect against failure):
- `avg_watersg_log` (–0.25)
- `enduralloy_len_log` (–0.22)

---

## 🚨 4. Outlier Handling
- Outliers were capped using the IQR method for six key features.
- This helped prevent extreme values from skewing the model.

---

## 🤖 5. Model Training & Performance
We trained two models:

### 📍 Logistic Regression
- Accuracy: **79.0%**
- Precision: **80.0%**
- Recall: **97.7%** ✅ High ability to catch failures!
- F1 Score: **87.9%**

### 📍 Random Forest
- Accuracy: **80.3%**
- Precision: **84.8%**
- Recall: **91.3%**
- F1 Score: **87.9%**

✅ **Both models performed well**, especially on detecting failures. Logistic Regression had slightly higher recall, while Random Forest balanced precision better.

---

## 🌟 6. Top 5 Important Features (from Random Forest)
| Rank | Feature              | Importance |
|------|----------------------|------------|
| 1️⃣   | `stroke_power`        | 29.4%      |
| 2️⃣   | `fillage_log`         | 25.3%      |
| 3️⃣   | `avg_diff_press`      | 24.1%      |
| 4️⃣   | `oil_ratio`           | 21.1%      |
| 5️⃣   | `enduralloy_len_log`  | 0.0%       *(not influential)*

These top features suggest that **movement effort**, **pressure stress**, and **fluid mix** are key drivers of rod pump failure.

---

## ✅ Summary:
Our model can **reliably detect rod pump failures**, and we now know which features are most predictive. This gives operators clear warning signals to watch for in future installations or maintenance scheduling.
