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

## Methodology and Workflow
 TODO

## Model Architecture ML Topics

TODO

## Further Methodological Details

For a comprehensive description of this project, please refer to the associated publication:

- IEEE Xplore: https://ieeexplore.ieee.org/document/10781542

This paper provides the full technical context beyond what is summarized in this repository.
