# Questions and Tasks

**1. Data Usage**

 ``` (a) What outside data have you appended to the original data set? Why did you choose this data?```
  - We appended a NYC DOE High School Directory as my external dataset. I chose this dataset 
    because it included columns with common values with the SE dataset, making merging easier. 
    Also the dataset was an interesting addition to apartment rentals, as families looking for 
    apartments could easily see what the best school in the borough would be. For future development 
    we hope to include the best school near the apartment listing as a oppose to just in the same borough.


 ```(b) Does the inclusion of this additional data raise any ethical considerations?```
 - The inclusion of this dataset does not itself raise any ethical concerns as 
   there is no fragile information being disclosed. Also, the dataset does not include 
   any information with regards to demographics in the schools and the data is solely 
   dependent on academic opportunities and performance of each individual school. 

    
**2. Data Exploration**

```(a) What outliers present issues for your analysis? How have you chosen to handle them? Why?```

   - We had outliers present when we observed our individual features like bedrooms, bathrooms,and size_sqft vs rent. We had observations that did not follow the general trend of the data,and proved difficult for our models to accurately predict with such discrepancies. In order to handle the outliers we chose to delete them from our datasets and after some observations, less than 1% of the data was dropped.

 ```(b) To what extent do missing values pose a challenge for your analysis? How have you chosen to handle them? Why?```

- |                 | Missing Ratio |
  | :-------------- | ------------- |
  | `line`          | 29.497534     |
  | `floornumber`   | 10.706883     |
  | `size_sqft`     | 7.254664      |
  | `year_built`    | 3.352155      |
  | `min_to_subway` | 1.022086      |
  | `unit`          | 0.800515      |
  | `addr_unit`     | 0.771925      |
  | `neighborhood`  | 0.021442      |

- This dataset did have a decent amount of missing data but most of which were on features that weren’t critical to our models, like `line` and `unit`. One feature that did need an extensive amount of correcting was `size_sqft` as it had a lot of values with 0. In order to handle these values we imputed values based on the avg of listings with similar bedrooms and bathrooms. To impute the other

- In most cases, we impute missing values of a category by its mean. For missing `line` values, we used mode of `zipcode` and `line` in that area. 

```(c) Are there any other aspects of the data your exploration shows might be problematic?```
 - Our exploration showed potential issues with `floor_count` and `floor number` as they seemed to show 
   a positive correlation with increase in their respective values but there were a lot of seemingly high
   values. These values were hard to determine to be outliers are building height in nyc doesn't equate
   to better quality as those exist in good and bad neighborhoods, which would affect rent value.


```(d) Create at least one visualization that demonstrates the predictive power of your data.```

- Before Dropping Outliers:
 - ![rent_vs_sqft](https://i.gyazo.com/2eb3d18e077bd9eca6d9855b977c3b27.png)
- After Dropping Outliers:
 - ![rent_vs_sqft_after](https://i.gyazo.com/6feba016bd4ac849b99b8550b4ed40ca.png)

**3. Transformation and Modeling**

``` (a) Describe 5 features you think play the biggest role in your model.```
        
        • How did you create these features?
        
        • How do you know these features are playing key roles?
        
        • If your modeling process uses less than five features, explain why you think other features didn’tadd value.
        

   - At first we constructed a heatmap to show the correlations between each features versus `rent`

   - ![heatmap](https://i.gyazo.com/3900811bf8acdcc692892f47dfaf93e2.png)

   - |      | **Most Correlated Features**        |
     | ---- | ----------------------------------- |
     | 0    | ```size_sqft```                     |
     | 1    | ```bathrooms```                     |
     | 2    | ```bedrooms```                      |
     | 3    | ```has_washer_dryer```              |
     | 4    | ```zipcode``` - personal preference |

- For the `zipcode` feature, we expected a much higher rent price in specific areas. 

```(b) Describe how you are implementing your model. Why do you think this works well?```

- We are implementing our model's by simply starting from a less complex model to more advanced models until there is no
more room for improvement. We started with a basic linear regression model and judged our imputations and outlier handling
using that model as it is the most sensitive to those. Then we introduced basic ensemble methods like random forest and continued
with hyperparameter tuning. Finally, we moved on to gradient boosting regressors, as they are known to perform better than the
random nature of forest regressors. We think this worked well as it allowed us to try and better our data for modelling using
a simple model and improve the regressor once we felt our data was good for training.

```(c) Describe your methodology for selecting your model. Why do you think this type of model works well?```

- We used 3 (4) different models to find the lowest MSE (compare to test1.csv):
  - Linear Regression is the worst which yield the MSE around 2.6m
  - Random Forest Regressor model yields 1.7m~1.9m before hyperparameters tuning
  - Gradient Boosting Regressor model yields the same MSE with RFR before hyperparameters tuning.
  - After tuning:
    - RFR is stable around 1.6m~1.7m
    - Gradient Boosting Regressor is stable around 1.48m~1.54m
- We choose to use Gradient Boosting Regressor because of its stability and low MSE.

**4. Metrics, Validation, and Evaluation**

```(a) How well do you think you model will perform on the hold out test set? How do you know?```

- The model will perform decentely on the hold out test set as our model, for test2, had an MSE of 1.6 million with respect to test1 and 1.0 with respect to test2. We expect similar results for test3 and, perhaps, slightly better as our predictive model's MSE has improved to about 1.5 mil for test1. We expect our MSE to be about 0.9 million.
 
```(b) Is your model useful? Why or why not?```

- Our model is useful in that, given properly and well documented data, it can predict rent values and provide a rough estimate of what you could see yourself spending given a certain amount of space, bedrooms, and bathrooms. Our model is not useful in that it is not 100% accurate and fails to capture certain anomalies in the rental listings where the prices are somewhat too good to be true for their respective features. Overall, our model is best used as an estimate of what areas and features, like bedrooms and bathrooms, you could get given a certain price range.

```(c) Are there any special cases in which your model works particularly well or particularly poorly?```
 - Our model seems to work well for cases that are "normal" in the sense that they perfectly follow the trends in our training data. Our data performs poorly on listings with large number of bathrooms,bedrooms, or size_sqft that are unusually cheap or expensive. 


```(d) Create at least one visualization that demonstrates the predictive power of your model.```

- [![Image from Gyazo](https://i.gyazo.com/30bcdf6d33944feb4412d8dca66b183e.png)](https://gyazo.com/30bcdf6d33944feb4412d8dca66b183e)

**5. Conclusion**

```(a) How would you use this model?```

 - As mentioned before, we would use this model as an estimate of what someone could expect given a certain price range. For example our model could estimate what a listing in a desired area, given some number of bedrooms and bathrooms, would cost the buyer. 


```(b) If you could have additional modeling features, what would they be?```

- We would like to have ethic and racial data of tenants. Because humans tends to live within areas they feel comfortable, and the `rent` prices depend heavily on that. also additional modeling feature we would like to have is the crime rate in the area as i suspect that a listing in a safer neighborhood would entice a higher value while the opposite would get a lower value. 


```(c) Would you rather have more data, or more features?```

- Because of **Law of Large Number**. We would rather have more data as more feature could prove to just provide "noise" and distract our model from actually useful features. More data would also let our model train better and learn better with more information that would help generalize the data better in a way that isnt heavily influenced by a few outliers.


**References**
[Modeling Inspiration](https://www.kaggle.com/erick5/predicting-house-prices-with-machine-learning)
- The above kaggle demo served as inspiration for handling outliers and missing data, it was crucial in visualizing our data
and general steps when approaching a new dataset
