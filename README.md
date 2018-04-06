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

The region where more people live may have a lower income level.
### Male Percentage vs. Income
![MenMap](/Men.png)

The plot suggests that the amount of male influences the income positively.

### White People Percentage vs. Income
![WhiteMap](/White.png)

The regions with more white people tend to earn higher income.

### Professional(Management,business,science and arts) Jobs vs. Income
![ProfessionalMap](/Professional.png)
A higher professional rate would slightly increase the income level.

## Conclusions & Implications

#### Final Model for Household Median Income Prediction
Comparing the prediction accuracies, the *Best Subset Regression* model stands out as the best model. In order to increase the R-sqaured,we took the log of the household median income as the explained varible.

#### Final Model for Income per Capita Prediction
In this case, the *Best Subset Regression* model still yields the best accuracy. We transformed the income per capita into the log form. 

#### Results in the Household Median Income Prediction Model
The best model contains 27 variables including, total population, gender, citizenship, race, employment type, commute type, etc. 

It also includes three interaction terms, which are Poverty with ChildPoverty, Professional with Servive, and IncomePerCap with IncomePerCapErr. Each pair of variables influence each other internally. For example, higher poverty level would lead to higher child poverty level. Adding interaction terms would help us yield a more accurate model.

Among all the variables, poverty rate and native rate possess relatively large coefficients. As the poverty rate increase by 1 percent, the income would decrease by 0.017 percent approximately. As the native rate increases by 1 percent, the income would decrease by 0.026 percent approximatly. These results make sense because higher poverty rate means more people in this region make very low income. At the same time, higher native rate means that less people are not local. Generally, nonnative people make higher income because they choose to move to NYC for high salaries.

#### Results in the Income per Capita Prediction Model
The best model possesses 23 variables, which include total population, gender, poverty level, labor force size, commute type, etc.

It also includes three interaction terms: Poverty with ChildPoverty, Professional with Service, and TotalPopulation with Employed.

The poverty rate and citizens' amount yield large coefficients in the model. As the poverty rate increases by 1 percent, the income per capita decreases by 0.0057 percent. At the same time, one more citizen in the region would bring a 0.0057 percent increase in income per capita. Generally, citizens are more easily to be hired by companies comparing to foreigners, and they tend to have better networking. These factors would potentially influence the income per capita.

The model results in a very high R-square--0.9637, which means 96.37% of the income per capita could be explained by the variables that we found. 

#### Comparison between two models
The prediction model for income has more variables than the prediction model for income per capita.

One of the interesting things is that many varibles influence the income and the income per cap in different ways. Asian rate influences the household median income negatively but influences the income per capita positively. At the same time, higher commute time would increase median household income but decrease income per capita. The possible reason for this phenomenon would be all the coefficients in the model are very small, they could be very sensitive to the change of other variables in the model. We could also see that the median household income and the income per capita contain different kinds of information. We could not treat them as similar factors. 

We also visualized the feature importance of the Income Prediction Model and the Income Per Cap Prediction Model using random forest. “Men”, “Office”, “Hispanic”, “Income Err” and “Total Population” are five most important features for both models. income and income per capita are highly correlated (correlation is about 0.84) but are not important features to each other. Income error is more important than income per capita error, probably because it contains more information. In addition, poverty rate is an important indicator of income level both from regression analysis and common sense. And mean commute time and commute type also have strong causal relationship with Income and Income per capita.


### Conclusion
From the prediction models, we know that, the factors such as citizenship and riving rate, could bring positive effects to both the median household income and the income per capita. However, the factors such as poverty level and unemployment rate, would influence the income and the income per capita negatively.

Placing the two models together, we can see that most of the variables in the Income Per Capita model are included in the Income prediction model, which explains to some degree that Income and Income Per Capita shares a significant amount of elements when trying to make predictions. The fact that Income model has more variables than Income Per Capita model suggests that median household income contains more information than simply adding up per capita of every member. Some of the coefficients of have completely different effects in these two models, which brings us a thought that the median household income could not reflect the average income level in one region 

