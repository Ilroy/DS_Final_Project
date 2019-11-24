# Initial Findings

(i) We expect the model to perform decently on the test2 set. The potential MSE will be around 2 million based on the MSE that we got from test1 being about 1.5 million. We suspect test2 MSE will be slightly higher because the MSE from test1 may have some potential data leakge from it being used for some feature imputation. The main features driving the model are the size_sqft, bedrooms, bathrooms, encoded_zip, encoded_bor, and encoded_neighborhood, floornumber. They are the key features because they are the ones most correlated with the 'rent' target. The model also used other features like has_concierge, has_washer_dryer, has_gym, and has_doorman because they do show positive correlation with 'rent' but arent as extreme as the other features.

- Plans to improve our predictions:
  - Next we are going to try different regression methods to reduce MSE instead of just Random Forest Regressor:
    - Gradient Boosting Regressor.
  - We are also looking for datasets with features to attach to improve our prediction: 
    - Area of a race.
    - School area.
    - Restaurants area. 
  - With given enough time, we will validate those data we assume "non-sense":
    - Place with 0 bedroom/bathroom.
    - Place is insanely wide > 80000 sqrft.
    - Place with lots of bathrooms. 
  - We will try to come up with better imputations techniques by revisiting features like floornumber.
  _ we will try to test linear models like lasso, ridge, and ELastic regressors and their different regularizations methods to try and create predictors that best adjust weights of coefficients.
