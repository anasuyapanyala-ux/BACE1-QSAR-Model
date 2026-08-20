# BACE1 QSAR Model — Alzheimer's Disease Drug Repurposing

This repository contains the QSAR (Quantitative Structure–Activity Relationship) modeling pipeline for **BACE1 (PDB: 4X7I)**, one of three targets in a multi-target Alzheimer's disease drug repurposing study.

## Run it — one click, nothing to upload

Click a badge below to open the notebook directly in Google Colab. Each notebook automatically downloads the data it needs from this repository — just go to **Runtime → Run all**.

| Notebook | Open in Colab |
|---|---|
| 1. Descriptor Generation | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/anasuyapanyala-ux/BACE1-QSAR-Model/blob/main/BACE1_QSAR_Pipeline_ChEMBL_to_Descriptors.ipynb) |
| 2. Model Building & Testing | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/anasuyapanyala-ux/BACE1-QSAR-Model/blob/main/BACE1_QSAR_Model_Building_and_Testing.ipynb) |

Run notebook 1 first (it builds `BACE1_merged_descriptors.csv`), then notebook 2. If you open notebook 2 on its own, it will automatically pull the pre-generated descriptor file from this repo, so it also works standalone.

## Contents

| File | Description |
|---|---|
| `BACE1_QSAR_Pipeline_ChEMBL_to_Descriptors.ipynb` | Retrieves bioactivity data for BACE1 from ChEMBL (CHEMBL4822) and generates 2D molecular descriptors (topological, Lipinski, QED, etc.) using RDKit. |
| `BACE1_QSAR_Model_Building_and_Testing.ipynb` | Builds and validates QSAR regression models using multiple ML algorithms with GridSearchCV, then applies the best model to predict activity for BBB-permeable candidate compounds. |
| `BACE1_raw_chembl.csv` | Raw bioactivity data exported from ChEMBL for this target. |
| `candidates_featurized.csv` | 113 blood–brain-barrier-permeable candidate compounds (from upstream BBB screening), pre-featurized for prediction. |

## Methodology Summary

1. **Data source**: Bioactivity data from ChEMBL (target CHEMBL4822).
2. **Descriptors**: 2D molecular descriptors generated with RDKit (topological indices, Lipinski descriptors, QED drug-likeness score, etc.).
3. **Modeling**: Multiple ML algorithms compared via GridSearchCV; train/test split performed before scaling to avoid data leakage.
4. **Validation**: Diagnostics include actual-vs-predicted plots, residual analysis, and feature importance.
5. **Application**: Best model used to predict BACE1 activity for candidate compounds that passed BBB permeability screening.

## Running locally instead of Colab

```
pip install rdkit networkx pandas numpy scikit-learn matplotlib seaborn joblib
jupyter notebook
```
Then run `BACE1_QSAR_Pipeline_ChEMBL_to_Descriptors.ipynb` followed by `BACE1_QSAR_Model_Building_and_Testing.ipynb`.

## Part of a Larger Project

This is one of three target-specific repositories in a multi-target Alzheimer's disease drug repurposing project:
- **BACE1** — this repository
- **GSK-3β** — companion repository
- **AChE** — companion repository

Candidate compounds were screened for blood–brain barrier permeability, evaluated with target-specific QSAR models, docked (GNINA) against each target structure, and analyzed for protein–ligand interactions (PLIP).
