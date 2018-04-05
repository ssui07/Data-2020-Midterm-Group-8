# What Factors Impact NYC Median Household Income?

This site hosts the midterm project for Data2020.

Contributors:
Siyao Sui, Chuqing Wang, Xiao Sun


## Data

The dataset for our project comes from the New York City census data taken from the 2015 American Community Survey 5-Year Estimates. 

The originial dataset contains 36 columns and 2168 rows.

It contains information including *income, income percapita, total population, gender distribution, racial distribution, citizenship, poverty rate, job type, employment rate, employment type, poverty level etc.*

Some of the categorical variables are complemental (percentage sum to 100%):

*By Gender: Men, Women*

*By Race: Hispanic, White, Black, Native, Asian*

*By Citizenship: Citizen, Non-citizen*

*By Job Type: Professional, Service, Office, Construction, Production*

*By Commute Type: Drive, Carpool, Transit, Walk, OtherTransp, WorkAtHome*

*By Employment Type: PrivateWork, PublicWork, SelfEmployed*

## Purpose

We want to perform regression analysis on the census data by constructing good estimation models for median household income and income per capita. By analyzing and comparing these two models, we can investigate the causal effect relationship between the predictors as well as their strength of impact on income in NYC and the surrounding area.

We want to study the data set and develop some insights by investigating the following:

- What is the distribution of income in the given NYC area?
- What impact do gender, race, citizenship, job type, commute type and employment type have on income levels?
- What impact does median household income have on poverty levels?
- What impact does commute time to workplace have on income levels?

## Methodology



### Choices of Models 

We decided to use the following regression models.

*1.General Linear Regression*

*2.Multiple Linear Regression*

*3.Ridge Regression*

*4.Stepwise Regression*

### Testing the Prediction Accuracy

We divide the dataset into one training set and one testing set randomly. We conducted model selections on the training set, and applied the model onto the testing set. For each sample in the testing set, we made prediciton using the selected model and constructed an 95% confidence interval for the prediction value. If the actual value of income or income per capita falls into the range of the predicition's confidence interval, we think this prediction is accurate. 

## Visualization and Observasions

### Income Heatmap
![incomeMap](/Income.png) 
### (left:) Commute Time vs. Income;  (right:) Commuters traveling by Drive vs. Income
![CommuteTypeMap](/Commute.png)
### Poverty Level vs. Income
![PovertyMap](/Poverty.png)
### Population Size vs. Income
![TotalPopMap](/TotalPop.png) 
### Male Percentage vs. Income
![MenMap](/Men.png)
### White People Percentage vs. Income
![WhiteMap](/White.png)
### Professional(Management,business,science and arts) Jobs vs. Income
![ProfessionalMap](/Professional.png)

