# Decision Tree

## **Imeplementation**
- *Other steps are same as previous classifications.*

- ## Training Decision tree model on Training dataset
	```py
	from sklearn.tree import DecisionTreeClassifier
	classifier = DecisionTreeClassifier(criterion='gini',  random_state=0)   # Here you can choose b/w `gini` and `entropy`
	classifier.fit(X_train, y_train)
	```

---

- **CART** : Classification And Regression Trees
	- Classification Trees
	- Regression Trees
- This is very OLD model
- This method Reborn with upgrades
	- Random Forest
	- Gradient Boosting etc.

- Gini index is always lies b/w 0 and 1.
	- Best case is when gini index is zero.
	- Gini is the default splitting criteria in this algorithm.
	- Whenever algorithm encounter the minimum gini index, it'll be used as splitting.
	- Gini calculation is little faster than IG/Entropy
- Lowest information gain will be selected as splitting for the tree.
	- Here as `log function` comes in computation, this is little slower to compute than gini.
- *At last, it depends on `the data` to choose which criteria and what will be the best fit for that particular data.*
- Helpful Tutorials: 
	- Articles
		- [Understanding Gini Index and Information Gain](https://medium.com/analytics-steps/understanding-the-gini-index-and-information-gain-in-decision-trees-ab4720518ba8)
	- *In Hindi (Videos)*
		- [Information gain and Entropy calculation](https://youtu.be/RVuy1ezN_qA)
		- [Decision tree making](https://youtu.be/ffZ0ShPi-wg)
		- [Brief about decision tree](https://youtu.be/oeKBs41MkNo)
		- [Understand gini index and Entropy/Information Gain](https://youtu.be/-W0DnxQK1Eo)
	
- Gini index and Information Gain are used for the analysis of the real-time scenario, and data is real that is captured from the real-time analysis. In numerous definitions, it has also been mentioned as “impurity of data” or “ how data is distributed. So we can calculate which data is taking less or more part in decision making.

| Gini index | Entropy |
|---|---|
| ![Formula](https://miro.medium.com/max/442/1*vRlwRFknvfgWLBed1vsGoQ.jpeg) | ![Formula](https://miro.medium.com/max/442/1*efLrD1ECWl-utII0KYb7tQ.jpeg) |
|The Gini Index facilitates the bigger distributions so easy to implement| the Information Gain favors lesser distributions having small count with multiple specific values.|
|The method of the Gini Index is used by CART algorithms|  in contrast to it, Information Gain is used in ID3, C4.5 algorithms.|
|Gini index operates on the categorical target variables in terms of “success” or “failure” and performs only binary split|  in opposite to that Information Gain computes the difference between entropy before and after the split and indicates the impurity in classes of elements.|

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