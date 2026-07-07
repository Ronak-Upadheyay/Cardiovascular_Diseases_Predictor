# Cardiovascular Disease ML – Retrain & Redeploy

This guide explains how to **retrain** the model (notebook) and **redeploy** the Streamlit app.

---

## Prerequisites

- Python 3.8+
- Dependencies from `requirements.txt`:
  - pandas, numpy, scikit-learn, joblib, matplotlib, seaborn, streamlit

Install:

```bash
pip install -r requirements.txt
```

---

## 1. Retrain the model

1. **Data**
   - Use the cleaned dataset: `cleaned_dataset.csv` (output of your preprocessing notebook).
   - It must contain the target column `cardio` and the same 13 feature columns used in training.

2. **Run the training notebook**
   - Open `model_training.ipynb` in Jupyter or VS Code.
   - Run **all cells** in order (Kernel → Run All).
   - The notebook will:
     - Train Logistic Regression, Decision Tree, Random Forest, and K-Nearest Neighbors.
     - Evaluate with Accuracy, Precision, Recall, F1, Confusion Matrix, ROC-AUC.
     - Show model comparison table and bar chart.
     - Run 5-fold cross-validation for all models.
     - Run RandomizedSearchCV on Random Forest (n_estimators, max_depth, min_samples_split, max_features) for fast tuning.
     - Select the best (tuned) model and check overfitting/underfitting.
     - Plot Learning Curve, Feature Importance, and ROC Curve.
     - Save everything to **`cardio_model.pkl`**.

3. **Output**
   - `cardio_model.pkl` is overwritten in the same folder as the notebook.
   - It contains: `model`, `columns`, `train_accuracy`, `test_accuracy`, `cv_score`, `feature_importance`, `roc_fpr`, `roc_tpr`, `learning_curve`, `model_comparison`.

---

## 2. Redeploy the Streamlit app

1. **Use the new model file**
   - Ensure `cardio_model.pkl` is in the **same directory** as `app.py` (or update the path in `app.py` if you save it elsewhere).

2. **Run the app locally**
   ```bash
   streamlit run app.py
   ```
   - Open the URL shown in the terminal (e.g. http://localhost:8501).

3. **What the app does**
   - **Prediction:** User enters patient info → app shows risk (low / moderate / high) and doctor’s summary (unchanged).
   - **Detailed analysis (if the new artifact is present):** Expand **“🔬 View Detailed Model Analysis”** to see:
     - Training accuracy, testing accuracy, 5-fold CV score.
     - Model comparison table.
     - Feature importance bar chart.
     - ROC curve.
     - Learning curve.

---

## 3. Reproducibility

- The notebook uses `RANDOM_STATE = 27` for:
  - `train_test_split`
  - All model constructors
  - `cross_val_score`, `RandomizedSearchCV`, `learning_curve`
- Keeping the same `cleaned_dataset.csv` and running the notebook again will produce the same `cardio_model.pkl` (up to floating point).

---

## 4. Backward compatibility

- If `cardio_model.pkl` was saved by the **old** notebook (only `model` and `columns`), the app still runs and only the prediction part is used; the “View Detailed Model Analysis” section is hidden.
- After retraining with the **new** notebook, the expandable analysis section appears automatically.

---

## 5. Optional: change test size or CV

- In `model_training.ipynb`:
  - **Train/test split:** `test_size=0.2` in `train_test_split` (change to e.g. `0.1` if you prefer).
  - **Cross-validation:** `cv=5` in `cross_val_score` and `learning_curve`; `cv=2` and `n_iter=8` in `RandomizedSearchCV` (you can increase for more stable tuning at the cost of time).

---

## 6. File layout (reference)

```
Cardiovascular_Diseases_ML/
├── app.py                 # Streamlit app
├── cardio_model.pkl       # Produced by model_training.ipynb
├── cleaned_dataset.csv    # Input to training
├── model_training.ipynb   # Training + evaluation + save
├── requirements.txt
└── DEPLOYMENT.md          # This file
```

After any change to the dataset or the notebook, run the notebook to regenerate `cardio_model.pkl`, then run `streamlit run app.py` to use the updated model.
