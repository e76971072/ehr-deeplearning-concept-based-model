# 🩺 RNN Time Series Forecasting for Acute Kidney Injury (AKI)

**Authors:** Kevin Nguyen and Creon Creonopoulos

**Dataset:** MIMIC-III 🏥

**Reference Paper:** [Concept-based model explanations for Electronic Health Records](https://arxiv.org/pdf/2012.02308) 📄

**Project Demo:** [DEMO](https://youtu.be/bIoudRRiIgo) 🎥


## 🎯 Purpose

This project aims to replicate or adapt the methodology from the referenced paper for predicting Acute Kidney Injury (AKI) using Recurrent Neural Networks (RNNs) on the MIMIC-III dataset. The primary goal is typically to predict the onset of AKI within a future time window (e.g., 48 hours) based on past hourly clinical data sequences.

The scripts generally cover:
1. Loading and preprocessing MIMIC-III data (Labs, Vitals, etc.) 📊.
2. Creating hourly time series sequences ⏳.
3. Defining AKI labels based on criteria like KDIGO 🏷️.
4. Building and training an RNN model using PyTorch 🧠.
5. Evaluating the model using relevant metrics (AUROC, AUPRC) 📈.
6. (Optional) Implementing and applying TCAV for model explainability as described in the paper 🤔.

## 🏗️ Code Structure

The typical workflow involves:

1.  **Configuration & Setup:** Import libraries, set paths, define constants ⚙️.
2.  **Data Loading:** Load necessary MIMIC-III tables (PATIENTS, ADMISSIONS, ICUSTAYS, LABEVENTS, CHARTEVENTS, OUTPUTEVENTS, PRESCRIPTIONS,PROCEDURES_ICD )  using `pyhealth` library 💾.
3.  **Preprocessing:** Convert raw timestamped data into fixed-interval (e.g., hourly) sequences, handling missing values (e.g., using presence flags) and scaling numeric features ✨.
4.  **Task Definition / Labeling:** Generate target labels based on the specific AKI prediction task (e.g., predicting onset in the next 48 hours for each hour, or classifying pre-AKI windows) 🏷️.
5.  **Data Splitting:** Divide data into training, validation, and test sets, usually splitting by patient ID 🔪.
6.  **Dataset & DataLoader:** Create PyTorch `Dataset` and `DataLoader` classes to handle the sequential data and batching 📦.
7.  **Model Definition:** Define the RNN architecture (e.g., using `torch.nn.RNN`) 🤖.
8.  **Training Loop:** Train the model using an appropriate loss function (`Binary Cross Entropy Loss`) and optimizer (`Adam`) 💪.
9.  **Evaluation:** Evaluate the trained model on the test set using metrics like AUROC and AUPRC 💯.
10. **(Optional) TCAV Analysis:** Implement concept definition, activation extraction, CAV training, and metric calculation (tCAV, CAV) to explain model behavior 🧐.

## 🚀 How to Run

1.  **Dependencies:** Install required libraries:
    ```bash
    pip install torch==2.2.2 pandas==2.2.2 matplotlib scikit-learn pyhealth
    # Note: Ensure pandas version is compatible with other libraries if needed.
    # Consider using a virtual environment.
    ```
2.  **Data:**
    * Obtain access to the MIMIC-III dataset via PhysioNet.
    * Update the script's configuration (`MIMIC_III_RAW_DIR`, `PYHEALTH_ROOT`) to point to your data locations 📁.
3.  **Configuration:** Adjust model hyperparameters (`HIDDEN_DIM`, `NUM_LAYERS`, `DROPOUT`, `LEARNING_RATE`, etc.) and task parameters (e.g., `WINDOW_HOURS`, `LOOKAHEAD_HOURS`) in the script 🔧.
4.  **Execution:** Run the Python script/notebook ▶️. Preprocessing can take significant time and disk space.

## 🛠️ Customization

* **Features:** Modify the `FEATURE_MAP`, `NUMERIC_FEATURES`, and preprocessing logic to include different clinical variables from MIMIC-III tables (ensure the tables are loaded) 📝.
* **Model:** Experiment with different RNN types (`GRU`, `LSTM`), hyperparameters, or add other layers (Attention, etc.) 💡.
* **Task:** Adapt the label generation (Section 4) and potentially the model's output layer/loss function for different prediction tasks (e.g., different prediction windows, multi-class AKI stage prediction) 🔄.
* **TCAV:** If implementing TCAV, carefully define concepts and adapt the placeholder functions for activation extraction and analysis based on the paper and your trained model 🤔.
