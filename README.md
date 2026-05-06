# Crop Yield Prediction Model

A machine learning pipeline for predicting global crop yields using historical FAO data (1961–2016). Three models were implemented and compared  Linear Regression, Random Forest, and ANN  with an optimized Random Forest achieving **R² = 0.97**.

---

## Project Structure

```
crop-yield-prediction/
│
├── crop_yield_prediction.ipynb   # Main ML pipeline notebook
├── app.py                        # Streamlit web app
├── crop_yield_data.csv           # FAO dataset (56,717 records)
├── project_report.pdf            # Full project report
├── requirements.txt              # Python dependencies
└── README.md
```

---

## Dataset

- **Source:** [FAO - Food and Agriculture Organization](http://www.fao.org/faostat/)
- **Size:** 56,717 records
- **Period:** 1961–2016
- **Coverage:** Global (multiple countries)
- **Crops:** 27 different crop types
- **Target:** Crop yield in hectograms per hectare (hg/ha)

---

## ML Pipeline

### Data Preprocessing
- Log transformation of target variable (skewness reduced from 3.2 → 0.4)
- Outlier capping at 1st and 99th percentiles
- One-hot encoding for categorical features (Area, Item)
- 80/20 train-test split

### Feature Engineering
Created 224 features from 4 base columns:
- Crop average yield & region average yield
- Year², Year³ (polynomial temporal trends)
- Crop-region interaction features
- Statistical features (std, median, coefficient of variation)

---

## Models & Results

| Model | RMSE (log) | MAE (log) | R² Score |
|---|---|---|---|
| Linear Regression | 0.50 | 0.38 | 0.772 |
| Random Forest | 0.27 | 0.16 | 0.940 |
| ANN (128→64→32→1) | 0.27 | 0.20 | 0.932 |
| **Optimized Random Forest** | **0.17** | **0.10** | **0.972** |

### Best Model: Optimized Random Forest
- `n_estimators = 100`
- `max_depth = 25`
- `min_samples_leaf = 1`
- `max_features = 'sqrt'`
- Tuned using GridSearchCV with cross-validation
- **50% reduction in prediction error** compared to baseline

---

## Top Features (by importance)
1. Crop-Region Interaction
2. Region Standard Yield
3. Region Median Yield
4. Year-Crop Interaction
5. Region Average Yield

---

## How to Run

### 1. Clone the repository
```bash
git clone https://github.com/ShahwarYasir/crop-yield-prediction.git
cd crop-yield-prediction
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Run the notebook
Open `crop_yield_prediction.ipynb` in Jupyter Notebook or VS Code.

### 4. Run the Streamlit app
```bash
streamlit run app.py
```

---

## Requirements

```
pandas
numpy
scikit-learn
tensorflow
streamlit
matplotlib
seaborn
jupyter
```

---

## Authors

- **Hasana Zahid**
- **Dur-e-Shahwar** 


---

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
