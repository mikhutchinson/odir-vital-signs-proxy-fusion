# Writeup: Portable ODIR-5K + Vital Signs Proxy Fusion

## Summary

This repository provides a portable proof-of-concept for multimodal fusion between retinal/fundus image features and vital-sign time-series embeddings.

It is based on a prior internal prototype that explored whether retinal images could add predictive signal beyond vital signs for neonatal shock/sepsis risk stratification. That prior prototype used a bespoke workflow system. This repo removes those dependencies and provides a standard Python/Jupyter version suitable for public sharing.

## Research question behind the prototype

Can retinal/fundus image features contribute additive signal beyond vital-sign time-series data for early clinical deterioration detection, such as neonatal shock or sepsis risk?

This repo does **not** answer that clinical question directly. It demonstrates the data pipeline needed to test it once matched clinical data is available.

## Public proxy datasets

The notebook uses two unrelated Kaggle datasets:

1. **ODIR-5K / Ocular Disease Recognition**  
   Kaggle slug: `andrewmvd/ocular-disease-recognition-odir5k`  
   Used as a stand-in for retinal/fundus imaging.

2. **Human Vital Sign Dataset**  
   Kaggle slug: `nasirayub2/human-vital-sign-dataset`  
   Used as a stand-in for longitudinal physiologic vital-sign streams.

Because these datasets do not describe the same patients, fusion is done by sequential `fusion_id`. That makes the experiment useful for technical validation only.

## Pipeline

The notebook performs the following steps:

1. Download both Kaggle datasets.
2. Locate the ODIR `data.xlsx` metadata file and `Training Images/` folder.
3. Parse ODIR labels: `N, D, G, C, A, H, M, O`.
4. Create one row per left/right eye image.
5. Extract portable retinal image features using PIL/numpy by default.
6. Load the vital-sign CSV.
7. Parse timestamps, sort records, remove problematic derived columns if present, encode categoricals, and interpolate/fill missing values.
8. Create 60-timestep windows for time-series forecasting.
9. Produce 64-dimensional vital-sign proxy embeddings using PCA over standardized windows.
10. Concatenate retinal features and vital-sign embeddings into a proxy multimodal fusion table.

## Why PCA instead of the original LSTM?

The earlier internal version used a PyTorch LSTM and extracted 64-dimensional hidden-state embeddings. For public reproducibility, this repo defaults to PCA embeddings so the notebook can run easily on ordinary machines without private model checkpoints.

The notebook still prepares `X_seq` and `y_seq` arrays, so collaborators can replace the PCA block with a true LSTM encoder later.

## Clinical limitations

This repo must not be interpreted as evidence that retinal images predict sepsis or shock. The datasets are unrelated and contain no matched neonatal outcomes.

A real study would require:

- neonatal fundus images,
- synchronized NICU vital-sign streams,
- patient identifiers and timestamps,
- clinically adjudicated shock/sepsis labels,
- patient-level train/test separation,
- sensitivity/specificity/AUROC/AUPRC/calibration reporting,
- clinician review of explanations.

## Value of this repo

The value is practical: it gives collaborators a public, runnable starting point for the data contract and preprocessing pipeline before private clinical data is available.
