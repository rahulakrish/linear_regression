# Phase_2 Project

## Description
  To help clients estimate selling prices of their home based on established factors. Also, to recommend any renovations that can be made to improve the resale value of the house
  
## Data Source
  King County House Sales dataset, which can be found in kc_house_data.csv
  
## Methodology
  Develop linear regression model to help predict house values. Dependent variable 'X' = price. 
  y = Independent(predictor) variables are the rest of the factors in the dataset.
  
  ![image](https://user-images.githubusercontent.com/108379254/196785246-257a1c9f-f82b-4ff3-ad2f-39cfba67d395.png)

  
### Step -1
Initially, we will look at the distribution of the variables in the dataset to check for normality. Though not mandatory, having normally distibuted varibales help the efficiency of the model.

![image](https://user-images.githubusercontent.com/108379254/196785216-d0e635b3-3f2f-4bbd-88b9-13c2cfa8cd96.png)


### Step-2
We will then apply log transformation of the non-nomral variables to make them normal and help increase the efficiency of the model.

![image](https://user-images.githubusercontent.com/108379254/196785314-597744c4-631d-4485-9db9-bb7b4dacc24d.png)


### Step-3
Next, since different variables have different values, we will apply scaling methods to make them more interpretable for the model. For eg. sqft_living is measure in thousands of sqft while price is in hundreds of thousands of dollars. Bringing them to a common scale will help boost model efficency

![image](https://user-images.githubusercontent.com/108379254/196785458-4c928354-7421-461a-8bba-23c1c5fd5ff7.png)


### Step-4
Model diagnostics : Using metrics like R-squared, RMSE values and Q-Q plots to interepret the fit of the final model. Also, check to see if the model fit violates linear regression assumptions

![image](https://user-images.githubusercontent.com/108379254/196786550-ccfda53a-9c50-4730-96bd-00e82f1a637a.png)

![image](https://user-images.githubusercontent.com/108379254/196786585-d8ce0b03-773d-403e-aeaf-72d75071f8db.png)


### Step-5 
Interpret the coeffecients of the predictor variables and pick out 2 to recommend to clients that will have the highest effect on the sale price of a house.

![image](https://user-images.githubusercontent.com/108379254/196786803-a70e32e2-3409-4403-a006-c0e6deb482dd.png)

## Model Results

![image](https://user-images.githubusercontent.com/108379254/196297573-d63eee13-725c-4f1c-8027-4661e6b71dde.png)

![image](https://user-images.githubusercontent.com/108379254/196786878-b6f48f2d-7ed3-41fd-b05d-50939eb53094.png)


## Conclusions
1. The model will be off by $184,335 when predicting the price of a house

2. Being on the waterfront is the most valuable asset when it comes to selling the house. It increases the value by nearly 50%. A unit increase in the grade, number of bathrooms and condition of the house yield 17.6%, 7.2% and 5.5% increase respectively

![image](https://user-images.githubusercontent.com/108379254/196786172-673019e5-911f-43fe-bfc6-c56ada113763.png)

