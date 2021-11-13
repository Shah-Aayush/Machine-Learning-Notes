# XGBoost *(Extreme Gradient Boosting)*

- Training XGBoost on Training set
	- No feature scaling is required here unlike other classification models.
	```py
	from xgboost import XGBClassifier   # Similarly for regression, there is a class named as `XGRegressor` 
	classifier = XGBClassifier()
	classifier.fit(X_train, y_train)
	```
	
- See whole implementation [here](./xg_boost.ipynb)

---

- an implementation of Gradient Boosting machines which exploits various optimizations to train powerful predictive models very quickly.
- XGBoost is an optimized distributed gradient boosting library designed to be highly efficient, flexible and portable. It implements machine learning algorithms under the Gradient Boosting framework. XGBoost provides a parallel tree boosting (also known as GBDT, GBM) that solve many data science problems in a fast and accurate way. The same code runs on major distributed environment (Hadoop, SGE, MPI) and can solve problems beyond billions of examples.

- [XGBoost Documentation](https://xgboost.readthedocs.io/en/latest/)
- [Learn more about XGBoost...](https://towardsdatascience.com/the-intuition-behind-gradient-boosting-xgboost-6d5eac844920#b18a)