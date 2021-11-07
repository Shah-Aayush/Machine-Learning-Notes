# Regression types : 

1. Simple Linear Regression
2. Multiple Linear Regression
3. Polynomial Linear Regression
4. Support Vector Machine
5. Decision Tree Regression
6. Random Forest Regression
	
# Pros and Cons of Regressions : 

| Regression Model | Pros | Cons |
|---|---|---|
Linear Regression | Works on any size of dataset, gives informations about relevance of features | The Linear Regression Assumptions |
Polynomial Regression | Works on any size of dataset, works very well on non linear problems | Need to choose the right polynomial degree for a good bias/variance tradeoff |
SVR | Easily adaptable, works very well on non linear problems, not biased by outliers | Compulsory to apply feature scaling, not well known, more difficult to understand |
Decision Tree Regression | Interpretability, no need for feature scaling, works on both linear / nonlinear problems | Poor results on too small datasets, overfitting can easily occur |
Random Forest Regression | Powerful and accurate, good performance on many problems, including non linear | No interpretability, overfitting can easily occur, need to choose the number of trees |

# Regularization :

- No Regularization
	![No Regularization](/assets/no_regularization.png "No Regularization formula")
- Lasso Regression (L1 regularization)
	![Lasso Regression (L1 regularization)](/assets/lasso_regression.png "Lasso Regression (L1 regularization)")
- Ridge Regression  (L2 regularization)
	![Ridge Regression  (L2 regularization)](/assets/ridge_regression.png "Ridge Regression  (L2 regularization) formula")
- Elastic Net Regression
	![Elastic Net Regression](/assets/elastic_net_regression.png "Elastic Net Regression formula")

> [Learn more...](https://www.datacamp.com/community/tutorials/tutorial-ridge-lasso-elastic-net)