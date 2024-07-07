US Election Analysis
====================

This project analyzes US election data from 1976-2020, with a focus on predicting voter turnout percentages and election outcomes. T

PCA and t-SNE Analysis
---------------------------------

In this section, PCA and t-SNE dimensionality reduction techniques were used to visualize relationships between different states based on demographic and geographic features.


To determine which features were most important for distinguishing between states, a series of experiments were run where each feature was removed in turn, and the PCA and t-SNE were re-run. By comparing the resulting plots, it was determined that removing the 'fips' feature resulted in worse separation between states, indicating that 'fips' was an important distinguishing feature. On the other hand, removing 'pop2019' and 'sales_per_capita' had little effect on the state groupings, suggesting these features were less important.
<details>
  <summary>Removing 'pop2019'</summary>

![image](https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/d5ea75ad-7bd6-43c4-9675-cf82d4deb7fd)

![image](https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/f42de794-bfeb-418c-bb89-413869b09068)


</details>
<details>
  <summary>Removing 'fips'</summary>
  
![image](https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/75b9169a-e144-4c45-94fc-e404927bf604)
  
![image](https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/f9b590dd-1a0f-4c53-a926-06d858295f58)

![image](https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/440290ae-c135-4fd5-9fb5-a3374ee5a85e)

</details>

Voter Turnout Prediction
-----------------------------------

This section focuses on predicting voter turnout percentages for each state in presidential election years from 2000-2020. The analysis involved several key steps:

### Data Preprocessing

The first step was to preprocess the data, which included:

-   Handling missing data: KNN imputation was used to estimate missing values based on similar records.
-   Feature scaling: Features were scaled using StandardScaler to have zero mean and unit variance.
-   Encoding categorical variables: Categorical features like 'smoking_ban_2010' were encoded using ordinal encoding.
-   Calculating total votes per state per year: A new feature 'totalvotes_state/year' was created by summing the 'candidatevotes' for each state and year.

### Exploratory Data Analysis

Next, exploratory data analysis was performed to understand trends in voter turnout. This included:

-   Calculating the voting-eligible population (VEP) per state per year based on Census data.
-   Visualizing trends in voter turnout percentage (total votes / VEP) over time for each state.

<details>
<summary>Voter Turnout Rates Plots 2002 - 2012</summary>
<img width="566" alt="image" src="https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/72817c17-6a01-4a89-bfcd-ba213d373757">

<img width="577" alt="image" src="https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/4f24b8a5-2bb0-449a-b3d0-32d48d7aa6ab">

<img width="498" alt="image" src="https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/4fe70ca8-a339-4a72-b553-d5134888d16a">

<img width="549" alt="image" src="https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/563632e3-3a94-4feb-89a0-9c8fa0615c7a">

<img width="549" alt="image" src="https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/812390ef-b2f4-4800-a7e5-37a6ad587613">

<img width="512" alt="image" src="https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/e476f170-fbc1-4ec5-a288-cbb373ed5057">

</details>

This analysis revealed that some states consistently had higher turnout than others, and that turnout tended to be higher in presidential election years than in midterm years.

### Feature Engineering

Based on domain knowledge and data exploration, several new features were engineered, including:

-   Percentage of population in each race/ethnicity group (White, Black, Hispanic)
-   Percentage of population with bachelor's degree
-   Unemployment rate
-   Poverty rate

These features were calculated for each state and year based on Census data.

### Feature Selection

To select the most predictive features, a correlation analysis was performed. Highly correlated features (r > 0.95) were removed to avoid multicollinearity. The remaining features were used to train the predictive models.

### Model Building and Evaluation

Several machine learning models were compared for predicting voter turnout percentage, including:

-   Gradient Boosting Regressor
-   Random Forest Regressor
-   KNN Regressor

Models were tuned using GridSearchCV to find the best hyperparameters. The best performing model was the KNN Regressor with the following metrics:

-   MSE: 0.00555

<img width="279" alt="image" src="https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/c476b550-0cfa-4e7b-ba6f-110bd5cbd71e">

<img width="253" alt="image" src="https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/a1a7ea30-5fa5-4480-94c7-0a3193ead3e4">

The feature importances from the tuned Gradient Boosting model showed that the most predictive features were the race/ethnicity percentages, education level, and economic indicators like unemployment and poverty rates.

<img width="301" alt="image" src="https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/06442aed-8cfe-45b4-b6a1-0c4e5cbdc3f4">

### Analysis of Results

The model results suggest that demographic and economic factors play a significant role in predicting voter turnout. States with higher percentages of college-educated residents and lower poverty rates tended to have higher turnout. There were also differences in turnout by race, with White residents having the highest turnout on average, followed by Black and then Hispanic residents.

Applying the tuned KNN model to the 2010 and 2012 data for California, Florida, South Dakota, and Wyoming, we can see that the model performs quite well in most cases, with predictions close to the actual turnout values.

<details>
<summary>Prediction Plots</summary>
  <img width="255" alt="image" src="https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/9ac19a48-37e5-4bd1-8f82-fc8f53faeb30">

  <img width="255" alt="image" src="https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/4c80f4f4-6373-4389-8659-d430011c9bc1">

<img width="436" alt="image" src="https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/23c7b137-220b-411a-87f2-77cced5bf924">

</details>

However, there are a few instances where the model over or under-predicts turnout by a significant margin. This suggests that there may be other factors influencing turnout in these specific state-year combinations that are not fully captured by the model.

Looking at the states with the lowest mean squared error, we see that the model performs best for Arkansas, Kentucky, and Washington. This suggests that the demographic and economic features used in the model are particularly good predictors of turnout in these states.

<details>
  <summary>Predicted vs Actual Turnout Rates</summary>
<img width="469" alt="image" src="https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/cd4e1852-4d03-4ea2-a418-a0a791f4639f">
</details>


Section D: House of Representatives Election Prediction
-------------------------------------------------------

This section predicts which party (Democrat or Republican) will win the most votes in each state in House of Representatives elections from 2000-2020.

### Data Preprocessing

Data preprocessing steps included:

-   Removing rows with 'writein' candidates, as they are not associated with either major party
-   Handling missing data via dropping rows
-   Summming the total votes for each party in each state in each election year
-   Keeping only the party with the highest total votes per state per year
-   One-hot encoding the party labels as 1 (Democrat) and 0 (Republican)

### Feature Selection

The same feature set was used as in Section C, including demographic percentages, education levels, unemployment rates, and poverty rates. These features were calculated for each state and year based on Census data.

Years prior to 2000 were excluded from the analysis, as predicting data that far back based on 2010-2019 Census data was deemed likely to produce inaccurate results.

### Missing Data Imputation

For the selected features, missing data for non-Census years was imputed using a linear interpolation method based on the state's population growth rate between the 2010 and 2019 Census years. The formula used was:

`P_t = P_0 * (1 + r)^t`

Where:

-   P_t is the population in the target year
-   P_0 is the population in the base year (2010 Census)
-   r is the annual growth rate calculated based on the 2010 and 2019 Census populations
-   t is the number of years between the base year and the target year

### Model Building and Evaluation

The same set of classification models were compared as in Section C:

-   SVC
-   AdaBoost Classifier
-   Random Forest Classifier
-   KNN Classifier

The best performing model was the Random Forest Classifier with 87.5% accuracy.

<img width="244" alt="image" src="https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/911269ff-5ff3-4057-8fff-26c3d99ebb52">

The most important features according to the Random Forest model were the racial demographic percentages.

<img width="259" alt="image" src="https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/55840d9e-05f7-43be-b258-101690103be9">

Section E: 2022 Senate Election Predictions
-------------------------------------------

This section applies the methodology from Section D to predict the 2022 Senate election results in each state. It's important to note that this analysis was conducted in June 2022, several months before the actual elections in October.

The same data preprocessing and feature engineering steps were used as in Section D. The only difference was that for 2022, the demographic and economic feature values had to be extrapolated based on the 2010 and 2019 Census data.

Each of the four classification models tuned in Section D were applied to the 2022 data. The predictions were as follows:

-   SVC:
  <img width="565" alt="image" src="https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/58cfaf24-74cf-4db3-9244-de7835795d0f">
-   AdaBoost:
  <img width="565" alt="image" src="https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/4b380cca-d9f8-4621-aeb7-87d74984e9ea">

-   Random Forest:
  <img width="565" alt="image" src="https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/c329ee9a-d4f6-4eb7-bc99-f5755a0ae59d">
  
-   KNN:
  <img width="565" alt="image" src="https://github.com/mlk500/ML-US-elections-prediction/assets/57171298/723a1f07-e86a-4ad6-8863-58bf4b241101">


Comparing to the actual 2022 Senate results, the AdaBoost and Random Forest models performed best, each correctly predicting the winner in 24 out of the 33 states included in the analysis (72.73% accuracy). The SVC model had a slightly lower accuracy at 63.64%, while the KNN model performed worst at 48.48%.

It's important to note that these predictions were made in June 2022, several months before the actual elections in November. The models' performance was likely hindered by the need to extrapolate 2022 feature values from 2010-2019 data, as well as the inherent uncertainty in predicting future events.

Key takeaways:

-   The models tended to perform better in states where demographic trends have been more stable over time. States that have seen rapid demographic shifts in recent years were harder to predict.
-   Extrapolating 2022 feature values based on past Census data introduces significant uncertainty. Model predictions would likely be improved with more recent data inputs.

Conclusion
----------

This project demonstrates the potential for using demographic and economic data to predict election outcomes at the state level. Through extensive data preprocessing, feature engineering, and model tuning,  models built to predict both voter turnout percentages and House of Representatives election results with reasonably high accuracy.

Key predictive features included racial demographic percentages, education levels, and economic indicators like unemployment and poverty rates. These results align with existing political science research showing the importance of these factors in driving voting behavior.

However, the project also highlights the challenges of election forecasting, particularly when trying to predict future results. The further out the prediction, the more uncertainty there is around how predictive features may change over time. The 2022 Senate predictions, while reasonably accurate, were likely hindered by the need to extrapolate 2022 feature values from 2010-2019 data.

Despite these challenges, the insights generated from this analysis could be valuable for campaigns seeking to target their voter outreach efforts and optimize their strategies. By understanding which factors are most predictive of turnout and vote choice in each state, campaigns can more efficiently allocate their resources to maximize their chances of success.

Going forward, this work could be extended in several ways:

-   Incorporating more granular geographic data (e.g. county-level) to capture within-state variation
-   Adding additional features capturing voter attitudes and preferences from polling data
-   Exploring more sophisticated modeling techniques like neural networks or ensemble methods

