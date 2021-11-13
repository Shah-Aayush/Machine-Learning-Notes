# Support Vector Machine [SVM]

- Here particularly in this section, only support linear vector regression will be discussed.

- ## Importing the libraries
	```py
	import numpy as np
	import pandas as pd
	import matplotlib.pyplot as plt
	```

- ## Importing the dataset
	```py
	dataset = pd.read_csv('Position_Salaries.csv')
	X = dataset.iloc[:, 1:-1].values
	y = dataset.iloc[:, -1].values
	```
	- Here we need to reshape `y` variable as In Feature Scaling,  `StandardScaler` class expected dependent variables list as 2-D array.
	```py
	y = y.reshape(len(y), 1)
	```
	
- ## Feature Scaling
	- Here we have to apply explicit feature scaling which is requirement of this model. Unlike Linear, Multiple and Polynomial Regression , 
	- Here we need feature scaling as its required by formula of this algorithm, whereas other regression models' variables' coefficients can compensate with higher or lower values of variables.
	- We don't have to apply feature-scaling, if the values are b/w -1 to 1 range or similar... 
	- Here dependent variable Y : Salaries' values are not b/w -1 to 1 so we'll preprocess them.
	- Also here we'll create two different `StandardScaler` models so that we can reverse transform X and y's values later on.
	```py
	from sklearn.preprocessing import StandardScaler
	sc_X = StandardScaler()
	sc_y = StandardScaler()
	sc_X.fit_transform(X)
	sc_y.fit_transform(y)
	```
	
- ## Training the SVR model on the whole dataset
	- Available kernels : {‘linear’, ‘poly’, ‘rbf’, ‘sigmoid’, ‘precomputed’}, default=’rbf’
	
	```py
	from sklearn.svm import SVR
	regressor = SVR(kernel = 'rbf') # using Radial Basis Kernel here
	regressor.fit(X, y)
	```
 - ##  Predicting a new result
	- Here we have to give transformed value to predict method.so we'll convert our value to required transformed value by `.transform`.
	- Now the regressor will give predicted value preprocessed. so we have to convert that value back to original value.
	- Notice that here we have only used `transform` and not `fit_transform`. because we don't want to calculate new mea and variance from sc_X. we just want to use previous data to predict the new one! 
	```py
	# Method 1
	print('Method 1 :', sc_y.inverse_transform(regressor.predict(sc_X.transform([[6.5]]))))
	
	# Method 2
	X_temp = [[6.5]]
	X_temp = sc_X.transform(X_temp)
	
	y_pred = regressor.predict(X_temp)
	y_pred = sc_y.inverse_transform(y_pred)
	print('Method 2 :', y_pred)
	```
	
- ## Visualising the SVR results
	- Here we have to inverse transform values to plot graph in original scale.
	```py
	plt.scatter(sc_X.inverse_transform(X), sc_y.inverse_transform(y), color='red')
	plt.plot(sc_X.inverse_transform(X), sc_y.inverse_transform(regressor.predict(X)), color='blue')
	plt.title('Truth or Bluff (Support Vector Regression)')
	plt.xlabel('Position Level')
	plt.ylabel('Salary')
	plt.show()
	```
	
- Visualising the SVR results (for higher resolution and smoother curve)
	- If there is a point far from other samples, SVR will not consider that point!
	```py
	X_grid = np.arange(min(sc_X.inverse_transform(X)), max(sc_X.inverse_transform(X)), 0.1)
	X_grid = X_grid.reshape(len(X_grid), 1)
	
	plt.scatter(sc_X.inverse_transform(X), sc_y.inverse_transform(y), color='red')
	plt.plot(X_grid, sc_y.inverse_transform(regressor.predict(sc_X.transform(X_grid))), color='blue')
	plt.title('Truth or Bluff (Support Vector Regression HD )')
	plt.xlabel('Position Level')
	plt.ylabel('Salary')
	plt.show()
	```
	
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