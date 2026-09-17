# AlphaEarth Embeddings and Model-Based Inference for Remote Forest Inventory

Code accompanying the manuscript:

**Bridging Forest Inventory Gaps in Remote and Inaccessible Temperate
Mountain Forests Using AlphaEarth Embeddings and Model-Based Inference**

Authors: Hormoz Sohrabi, Sasan Vafaei, Ramin Mansour Samaei, Markus
Immitzer, and Ardalan Daryaei.

## Overview

This repository contains the Python/Jupyter workflow used to integrate
National Forest Inventory (NFI) observations with AlphaEarth Foundation
(AEF) embeddings for estimation of forest structural attributes in the
Hyrcanian forests of northern Iran.

The workflow covers field-data preparation, extraction of AEF embeddings
through the Google Earth Engine Python API, environmental
characterization, exploratory PCA/UMAP analyses, Random Forest
regression, cross-validation, prediction for unmeasured inventory
locations, wall-to-wall mapping, and bootstrap-based prediction
uncertainty.

The modeled forest attributes are:

-   Standing volume (`Volume`; m³ ha⁻¹)
-   Tree density (`n_trees`; trees ha⁻¹)
-   Canopy height (`max_h`; m)

The Random Forest predictor set consists of the 64 AEF embedding
dimensions (`A00`--`A63`).

## Repository structure

``` text
remote-forests-aef-mbi/
├── notebooks/
│   └── AEF_MBI_remote_forests.ipynb
│   └── README.md
├── README.md
├── requirements.txt
├── .gitignore
├── CITATION.cff
├── .zenodo.json
├── DATA_AVAILABILITY.md
└── REPRODUCIBILITY_NOTES.md
```

## Data availability

The National Forest Inventory data used in the study are not included in
this repository. They are owned/restricted by the Natural Resources and
Watershed Management Organization of Iran and cannot be redistributed
without permission from the data provider.

The workflow also uses publicly accessible Earth-observation products,
including AlphaEarth annual satellite embeddings through Google Earth
Engine. Users wishing to reproduce the workflow with their own
authorized field data must update the input paths and Earth Engine
project configuration in the notebook.

## Software requirements

The analysis was developed in Python and was run in a Google Colab /
Google Earth Engine workflow. Install the Python dependencies with:

``` bash
pip install -r requirements.txt
```

A Google Earth Engine account and a Google Cloud project configured for
Earth Engine are required for the Earth Engine portions of the notebook.

## Running the notebook

1.  Clone or download this repository.
2.  Install the dependencies in `requirements.txt`.
3.  Open `notebooks/AEF_MBI_remote_forests.ipynb` in Google Colab or
    Jupyter.
4.  Replace `YOUR_GCP_PROJECT_ID` with your own Earth Engine-enabled
    Google Cloud project ID.
5.  Update the input/output paths to point to your authorized copies of
    the field and spatial datasets.
6.  Authenticate Google Drive and Google Earth Engine when prompted.
7.  Run the notebook sequentially, checking the notes in
    `REPRODUCIBILITY_NOTES.md` before attempting exact reproduction of
    the manuscript results.

## Main Earth observation dataset

The notebook accesses the annual AlphaEarth embedding collection:

`GOOGLE/SATELLITE_EMBEDDING/V1/ANNUAL`

The study workflow extracts the 2023 annual embedding for the Hyrcanian
forest domain.

## Modeling and uncertainty

Random Forest regression is implemented with scikit-learn using 500
trees and the 64 AEF embedding dimensions. The notebook also contains
bootstrap resampling (100 iterations) for prediction uncertainty and
produces relative uncertainty measures for spatial prediction outputs.

## Reproducibility and restricted data

Because the NFI field observations and some spatial inputs cannot
legally be redistributed, this repository is a **code repository rather
than a complete data-and-code reproducibility package**. The analysis
can be adapted to equivalent user-supplied data with the required
schema. See `DATA_AVAILABILITY.md`.

## Citation

If you use this code, please cite the associated article and the
archived Zenodo release. The Zenodo DOI should be added to this README
and `CITATION.cff` after the first GitHub release is archived.

## License

No software license has been assigned yet. Before making the GitHub
repository public, the authors should select an appropriate open-source
license if they intend to permit reuse, modification, and redistribution
of the code. Until a license is added, normal copyright restrictions
apply.
