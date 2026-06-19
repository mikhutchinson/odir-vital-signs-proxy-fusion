# ODIR-5K + Human Vital Signs Proxy Fusion

Portable public-repo version of a proof-of-concept multimodal pipeline: retinal/fundus image features from ODIR-5K plus time-series vital-sign embeddings from a public Kaggle vital-sign dataset.

> **Clinical caveat:** this is a technical proxy experiment only. The two datasets are unrelated public datasets. Sequentially pairing them validates the data pipeline shape, not a sepsis/shock prediction model.

## What this repo contains

- `notebooks/odir5k_vital_signs_proxy_fusion_reproducible.ipynb` — end-to-end reproducible notebook.
- `notebooks/odir5k_vital_signs_proxy_fusion_requirements.txt` — Python dependencies.
- `docs/WRITEUP.md` — plain-English project writeup and clinical caveats.
- `docs/PLAN.md` — project plan.
- `docs/EXPERIMENTS.md` — experiment log/template.
- `docs/CHANGELOG.md` — repo changelog.

## Datasets

The notebook downloads these public Kaggle datasets:

- ODIR-5K / Ocular Disease Recognition: `andrewmvd/ocular-disease-recognition-odir5k`
- Human Vital Sign Dataset: `nasirayub2/human-vital-sign-dataset`

You need Kaggle access configured locally, or you can manually download and place the datasets under `data/kaggle/`.

## Quickstart

```bash
git clone <this-repo-url>
cd odir-vital-signs-proxy-fusion
python3 -m venv .venv
source .venv/bin/activate
pip install -r notebooks/odir5k_vital_signs_proxy_fusion_requirements.txt
jupyter notebook notebooks/odir5k_vital_signs_proxy_fusion_reproducible.ipynb
```

If you do not have Jupyter installed:

```bash
pip install notebook
```

## Outputs

The notebook writes generated data locally under the repository root:

- `data/kaggle/` — downloaded datasets
- `artifacts_portable/processed/` — processed manifests, features, time-series arrays, and proxy fusion table

These outputs are intentionally ignored by git.

## Intended use

Use this repo as a runnable demonstration of the proposed data contract:

1. retinal image ingestion/features,
2. vital-sign time-series preprocessing,
3. 60-step sequence windows,
4. 64-dimensional vital-sign embeddings,
5. multimodal fusion table.

For a real NICU study, replace public proxy data with matched neonatal fundus images, synchronized NICU vitals, and clinically adjudicated shock/sepsis labels.
