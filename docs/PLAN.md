# Plan

## Goal

Create a small, public, reproducible repo that demonstrates the multimodal fusion workflow without any private/bespoke NeoXi tooling.

## Scope

Included:

- Public Kaggle dataset download instructions and notebook code.
- ODIR-5K metadata parsing and one-row-per-eye manifest.
- Portable retinal image feature extraction.
- Human vital-sign EDA and preprocessing.
- 60-step time-series sequence generation.
- 64-dimensional vital-sign proxy embeddings.
- Sequential proxy fusion table.
- Clear clinical limitations.

Excluded:

- Private NICU data.
- NeoXi workflow engine code.
- Clinical claims of sepsis/shock prediction performance.
- Generated dataset files and model artifacts.

## Milestones

1. Bootstrap repo skeleton.
2. Add reproducible notebook and requirements file.
3. Add writeup, plan, experiments log, changelog, and README.
4. Initialize git repo.
5. Optional: push to public GitHub.

## Validation

- Notebook file is valid JSON.
- Notebook code cells parse as Python.
- Repo contains only portable public-demo materials.
