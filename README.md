# SRS_Project_2

Google Drive Folder (containing .zip data file): https://drive.google.com/drive/folders/1duzNGo5EVhPuD7NN8ipNjuUqLYmhyQxR?usp=sharing

Overleaf: https://www.overleaf.com/6786221333tbsdhqpqqnpk#5d7299

Research Question:
1. How do long-term temporal trends, spatial dependence, and geographic covariates (elevation and distance to coast) explain monthly temperature anomalies over the USA (1991–2024)?
2. To what extent do Bayesian spatio-temporal models, incorporating elevation and distance-to-coast covariates, improve predictive accuracy for recent anomalies (2021–2024) compared to simpler Bayesian baselines?

Objectives :
1. Construct temperature anomalies from raw temperature data so that values represent departures from a baseline climatology.
2. Fit a sequence of Bayesian hierarchical models:
   - Baseline
   - Baseline + smooth trend (RW2)
   - Baseline + smooth trend (RW2) + spatial (BYM2)
   - Baseline + smooth trend (RW2) + spatial (BYM2) + covariates (elevation, distance to coast)
3. Evaluate model performance using:
   - Bayesian: WAIC, DIC
   - Predictive: MAE and RMSE on a held-out period (test 2021–2024; train 1991–2020)

Datasets used:
1. Core NetCDF: cru_ts4.09.1901.2024.tmp.dat.nc
   - raw temperature: tmp
   - temperature anomaly relative to climatology baseline: anom
   - coordinates: lon, lat
   - monthly time 1991–2024: time
2. Derived analysis table:
   - long-format panel data with one row per (cell, month)
   - includes covariates: elevation and distance_to_coast
   
Preprocessing :
1. Read NetCDF and align time
   - Load tmp (raw temperature) and grid/time metadata.
   - Ensure monthly time index exists and is correctly mapped to layers
   - Keep only grid cells whose centroids fall within USA boundary
2. Calculate temperature anomalies (Python)
   - Use climatology window 1961–1990 (WMO convention) per grid cell.
   - Anomalies = deviations from baseline to remove spatial differences in mean climate.
   - Keep missing cells (sea/outside USA) as NaN.
   - Calculate distance to coast covariate.
   - Save ds_us.nc containing tmp, anom, lon, lat, distance_to_coast, and time.
3. Generate elevation data add it to other layers (R)
   - Save ds_usa.nc containing anom, lon, lat, elevation, distance_to_coast, and time.
4. Convert the data to long format in R and remove invalid/non-USA grids (sea / outside mask)
5. Slicing the data. Focus analysis on 1991–2024 to capture recent warming dynamics relative to the 1961–1990 climatology.
6. Create model indices
   - space_id = integer id per remaining cell
   - time_id = integer month index (1…T)
   - Data split:
        - Train: 1991–2020
        - Test: 2021–2024
7. Construct spatial adjacency for BYM2
   - Define neighbours (rook/queen adjacency)
   - Build adjacency matrix
   - Convert to INLA graph object
8. Fit all proposed models
9. Model evaluation

To do:
- look for papers to cite
