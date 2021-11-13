# Naive Bayes

## **Implementation**
- *Other steps are same as previous classifications.*

- ## Training the Naïve bayes model on training set 
	```py
	from sklearn.naive_bayes import GaussianNB  
	classifier = GaussianNB()   
	classifier.fit(X_train, y_train)	
	```

---

- Steps : 
	- Bayes Theorem
		![Bayes Theorem](./assets/bayes_theorem.png "Formula of Bayes Theorem")
	- Naive Bayes Classifier
		- Classify as goes to job by `walking` or `driving`
			![Data](./assets/data.png "data")
			- Step 1
			![Data](./assets/step1.png)
			- Step 2
			![Data](./assets/step2.png)
			- Step 3
			![Data](./assets/step3.png)
	
		- Why *Naïve* ?
			> Independence assumption

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