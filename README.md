# Data Analysis and Modeling Project

## Project Overview
This project implements a hybrid approach to more accurately predict revenue by first classifying clients by revenue class and then predicting revenue within each class using separate regression models. The project involves data extraction, exploratory data analysis (EDA), classification, and regression modeling.

### Hybrid Classification and Regression Approach

To improve revenue prediction, a two-stage approach was employed:
1. **Revenue Class Definition**: Clients are classified into different revenue classes based on revenue thresholds. This classification simplifies revenue prediction by creating separate groups with distinct patterns.
   - **Class 0**: Negative revenue over 6 months.
   - **Class 1**: Low or typical revenue (from 0 to 10,000).
   - **Class 2**: Medium revenue (from 10,000 to 50,000).
   - **Class 3**: High revenue (50,000 and above).

2. **Revenue Class Labeling and EDA**: A `revenue_class` label was added to the dataset to serve as the target variable for classification. EDA was conducted to assess data distribution, balance, and patterns across classes, and visualizations provided insights into feature relationships and class distribution.

3. **Classification Model Training**: A classifier was trained to predict the `revenue_class` label based on client characteristics. This model predicts a revenue class for new clients and serves as the first stage of the hybrid approach.

4. **Regression Models for Each Revenue Class**: Separate regression models were created for each revenue class. For each subset (e.g., Class 0, Class 1, etc.), the dataset was filtered, and a regression model was trained specifically for clients in that class. This approach refines the revenue prediction by focusing on patterns unique to each class. Currently, the regression step has been implemented primarily for Class 1, the most prevalent class.

### Repository Contents

- **`get_data.py`** — A Python script that connects to the database, runs SQL queries, loads data into a Pandas DataFrame, and saves it to a CSV file for analysis.
- **`data/`** — Folder containing the extracted data in CSV format.
- **`SQL/`** — Folder with SQL queries used to retrieve data.
- **`EDA.ipynb`** — Jupyter Notebook for exploratory data analysis, including statistical analysis, data visualization, and revenue class labeling.
- **`Classifier/`** — Folder containing notebooks and files for building and testing the classifier:
  - **`classes.ipynb`** — Sets up and trains the classifier on EDA-prepared data.
  - **`classes_test.ipynb`** — Applies the saved classifier and preprocessing pipeline to new test data, including all necessary supporting files.
- **`Regressor/`** — Folder with notebooks and files for building and testing the regression models:
  - **`Regressor_on_main_class.ipynb`** — Sets up and trains the regressor for data labeled as Class 1.
  - **`Regressor_on_main_class_test.ipynb`** — Applies the saved regressor and preprocessing pipeline to new test data for Class 1, including supporting files.

---

## Step-by-Step Guide

### Step 1: Data Extraction
1. Run the **`get_data.py`** script to connect to the database, execute SQL queries, and save data as a CSV file.
2. The data is saved to the **`data/`** folder for further processing.

### Step 2: Exploratory Data Analysis (EDA)
1. Open **`EDA.ipynb`** to analyze data distributions, visualize key statistics, and assign the revenue class labels.
2. EDA provides insights into data patterns and balance across revenue classes, helping refine the classification and regression stages.

### Step 3: Train the Classifier
1. Open **`Classifier/classes.ipynb`** to set up and train the classifier on revenue classes.
2. This model saves the classifier and preprocessing steps for future use on new data.

### Step 4: Test the Classifier
1. Run **`Classifier/classes_test.ipynb`** to apply the saved classifier and preprocessing steps to new data, assessing classification accuracy.

### Step 5: Train the Regressor for Class 1
1. Open **`Regressor/Regressor_on_main_class.ipynb`** to set up and train the regressor on data labeled as Class 1.
2. The regressor is optimized using Optuna and the Yeo-Johnson transformation, which achieved the best performance for this subset.

### Step 6: Test the Regressor on New Data
1. Run **`Regressor/Regressor_on_main_class_test.ipynb`** to apply the saved regressor to new test data with Class 1 labels, evaluating performance on unseen data.

---

## Notes
- **Log Transformation and Ensembling**: Both log transformation of the target variable and ensembling were explored but did not outperform the Optuna-tuned model with the Yeo-Johnson transformation.
- **Hyperparameter Tuning**: Optuna was used for extensive hyperparameter tuning, significantly improving model performance, especially for the regressor on Class 1 data.

This project demonstrates a complete pipeline from data extraction to predictive modeling, with the flexibility to apply and extend the hybrid classification-regression approach to future datasets.
