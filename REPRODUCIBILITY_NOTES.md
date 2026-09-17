# Reproducibility notes

This file records items that should be checked before the repository is
cited as the exact computational workflow for the submitted manuscript.

## 1. Cross-validation definition

The notebook implements four-fold leave-one-management-region-out spatial cross-validation using the four forest management regions: Gilan, Nowshahr, Sari, and Golestan. In each fold, all plots from one management region are withheld for validation, while plots from the remaining three regions are used for model training. This spatial blocking strategy reduces spatial dependence between training and validation data and provides a more realistic assessment of model transferability to geographically independent forest areas.

## 2. Outlier threshold

The notebook contains inconsistent values for `OUTLIER_SD_THRESH`: one
model-evaluation cell sets it to `3`, while later prediction/bootstrap
code refers to or sets it to `0.8`.

Before release, confirm the threshold actually used for the reported
results and use one consistent value throughout the workflow.

## 3. Random Forest predictor sampling

`RandomForestRegressor` is instantiated without an explicit
`max_features` argument. In current scikit-learn versions this means the
default regressor behavior is used. For long-term reproducibility,
explicitly record the scikit-learn version and, preferably, set the
intended `max_features` value in the final archived notebook.

## 4. Environment versions

`requirements.txt` intentionally lists package names without guessed
version pins because the uploaded notebook does not contain a complete
verified environment lock file. For exact reproducibility, run the final
analysis environment and save package versions (for example, with
`pip freeze`) before creating the Zenodo release.

## 5. File paths and Google Cloud project

The public notebook has had the original Google Cloud project identifier
replaced with `YOUR_GCP_PROJECT_ID`. Google Drive paths remain
workflow-specific and must be updated by users to match their authorized
data locations.

## 6. Restricted inputs

The repository cannot reproduce numerical results without the restricted
NFI and associated spatial inputs. This limitation should be stated both
in the manuscript Data Availability section and in the Zenodo record.
