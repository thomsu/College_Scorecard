# Predicting College Completion Rate

## Purpose
Using publically available data we looked at predicting the completion rate for a college based on a set of features provided by the US Department of Education. Their College Scorecards effort collected information from the last 20 years for information like student body demographics, the percentage of students receiving certain federal loans, and the retention rate of incoming students, just to name a few. We looked at this information from the latest year in the dataset and built a model using multiple linear regression with a resulting R^2 value of .71.

## Procedure

### Getting the Data
In order to recreate our process, run the Data Gathering Jupyter notebook. Create a txt file in the same folder as the notebook with your API key. The notebook goes through the process of calling the API for a list of features we were interested in (look through the documentation and get_scorecard functions in order to change these features) and then storing that information into a SQLite database.

### Cleaning the Data
The process for cleaning the raw data is covered in the Data Cleaning Jupyter notebook. Entries with missing values for our predictor (student completion rate at a college) are dropped. Based on the sample sizes we then choose to focus on colleges with 4 year programs. Features are then dropped if they are primarily missing as are entries with a substantial number of missing values. The remaining missing values are replaced with the medians. Outliers are then detected and those entries dropped from the sample. Entries with unlikely values based on parameter definitions (for example, schools with a 0.0 retention rate or completion rate) are then dropped. Our sample size started at 2077 entries and ended at 1779 entries after cleaning.

### Exploring and Engineering the Data
Visualization of the data and the choices made for engineering new features can be found in the EDA & Feature Engineering Jupyter notebook. In here we look at the distributions for the individual features as well as any potential collinearity. Most of the features measure percentages and are represented as values from 0-1 and so we min-max normalized other features to match these more closely in scale. Potential interactions are explored based on our intuition and verified by splitting the data and looking at individual linear regressions. 

### Modeling the Data
The final model and the reasoning behind which features were included and excluded can be found in the Modeling Jupyter notebook. Our initial sample was split into a testing and training set. We first narrowed down our potential predictors into features with the highest correlation values to the target. From here we checkedfor homoschedasticity and normally distributed residual values. From these tests we chose to exclude some potential predictors and build a model with the remaining features. This model achieved an R^2 value of .716. From the P-values for our features we then excluded more features which were shown to not be statistically significant. The final resulting model achieved an R^squared value of .712 with 9 total predictors (2 of which were engineered features). The mean squared error for our predicted values and the observed values of our test set was .011 (completion rate is a value from 0-1).