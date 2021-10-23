# Simple Linear Regression

- Libraries to be imported : 
	```py
	import numpy as np
	import matplotlib.pyplot as plt
	import pandas as pd
	```

- ## Importing dataset : 
	```py
	dataset = pd.read_csv('Salary_Data.csv')
	X = dataset.iloc[:,:-1].values
	y = dataset.iloc[:,-1].values
	print('X data-type',type(X))
	print('X data-type',type(y))
	```
	
- ## Splitting the dataset into the Training set and Test set
	```py
	from sklearn.model_selection import train_test_split
	X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 1/3, random_state = 0)
	```
	
- ## Training the Simple Linear Regression model on the Training set
	```py
	from sklearn.linear_model import LinearRegression
	regressor = LinearRegression()
	regressor.fit(X_train, y_train)   # trains the model
	```

- ## Predicting the Test set results
	```py
	y_pred = regressor.predict(X_test)
	```
	
- ## Visualising the Training set results
	- Here `scatter` will draw dots in the graphs
	- Here `plot` will draw line in the graphs
	```py
	plt.scatter(X_train, y_train, color = 'red')
	plt.plot(X_train, regressor.predict(X_train), color = 'blue')
	plt.title('Salary vs Experience (Training set)')
	plt.xlabel('Years of Experience')
	plt.ylabel('Salary')
	plt.show()
	```
	
- ## Visualising the Test set results
	```py
	plt.scatter(X_test, y_test, color="red")
	plt.plot(X_test, regressor.predict(X_test), color="blue")
	# plt.plot(X_test, y_pred, color="blue")    # because regressor.predict(X_test) is same as y_pred
	# here `plt.plot(X_test, regressor.predict(X_test), color="blue")` and `plt.plot(X_train, regressor.predict(X_train), color="blue")` will give same regresssion line.
	plt.title('Salary vs Experience [Testing set]')
	plt.xlabel('Years of Experience')
	plt.ylabel('Salary')
	plt.show()
	```

- ## Train and Test set result (both):
	```py
	plt.scatter(X_train, y_train, color="red")
	plt.scatter(X_test, y_test, color="blue")
	plt.scatter(X_test, y_pred, color="black")
	plt.plot(X_test, y_pred, color="yellow")
	plt.show()
	```
		
- ## Making a single prediction (for example the salary of an employee with 12 years of experience)
	```py
	print(regressor.predict([[12]]))
	```
	> [138967.5015615]
	- **Note** : 
		> Therefore, our model predicts that the salary of an employee with 12 years of experience is $ 138967,5.
		> Important note: Notice that the value of the feature (12 years) was input in a double pair of square brackets. That's because the "predict" method always expects a 2D array as the format of its inputs. And putting 12 into a double pair of square brackets makes the input exactly a 2D array. Simply put:
		
		> 12→scalar 
		
		> [12]→1D array 
		
		> [[12]]→2D array
		
- ## Getting the final linear regression equation with the values of the coefficients
	```py
	print(regressor.coef_)
	print(regressor.intercept_)
	```
	> [9345.94244312]
	26816.192244031183
	
	- **Note** : 
		> Therefore, the equation of our simple linear regression model is:

		> Salary=9345.94×YearsExperience+26816.19 
		
		> Important Note: To get these coefficients we called the "coef_" and "intercept_" attributes from our regressor object. Attributes in Python are different than methods and usually return a simple value or an array of values.
		
- ### `Salary_Data.csv` : 

	| YearsExperience | Salary    |
	| --------------- | --------- |
	| 1.1             | 39343.00  |
	| 1.3             | 46205.00  |
	| 1.5             | 37731.00  |
	| 2.0             | 43525.00  |
	| 2.2             | 39891.00  |
	| 2.9             | 56642.00  |
	| 3.0             | 60150.00  |
	| 3.2             | 54445.00  |
	| 3.2             | 64445.00  |
	| 3.7             | 57189.00  |
	| 3.9             | 63218.00  |
	| 4.0             | 55794.00  |
	| 4.0             | 56957.00  |
	| 4.1             | 57081.00  |
	| 4.5             | 61111.00  |
	| 4.9             | 67938.00  |
	| 5.1             | 66029.00  |
	| 5.3             | 83088.00  |
	| 5.9             | 81363.00  |
	| 6.0             | 93940.00  |
	| 6.8             | 91738.00  |
	| 7.1             | 98273.00  |
	| 7.9             | 101302.00 |
	| 8.2             | 113812.00 |
	| 8.7             | 109431.00 |
	| 9.0             | 105582.00 |
	| 9.5             | 116969.00 |
	| 9.6             | 112635.00 |
	| 10.3            | 122391.00 |
	| 10.5            | 121872.00 |