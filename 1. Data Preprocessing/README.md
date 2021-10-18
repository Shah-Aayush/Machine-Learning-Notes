# Data Preprocessing

- Libraries to be imported : 
	```py
	import numpy as np
	import matplotlib.pyplot as plt
	import pandas as pd
	```

- Importing dataset : 
	```py
	dataset = pd.read_csv('Data.csv')
	X = dataset.iloc[:,:-1].values
	y = dataset.iloc[:,-1].values
	```

- Taking care of missing data : 
	```py
	from sklearn.impute import SimpleImputer
	imputer = SimpleImputer(missing_values=np.nan, strategy='mean')
	imputer.fit(X[:,1:3])		# calculates mean for all specified columns
	X[:,1:3] = imputer.transform(X[:,1,3])	# applies mean in missing places
	```

- Encoding categorical data
	
	- Encoding the independent variable (when variable values are independent from each others like colors, places, names etc.)
		- Generates binary values for different categorical data.
		```py
		from sklearn.compose import ColumnTransformer
		from sklearn.preprocessing import OneHotEncoder
		ct = ColumnTransformer(transformers=[('encoder', OneHotEncoder(),[0])], remainder='passthrough')
		X = np.array(ct.fit_transform(X))		# fits and transforms both in one line
		```
	
	- Encoding the dependent variable
		- Generates decimal values continuously from zero like 0,1,2,...
		```py
		from sklearn.preprocessing import LabelEncoder
		le = LabelEncoder()
		y = le.fit_transform(y)
		```
	
- Splitting the dataset into the Training set and Test set
	```py
	from sklearn.model_selection  import train_test_split
	X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=1)
	```

- Feature Scaling
	```py
	from sklearn.preprocessing import StandardScaler
	sc = StandardScaler()
	X_train[:,3:] = sc.fit_transform(X_train[:,3:])
	X_test[:,3:] = sc.fit_transform(X_test[:,3:])
	```