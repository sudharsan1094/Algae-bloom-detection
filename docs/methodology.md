# Methodology

This document summarizes the stages visible in the supplied notebooks. It does not add unverified performance claims.

## 1. Satellite data and reference labels

The dataset-generation notebook accesses the `COPERNICUS/S2_SR_HARMONIZED` collection through Google Earth Engine, applies a scene-classification cloud mask, builds date-window composites, and derives spectral features. It also reads CyAN raster files and uses their digital-number ranges to assign bloom/no-bloom labels.

## 2. Spectral feature extraction

The dataset-generation notebook computes spectral indices and additional Sentinel-2 band-derived features. The exact feature definitions should be taken from the implementation in `01_dataset_generation.ipynb`.

## 3. Dataset preparation

`02_dataset_preparation.ipynb` contains the supplied data preparation and augmentation workflow. Preserve its actual split and augmentation strategy when reporting experimental methodology.

## 4. SNN training and optimization

`03_snn_training.ipynb` contains the BCPO/SNN training workflow and optimization code. `04_bayesian_comparison.ipynb` compares the experiment variants implemented there.

## 5. Ensemble and evaluation

`05_ensemble_experiments.ipynb` contains the ensemble experiments. `06_model_evaluation.ipynb` contains the evaluation and visualization workflow.

## 6. Interactive inference

`07_interactive_viewer.ipynb` combines a selected Lake Erie location/date, Sentinel-2 imagery, feature computation, and a trained model to display a classification overlay. It requires a compatible trained model checkpoint and Earth Engine access.
