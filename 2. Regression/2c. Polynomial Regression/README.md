# Polynomial Regression

- ## Libraries to be imported : 
	```py
	import numpy as np
	import matplotlib.pyplot as plt
	import pandas as pd
	```

- ## Importing Dataset
	```py
	dataset = pd.read_csv('Position_Salaries.csv')
	X = dataset.iloc[:,1:-1].values
	y = dataset.iloc[:,-1].values
	```
	- If we have very small dataset, and we just want to compare different models working on the datasets, we need not to split datasets in train and test sets.
		- If we want to split dataset in train-test sets then : 
			```py
			from sklearn.model_selection import train_test_split
			X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
			```
		- **Here, we are skipping this SPLITTING STEP.**
	
- ## Training the Linear Regression model on the whole dataset
	- This is just a Simple linear regression.
	```py
	from sklearn.linear_model import LinearRegression
	lin_reg = LinearRegression()
	lin_reg.fit(X, y)
	```

- ## Training the Polynomial Regression model on the whole dataset
	- This is polynomial regression with degree 2. we can specify degree in PolynomialFeature function.
	- here we are doing following steps : 
		1. Create Polynomial Features Model of required degrees
		2. Apply polynomial model (fit_transform model on X) to get required variables.
		3. Create LinearRegression model
		4. Fit that LinearRegression model with newly created X_poly variables and y.
	```py
	from sklearn.preprocessing import PolynomialFeature
	poly_reg = PolynomialFeatures(degree=2)
	X_poly = poly_reg.fit_transform(X)
	lin_reg_2 = LinearRegression()
	lin_reg_2.fit(X_poly, y)
	```
	
- ## Visualising the Linear Regression results
	```py
	plt.scatter(X, y, color='red')
	plt.plot(X, lin_reg.predict(X), color='blue')
	plt.xlable('Position Level')
	plt.ylable('Salary')
	plt.title('Truth or Bluff (Linear Regression)')
	plt.show()
	
	```

- ## Visualising the Polynomial Regression results
	- Here we have to give `X as normal X` and `X_poly as Y predicted`. because this lin_reg_2 model requires X_poly's degree 2 variables to predict the salary.
	```py
	plt.scatter(X, y, color='red')
	plt.plot(X, lin_reg_2.predict(X_poly), color='blue')
	plt.xlabel('Position Level')
	plt.ylabel('Salary')
	plt.title('Truth or Bluff (Polynomial regression)')
	plt.show()
	```

- ## Predicting a new result with Linear Regression 
	```py
	lin_reg.predict([[6.5]])
	```

- ## Predicting a new result with Polynomial Regression 
	```py
	poly_reg = PolynomialFeatures(degree=4)
	X_poly = poly_reg.fit_transform([[6.5]])

	print('method 1 :',lin_reg_2.predict(X_poly))
	print('method 2 :',lin_reg_2.predict(PolynomialFeatures(degree=4).fit_transform([[6.5]])))
	```

---

- ## Difference between Simple Linear, Multiple Linear, Polynomial Linear Regression : 
	- Simple Linear Regression : y = b<sub>0</sub> + b<sub>1</sub>x<sub>1</sub>
	- Multiple Linear Regression : y = b<sub>0</sub> + b<sub>1</sub>x<sub>1</sub> + b<sub>2</sub>x<sub>2</sub> + b<sub>3</sub>x<sub>3</sub> + ... + b<sub>n</sub>x<sub>n</sub>
	- Polynomial Linear Regression : y = b<sub>0</sub> + b<sub>1</sub>x<sub>1</sub> + b<sub>2</sub>x<sub>1</sub><sup>2</sup> + b<sub>3</sub>x<sub>1</sub><sup>3</sup> + ... + b<sub>n</sub>x<sub>1</sub><sup>n</sup>
	
- In Polynomial non linear regression, there can be multiple coefficients in one single term. Like one in numerator and another one in denominator.
- We can say that *Polynomial regression is a special case of Multiple Linear regression* <u>*(btw, we should not 😅)*</u>

---

# `Position_Salaries.csv`
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