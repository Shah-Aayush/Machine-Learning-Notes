# K-Nearest Neighbor

- Steps : 
	1. Choose the number K of neighbors
		> Default value for K is `5`
	2. Take the  K nearest neighbors of the new data point, according to the Euclidean distance
	3. Among these K neighbors, count the number of  data points in each category
	4. Assign the new data point to the category where you counted the most neighbors
	
	- Your Model is READY.
	
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
	X = dataset.iloc[:, :-1].values
	y = dataset.iloc[:, -1].values
	```

- ## Splitting the dataset into the Training set and Test set
	```py
	from sklearn.model_selection import train_test_split
	X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.25, random_state=0)
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
	
- ## Training the K-NN model on the Training set
	- Here metric set to `minkowski` and p=2 means equivalent to the **STANDARD EUCLIDEAN METRIC**.
	```py
	from sklearn.neighbors import KNeighborsClassifier
	classifier = KNeighborsClassifier(n_neighbors = 5, metric = 'minkowski', p = 2)   # metric set to `minkowski` and p=2 means equivalent to the STANDARD EUCLIDEAN METRIC.
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
	

	