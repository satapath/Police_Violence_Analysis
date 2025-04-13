# Police_Violence_Analysis
_EECS 398 Winter 2025 Final Project_

By **Tisha Jain** and **Rishika Satapathy**

---

## 📊 Introduction
Police violence is a significant public health issue. It impacts families and erodes the trust between law enforcement and the citizens they should protect. This project analyzes trends in police violence across the United States using publicly available datasets to answer the question: How do deaths from police vary? Do they vary by race? By gender? By location?

The columns we plan to look at are Age, Gender, Race, Date, City, State, County, and Encounter Type. There are 14254 rows in the dataset.

## 🖼️ Data Cleaning and Exploratory Data Analysis
1. We created a list of all the columns we needed and created a new dataset with it
2. We checked for null values in each of our columns and imputated missing values based on column variable type
- Age is numerical, so we thought unconditional mean imputation was best
- Gender is categorical, so we thought unconditional mode imputation was best
- Encounter type is categorical, so we thought unconditional mode imputation was best
- County relies on the state and city, so we thought to create a function that applies conditional mode to each city/state pair with a null value
- Race, Date, City, and State had no missing values, therefore we didn't have to imputate them
3. Once the dataset was cleaned, we conducted two EDA plots
<!--- Embed plot here ---->
- This is a bivariate analysis between race and age. We can see that White, Hispanic, and Black groups have the lowest minimum age of death.
<!--- Embed plots here ---->
- This is a univariate analysis of state. We can see that California and Texas have the highest count of police killings.
4. We also checked for any interesting aggregrates/grouped data
<!--- Embed table here ---->
- We grouped by year and found that deaths in 2025 was the lowest, but that makes sense because we're only 3 months in. Fatalities have increased from 2013-2015 before dipping in 2016, increasing till 2018, and then dipping again before increasing every year after.

## 🔍 Framing a Prediction Problem
We want to predict the encounter type based on age, race, date, and location. This would be a multiclass classification problem because encounter type is a categorical variable with multiple outputs.

We chose encounter type as it would help us understand which situations are more likely to lead to fatalities. We plan to use all the metrics and see which one we want to weigh more heavily afterwards.

## Baseline Model

## Final Model

<!---Example of how to add images ![Police Violence Graph](images/police_violence_graph.png)--->