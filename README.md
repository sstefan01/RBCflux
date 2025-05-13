# RBC Flux Estimation from OCT Time-Traces using Deep Learning

This repository provides MATLAB code and a pre-trained Convolutional Neural Network (CNN) model for estimating Red Blood Cell (RBC) flux and its associated uncertainty from Optical Coherence Tomography (OCT) time-traces. The methodology is based on the research paper:

Stefan S, Kim A, Marchand PJ, Lesage F and Lee J (2022) **Deep Learning and Simulation for the Estimation of Red Blood Cell Flux With Optical Coherence Tomography.** *Front. Neurosci. 16:835773.* doi: [10.3389/fnins.2022.835773](https://doi.org/10.3389/fnins.2022.835773)

## Overview

The provided MATLAB script (`estimate_rbc_flux.mlx` or `estimate_rbc_flux.m`) uses a pre-trained 1D CNN (`net_flux.mat`) to analyze OCT time-series data. The network outputs an RBC flux estimate and a corresponding uncertainty value for each input time-trace. The script also includes functionality to compare these estimates against ground truth data if available.

## Files in this Repository

* **`RBC_flux_estimation.mlx`**: A MATLAB Live Script providing a step-by-step guide to load data, run the model, and visualize results. This is recommended for an interactive experience. (Alternatively, an `estimate_rbc_flux.m` plain script might be provided).
* **`net_flux.mat`**: A MATLAB data file containing the pre-trained 1D CNN model.
* **`OCT_timetraces.mat.zip`**: A zipped archive containing sample OCT data.
    * **IMPORTANT:** You must **unzip this file** after downloading to obtain `OCT_timetraces.mat`.
    * `OCT_timetraces.mat` contains:
        * `p`: A matrix of OCT time-traces (each column or row typically representing a time-trace of 512 points).
        * `tpm_peak`: A vector containing the ground truth RBC counts obtained from Two-Photon Microscopy (TPEF), corresponding to each time-trace in `p`.

## Prerequisites

* **MATLAB**: Version R2016a or later is recommended for `.mlx` files (Live Scripts).
* **MATLAB Deep Learning Toolbox**: Required for the `activations` function and to run the neural network.

## Instructions for Use

1.  **Clone or Download the Repository:**
    Obtain all files from this repository.

2.  **Unzip the Sample Data:**
    Locate the `OCT_timetraces.mat.zip` file and **unzip it**. This will create the `OCT_timetraces.mat` file in the same directory.

3.  **Set up MATLAB Environment:**
    * Open MATLAB.
    * Navigate to the directory where you downloaded and unzipped the files.
    * Ensure that `estimate_rbc_flux.mlx` (or `.m`), `net_flux.mat`, and the unzipped `OCT_timetraces.mat` are in the MATLAB path or the current working directory.

4.  **Run the Script:**
    * **If using `estimate_rbc_flux.mlx`:** Open it in the MATLAB Live Editor and run the sections sequentially or click "Run All".
    * **If using `estimate_rbc_flux.m`:** Open it in the MATLAB Editor and click "Run", or type `estimate_rbc_flux` in the MATLAB command window and press Enter.

## Input Data Format

The pre-trained model (`net_flux.mat`) expects OCT time-traces as input. The sample data in `OCT_timetraces.mat` provides:
* `p`: The OCT time-series data. The model was trained with traces consisting of **512 time points** each, acquired over 768ms (1.5ms interval per point). The script attempts to handle data where traces are organized as columns (e.g., `512 x NumberOfTraces`).
* `tpm_peak`: Ground truth values used for validation in the provided script.

## Output

The script will:
1.  Load the OCT time-traces and the pre-trained network.
2.  Estimate RBC flux (`flux_estimate`) and its uncertainty (`flux_std`) for each time-trace.
3.  Display the number of traces processed and an example of the estimated flux and uncertainty.
4.  Generate a scatter plot comparing the CNN-estimated flux against the ground truth flux (derived from `tpm_peak`), along with an R-squared value.

## Generating OCT Time-Traces from Raw Microangiograms

If you wish to process your own OCT microangiogram data to extract the 1D time-traces required as input for this model, please refer to the tools and methods described in:
* [OCTA_microangiogram_properties GitHub repository](https://github.com/sstefan01/OCTA_microangiogram_properties) (Stefan and Lee, 2020, "Deep learning toolbox for automated enhancement, segmentation, and graphing of cortical optical coherence tomography microangiograms").

## Citation

If you use this code or the pre-trained model in your research, please cite the following paper:

```bibtex
@article{Stefan2022flux,
    author = {Stefan, Sabina and Kim, Anna and Marchand, Paul J. and Lesage, Frederic and Lee, Jonghwan},
    title = {Deep Learning and Simulation for the Estimation of Red Blood Cell Flux With Optical Coherence Tomography},
    journal = {Frontiers in Neuroscience},
    volume = {16},
    pages = {835773},
    year = {2022},
    doi = {10.3389/fnins.2022.835773},
    url = {[https://www.frontiersin.org/articles/10.3389/fnins.2022.835773](https://www.frontiersin.org/articles/10.3389/fnins.2022.835773)}
}
