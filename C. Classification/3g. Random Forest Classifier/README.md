# Random Forest Classifier

## **Implementation**
- *Other steps are same as previous classifications.*

- ## Training Decision tree model on Training dataset
	Here, 
	- `n_estimators` : Number of trees (default value is `100`)
		> As we have smaller datasset, our model will work fine with `10` trees. 
	- criterion : `gini` or `entropy`
	```py
	from sklearn.ensemble import RandomForestClassifier
	classifier = RandomForestClassifier(n_estimators = 10, criterion = 'entropy', random_state = 0)
	classifier.fit(X_train, y_train)
	```


---

- **Ensemble Learning** : a machine learning technique that combines several base models in order to produce one optimal predictive model.

- Random Forest Intuition
	1. Pick at random K data points from the Training set.
	2. Build the Decision Tree associated to these K data points.
	3. Choose the number Ntree of trees you want to build and repeat STEPS `1` and `2`
	4. For a new data point, make each one of your Ntree trees predict the category to which the data points belongs, and assign the new data point to the category that wins the majority vote.

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