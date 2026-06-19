# Experiments

## Experiment 001 — Portable proxy fusion notebook

**Status:** validated with nbconvert from a fresh throwaway clone  
**Notebook:** `notebooks/odir5k_vital_signs_proxy_fusion_reproducible.ipynb`

### Purpose

Validate that an outside collaborator can reproduce the proxy pipeline using standard Python libraries and public Kaggle datasets.

### Inputs

- `andrewmvd/ocular-disease-recognition-odir5k`
- `nasirayub2/human-vital-sign-dataset`

### Steps

1. Download datasets.
2. Parse ODIR metadata and image paths.
3. Extract portable retinal image features.
4. Load and preprocess vital signs.
5. Create 60-timestep vital-sign windows.
6. Create 64-dim vital-sign proxy embeddings.
7. Sequentially fuse retinal and vital-sign features.
8. Save generated artifacts locally.

### Expected artifacts

- `artifacts_portable/processed/odir5k_eye_manifest.csv`
- `artifacts_portable/processed/odir5k_image_features.pkl`
- `artifacts_portable/processed/vital_signs_processed_data.csv`
- `artifacts_portable/processed/vital_X_seq.npy`
- `artifacts_portable/processed/vital_y_seq.npy`
- `artifacts_portable/processed/vital_embeddings_64.npy`
- `artifacts_portable/processed/odir5k_vital_signs_proxy_fusion.csv`

### Interpretation

This validates pipeline mechanics only. It does not validate clinical prediction of shock, sepsis, or any neonatal outcome.
