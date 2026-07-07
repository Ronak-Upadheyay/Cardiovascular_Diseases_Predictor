# Cardiovascular Disease Risk Prediction App

This project is a Streamlit-based machine learning application that predicts the likelihood of cardiovascular disease using patient health and lifestyle data. It provides a simple and interactive interface for entering health information and receiving a risk assessment along with a basic medical-style summary.

## Project Description

The app uses a trained machine learning model to analyze input features such as:

- Age
- Gender
- Weight
- Blood pressure
- Cholesterol level
- Glucose level
- Smoking status
- Alcohol consumption
- Physical activity

Based on these values, the system predicts whether the risk level is low, moderate, or high.



## Tech Stack

- Python
- Streamlit
- pandas
- NumPy
- scikit-learn
- joblib
- Matplotlib
- Seaborn

## How to Run

1. Clone or open the project folder.
2. Install the required dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. Run the Streamlit app:

   ```bash
   streamlit run app.py
   ```

4. Open the local URL shown in the terminal, usually:

   ```text
   http://localhost:8501
   ```

## Project Files

- app.py - Main Streamlit web application
- cardio_model.pkl - Pretrained machine learning model
- cleaned_dataset.csv - Cleaned dataset used for training
- preprocessing.ipynb - Notebook for data preprocessing
- requirements.txt - Python dependencies
