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

### Data Cleaning

The originial dataset contains 36 columns and 2168 rows.
72 (about 3%) rows contain NA‘s and are removed.

### Data Analysis

We first explored the data with plots in both ggplot2 and leaflet. 
Then we built two sets of models to predict median household income and income per capita.
In building the models, we added some interaction terms and log transformed the predictor.

#### Choices of Models 

We decided to use the following regression models:

*1.Multiple Linear Regression*

*2.Best Subset Regression*

*3.Linear Regression with Ridge Penalization*

*4.Linear Regression with Lasso Penalization*

#### Testing the Prediction Accuracy

We divide the dataset into one training set and one testing set randomly. We conducted model selections on the training set, and applied the model onto the testing set. For each sample in the testing set, we made prediciton using the selected model and constructed an 95% confidence interval for the prediction value. If the actual value of income or income per capita falls into the range of the predicition's confidence interval, we think this prediction is accurate. We also performed cross-validation to find the best set of parameters for each model. By comparing the test accuracy under Confidence Interval and Prediction Interval, and adjusted R squared value, we were able to find the best model.

### Visualization

Visualizations are done in ggplot2 and leaflet.

## Visualization and Observasions

### Income Distribution
![incomeDist](/image/Income Distribution.png)
![incomeBox](/image/Income Boxplot.png)

The NYC Median Household Income distribution is heavily right-skewed and has many extreme values, meaning there are many high-income groups living in this area causing the median household income higher than "normal". The income heatmap shows that these high-income groups cluster in the Manhattan area. Income level is highly correlated to difference in areas.

### Income Heatmap
![incomeMap](/Income.png) 

*50 records are chosen randomly from the data set to plot the circles on the following maps. Radius of each circle corresponds to different maginitude of predictors.*

### (left) Commute Time vs. Income;  (right) Commuters traveling by Drive vs. Income
![CommuteTypeMap](/Commute.png)

Image on the left shows the relationship between Mean Commute time to Work and Income; image on the right shows relationship between Percentage of People Driving to Work and Income.
Both the graphs and our model implicate that less cummute time to work and driving to work are positively correlated to Median Household Income. 
Median household income near Manhahttan is the highest, while commute time around this area is lowest (and percentage of driving to work is highest). This finding is reasonable and explains the difference of Income level amongst different areas.

### Poverty Level vs. Income
![PovertyMap](/Poverty.png)

The plot above suggests that Poverty Level is generally negatively correlated to Income.

Plots below suggests that predictors such as population size, gender, race, and job type have certain impact on Income levels but are not as highly correlated as the ones mentioned above.

### Population Size vs. Income
![TotalPopMap](/TotalPop.png) 
### Male Percentage vs. Income
![MenMap](/Men.png)
### White People Percentage vs. Income
![WhiteMap](/White.png)
### Professional(Management,business,science and arts) Jobs vs. Income
![ProfessionalMap](/Professional.png)

#### Conclusions & Implications

### Final Model for Household Median Income Prediction
Comparing the prediction accuracies, the *Best Subset Regression* model stands out as the best model. In order to increase the R-sqaured,we take the log of the household median income as the explained varible.

### Final Model for Income per Capita Prediction
In this case, the *Best Subset Regression* model still yields the best accuracy. We transformed the income per capita into the log form. 

### Conclusion for the Household Median Income Prediction
The best 

### Conclusion for the Income per Capita Prediction Model


### Comparsion bewteen the *Household Median Income Prediction Model* and the *Income per Capita Prediction Model*


