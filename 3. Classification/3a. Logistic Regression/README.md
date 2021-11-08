# Logistic Regression  

- Logistic regression is a **Linear** Classifier
- Basic Formulas : 
	- <a href="https://www.codecogs.com/eqnedit.php?latex=\large&space;{\color{Golden}&space;y&space;=&space;b_{0}&space;&plus;&space;b_{1}*x}" target="_blank"><img src="https://latex.codecogs.com/png.latex?\large&space;{\color{Golden}&space;y&space;=&space;b_{0}&space;&plus;&space;b_{1}*x}" title="Simple Regression formula" /></a>
	
	- <a href="https://www.codecogs.com/eqnedit.php?latex=\large&space;{\color{Golden}&space;p&space;=&space;\frac{1}{1&plus;e^{-y}}}" target="_blank"><img src="https://latex.codecogs.com/png.latex?\large&space;{\color{Golden}&space;p&space;=&space;\frac{1}{1&plus;e^{-y}}}" title="Sigmoid Function" /></a>
	
	- <a href="https://www.codecogs.com/eqnedit.php?latex=\large&space;{\color{Golden}&space;ln(\frac{p}{1-p})&space;=&space;b_{0}&space;&plus;&space;b_{1}*x}" target="_blank"><img src="https://latex.codecogs.com/png.latex?\large&space;{\color{Golden}&space;ln(\frac{p}{1-p})&space;=&space;b_{0}&space;&plus;&space;b_{1}*x}" title="Formula for logistic regression" /></a>

---

- ## Importing the libraries
	```py
	import numpy as np
	import pandas as pd
	import matplotlib.pyplot as plt
	```

- ## Importing the dataset
	```py
	dataset = pd.read_csv('Social_Network_Ads.csv')
	X = dataset.iloc[:,:-1].values
	y = dataset.iloc[:, -1].values
	```

- ## Splitting the dataset into the training set and test set
	```py
	from sklearn.model_selectin import train_test_split
	X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.25, random_state=0)
	```

- ## Feature Scaling
	- Here Feature Scaling is not mandatory, but applying it can improve training performance.
	- In SVR, it was necessary. but here it is not.
	- Here we are doing Feature Scaling after splitting the dataset, in order to  avoid information leakage.
	```py
	from sklearn.preprocessing import StandardScaler
	sc = StandardScaler()
	X_train = sc.fit_transform(X_train)
	X_test = sc.transform(X_test)
	```

- ## Training the Logistic Regression model on the Training set
	- Here parameter `C` is the inverse Regularization.
	- The smaller the C, the stronger the regularization. => The more protection towards overfitting. 	
	```py
	from sklearn.linear_model import LogisticRegression
	classifier = LogisticRegression(random_state=0)   # can also name the variable from `classifier` to `clf`
	classifier.fit(X_train, y_train)
	```
	
- ## Predicting a new result
	- Here there are three functions for predicting the results
		1. `predict()`
		2. `predict_log_proba()`
		3. `predict_proba()`
	- ### 1. predict() : 
		```py
		classifier.predict(sc.transform([[36,144000]]))   # test set sample without feature scaling
		```

	- ### 2. predict_proba() : 
		> Will give two values : first one is for `0`, second one is for `1`
		```py
		classifier.predict_proba(sc.transform([[36,144000]]))
		```

- ## Predicting the Test set results
	```py
	y_pred = classifier.predict(X_test)
	```

	- Priting predicted result and actual result side by side : 
	```py
	print(
    np.concatenate(
        ( y_pred.reshape(len(y_pred),1) , y_test.reshape(len(y_test),1) ) , 1
      )
     )
	```

- ## Making the Confusion Matrix

	- Priting the Confusion matrix and Accuracy Score
	```py
	from sklearn.metrics import confusion_matrix, accuracy_score
	cm = confusion_matrix(y_test, y_pred)
	print(cm)
	ac = accuracy_score(y_test, y_pred)
	print(ac)
	```

	**Understanding the Confusion matrix**
	> Here `65` is the correct prediction from class 1 : means test samples where `0` is the actual result and our model also predicted `0`. whereas `3` is the false prediction from class 1 : means test samples where `0` is the actual result but our model predicted `1`.
	
	> Here `24` is the correct prediction from class 2 : means test samples where `1` is the actual result and our model also predicted `1`. whereas `8` is the false prediction from class 2 : means test samples where `1` is the actual result but our model predicted `0`.
	
	**Understanding the Accuracy score**
	> Here we predicted `89` results correctly which is `65 + 24`. 


- ## Computing the accuracy with k-Fold Cross  Validation

	- Creates 10 accuracies and compute average to give final accuracy score.
	- Here standard deviation should be less as it displays that accuracies are not more deviated then each other.
	```py
	from sklearn.model_selection import cross_val_score
	accuracies = cross_val_score(estimator = classifier, X=X_train, y=y_train, cv=10)   # Here we can also put X as X and y as y instead of X_train and y_train
	# here cv is the number of folds.
	print(f"Accuracy : {accuracies.mean()*100 :.2f} %")     # displaying only 2 decimals.
	print(f"Standard Deviation : {accuracies.std()*100 :.2f} %")     # displaying only 2 decimals.
	```
- ## [OPTIONAL] 
	- ### Visualising the Training set results
		
		- This visualisation will not helpful in most of the cases as there can be many features. 
		- Here we can visualise, as there are only two parameters.
		- Here prediction boundry is linear as this is a linear model but kernel or naive bias, it will be non linear.
		```py
		from matplotlib.colors import ListedColormap
		X_set, y_set = sc.inverse_transform(X_train), y_train
		X1, X2 = np.meshgrid(np.arange(start = X_set[:, 0].min() - 10, stop = X_set[:, 0].max() + 10, step = 0.25),
							np.arange(start = X_set[:, 1].min() - 1000, stop = X_set[:, 1].max() + 1000, step = 0.25))
		plt.contourf(X1, X2, classifier.predict(sc.transform(np.array([X1.ravel(), X2.ravel()]).T)).reshape(X1.shape),
					alpha = 0.75, cmap = ListedColormap(('red', 'green')))
		plt.xlim(X1.min(), X1.max())
		plt.ylim(X2.min(), X2.max())
		for i, j in enumerate(np.unique(y_set)):
			plt.scatter(X_set[y_set == j, 0], X_set[y_set == j, 1], c = ListedColormap(('red', 'green'))(i), label = j)
		plt.title('Logistic Regression (Training set)')
		plt.xlabel('Age')
		plt.ylabel('Estimated Salary')
		plt.legend()
		plt.show()
		```


	- ### Visualising the Test set results
		```py
		from matplotlib.colors import ListedColormap
		X_set, y_set = sc.inverse_transform(X_test), y_test
		X1, X2 = np.meshgrid(np.arange(start = X_set[:, 0].min() - 10, stop = X_set[:, 0].max() + 10, step = 0.25),
							np.arange(start = X_set[:, 1].min() - 1000, stop = X_set[:, 1].max() + 1000, step = 0.25))
		plt.contourf(X1, X2, classifier.predict(sc.transform(np.array([X1.ravel(), X2.ravel()]).T)).reshape(X1.shape),
					alpha = 0.75, cmap = ListedColormap(('red', 'green')))
		plt.xlim(X1.min(), X1.max())
		plt.ylim(X2.min(), X2.max())
		for i, j in enumerate(np.unique(y_set)):
			plt.scatter(X_set[y_set == j, 0], X_set[y_set == j, 1], c = ListedColormap(('red', 'green'))(i), label = j)
		plt.title('Logistic Regression (Test set)')
		plt.xlabel('Age')
		plt.ylabel('Estimated Salary')
		plt.legend()
		plt.show()
		```

---

- # `Social_Network_Ads.csv`
	- First 10 rows ...
	
	|Age|EstimatedSalary|Purchased|
	|---|---------------|---------|
	|19 |19000          |0        |
	|35 |20000          |0        |
	|26 |43000          |0        |
	|27 |57000          |0        |
	|19 |76000          |0        |
	|27 |58000          |0        |
	|27 |84000          |0        |
	|32 |150000         |1        |
	|25 |33000          |0        |
	|35 |65000          |0        |
	

---
	
- [Revise Regression and Classification](https://www.superdatascience.com/blogs/the-ultimate-guide-to-regression-classification) *(Optional)*
- [Practice Logistic Regression](./Practice) *(Optional)*