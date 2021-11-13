# Data Preprocessing

- Libraries to be imported : 
	```py
	import numpy as np
	import matplotlib.pyplot as plt
	import pandas as pd
	```

- ## Importing dataset : 
	```py
	dataset = pd.read_csv('Data.csv')
	X = dataset.iloc[:,:-1].values
	y = dataset.iloc[:,-1].values
	```

- ## Taking care of missing data : 
	```py
	from sklearn.impute import SimpleImputer
	imputer = SimpleImputer(missing_values=np.nan, strategy='mean')		#replace only np.nan values i.e. EMPTY VALUES
	imputer.fit(X[:,1:3])		# calculates mean for all specified columns (only applying for columsn which have numerical values; Remember to exclude columns which has string values)
	X[:,1:3] = imputer.transform(X[:,1,3])	# applies mean in missing places (this transform method returns new variable with replacement)
	```

- ## Encoding categorical data
	
	- ### Encoding the independent variable (when variable values are independent from each others like colors, places, names etc.)
		- Generates different values for different categorical data. 
		- It will create the number of columns equal to the number of unique values. Here as we have three unique values, i.e. France, Spain, Germany => It will create three different columns
		- Here in `ColumnTransformer` we have to give two arguments : 
			1. Encoding type and indecies of columns *(on which we want to perform encoding)*
				> `OneHotEncoder` is type and index is only **0**.
			2. what to do of remaining columns ?
				> `passthrough` *(leaves unaffected)*
		- As `columnTransform`'s `fit_transform` method doesn't return `numpy array` we have to manually convert into nparray.
		- No numerical order will be given in this.
		```py
		from sklearn.compose import ColumnTransformer
		from sklearn.preprocessing import OneHotEncoder
		ct = ColumnTransformer(transformers=[('encoder', OneHotEncoder(),[0])], remainder='passthrough')
		X = np.array(ct.fit_transform(X))		# fits and transforms both in one line
		```
	
	- ### Encoding the dependent variable
		- Generates decimal values continuously from zero like 0,1,2,...
		- As this is dependent variable, we don't need it to be a numpy array so we are not converting it to np array here unlike in previous code snippet
		```py
		from sklearn.preprocessing import LabelEncoder
		le = LabelEncoder()
		y = le.fit_transform(y)
		```

- **We have to split our training and testing datasets before applying feature scaling**
	- because applying feature scaling can cause **information leakage** as it uses mean and standard deviation for scaling data.
	- we want our model to have a brand new test set and no information from training set should be given to test set so we will always apply feature scaling after we split our data.
	
- ## Splitting the dataset into the Training set and Test set
	- `test_size` is split size for test set. here we will give it `0.2` value which is *20%* of whole data.
	- setting random_state at 1 will fix the random values. every time we execute this code it will give same randomized values.
	- by default `random_state` is set to `None`. which means that each time we execute this, will give different result.  upon setting fix integer value to this, will seed a number to random generator and give the same output each time we execute the snippet.
	```py
	from sklearn.model_selection import train_test_split
	X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=1)
	```

- ## Feature Scaling
	- to avoid some feature to be dominated by other features in *some* machine learning models
	- Two methods: 
		1. Standardisation : 
			
			<img src="https://render.githubusercontent.com/render/math?math=X_{stand}\=\frac{x-mean(x)}{standard deviation(x)}">
			
			- all the features will take values in (-3,3)
			- This will work all the time *[RECOMMENDED APPROACH]*
		2. Normalisation : 
			
			<img src="https://render.githubusercontent.com/render/math?math=X_{norm}\=\frac{x-min(x)}{max(x) - min(x)}">
			
			- all the features will take values in (-1,1)
			- This will work we have normal distribution in most of features
	- We don't have to apply feature scaling on dummy variables which are generated here with `ColumnTransformer`,`OneHotEncoder` and `LabelEncoder`.
	- Applying Feature scaling on dummy variable may end up loosing information. also values in dummy variables are already in range.
	- Notice that we have used only `.transform` method for `x_test`. because we don't want apply scaling based on the test set. we just fitted our training model's mean,std on testing set.
		> As our model will be trained on test set so in order to perfect comparison b/w predicted and test sets, we should apply only transform method on x_test.
	```py
	from sklearn.preprocessing import StandardScaler
	sc = StandardScaler()
	X_train[:,3:] = sc.fit_transform(X_train[:,3:])
	X_test[:,3:] = sc.transform(X_test[:,3:])
	```
	
- ### `Data.csv` : 

	| Country | Age | Salary | Purchased |
	| ------- | --- | ------ | --------- |
	| France  | 44  | 72000  | No        |
	| Spain   | 27  | 48000  | Yes       |
	| Germany | 30  | 54000  | No        |
	| Spain   | 38  | 61000  | No        |
	| Germany | 40  |        | Yes       |
	| France  | 35  | 58000  | Yes       |
	| Spain   |     | 52000  | No        |
	| France  | 48  | 79000  | Yes       |
	| Germany | 50  | 83000  | No        |
	| France  | 37  | 67000  | Yes       |