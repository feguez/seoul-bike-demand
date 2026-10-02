\# Data



\## Source



This project uses the \*\*Seoul Bike Sharing Demand\*\* dataset from the UCI Machine Learning Repository.



\- Dataset: Seoul Bike Sharing Demand

\- Repository: UCI Machine Learning Repository

\- UCI dataset ID: 560

\- DOI: `10.24432/C5F62R`

\- License: CC BY 4.0



Official dataset page:

https://archive.ics.uci.edu/dataset/560/seoul+bike+sharing+demand



The original file used in this project is:



`SeoulBikeData.csv`



\## Dataset Description



The dataset contains hourly bicycle rental demand from the Seoul Bike Sharing System together with weather and calendar information.



The uploaded project data contains:



\- \*\*8,760 hourly observations\*\*

\- \*\*14 columns\*\*

\- \*\*365 days of data\*\*

\- No missing values

\- One observation for each hour of each day



The project focuses on the \*\*2,208 summer observations\*\* from June through August.



\## Variables



The full dataset contains:



\- `Date`

\- `Rented\_Bike\_Count`

\- `Hour`

\- `Temperature`

\- `Humidity`

\- `Wind\_speed`

\- `Visibility`

\- `Dew\_point\_temperature`

\- `Solar\_Radiation`

\- `Rainfall`

\- `Snowfall`

\- `Seasons`

\- `Holiday`

\- `Functioning\_Day`



\## Modeling Variables



The response variable is:



`Rented\_Bike\_Count`



The primary models use eight quantitative predictors:



\- `Hour`

\- `Temperature`

\- `Humidity`

\- `Wind\_speed`

\- `Visibility`

\- `Dew\_point\_temperature`

\- `Solar\_Radiation`

\- `Rainfall`



`Seasons` is used to restrict the modeling analysis to summer observations.



`Snowfall`, `Holiday`, and `Functioning\_Day` are not included in the original model specification.



\## Scope



The models predict aggregate hourly rental demand across the system.



The dataset does not contain station-level inventory or routing information, so this project should be interpreted as a demand-prediction case.



\## Citation



Seoul Bike Sharing Demand \[Dataset]. (2020). UCI Machine Learning Repository.



DOI: https://doi.org/10.24432/C5F62R

