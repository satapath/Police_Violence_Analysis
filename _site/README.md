 # Police_Violence_Analysis
_EECS 398 Winter 2025 Final Project_

By **Tisha Jain** and **Rishika Satapathy**

---

## 📊 Introduction
Police violence is a significant public health issue. It impacts families and erodes the trust between law enforcement and the citizens they should protect. This project analyzes trends in police violence across the United States using publicly available datasets to answer the question: How do deaths from police vary? Do they vary by race? By gender? By location?

# Our Dataset
There are 14254 rows and 61 columns in the dataset. However, over half of these columns are missing majority of their data and others did not seems usueful in answering our question. Therefore, we ended up choosing eight columns: 
- Age: Age of the Victim
- Gender: Gender of the Victim
- Race: Race of the Victim
- Date: Date when the event occurred (from 2013-2025)
- City: City where the event occurred
- State: State where the event occurred
- County: County where the event occurred
- Encounter_Type: Nature of Interaction between individual and law enforcement

## 🖼️ Data Cleaning and Exploratory Data Analysis
1. We created a list of all the columns we needed and created a new dataset with it

2. We checked for null values in each of our columns and imputated missing values based on column variable type
- Age is numerical, so we thought unconditional mean imputation was best
- Gender is categorical, so we thought unconditional mode imputation was best
- Encounter type is categorical, so we thought unconditional mode imputation was best
- County relies on the state and city, so we thought to create a function that applies conditional mode to each city/state pair with a null value
- Race, Date, City, and State had no missing values, therefore we didn't have to imputate them

An example of our cleaned dataset:
<iframe src="assets/filtered_data.html" width="600" height="300" frameborder="0">
</iframe>

3. Once the dataset was cleaned, we constructed two EDA plots
<iframe
 src="assets/univariate.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>
- This is a univariate analysis of state. We can see that California and Texas have the highest count of police killings.
 <iframe
 src="assets/bivariate.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>
- This is a bivariate analysis between race and age. We can see that White, Hispanic, and Black groups have the lowest minimum age of death.

4. We also checked for any interesting aggregrates/grouped data

|   year |   count |
|-------:|--------:|
|   2013 |    1078 |
|   2014 |    1040 |
|   2015 |    1103 |
|   2016 |    1067 |
|   2017 |    1101 |
|   2018 |    1148 |
|   2019 |    1115 |
|   2020 |    1159 |
|   2021 |    1190 |
|   2022 |    1269 |
|   2023 |    1361 |
|   2024 |    1365 |
|   2025 |     249 |

- We grouped by year and found that deaths in 2025 was the lowest, but that makes sense because we're only 3 months in. Fatalities have increased from 2013-2015 before dipping in 2016, increasing till 2018, and then dipping again before increasing every year after.

## 🔍 Framing a Prediction Problem
We want to predict the encounter type based on age, race, date, and location. This would be a multiclass classification problem because encounter type is a categorical variable with multiple outputs.

We chose encounter type as it would help us understand which situations are more likely to lead to fatalities. Since we are using a multiclass classification model, we will evaluate performance using accuracy and the F1 score for simplicity and clarity.
<iframe
 src="assets/encounter.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

## Baseline Model
We trained a K-Nearest Neighbors model as our baseline. We used five features: Race, State, Age, Top_10_cities, and Year. We chose:
- Race as different racial groups experience different levels of interaction with the police
- State as policies, crime rates, and laws vary widely across states
- Age as it was the only quantitative variable and could give insights into how different age groups may be associated with different encounter_types.
- Year as it could help capture trends and shifts over time.
- Top 10 Cities to identify locations where certain encounters are more likely to occur.

Our model performed reasonably well for a baseline, achieving 23.2% accuracy and a F1 Score of 15.9%. Given that our response variable has 8 possible cases, a random guess would result in an accuracy of 12.5%, meaning our model surpasses random guessing. However, while this is a positive start, there is room for improvement.

## Final Model
We ended up choosing a Logistic Regression model with Ridge regression as our final model. Our model ended up with a 30.7% accuracy and a F1 score of 16.3%.

After discussing with our professor, we realized the primary issue was the lack of quantitative variables in our prediction model. Unfortunately, the dataset contains only one quantitative variable, meaning our model's performance will not be able to improve from this point.

# Confusion Matrix
<iframe
 src="assets/log_matrix.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

