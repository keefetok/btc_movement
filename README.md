Data Sourcing:
Data on historical price is/was readily available during the time period of 2024. Aside from this, more convoluted data such as open interest and ETF flows were not as readily available, and had to be sourced (and created/collated) with greater work done.
The data obtained on price was clean, and ready to be used but ETF was more messy with the need to manage only total_flows. However, difficulty was found with inconsistent usage of date formats from both files used (thus that giant line of date cleanup you see twice).
Also, there was a need to convert data from 'string' values to 'doubles' for querying use in pyspark sql.

Why pyspark sql over dbs such as bigquery, etc...?: 
Pyspark sql used for ease of transition downstream and for the spark ML properties that can be found later.

We then test and fit data accordingly to produce results that show us why predicting prices do not (even with help of computers) necessarily mean a 100% hit rate... even 50% is good enough... 

Star Schema/ER:

Fact Tables --Measures--> Fact Daily Price / Fact ETF flows / ML Predictions
Dimension Tables --Provides context--> Date/Trend/Volatility/ETF performance/Model
*Connection is primarily through date key, except ML prediction that needs model (which is independent to ML only).

fact table for daily price has date, trends and volatility (using primary key: date_key)
fact table for etf flows has date, etf performance (using primary key: date_key again)
ml_prediction will utilise date key for date and model 

makes it very easy to connect through an observable primary join key: date key
also, fact tables being further broken down allows for optimised querying

and scalability + flexibility is there with the fact that primary join key is the only concern here

ML is very basic design using random forest + linear regression (to test)


Overall, it can be seen that there are a plethora of data that correlate and must overlap to create an accurate prediction, which even then is still a good enough guess. 
