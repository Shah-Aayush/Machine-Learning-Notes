# Model Selection

## K-Fold Cross Validation

- ## Applying k-Fold Cross Validation

	- We have to apply this method on Training set.
		- Hyperparameters : 
			- `estimator` : classifier model
			- `X` : classifier
			- `y` : classifier
			- `cv` : number of train folds.
		```py
		from sklearn.model_selection import cross_val_score
		accuracies = cross_val_score(estimator=classifier, X=X_train, y=y_train, cv=10)
		print(f"Accuracy : {accuracies.mean()*100:.2f}%")
		print(f"Standard Deviation : {accuracies.std()*100:.2f}%")
		```

- ## Grid Search 

	- Same like K-fold Cross validation, We have to apply this method on Training set.
	
	## Applying Grid Search to find the beset model and the best parameters
	
	- Here `pareameters` is a `list` of `dictionaries`.
	- Here we have to create two dictionaries as there is no value for tunning of `gamma` in SVM when kernel is set to `linear`. `gamma` can only be set when kernel is either `rbf`,`poly` or `sigmoid`.
	```py
	from sklearn.model_selection import GridSearchCV
	parameters = [
				{
					'C' : np.linspace(0,1,num=5).tolist(),    # [0, 0.25, 0.5, 0.75, 1]
					'kernel' : ['linear'],
					'degree' : [3, 4, 5],
				},
				{
					'C' : np.linspace(0,1,num=5).tolist(),    # [0, 0.25, 0.5, 0.75, 1]
					'kernel' : ['rbf','poly','sigmoid'],
					'gamma' : np.linspace(0.1,0.9,num=9).tolist(), # [0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9]
					'degree' : [3,4,5],
				}
				]
	grid_search = GridSearchCV(estimator=classifier, 
								param_grid=parameters,
								scoring='accuracy',  # As we are doing classification, we are using accuracy for scoring models
								cv=10, # number of folds (same like k-fold cross validation)
								n_jobs=-1 # all your processors will be used available in hardware
								)
	grid_search.fit(X_train, y_train)
	```