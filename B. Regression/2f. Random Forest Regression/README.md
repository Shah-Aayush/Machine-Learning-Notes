# Random Forest Regression

- ## Importing the Libraries
	```py
	import numpy as np
	import pandas as pd
	import matplotlib.pyplot as plt
	```
	
- ## Importing the dataset
	```py
	dataset = pd.read_csv('Position_Salaries.csv')
	X = dataset.iloc[:,1:-1].values
	y = dataset.iloc[:, -1].values 
	```
- ## Training the Random Forest Regression model on the whole dataset
	- Here we can tune the number of trees *(n_estimators)*.
		> Ususally we should start with `10`.
	```py
	from sklearn.ensemble import RandomForestRegressor
	regressor = RandomForestRegressor(n_estimators=10, random_state=0)
	regressor.fit(X, y)
	```
	
- ## Predicting a new result
	```py
	regressor.predict([[6.5]])
	```

- ## Visualising the Random Forest Regression results (Higher Resolution)
	- As we have more trees here, so we hav more steps then previous decision tree model in graph.
	```py
	X_grid = np.arange(min(X), max(X), 0.1)
	X_grid = X_grid.reshape(len(X_grid), 1)
	
	plt.scatter(X, y, color='red')
	plt.plot(X_grid, regressor.predict(X_grid), color='blue')
	plt.title('Truth or Bluff (Random Forest Regression)')
	plt.xlabel('Position level')
	plt.ylabel('Salary')
	plt.show()
	```

---

- Here we are going to discuss about Random Forest Regression Trees. *(Not about Random Forest Classification Trees.)*
- Random Forest Regression is a version of **Ensemble Learning**
	- **Ensemble Learning** : Ensemble methods is a machine learning technique that combines several base models in order to produce one optimal predictive model . To better understand this definition lets take a step back into ultimate goal of machine learning and model building.
	- Ensemble learning is the process by which multiple models, such as classifiers or experts, are strategically generated and combined to solve a particular computational intelligence problem. Ensemble learning is primarily used to improve the (classification, prediction, function approximation, etc.) performance of a model, or reduce the likelihood of an unfortunate selection of a poor one.
	
- Random Forest Intuition
	1. Pick at random K data points from the Training set.
	2. Build the Decision Tree associated to these K data points
		- Rather than building on the whole dataset, only build model upon this comparatively smaller subset of dataset.
	3. Choose the number Ntree of trees you want to build and repeat STEP `1` & `2`.
	4. For a new data point, make each one of your Ntree trees predict the value of Y to for the data point in question, and assign the new data point the average across all of the predicted Y values.
	
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