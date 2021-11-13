# CatBoost

- Training XGBoost on Training set
	- No feature scaling is required here unlike other classification models.
	```py
	from catboost import CatBoostClassifier   # The same CatBoostRegressor is available for Regression.
	classifier = CatBoostClassifier()
	classifier.fit(X_train, y_train)
	```

- See whole Implementation [here](./catboost.ipynb)

--- 

- **The best part of this method is, you don't need to tune parameters. Reduce time spent on parameter tuning, because CatBoost provides great results with default parameters!**
- **Improve your training results with CatBoost that allows you to use non-numeric factors, instead of having to pre-process your data or spend time and effort turning it to numbers.**
- **Train your model on a fast implementation of gradient-boosting algorithm for GPU. Use a multi-card configuration for large datasets.**
- **Reduce overfitting when constructing your models with a novel gradient-boosting scheme.**
- **Apply your trained model quickly and efficiently even to latency-critical tasks using CatBoost's model applier.**

- About : 
	- CatBoost is an open-source software library developed by Yandex. It provides a gradient boosting framework which attempts to solve for Categorical features using a permutation driven alternative compared to the classical algorithm. 
	- CatBoost is an algorithm for gradient boosting on decision trees. It is developed by Yandex researchers and engineers, and is used for search, recommendation systems, personal assistant, self-driving cars, weather prediction and many other tasks at Yandex and in other companies, including CERN, Cloudflare, Careem taxi.
	- CatBoost is the only boosting algorithm with very less prediction time. Thanks to its symmetric tree structure. It is comparatively 8x faster than XGBoost while predicting.
	- CatBoost is based on gradient boosted decision trees. During training, a set of decision trees is built consecutively. Each successive tree is built with reduced loss compared to the previous trees. The number of trees is controlled by the starting parameters.

- [Official website](https://catboost.ai/)
- [Tutorial video](https://youtu.be/CT_oawxj1ek)