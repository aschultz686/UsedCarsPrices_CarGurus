# `Used Cars Prices from CarGurus`


## `Summary`
In this project, the various features of cars including the price of used cars were examined and evaluated using various algorithms with hyperparameter optimization. 


## `Objectives`

- Which features of used vehicles should be used in predictive modeling? 
- Does location and time affect the price of used cars, and how could this contribute to building models to predict the price of vehicles?


## `Data`
The `used_cars_data` was retrieved from [Kaggle](https://www.kaggle.com/ananaymital/us-used-cars-dataset). The individal who posted the data used a webcrawler on the Cargurus inventory in September 2020. This data contains a vast amount of information about the physical and mechanical components of cars that can provide insight into what might contribute to the increase in value of a vehicle.


## `Preprocessing`
The data was processed for missingness, relevancy and high dimensionality of categorical variables. Features were enginereed using various approaches. The data was then filtered for year, price and location after examining the distributions. Exploratory data analysis was completed for the quantitative and qualitative features. 


## `Modeling`


### `Machine Learning`
Models were trained using:
- `XGBoost` 
- `Catboost` 
- `LightGBM`
- `RAPIDS`: `Logistic`/`Ridge`/`Elastic Net`, `LinearSVR`, `Random Forest`, `XGBoost`, `Catboost`, `LightGBM`, `K-Nearest Neighbors` Regression


#### `Hyperparameter Optimization`
For hyperparameter tuning, `hyperopt` and `optuna` were utilized to explore the model parameters that resulted in the lowest error (`rmse`). Various trial/experiment sizes were completed to determine which parameters when incorporated into the model resulted in the lowest error. `Weights & Biases` was utilized for examining the models during HPO.


#### `Model Explanations`
To explain the results from modeling, `eli5`, `shap` and `lime` were utilized.


#### `Testing Various GPUs`
Using `XGBoost`, `Catboost` and `LightGBM`, various GPUs (`Quadro RTX 4000`, `Quadro RTX 5000`, `RTX A4000`, `Quadro P5000`) were tested using set parameters and various hyperparameter spaces. Subsequently, set parameters using only a `Quadro RTX 4000` and a set number of `Optuna` trials were utilized to compare hyperparameter optimization with/without `cuML` using a train/test split using a `XGBoost DMatrix`, `Scikit-Learn Wrapper interface for XGBoost` and differing cross validation (3, 5 and 10-fold) using `xgboost.cv`. `Weights & Biases` was used for tracking.


### `Deep Learning`
Models were trained using:
- `tensorflow` library


#### `Hyperparameter Optimization`
`keras-tuner` was used for tuning the MLP parameters. Various `num_layers`, `layer_size` and `learning_rate` values were used to tune the model. A `Dropout` layer = `0.3` was used before the `Dense` layer. `mae` was used for the loss of the model. Different combinations were tested during HPO with `executions_per_trial=2`. Subsequent models were fit, saved and evaluated for the predicted vs. actual price of used cars.


## `Deploy Models`
The `Streamlit` frontend was deployed using `Streamlit Cloud` and `Heroku`. The `Streamlit` frontend and the `FastAPI` backend was deployed using `CloudRun` on `Google Cloud Platform` where the user can upload a dataset in a `csv` file and predictions are generated for the `predicted price`, the `predicted difference` and the `predicted percentage difference` compared to the actual vehicle `price` using `LightGBM`, `Catboost` and `XGBoost`.
