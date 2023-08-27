# Predict housing prices in using Linear Regression

## Business Problem
1. To develop a model for ACME Real Estate Agency to accurately predict a value of a house based on avaliable data. This will help their clients, either buy or sell their homes at a fair price.
2. To identify if renovations can be made to improve the selling price of the house.

## Methodology
By developing using a Linear Regression model, we will try to predict the selling price of a house based on attributes like size, number of bedrooms/bathroorms etc. Model performance will be assesed by checking MAE and R-squared values.
MAE can tell us how accurate the model is in terms of pricing while R2 value tells us how much of the variance in the price the model can account for using the features in the dataset.

## Dataset
Dataset used will be the King County House Sales dataset : `kc_house_data.csv`

### Mapping house prices

Since location is king in real-estate, let's plot the listings in a map of King's county and highlight the distribution of prices.

![m](https://github.com/rahulakrish/linear_regression/assets/108379254/4b1f6f81-7c75-46b7-911c-fa4f984993a5)

## Baseline Regression Model - OLS using Statsmodels

Statsmodels is a powerful package for statistical analysis in Python. The Ordinary Least Squares regression is a method to estimate the unknown parameters in a linear regression model. It minimizes the sum of squared vertical distances between the observed values and the values predicted by linear approximation.

|   **_Model_**  | **_MAE_** | **_R-squared_** |
|:--------------:|:---------:|:---------------:|
| baseline_model | 125916.46 |             0.7 |


## Multicollinearity
Ideally, features in the dataset should be independent of each other. If not, this would make difficult to asceratin the effect of each feature on the dependent variable. By running a heatmap and removing coorelated features we hope tp see an improvement in
model performance:

![mc](https://github.com/rahulakrish/linear_regression/assets/108379254/0c638986-c08c-4bfc-b510-38675bb3b6b7)

Running a new model with correlated features removed:

|   **_Model_**  | **_MAE_** | **_R-squared_** |
|:--------------:|:---------:|:---------------:|
| baseline_model | 125916.46 |             0.7 |
|     multi_coll | 126148.38 |           0.699 |

## Scaling

If the independent variables all have different scales, then this could lead to misinterpretation i.e. features represented on a larger scale might have larger coefficents. By making the scale uniform across the data set, this will help improve model performance.

|   **_Model_**  | **_MAE_** | **_R-squared_** |
|:--------------:|:---------:|:---------------:|
| baseline_model | 125916.46 |             0.7 |
|     multi_coll | 126148.38 |           0.699 |
|         scaled | 126148.38 |           0.699 |


## Log-Transformation

Linear Rergression works well with normally distributed variables. Let's check to see if the data satisfies this condition:

![d](https://github.com/rahulakrish/linear_regression/assets/108379254/238856c1-ad36-4f5a-a062-59f94205e5d7)

Doing a log-transformation of the dependent variable,'price':

![p](https://github.com/rahulakrish/linear_regression/assets/108379254/885f923e-1999-421d-98f8-8673c8affe49)

It's clear to see how applying a log-transformation has made the variable more normally distributed. Running the model:

|     **_Model_**     | **_MAE_** | **_R-squared_** |
|:-------------------:|:---------:|:---------------:|
|      baseline_model | 125916.46 |             0.7 |
|          multi_coll | 126148.38 |           0.699 |
|              scaled | 126148.38 |           0.699 |
| log_transform_price | 540075.09 |           0.765 |

There is quite a jump in performance.

## Regression model diagnostics
Since we've built a few different models, it is probably a good idea now to check if the models satisfy if they satisfy some of the conditions of Linear Regression. Follwing are the conditions:

1. Linearity: There is a linear relationship between the dependent and independent variables
2. Homoscedasticity: The variance of the residuals are the same for any value of x
3. Normality: The residuals are normally distributed

### Linearity
We can check to see how the predicted values line up against the actual values and check for linearity:

![l](https://github.com/rahulakrish/linear_regression/assets/108379254/5ea3cf71-a1ca-4722-9d60-083cbe7e0f1d)

We can see that the model does a decent job of trying to fit to the data and also the presence of outliers in the data

### Homoscedasticity
This states that the variance of the residuals should be random i.e. there residuals smust have equal variance over the entire regression model.

This can be verified using a scatter plot of the predicted values against residuals:

![h](https://github.com/rahulakrish/linear_regression/assets/108379254/7ae0aec9-636c-42cc-866b-9a4f3c08ade9)

### Normality residuals : Q-Q plot
used to check for the normality of the residuals

![q](https://github.com/rahulakrish/linear_regression/assets/108379254/9ead41fb-55f8-42d6-b8b2-e775b1740fbe)

## Removing Outliers
Since we detected outliers while running model diagnostics, let's remove them to see if model performance improves.
A box-plot is most useful when it comes to looking for outliers:

![o](https://github.com/rahulakrish/linear_regression/assets/108379254/0d012024-058c-4c9b-8b58-e612061d6f9d)

Looks like there are lots of houses worth more than a million USD. Let's filter them out:

![o](https://github.com/rahulakrish/linear_regression/assets/108379254/c6b7e096-71ef-4e1b-8040-c7bc0c344a04)

Running a new model:

|     **_Model_**     |   **_MAE_**  | **_R-squared_** |
|:-------------------:|:------------:|:---------------:|
|      baseline_model |    125916.46 |             0.7 |
|          multi_coll |    126148.38 |           0.699 |
|              scaled |    126148.38 |           0.699 |
| log_transform_price |    540075.09 |           0.765 |
|     outlier_removed | 84387.020000 |           0.681 |

## Log-Transform of outlier removed data

Like earlier, we can also apply log-transformations to 'price' and build a new model:

|       **_Model_**      |   **_MAE_**  | **_R-squared_** |
|:----------------------:|:------------:|:---------------:|
|         baseline_model |    125916.46 |             0.7 |
|             multi_coll |    126148.38 |           0.699 |
|                 scaled |    126148.38 |           0.699 |
|    log_transform_price |    540075.09 |           0.765 |
|        outlier_removed | 84387.020000 |           0.681 |
| transf_outlier_removed | 86649.343354 |           0.692 |

## Log-Transformation of more features
Since model performance imporved considerably by log-transforming the dependent variable, let's transforms some of the other continuous features and check for performance

|       **_Model_**      |   **_MAE_**   | **_R-squared_** |
|:----------------------:|:-------------:|:---------------:|
|         baseline_model |     125916.46 |             0.7 |
|             multi_coll |     126148.38 |           0.699 |
|                 scaled |     126148.38 |           0.699 |
|    log_transform_price |     540075.09 |           0.765 |
|        outlier_removed |  84387.020000 |           0.681 |
| transf_outlier_removed |  86649.343354 |           0.692 |
|     more_log_transform | 109612.076092 |           0.766 |

## Model Selection

We have 2 objectives for our model:
1. To be able to predict a value of a house - depends on MAE value
2. To determine factors that will increase the value of the house - depends upon the R-squared value.

Based on the results of the different models, we will have to strike a balance between both objectives. We can choose the model with **outliers_removed and log transformed dependent variable** since the it can explain approx. 70% of the variance in the price and has the second lowest MAE value.

## Model Interpretation

To find out which factors play a significant role in the price of a house, we need to look at the model coefficients:

![f](https://github.com/rahulakrish/linear_regression/assets/108379254/dee070d8-291f-4658-9f0f-d9b35e584019)

Unsurprsingly, being on the waterfront is the biggest contributor to a house's value, approx 35%. Grade, which refers to the the quality of the materials used to build the house, is the second biggest contributor at 7%. Floors, condition and number of bathrooms all have similar impacts between 5% and 7%.

## Limitations

Since the dataset has nearly 7% of houses with values greater than $1 million USD, this impacts the linear regression model. A seperate analysis will have to be done for the high-value houses.

## Conclusion

1. The model is not very accurate since the predicted values are off by approx. $87,000. Other modelling techniques may yield more accurate predictions.

2. Next to having a waterfront, build quality, number of bathrooms and overall condition of the house play the biggest factors when it comes to the resale value of a house


