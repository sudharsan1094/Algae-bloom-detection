# Experimental Results

This folder contains selected output figures from the Algae Bloom Detection project.

## Figures

### 1. Individual SNN models vs. ensemble performance
`images/individual_snn_vs_ensemble_performance.png`

Compares accuracy and F1-score for nine individual SNN models and shows the mean individual accuracy and ensemble accuracy reference lines.

### 2. Nine-SNN ensemble confusion matrix
`images/nine_snn_ensemble_confusion_matrix.png`

Confusion matrix on the real test set:

| Actual class | Predicted No Bloom | Predicted Bloom |
|---|---:|---:|
| No Bloom | 1,737 | 199 |
| Bloom | 76 | 3,328 |

The matrix contains 5,340 test samples. Accuracy calculated from the displayed counts is 94.85%.

### 3. Lake Erie actual vs. predicted bloom
`images/lake_erie_actual_vs_predicted_bloom.png`

Compares the actual labels from real CyAN data with the SNN-predicted bloom probability at the sampled Lake Erie locations.

## Notes

- These are project-generated figures supplied for the public repository.
- Keep figure labels and reported metrics consistent with the final experiment and test split.
- Do not describe the probability map as a full-coverage satellite classification map: it visualizes predictions at the sampled locations shown.
- The original CyAN GeoTIFF input files were not copied into this results folder. Store source rasters separately under `data/` only after checking redistribution permissions and documenting their source.
