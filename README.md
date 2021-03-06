# **_A Look at World Happiness through Machine Learning_**  

Utilizing machine learning and data from the World Happiness Report, this project aimed to predict a country’s happiness score from features such as GDP, Health, and Social Support and also to draw insights into the most important factors that go into a country’s happiness score.  

## Background  

The project is based on The World Happiness Report issued annually by the United Nations. This concept goes well with the idea of Machine Learning because it is an attempt to quantify human emotion. Respondents in each country were asked a basic question: _"Imagine that life is a ladder, with the bottom rung being the worst life you can imagine and the top rung being the best life you can imagine, where are you on the ladder?"_

## Data Source  

* [World Happiness Report](https://worldhappiness.report/)  

* Training Set: **_2005 - 2019_**  

* Test Set: **_2020_**  

## Data Prep  

* Unnecessary columns removed  

* Rows removed with empty cells  

* Target Variables  _<sub>(min, mean, max)</sub>_  

	- `Ladder Score`  _<sub>(2.375092,  5.445810,  8.018934)</sub>_  

* Features Variables  _<sub>(min, mean, max)</sub>_  

	- `GDP per capita`  _<sub>(6.456574,  9.244531,  11.728235)</sub>_  

	- `Social support`  _<sub>(0.290184,  0.290184,  0.987343)</sub>_  

	- `Healthy life expectancy at birth`  _<sub>(32.299999,  63.169525,  77.099998)</sub>_  

	- `Freedom to make life choices`  _<sub>(0.257534,  0.738467,  0.985178)</sub>_  

	- `Generosity`  _<sub>(-0.331775,  0.000109,  0.679921)</sub>_  

	- `Perceptions of corruption`  _<sub>(0.035198,  0.749064,  0.983276)</sub>_  

## Data Exploration  

### 2-D Relationships between each Feature and the Target variable (Ladder Score)  

![scatter_matrix](resources/scatter_matrix.png)  

### Feature Selection  

#### Correlation Matrix  

![heatmap](resources/heatmap.png)  

* Strongest correlations with the target variable **Ladder** are **GDP**, **Support**, and **Health** (with **0.779501**, **0.710214**, and **0.750692**)  

* A bit weaker correlated w/**Ladder** are **Freedom**, **Generosity**, and **Corruption** (with **0.521902**, **0.190646** and **-0.441650**)  

* The highest correlation between features is between **GDP** and **Health** with **0.843902**  

* No features have a correlation greater than 0.9, so no features will be dropped based on the correlation matrix  
---

#### Based on P-value  

![OLS](resources/OLS.PNG)  

* No p-values are greater than the significance level of 0.5  

* All features will be kept

### Feature Engineering  

#### Visualizing all possible relationships between features in 2-dimensions  

* Made the Ladder score a Category by saying any value greater-than 6 is a 1 ("Happy"), and a 0 otherwise  

* Red dots are "Happy"  

![Categorical_Relationships](resources/Categorical_Relationships.png)  

## Multivariable Linear Regression  

### Feature Scaling

* Feature scaling wasn't required for sklearn's `LinearRegression` regressor  

### Results

* Using all the features in a linear regression we obtained a score of **_R<sup>2</sup> = 0.745_** on the training set and a score of **_R<sup>2</sup> = 0.736_** on the test set from the year 2020.  

* The adjusted R<sup>2</sup> on the test set was **_R<sup>2</sup><sub>adjusted</sub> = 0.727_**  

* Loose interpretation based on removing one feature, each time, and calculating the adjusted R<sup>2</sup>

| **Feature Removed** |**_R<sup>2</sup><sub>adjusted</sub>_**|
|:--------------------|:------------------------------------:|
|    None             |        _0.727_                       |
|    GDP              |        _0.714_                       |
|  **Support**        |      **_0.691_**                     |
|    Health           |        _0.714_                       |
|    Freedom          |        _0.715_                       |
|    Generosity       |        _0.723_                       |
|    Corruption       |        _0.722_                       |   

* The highest score was with no features removed. When Support was removed, it reduced the score the most, indicating it may be the most important feature in this linear model. Additionally, when Generosity and Corruption were individually removed, the adjusted score was not impacted as much, suggesting they are slightly less important than the other features.  

* The order of importance would then be: **Support, GDP, Health, Freedom, Corruption, Generosity**  


## Random Forest Regression  

### Feature Scaling

* Feature scaling wasn't required for sklearn's `RandomForestRegressor` regressor.  

### Tuning Hyperparameters

* Using `GridSearchCV` the parameters varied were `n_estimators` and `max_depth`.  

* The plot below revealed that increasing `n_estimators` beyond a certain point did not improve accuracy, yieding diminishing returns. Similarly, increasing `max_depth` improved accuracy up to a certain point, then reduced it.  

![Grid_Search_RFR](resources/grid_search_RFR.png)  
 
* With a more thorough GridSearch, the best parameters found are in the table below; yielding scores of **_R<sup>2</sup> = 0.911_** on the training set and **_R<sup>2</sup> = 0.859_** on the test set from the year 2020.  

| **Hyperparameter** |**Tuned Value**|
|:-------------------|:-------------:|
| `n_estimators`     |     500       |
| `max_depth`        |      8        |
| `max_features`     |     sqrt      |
| `min_sample_leaf`  |      1        |
| `min_sample_split` |      2        |
| `bootstrap`        |     True      |

### Feature Importance  

* Seems on par with the correlation matrix, Health, GDP, and Support being the most impotant (Health is ranked the most important here)

![Variable_Importance](resources/variable_importance.png)

## SVM  

* Should we include?  

* Does it add any value or insight?  

* I'm thinking NO  (aside from puurrdy plots)  
 

![SVM_Support_Health](resources/SVM_Support_Health.png)  

![SVM_Health_Corruption](resources/SVM_Health_Corruption.png)

## Conclusions  

* Methods of feature selection indicated all features were meaningful additions to models _(correlation matrix and p-values)_  

* Linear Regression (LR) resulted in _R<sup>2</sup><sub>adjusted</sub> = 73%_ (higher than first project)  

* Feature importance in LR indicated Support to be most important feature, reducing score the most _(R<sup>2</sup><sub>adjusted</sub> = 69%)_  

* Random Forest Regression (RFR) was more accurate with _R<sup>2</sup><sub>adjusted</sub> = 85%_ on the test set  

* Limiting the max_depth in RFR seemed to keep testing and training scores closer together, indicating less overfitting of the training set  

* Feature importance in RFR indicated Health to be the most important, followed by GDP and Support  

* Health, GDP, and Support are rated the most important features in predicting the Ladder score with the RFR model  

* They are also found to correlate the strongest with Ladder in the correlation Matrix  

* Although GDP is highly ranked, if we were able to do a more thorough analysis of feature importance, I think we would find that it is more a "means to an end". That a human's deeper (or essential) sense of well-being is more tied to Health and social factors like Support/Family. Economy helps us get there by putting food on our tables, providing for our families and friends, and having access to better healthcare. Machine learning seems like an interesting tool to help us understand and dissect the complexities and hidden variables behind human emotions.  


## Contributors 

* __Claudia Palmer-Martinez:__ [github](https://github.com/Claud50623)  

* __Alexandra Solano:__ [github](https://github.com/alexsolano36)  

* __Donatienne Noel:__ [github](https://github.com/donatiennenoel)  

* __John S. Chapek:__ [github](https://github.com/code-sparrow)


