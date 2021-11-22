# Artificial Neural Network on Classification

# **Implementation**

- ## Importing the libraries
	```py
	import numpy as np
	import pandas as pd
	import tensorflow as tf
	```
	- know tensorflow version : 
	`tf.__version__`

- ## **1. Data Preprocessing**
	```py
	dataset = pd.read_csv('Churn_Modelling.csv')
	X = dataset.iloc[:,3:-1].values   # excluding roll-numbers, customer-IDs and Surname like non-imp columns
	y = dataset.iloc[:,-1].values
	```

- ## Encoding categorical data
	- with the use of `LabelEncoder` and `OneHotEncoder`
	```py
	from sklearn.preprocessing import LabelEncoder
	le = LabelEncoder()
	X[:, 2] = le.fit_transform(X[:, 2])
	```
	
	```py
	from sklearn.preprocessing import OneHotEncoder
	from sklearn.compose import ColumnTransformer
	
	ct = ColumnTransformer(transformers=[('encoder', OneHotEncoder(), [1])], remainder='passthrough')
	X = np.array(ct.fit_transform(X))
	```

- ## Splitting the dataset into the training set and testing set
	```py
	from sklearn.model_selection import train_test_split
	X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2, random_state=0)
	```

- ## Feature Scaling 
	```py
	from sklearn.preprocessing import StandardScaler
	sc = StandardScaler()
	X_train = sc.fit_transform(X_train)
	X_test = sc.transform(X_test)   # only transforming to avoid Information Leakage
	```

- ## **2. Building the ANN**
	- **Initializing the ANN**
	```py
	ann = tf.keras.models.Sequential()
	```
	
	- **Adding the input layer and the first hidden layer**
		- `units` : Number of neurons in the layer.
			> Here there is no rule of thumb to decide how to choose optimal number of units. this can only be chosen by experimenting with different values.
		- `relu` : **Rectifier** Activation Function 
	```py
	ann.add(tf.keras.layers.Dense(units=6, activation='relu'))
	```
	
	- **Adding the second hidden layer**
		- Here adding second layer will be no different process then the first one. although,  
			> we can make some tweaks in that too!
	```py
	ann.add(tf.keras.layers.Dense(units=6, activation='relu'))	
	```
	
	- **Adding the output layer**
		- Here dimention of the output `y` is 1, so we'll choose the number of neurons as 1.
		- Here as activation function, we are choosing SIGMA as we have binary classification.
	```py
	ann.add(tf.keras.layers.Dense(units=1, activation='sigmoid'))
	```

- ## **Training the ANN**
	- **Compiling the ANN**
		- Updating weights and reducing cost.
		- `optimizer` : gradient descent method. Here we are choosing `adam` as one of the method.
		- `loss` : as we are doing binary classification, we'll use `binary_crossentropy` which will apply `CROSS ENTROPY` eq.
			> For non-binary classification use `categorical_crossentropy` as `loss` function and `softmax` as `activation` function above.
		- `metrics` : choosing accuracy. although we can also choose multiple metrices.
	```py
	ann.compile(optimizer='adam', loss='binary_crossentropy', metrics=['accuracy'])
	```

	- **Training the ANN on the Training set**
		- we need two more arguments : `batch_size` & `epochs` rather than conventional method of only giving `X_train` and `y_train`.
		- Here we are also setting the `batch size` which means instead of checking predictions and comparing it with every example, we'll compare it after these number of examples.
	```py
	ann.fit(X_train, y_train, batch_size=32, epochs=100)
	```

- *Now you can simply predict the values through `.predict()` method.*
	
	
---

- ## Dataset : `Churn_Modelling.csv`

|RowNumber|CustomerId|Surname |CreditScore|Geography|Gender|Age|Tenure|Balance  |NumOfProducts|HasCrCard|IsActiveMember|EstimatedSalary|Exited|
|---------|----------|--------|-----------|---------|------|---|------|---------|-------------|---------|--------------|---------------|------|
|1        |15634602  |Hargrave|619        |France   |Female|42 |2     |0        |1            |1        |1             |101348.88      |1     |
|2        |15647311  |Hill    |608        |Spain    |Female|41 |1     |83807.86 |1            |0        |1             |112542.58      |0     |
|3        |15619304  |Onio    |502        |France   |Female|42 |8     |159660.8 |3            |1        |0             |113931.57      |1     |
|4        |15701354  |Boni    |699        |France   |Female|39 |1     |0        |2            |0        |0             |93826.63       |0     |
|5        |15737888  |Mitchell|850        |Spain    |Female|43 |2     |125510.82|1            |1        |1             |79084.1        |0     |
|6        |15574012  |Chu     |645        |Spain    |Male  |44 |8     |113755.78|2            |1        |0             |149756.71      |1     |
|7        |15592531  |Bartlett|822        |France   |Male  |50 |7     |0        |2            |1        |1             |10062.8        |0     |
|8        |15656148  |Obinna  |376        |Germany  |Female|29 |4     |115046.74|4            |1        |0             |119346.88      |1     |
|9        |15792365  |He      |501        |France   |Male  |44 |4     |142051.07|2            |0        |1             |74940.5        |0     |
|10       |15592389  |H?      |684        |France   |Male  |27 |2     |134603.88|1            |1        |1             |71725.73       |0     |
