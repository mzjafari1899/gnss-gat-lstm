# Explainable GAT-LSTM for GNSS Displacement Modeling

This repository provides a **reproducible Jupyter Notebook** implementation of an **explainable Graph Attention–LSTM (GAT-LSTM)** framework for spatiotemporal modeling and forecasting of GNSS displacements.

## What this repository contains

- `gnss_gat_lstm_explainable.ipynb`  
  End-to-end workflow:
  - data loading & preprocessing (station-wise scaling, sequence construction)
  - graph construction (k-nearest neighbors on station coordinates)
  - GAT–LSTM training and evaluation (RMSE/MAE/R², real-scale evaluation)
  - feature importance (SHAP and permutation)
  - dynamic attention extraction and visualization

- `requirements.txt`  
  Python dependencies (open-source).

## Data sources (not included)

Due to data volume and licensing/terms, datasets are not bundled in this repository.

- **GNSS displacement data**: EarthScope / UNAVCO archive  
  https://www.unavco.org/

- **Meteorological variables**: Copernicus Climate Data Store (ERA5-Land)  
  https://cds.climate.copernicus.eu/

### Expected local input files
The notebook expects the following CSV files in the working directory (you can adapt paths inside the notebook if needed):

- `stations_coordinates.csv` (station metadata with latitude/longitude and station IDs)
- `merged_gnss_weather.csv` (merged daily GNSS displacement + meteorological variables)

## Data Description

This repository includes two preprocessed input files used by the GAT-LSTM model:

- `stations_coordinates.csv`  
  Contains the geographic coordinates (latitude, longitude) and station identifiers for the GNSS network.

- `merged_gnss_weather.csv`  
  Contains the merged and preprocessed time series of GNSS displacement components (dN, dE, dU) and co-located meteorological variables derived from ERA5.

These files were generated through preprocessing of publicly available raw datasets:
- GNSS observations from the EarthScope (UNAVCO) archive
- Meteorological variables from the Copernicus Climate Data Store (ERA5)

The preprocessing steps include quality control, temporal alignment, interpolation to daily resolution, and normalization.  
The raw datasets are not redistributed here due to size considerations but are publicly accessible from the original data providers.


## Environment setup

### Option A — using `pip` (recommended)
1. Create and activate a virtual environment:
   ```bash
   python -m venv .venv
   # Windows:
   .venv\Scripts\activate
   # macOS/Linux:
   source .venv/bin/activate
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Launch Jupyter:
   ```bash
   jupyter lab
   ```
   Open `gnss_gat_lstm_explainable.ipynb` and run cells top-to-bottom.

### Notes on PyTorch
Install PyTorch following the official selector for your system (CPU or CUDA):
https://pytorch.org/get-started/locally/

## Reproducibility notes
- The notebook uses chronological train/validation/test splits to avoid temporal leakage.
- Results may vary slightly due to stochastic optimization and random initialization.  
  Multi-run averaging is included for attention stability analysis.

## License
MIT License (see `LICENSE`).
