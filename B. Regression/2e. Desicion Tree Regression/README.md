# Decision Tree

- ## Importing the libraries
	```py
	import numpy as np
	import pandas as pd
	import matplotlib.pyplot as plt
	```

- ## Importing the dataset
	```py
	dataset = pd.read_csv('Position_Salaries.csv')
	X = dataset.iloc[:,1:-1].values
	y = dataset.iloc[:,-1].values
	```
	- If we have missing values in the dataset, then we have to take care of those missing datas by `SimpleImputer` or other class.
	- If we have categorical data, then we also need to encode them by `OneHotEncoder` or `LabelEncoder`
	- No need to apply Feature Scalling here
	
- ## Training the Decision Tree Regression model on the whole dataset
	- Tunning the regressor model will be done on later sections. Here we are just building simple models.
	```py
	from sklearn.tree import DecisionTreeRegressor
	regressor = DecisionTreeRegressor(random_state = 0)     # fixing the random_state so that we get the same results on eveery execution.
	regressor.fit(X, y)
	```
	
-  ## Predicting a new result
	```py
	regressor.predict([[6.5]])
	```
	
- ## Visualising the Decision Tree Regression results (higher resolution)
	- Here as dataset is too small, the decision tree will not work any good. it just overfits !
	- We need more dimentional data for plotting graphs.
	```py
	X_grid = np.arange(min(X), max(X), 0.1)
	X_grid = X_grid.reshape(len(X_grid), 1)
	
	plt.scatter(X, y, color='red')
	plt.plot(X_grid, regressor.predict(X_grid), color='red')
	plt.title('Truth or Bluff (Decision Tree Regression)')
	plt.xlabel('Position Level')
	plt.ylabel('Salary')
	plt.show()
	```
	
---	

- Cart : 
	1. Classification Trees
	2. Regression Trees
		- Regression trees are much more complicated than classification trees.

- This Regression tree will return the average of specific split region as predicted value of some data.
- We don't have to apply Feature Scaling in this decision tree regression.
- This regression might not work well with given small dataset. but it will work fine on larger datasets.
	
---

- # `Position_Salaries.csv`

	|Position         |Level|Salary |
	|-----------------|-----|-------|
	|Business Analyst |1    |45000  |
	|Junior Consultant|2    |50000  |
	|Senior Consultant|3    |60000  |
	|Manager          |4    |80000  |
	|Country Manager  |5    |110000 |
	|Region Manager   |6    |150000 |
	|Partner          |7    |200000 |
	|Senior Partner   |8    |300000 |
	|C-level          |9    |500000 |
	|CEO              |10   |1000000|