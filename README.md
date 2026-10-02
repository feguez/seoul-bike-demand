\# Seoul Bike Rental Demand Prediction



Predicting hourly bicycle rental demand in Seoul using ensemble tree models, with a focus on whether model performance holds when evaluated on a genuinely later time period.



\## Business Problem



Bike-sharing demand changes throughout the day and under different weather conditions, creating planning challenges around bicycle availability, capacity, staffing, and peak-period preparation.



This project models hourly summer rental demand and compares several ensemble-learning approaches. In addition to the original random train/test split, I added a chronological holdout to test how well the models generalize to a future period.



\## Data



The dataset comes from the UCI Machine Learning Repository and contains:



\- 8,760 hourly observations covering one year

\- 2,208 summer observations used for modeling

\- Hourly bike rental counts

\- Weather and time-of-day variables



The response variable is:



`Rented\_Bike\_Count`



Eight quantitative predictors are used:



\- Hour

\- Temperature

\- Humidity

\- Wind Speed

\- Visibility

\- Dew Point Temperature

\- Solar Radiation

\- Rainfall



The original response was moderately right-skewed, so the modeling workflow retained a square-root transformation. Final model performance is also reported on the original bike-count scale for interpretability.



\## Modeling Approach



Three ensemble regression models were evaluated:



1\. \*\*Bagged Trees\*\*

&#x20;  - Implemented using `RandomForestRegressor`

&#x20;  - All eight predictors available at each split

&#x20;  - Number of trees tuned over 10, 100, and 1,000



2\. \*\*Random Forest\*\*

&#x20;  - `max\_features="sqrt"`

&#x20;  - Number of trees tuned over 10, 100, and 1,000



3\. \*\*Gradient Boosting\*\*

&#x20;  - Decision stumps (`max\_depth=1`)

&#x20;  - Number of trees: 10, 100, 1,000

&#x20;  - Learning rates: 0.001, 0.01, 0.1



Hyperparameters were selected using cross-validation rather than the final test sets.



\## Validation Strategy



\### Original Random Split



The original analysis randomly divided the 2,208 summer observations into:



\- 1,104 training observations

\- 1,104 test observations



All three models were evaluated using the same shuffled 5-fold cross-validation folds.



\### Temporal Holdout



To better represent future-period prediction, I added a chronological evaluation:



\- \*\*Training / model development:\*\* June 1 - August 8, 2018

\- \*\*Final test period:\*\* August 9 - August 31, 2018



Hyperparameters were selected using `TimeSeriesSplit` within the earlier training period before the final temporal test period was evaluated.



\## Results



\### Random-Split Test Performance



| Model | MAE | RMSE | R² |

| --- | ---: | ---: | ---: |

| Bagged Tree | \*\*191.7\*\* | \*\*291.3\*\* | \*\*0.818\*\* |

| Random Forest | 209.0 | 305.1 | 0.800 |

| Gradient Boosting | 218.3 | 314.2 | 0.788 |



\### Temporal Holdout Performance



| Model | MAE | RMSE | R² |

| --- | ---: | ---: | ---: |

| Bagged Tree | \*\*202.4\*\* | \*\*297.2\*\* | \*\*0.755\*\* |

| Random Forest | 227.7 | 312.1 | 0.730 |

| Gradient Boosting | 218.4 | 303.4 | 0.745 |



The \*\*Bagged Tree remained the strongest model under both validation approaches\*\*.



Performance weakened somewhat on the later temporal holdout, particularly in R², but the Bagged Tree's RMSE increased only moderately from approximately 291 to 297 bikes. This provides a more conservative estimate of performance than the random split while showing that the model retained useful predictive accuracy on a later period.



\## Demand and Error Patterns



Time of day was the strongest predictive feature across the fitted ensemble models.



The temporal error analysis also showed that prediction errors were larger during high-demand periods:



\- Peak-demand MAE: approximately \*\*269 bikes\*\*

\- Non-peak MAE: approximately \*\*180 bikes\*\*

\- Largest average errors occurred around \*\*8:00 and 18:00\*\*



These periods also correspond to major morning and evening demand peaks, making prediction error during those hours particularly relevant for operational planning.



\## Model Interpretation



A small four-leaf regression tree was also fit as an interpretability aid.



The first split separates earlier and later hours, while Solar Radiation and Rainfall appear in subsequent branches. These patterns describe predictive relationships in the historical data and should not be interpreted as causal effects.



\## Illustrative Hourly Scenario



The notebook includes an illustrative scenario in which weather variables are held constant at their summer means while Hour varies from 0 to 23.



This is a constructed scenario intended to illustrate model behavior. It is \*\*not\*\* used as a model-accuracy test or presented as a real operational deployment.



\## Repository Structure



```text

seoul-bike-demand/

│

├── README.md

├── seoul\_bike\_demand.ipynb

├── SeoulBikeData.csv

├── DATA.md

├── requirements.txt

└── .gitignore



\## Tools



Python, pandas, NumPy, scikit-learn, Matplotlib



\## Reproduction



1\. Clone the repository.

2\. Install the packages listed in requirements.txt.

3\. Open seoul\_bike\_demand.ipynb.

4\. Run the notebook from top to bottom with SeoulBikeData.csv in the repository root.

