# Police Violence Analysis
By **Tisha Jain** and **Rishika Satapathy**

---

# 📊 Introduction
Police violence is a significant public health issue. It impacts families and erodes the trust between law enforcement and the citizens they should protect. This project analyzes trends in police violence across the United States using publicly available datasets to answer the question: **How do deaths caused by police vary? Do they differ by race, gender, or location?**

## Our Dataset
There are 14254 rows and 61 columns in the dataset. However, over half of these columns were missing majority of their data and others did not seems useful in answering our question. Therefore, we ended up choosing eight columns: 
- **Age**: Age of the Victim
- **Gender**: Gender of the Victim
- **Race**: Race of the Victim
- **Date**: Date when the event occurred (from 2013-2025)
- **City**: City where the event occurred
- **State**: State where the event occurred
- **County**: County where the event occurred
- **Encounter_Type**: Nature of Interaction between individual and law enforcement

# 🖼️ Data Cleaning and Exploratory Data Analysis
We created a list of all the columns we needed and created a new dataset with it.

We checked for null values in each of our columns and imputated missing values based on column variable type.
- Since age is numerical, we determined that unconditional mean imputation was the most appropriate approach.
- Given that gender is categorical, we opted for unconditional mode imputation.
- Encounter type, also categorical, led us to choose unconditional mode imputation as well.
- Because county depends on both state and city, we devised a function to apply conditional mode imputation to each city/state pair containing null values.
- Race, Date, City, and State had no missing values, so imputation was unnecessary.

An example of our cleaned dataset:
<iframe src="assets/filtered_data.html" width="600" height="300" frameborder="0">
</iframe>

## Univariate Plot
<iframe
 src="assets/univariate.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>
This is a univariate analysis of state. We can see that California and Texas have the highest count of police killings.

## Bivariate Plot
 <iframe
 src="assets/bivariate.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>
This is a bivariate analysis between race and age. We can see that White, Hispanic, and Black groups have the lowest minimum age of death.

## Interesting aggregrates/grouped data

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

We grouped the data by year and observed that deaths in 2025 were the lowest—but that’s expected, given that we’re only three months in. Fatalities rose from 2013 to 2015, dipped in 2016, climbed again until 2018, then declined briefly before increasing steadily each year after. The pattern of dips in deaths was interesting. We wonder what policies were in place during those years and whether they could serve as possible solutions.

# 🔍 Framing a Prediction Problem
We want to predict the encounter type based on age, race, date, and location. This would be a multiclass classification problem because encounter type is a categorical variable with multiple outputs.

We chose encounter type as it would help us understand which situations are more likely to lead to fatalities. Since we are using a multiclass classification model, we will evaluate performance using accuracy and the F1 score for simplicity and clarity.
<iframe
 src="assets/encounter.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

# 🔍 Baseline Model
We trained a K-Nearest Neighbors model as our baseline. We used five features: Race, State, Age, Top_10_cities, and Year. We chose:
- **Race** as different racial groups experience different levels of interaction with the police
- **State** as policies, crime rates, and laws vary widely across states
- **Age** as it was the only quantitative variable and could give insights into how different age groups may be associated with different encounter_types.
- **Year** as it could help capture trends and shifts over time.
- **Top 10 Cities** to identify locations where certain encounters are more likely to occur.
We OneHotEncoded all the categorical variables (Race, State, Year, and Top 10 Cities) and standardized the one numerical variable, Age.

Our model performed reasonably well for a baseline, achieving 23.2% accuracy and a F1 Score of 15.9%. Given that our response variable has 8 possible cases, a random guess would result in an accuracy of 12.5%, meaning our model surpasses random guessing. However, while this is a positive start, there is room for improvement.

# 🔍 Final Model
We ended up choosing a Logistic Regression model with Ridge regularization (penalty='l2') and used polynomial features (degree=2). After testing different hyperparameter values, we found that setting C=0.21 performed best. Our model achieved a 30.7% accuracy and a F1 score of 16.5%, a small improvement from our baseline.

Initially, we used GridSearchCV to evaluate different hyperparameter combinations via cross-validation. However, the process quickly became computationally expensive, with excessive iterations leading to prolonged run times. To keep execution feasible, we limited the polynomial degree to a range of 1–3 and and C between 1–5. Despite this, the best accuracy achieved was only 30.2%, with an F1 score of 13.7%—falling short compared to our manually selected parameters. Ultimately, we chose a polynomial degree of 2 to introduce some complexity into our model and chose a low C value of 0.21 to prevent overfitting and improve generalization.

We were pretty disappointed with the 30.7% accuracy after trying so many models. After discussing with our professor, we realized the primary issue was the lack of quantitative variables in our prediction model. Unfortunately, the dataset contained only one quantitative variable, meaning our model's performance will not be able to improve anymore than this.

## Confusion Matrix
<iframe
 src="assets/log_matrix.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

Our Confusion Matrix shows that it does a good job in predicting Domestic Disturbances and Other Non_Violent Offenses, but not so well for the other six encounter types.