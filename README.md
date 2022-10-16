# Phase_2 Project

## Description
  To help clients estimate selling prices of their home based on established factors. Also, to recommend how they can improve their home values 
  
## Data Source
  King County House Sales dataset, which can be found in kc_house_data.csv
  
## Methodology
  Develop linear regression model to help predict house values. Dependent variable 'X' = price. 
  y = Independent(predictor) variables are the rest of the factors in the dataset.
  
### Step -1
Initially, we will look at the distribution of the variables in the dataset to check for normality. Though not mandatory, having normally distibuted varibales help the efficiency of the model.

### Step-2
We will then apply log transformation of the non-nomral variables to make them normal and help increase the efficiency of the model.

### Step-3
Next, since different variables have different values, we will apply scaling methods to make them more interpretable for the model. For eg. sqft_living is measure in thousands of sqft while price is in hundreds of thousands of dollars. Bringing them to a common scale will help boost model efficency

### Step-4
Model diagnostics : Using metrics like R-squared, RMSE values and Q-Q plots to interepret the fit of the final model. Also, check to see if the model fit violates linear regression assumptions

### Step-5 
Interpret the coeffecients of the predictor variables and pick out 2 to recommend to clients that will have the highest effect on the sale price of a house.
