# SRS_Project_2

Google Drive Folder (containing .zip data file): https://drive.google.com/drive/folders/1duzNGo5EVhPuD7NN8ipNjuUqLYmhyQxR?usp=sharing

Overleaf: https://www.overleaf.com/6786221333tbsdhqpqqnpk#5d7299

Research Question:
1. How do long-term temporal trend and spatial dependence explain monthly temperature anomalies over Scotland (1901–2024)?
2. Do Bayesian spatio-temporal models outperform simpler deterministic/frequentist baselines in explaining and predicting anomalies (especially 2021–2024)?

Objectives :
1. Construct anomalies from raw temperature (Python) so the response represents departures from a baseline climatology
2. Fit a sequence of Bayesian hierarchical models:
   - Baseline
   - Baseline + smooth trend (RW2)
   - Baseline + trend + spatial (BYM2)
   - Baseline + trend + spatial + space–time interaction
3. Add frequentist/deterministic models for comparison
4. Compare models using:
   - Bayesian: WAIC, DIC
   - Predictive: MAE and RMSE on a held-out period (test 2021–2024; train 1901–2020)

Datasets used:
1. Core NetCDF: ds_scotland.nc
   - raw temperature: tmp
   - temperature anomaly relative to climatology baseline: anom
   - coordinates: lon, lat
   - monthly time 1901–2024: time
2. Derived analysis table: long-format panel data with one row per (cell, month)
   
Preprocessing :
1. Read NetCDF and align time
   - Load tmp (raw temperature) and grid/time metadata.
   - Ensure monthly time index exists and is correctly mapped to layers
   - Keep only grid cells whose centroids fall inside Scotland boundary
2. Convert raw temperature to anomalies in Python using climatology window of 1961–1990 (WMO), computed per grid cell so spatial differences in mean climate are removed before modelling. Missing cells (sea/outside Scotland) are kept as NaN.
3. Export the dataset into ds_scotland.nc containing tmp, anom, lon, lat, and time
4. Convert the data to long format in R and remove invalid/non-Scotland grids (sea / outside mask)
5. Create model indices
   - space_id = integer id per remaining cell
   - time_id = integer month index (1…T)
   - Data split:
        - Train: 1901–2020
        - Test: 2021–2024
6. Construct spatial adjacency for BYM2
   - Define neighbours (rook/queen adjacency)
   - Build adjacency matrix
   - Convert to INLA graph object
7. Fit all proposed models
8. Model evaluation

To do:
- (Max and Jackson):
   - do same with frequentist model. use anomaly data and regular data like was done with bayesian - Done
   - (and maybe do same with deterministic too - climatology avg. 1961-1990). make chart like wind speed  - Done
   - try to fix the interaction term in bayesian model
   - change train,test split to a train,validation,test split (use validation for model/hyperpareter tuning, test on final model)
   - look for papers to cite
   - 
- (Fe and Nurma):
   - look for papers to cite
