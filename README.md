# final-project
Revisiting Project-1 with Machine Learning

# Data Source  

* [World Happiness Report](https://worldhappiness.report/)  

* Training Set: **_2005 - 2019_**  

* Test Set: **_2020_**  

# Data Prep  

* Unnecessary columns removed  

* Rows removed with empty cells  

* Target Variables  _(min, mean, max)_  

	- `Ladder Score`  $_(2.375092,  5.445810,  8.018934)$  

* Features Variables  _(min, mean, max)_  

	- `GDP per capita`  _(6.456574,  9.244531,  11.728235)_  

	- `Social support`  _(0.290184,  0.290184,  0.987343)_  

	- `Healthy life expectancy at birth`  _(32.299999,  63.169525,  77.099998)_  

	- `Freedom to make life choices`  _(0.257534,  0.738467,  0.985178)_  

	- `Generosity`  _(-0.331775,  0.000109,  0.679921)_  

	- `Perceptions of corruption`  _(0.035198,  0.749064,  0.983276)_  

# Data Exploration  

## 2-D Relationships between each Feature and the Target variable (Ladder Score)  

![Simple_Relationships](resources/Simple_Relationships.png)  

## Feature Selection  

### Correlation Matrix  

![heatmap](resources/heatmap.png)  

* Strongest correlations with the target variable **Ladder** are **GDP**, **Support**, and **Health** (with **0.779501**, **0.710214**, and **0.750692**)  

* A bit weaker correlated w/**Ladder** are **Freedom**, **Generosity**, and **Corruption** (with **0.521902**, **0.190646** and **-0.441650**)  

* The highest correlation between features is between **GDP** and **Health** with **0.843902**  

* No features have a correlation greater than 0.9, so no features will be dropped based on the correlation matrix  

### Based on P-value  

![OLS](resources/OLS.PNG)  

* No p-values are greater than the significance level of 0.5  

* All features will be kept

## Feature Engineering  

### Visualizing all possible relationships between features in 2-dimensions  

* Made the Ladder score a Category by saying any value greater-than 6 is a 1 ("Happy"), and a 0 otherwise  

* Red dots are "Happy"  

![Categorical_Relationships](resources/Categorical_Relationships.png)  

# Multivariable Linear Regression

Using all the features in a linear regression we obtained a score of $R^2 = 0.745$ on the training set and a score of `R<sup>2</sup> = 0.736` on the test set from the year 2020.  

# Contributors 

* __Claudia Palmer-Martinez:__ [github](https://github.com/Claud50623)  

* __Alexandra Solano:__ [github](https://github.com/alexsolano36)  

* __Donatienne Noel:__ [github](https://github.com/donatiennenoel)  

* __John S. Chapek:__ [github](https://github.com/code-sparrow)


