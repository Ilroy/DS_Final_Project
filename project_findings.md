# Questions and Tasks

**1. Data Usage**

 ``` (a) What outside data have you appended to the original data set? Why did you choose this data?```

- 

 ```(b) Does the inclusion of this additional data raise any ethical considerations?```
    
**2. Data Exploration**

```(a) What outliers present issues for your analysis? How have you chosen to handle them? Why?```

   - The outliers exists in Brooklyn and Manhattan areas.  Which brings the average rent up to 100% difference compares to other areas. Because we know there are reasons for them to be that high, we decided not to touch it and leave it there. 

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

- From initial finding, missing values in categories account for less than 10% of data in data set except `line` (29%). we expected the difference will not be significant

- In most cases, we impute missing values of a category by its mean. For missing `line` values, we used mode of `zipcode` and `line` in that area. 

```(c) Are there any other aspects of the data your exploration shows might be problematic?```

- 

```(d) Create at least one visualization that demonstrates the predictive power of your data.```

- 

**3. Transformation and Modeling**

``` (a) Describe 5 features you think play the biggest role in your model.```

        ```• How did you create these features?```
        ```• How do you know these features are playing key roles?```
        ```• If your modeling process uses less than five features, explain why you think other features didn’tadd value.```

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

- 

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

- 

```(b) Is your model useful? Why or why not?```

- 

```(c) Are there any special cases in which your model works particularly well or particularly poorly?```

- 

```(d) Create at least one visualization that demonstrates the predictive power of your model.```

- 

**5. Conclusion**

```(a) How would you use this model?```

- 

```(b) If you could have additional modeling features, what would they be?```

- We would like to have ethic and racial data of tenants. Because humans tends to live within areas they feel comfortable, and the `rent` prices depend heavily on that.

```(c) Would you rather have more data, or more features?```

- Because of **Law of Large Number**, we would like to have more data to work with.
