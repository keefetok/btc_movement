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
