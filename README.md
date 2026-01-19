# Glucose Prediction 
This project implements a machine learning–based approach for predicting interstitial glucose levels using non-invasive wearable sensor data. Biometric time-series signals are transformed into image representations using recurrence plots and analyzed with a deep learning model to improve glucose prediction accuracy. 

## Author and Context

This project was originally developed in 2023 as part of a research initiative conducted during my role as a Deep Learning Intern at the University of Massachusetts Lowell. The work contributed to a larger research effort focused on improving the precision of interstitial glucose level prediction using non-invasive wearable sensor data.

The broader research was accepted for publication at the **46th Annual International Conference of the IEEE Engineering in Medicine and Biology Society (EMBS)**. This repository contains the portion of the work that I directly implemented, including data preprocessing pipelines, image generation workflows, model training, evaluation, and experimental analysis.

While certain methodological components such as the use of signal-to-image encoding strategy, model architecture, etc., were based on prior research and collaborative contributions. I was responsible for integrating these methods. This repository reflects my individual implementation and experimentation within the context of that collaborative research effort.

## Dataset

The dataset used in this project is publicly available through **PhysioNet** and can be accessed at:  
https://physionet.org/content/big-ideas-glycemic-wearable/1.1.1/

Comprehensive documentation is provided on the PhysioNet website.

### Data Usage Details

- Only the following wearable sensor signals were used:
  - `BVP_XXX.csv` — Blood Volume Pulse  
  - `TEMP_XXX.csv` — Skin Temperature  
  - `EDA_XXX.csv` — Electrodermal Activity
- Ground-truth glucose values were obtained from:
  - `Dexcom_XXX.csv`

- Data from participants 1–14 only were included in this study due to technical issues with files from later participants.

No raw data files are redistributed in this repository. Users must download the dataset directly from PhysioNet.

## Methodology and Workflow Details

### 1. Data Preprocessing
- Merge wearable sensor data from the following CSV files:
  - BVP (Blood Volume Pulse)
  - TEMP (Skin Temperature)
  - EDA (Electrodermal Activity)
- BVP data are resampled to ensure alignment with other modalities.
- Clean the Dexcom glucose files by:
  - Extracting only the column containing ground-truth glucose values
  - Removing unnecessary rows and metadata

**Relevant files:**
- `glucose-prediction/Generate_RPs/Phasic/Preprocessing/Dexcom_cleanup.ipynb`
- `glucose-prediction/Generate_RPs/Phasic/Preprocessing/Merge.ipynb`


### 2. Input Generation: Recurrence Plot Images
- Convert each merged wearable data CSV (TEMP, BVP, EDA) into a structured NumPy array to enable consistent downstream processing.
- Segment the large merged data into multiple single fixed-length windows that align with glucose ground-truth measurements.
- Generate Recurrence Plot (RP) matrices from each biometric signal to capture repeating frequency-based patterns in the data.
- Normalize the RP matrices to ensure stable value ranges across samples.
- Combine the individual RP matrices for TEMP, BVP, and EDA into a single RGB image, where each biometric signal corresponds to one color channel.
- Use the resulting RGB recurrence plot images as inputs to the deep learning model.

**Relevant file:**
- `glucose-prediction/Generate_RPs/Phasic/RP_COMBO_Phasic.ipynb`

### 3. Training Preparation
#### a) Dataset Split
- The generated recurrence plot (RP) images are split into training (70%) and validation (30%) sets to enable model training and performance evaluation on unseen data.

**Relevant file:**
- `glucose-prediction/Model/split_train_val.ipynb`

#### b) Ground-Truth Mapping
- Each RP image is mapped to its corresponding ground-truth glucose value obtained from the Dexcom continuous glucose monitoring (CGM) files.

**Relevant file:**
- `glucose-prediction/Model/prepare_train_val_mappings.ipynb`

### 4. Optional: Hyperparameter Tuning
- Test different combinations of learning rates and batch sizes to find the settings that minimize validation loss and improve model performance.
- The model is trained and evaluated for each combination, and the best-performing configuration is saved.

**Relevant file:**
- `glucose-prediction/Model/hyperparameter_tuning.ipynb`

### 5. Model Training and Validation
- Train the model using the generated RGB images and their corresponding glucose ground-truth values.
- Use a supervised learning setup with separate training and validation datasets to monitor generalization performance.
- Optimize the model using stochastic gradient descent and a custom loss function designed for glucose prediction accuracy.
- Apply a learning rate scheduler to improve training stability over long runs.
- Track performance across epochs using multiple evaluation metrics, including loss, RMSE, and MAPE.

**Relevant file:**
- `glucose-prediction/Model/resNet18_model.ipynb`

## Further Methodological Details

For a comprehensive description of this project, please refer to the associated publication:

- IEEE Xplore: https://ieeexplore.ieee.org/document/10781542

This paper provides the full technical context beyond what is summarized in this repository.
