# SRS_Project_2

Google Drive Folder (containing .zip data file): https://drive.google.com/drive/folders/1duzNGo5EVhPuD7NN8ipNjuUqLYmhyQxR?usp=sharing


Question ideas:

1. Are some regions more impacted by global warming than others, and what characteristics distinguish these regions (ex. distance to coast, distance to equator, elevation, land cover type, etc.)?
2. When do we predict global warming to reach the "point of now return" in terms of global warming?
3. Using Bayesian Hierarchical spatio-temporal model to forecast temperature in Scotland.

   Three main objectives :
   1. Modelling with Bayesian Hierarchical spatio-temporal temperatures across scotland (until 2023)
   2. Evaluating model performance by comparing forecast temperature value in 2024 vs observed data
   3. Generate probabilistic temperature projections for the next 5 years (using datasets until 2024)
   
   Datasets/features : Temperature, Long, Lat, Time
   
   Preprocessing : Monthly temperature observations will be used to preserve temporal resolution and explicitly capture seasonal variability, which represents a key component of climate dynamics in Scotland. The available dataset spans the period 1901–2023, providing a long historical record suitable for analysing both long-term warming trends and intra-annual seasonal patterns. However, given the extensive temporal coverage and high spatial resolution of the data, it is not immediately clear whether the full dataset should be used for modelling. Therefore, an initial exploratory data analysis (EDA) will be conducted to examine the distributional characteristics of temperature at both annual and monthly scales, assess temporal stability and variability, and evaluate computational feasibility. This exploratory stage will inform decisions regarding the appropriate temporal window and spatial grid resolution to be included in the Bayesian hierarchical spatio-temporal framework. The final model will aim to capture temperature trends alongside spatially heterogeneous regional patterns across Scotland while accounting for seasonal effects and temporal dependence.
  
