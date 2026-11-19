# Algae Bloom Detection System

### Satellite-Based Harmful Algal Bloom Detection Using Sentinel-2 and Spiking Neural Networks

An AI-based remote sensing project for detecting and monitoring harmful
algal bloom (HAB) conditions in **Lake Erie, USA**, using Sentinel-2
satellite imagery, spectral features, CyAN reference data, and
machine-learning experiments.

> **Project status:** This repository contains the project notebooks,
> documentation, and selected experimental visualizations. The source
> datasets, CyAN GeoTIFF files, and trained model checkpoints are not
> included. They must be obtained or generated separately to reproduce
> the complete workflow.

------------------------------------------------------------------------

## Project Overview

Harmful Algal Blooms (HABs) are an environmental concern that can affect
aquatic ecosystems, water quality, and public health. Traditional water
sampling provides limited spatial coverage, making it challenging to
monitor large water bodies repeatedly.

This project explores a satellite-based workflow for identifying bloom
and non-bloom conditions over Lake Erie. It combines Sentinel-2 imagery,
spectral feature extraction, CyAN reference data, BCPO-based feature
selection, Spiking Neural Networks (SNN), Bayesian hyperparameter
optimization, and ensemble experiments.

## Objectives

-   Detect bloom and non-bloom conditions using satellite-derived
    features.
-   Extract spectral information from Sentinel-2 imagery.
-   Generate labeled samples using CyAN reference data.
-   Apply BCPO feature selection and train SNN models.
-   Explore Bayesian hyperparameter optimization.
-   Evaluate individual SNN models and ensemble experiments.
-   Visualize predicted bloom probabilities at sampled Lake Erie
    locations.

## Technologies Used

  Category                Technologies
  ----------------------- -------------------------------------------
  Programming             Python
  Satellite imagery       Sentinel-2
  Geospatial processing   Google Earth Engine, Rasterio, PyProj
  Spectral analysis       NDVI, NDWI, MNDWI, GNDVI, NDCI, FAI, AFAI
  Feature selection       BCPO
  Machine learning        Spiking Neural Networks
  Optimization            Optuna, Bayesian optimization
  Data processing         NumPy, Pandas, Scikit-learn
  Visualization           Matplotlib
  Development             Google Colab, Jupyter Notebook

## System Workflow

``` text
Sentinel-2 Satellite Imagery
             |
             v
     Image Preprocessing
             |
             v
    Spectral Feature Extraction
             |
             v
       CyAN Reference Data
             |
             v
       Dataset Generation
             |
             v
      Dataset Preparation
             |
             v
      BCPO Feature Selection
             |
             v
       SNN Model Training
             |
             v
    Bayesian Optimization
             |
             v
      Ensemble Experiments
             |
             v
       Model Evaluation
             |
             v
   Bloom Probability Mapping
             |
             v
       Interactive Viewer
```

## Methodology

### 1. Satellite Data Collection and Preprocessing

-   Sentinel-2 Surface Reflectance Harmonized imagery is accessed
    through Google Earth Engine.
-   Cloud masking is applied using the Scene Classification Layer (SCL).
-   Date-window image composites are generated for the Lake Erie study
    area.

### 2. Spectral Feature Extraction

Spectral indices and additional band-derived features are extracted from
Sentinel-2 imagery.

  Index   Description
  ------- ----------------------------------------------
  NDVI    Normalized Difference Vegetation Index
  NDWI    Normalized Difference Water Index
  MNDWI   Modified Normalized Difference Water Index
  GNDVI   Green Normalized Difference Vegetation Index
  NDCI    Normalized Difference Chlorophyll Index
  FAI     Floating Algae Index
  AFAI    Alternative Floating Algae Index

The dataset-generation notebook is configured to compute **31 spectral
and band-derived features**.

### 3. Dataset Generation and Labeling

-   Sentinel-2 spectral features are sampled over the selected Lake Erie
    regions and dates.
-   CyAN raster data is used by the notebook to assign bloom and
    non-bloom labels.
-   Duplicate records are removed during dataset preparation.
-   Missing and infinite feature values are checked.
-   Class balancing is performed in the dataset-generation workflow.

### 4. Dataset Preparation

The dataset-preparation notebook contains the preparation and
augmentation steps used for the model experiments. Review that notebook
for the exact split configuration and augmentation settings used in a
particular experiment.

### 5. BCPO Feature Selection

BCPO is used in the supplied training workflow to select features before
SNN model training. Refer to the training notebook for the exact
implementation and selected feature set.

### 6. Spiking Neural Network

Spiking Neural Networks are used for binary classification:

-   **No Bloom**
-   **Bloom**

The models use the selected spectral features as input.

### 7. Bayesian Hyperparameter Optimization

The supplied optimization workflow uses Optuna and a Tree-structured
Parzen Estimator (TPE) sampler to search for SNN hyperparameter
configurations. Consult the experiment notebook for the search space and
selected configuration.

### 8. Ensemble Experiments

The project includes experiments comparing nine individual SNN models
and an ensemble. The ensemble combines model predictions; its
performance is evaluated against the individual models rather than
assumed to be better.

### 9. Evaluation and Visualization

The evaluation workflow includes classification metrics and visual
outputs such as confusion matrices, model comparisons, and geographic
prediction visualizations.

------------------------------------------------------------------------

## Experimental Results

The following figures are outputs supplied for this project.

### 1. Individual SNN Models vs. Ensemble Performance

This chart compares accuracy and F1-score for nine individual SNN models
and displays the reference lines for mean individual accuracy and
ensemble accuracy.

![Individual SNN Models vs Ensemble
Performance](results/images/individual_snn_vs_ensemble_performance.png)

### 2. Confusion Matrix -- 9-SNN Ensemble

The confusion matrix below shows the classification counts on the test
set represented in the supplied figure.

![9-SNN Ensemble Confusion
Matrix](results/images/nine_snn_ensemble_confusion_matrix.png)

  Actual Class     Predicted No Bloom   Predicted Bloom
  -------------- -------------------- -----------------
  No Bloom                      1,737               199
  Bloom                            76             3,328

From these displayed counts:

-   True Negatives: 1,737
-   False Positives: 199
-   False Negatives: 76
-   True Positives: 3,328
-   Total test samples: 5,340
-   Accuracy: approximately **94.85%**

### 3. Lake Erie -- Actual vs. Predicted Bloom

This figure compares actual labels from real CyAN data with
SNN-predicted bloom probabilities at the sampled geographic locations.

![Lake Erie Actual vs Predicted
Bloom](results/images/lake_erie_actual_vs_predicted_bloom.png)

-   **Left:** Actual labels from CyAN reference data.
-   **Right:** SNN-predicted bloom probability.
-   The points represent sampled locations, not a continuous full-lake
    classification raster.

------------------------------------------------------------------------

## Repository Structure

``` text
algae-bloom-detection/
|
|-- README.md
|-- requirements.txt
|-- .gitignore
|
|-- notebooks/
|   |-- 01_dataset_generation.ipynb
|   |-- 02_dataset_preparation.ipynb
|   |-- 03_snn_training.ipynb
|   |-- 04_bayesian_comparison.ipynb
|   |-- 05_ensemble_experiments.ipynb
|   |-- 06_model_evaluation.ipynb
|   |-- 07_interactive_viewer.ipynb
|
|-- data/
|   |-- README.md
|
|-- results/
|   |-- README.md
|   |-- images/
|       |-- individual_snn_vs_ensemble_performance.png
|       |-- nine_snn_ensemble_confusion_matrix.png
|       |-- lake_erie_actual_vs_predicted_bloom.png
|
|-- docs/
    |-- methodology.md
```

## Installation and Execution

### 1. Clone the Repository

``` bash
git clone https://github.com/sudharsan1094/Algae-bloom-detection.git
cd Algae-bloom-detection
```

### 2. Create a Virtual Environment

``` bash
python -m venv venv
```

Activate the environment:

**Windows PowerShell**

``` powershell
venv\Scripts\Activate.ps1
```

**Linux / macOS**

``` bash
source venv/bin/activate
```

### 3. Install Dependencies

``` bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Open the Notebooks

The notebooks were authored primarily for Google Colab. Open them in
Google Colab or Jupyter and follow the workflow in this order:

1.  `01_dataset_generation.ipynb`
2.  `02_dataset_preparation.ipynb`
3.  `03_snn_training.ipynb`
4.  `04_bayesian_comparison.ipynb`
5.  `05_ensemble_experiments.ipynb`
6.  `06_model_evaluation.ipynb`
7.  `07_interactive_viewer.ipynb`

Some notebooks use Google Colab-specific features such as file upload
and Google Drive mounting. These cells may need adjustment when running
locally.

### 5. Google Earth Engine Setup

The dataset-generation and interactive-viewer notebooks require Google
Earth Engine access.

-   Configure a Google Cloud project enabled for Earth Engine.
-   Authenticate with the Earth Engine Python API.
-   Replace `YOUR_GEE_PROJECT_ID` in the relevant notebook with your own
    project ID.
-   Configure input and output paths for your environment.

Do not commit credentials, service-account keys, access tokens, or
private configuration files.

## Data and Model Files

The repository does not currently include the source datasets or trained
model checkpoints.

The workflow may require:

-   CyAN reference GeoTIFF files for labeling.
-   Previously generated or supplied CSV datasets.
-   Exported feature datasets.
-   Trained SNN model checkpoints for inference in the interactive
    viewer.

Obtain these files from their authorized sources or generate them using
the notebooks. Review `data/README.md` for additional notes. Large
datasets and model files are excluded from Git by the repository's
`.gitignore`.

## Limitations

-   Results depend on satellite scene availability, cloud cover,
    sampling dates, and data quality.
-   The experiments focus on Lake Erie; performance on other water
    bodies requires separate validation.
-   CyAN reference labels and Sentinel-2 acquisition dates may have
    temporal or labeling differences.
-   The interactive prediction figure shows sampled geographic
    locations, not complete spatial coverage of the lake.
-   A successful notebook execution requires the external datasets,
    Earth Engine access, and compatible model files.

## Future Enhancements

-   Extend the workflow to additional lakes and water bodies.
-   Incorporate more frequent satellite observations.
-   Improve temporal monitoring and spatial coverage.
-   Develop an automated monitoring dashboard.
-   Evaluate additional deep-learning and hybrid approaches.
-   Explore early-warning notifications for potential bloom events.

## Author

**Sudharsan S**\
Integrated M.Tech -- Software Engineering\
Vellore Institute of Technology, Chennai

GitHub: [@sudharsan1094](https://github.com/sudharsan1094)

## License

No license has currently been assigned to this repository. Reuse and
redistribution permissions should be clarified before adding an
open-source license.
