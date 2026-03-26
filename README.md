Solidago UAV Classification Workflow

This repository contains an R-based workflow for detecting and mapping invasive goldenrods (Solidago spp.) using high-resolution UAV RGB orthomosaics.

The script implements a complete pipeline from feature extraction to classification and accuracy evaluation, designed for reproducible creation of reference datasets for large-scale satellite mapping.

What this repository does

The workflow performs the following steps:

It extracts texture features (GLCM) from RGB imagery.
It computes multiple vegetation and colour-based spectral indices.
It builds a multilayer predictor stack.
It performs Random Forest classification with 10 repeated runs.
It evaluates model performance using precision, recall, and F1-score.
It generates a final prediction map.

The approach is designed for complex and heterogeneous landscapes where invasive species detection is difficult.

Input data requirements

The script expects the following files in the working directory:

Orthomosaic (GeoTIFF)
Filename: orthophoto.tif
The file must contain at least 3 bands (RGB). High-resolution UAV imagery is recommended.

Reference data (Shapefile)
Filename: reference.shp
The file must include a column named class.

Expected class labels:

goldenrod
other

All shapefile components such as .dbf, .shx, and .prj must be present.

Data availability

The data provided in this repository represent a sample dataset used in the study.
It includes one orthomosaic out of the 79 UAV datasets analysed in the article.

If you are interested in accessing the full dataset, please contact the corresponding author:

Bożena Omeliańska
Email: bomelianska@twarda.pan.pl

Installation

Install required R packages:

install.packages(c("glcm", "terra", "sf", "caret", "randomForest", "openxlsx", "raster"))
How to run
Place input files in your working directory:
orthophoto.tif
reference.shp
Open the script in R or RStudio.
Set the working directory if needed:
setwd("path/to/your/data")
Run the script from top to bottom.
Output files

The script generates several outputs.

Feature layers:

glcm_results_red.tif
glcm_results_green.tif
glcm_results_blue.tif
tgi_results.tif
veg_results.tif
bi_results.tif
bcc_results.tif
vndvi_results.tif
cive_results.tif
ipca_results.tif
mgrvi_results.tif
predictor_stack.tif

Model outputs:

classification_results.RData, models and metrics from all iterations
f1_scores.csv, F1 scores across repetitions
f1_scores_results_2classes.xlsx, final metrics from the last iteration

Final prediction map:

prediction_map.tif
Methodological notes
Texture features are computed using a 3 × 3 moving window for each RGB channel.
Spectral indices are derived from RGB imagery and do not require NIR data.
Training and validation split is performed at the pixel level with a 50:50 ratio.
Model robustness is assessed using 10 independent repetitions.
Random Forest is trained with 500 trees.
The final prediction map is generated using the model from the last repetition.
Intended use

This workflow is designed for:

creating high-quality UAV-based reference datasets,
supporting satellite-based classification workflows,
analysing feature importance in vegetation mapping,
monitoring invasive species in complex landscapes.
Limitations
Pixel-based sampling may introduce spatial autocorrelation.
Results depend strongly on the quality and representativeness of reference data.
RGB-based indices usually provide lower class separability than multispectral data.
Related publication

This repository accompanies the article:

Building a representative UAV RGB reference dataset for national-scale satellite mapping of invasive goldenrods (Solidago spp.): an efficient workflow and accuracy drivers

Citation

If you use this workflow, please cite the associated publication.

Contact

For questions or collaboration, contact:

Bożena Omeliańska
bomelianska@twarda.pan.pl
