# final-project
Revisiting Project-1 with Machine Learning

# Data Source  

* [World Happiness Report](https://worldhappiness.report/)

# Data Prep  

* Unnecessary columns removed  

* Rows removed with empty cells  

* Target Variables (min, mean, max)  

	- Ladder Score (2.375092, 5.445810, 8.018934)  

* Features Variables (min, mean, max)  

	- GDP per capita (6.456574, 9.244531, 11.728235)  

	- Social support (0.290184, 0.290184, 0.987343)  

	- Healthy life expectancy at birth (32.299999, 63.169525,77.099998)  

	- Freedom to make life choices (0.257534, 0.738467, 0.985178)  

	- Generosity (-0.331775, 0.000109, 0.679921)  

	- Perceptions of corruption (0.035198, 0.749064, 0.983276)  

# Data Exploration  

## 2-D Relationships between each Feature and the Target variable (Ladder Score)  

![Simple_Relationships](resources/Simple_Relationships.PNG)  

## Feature Selection  

### Correlation Matrix  

![heatmap](resources/heatmap.PNG)  

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

* Made the Ladder score a Category by saying any value grater-than 6 is a 1 ("Happy"), and a 0 otherwise  

* Red dots are "Happy"  

![Categorical_Relationships](resources/Categorical_Relationships.PNG)
