# Artificial Neural Network on Regression

- Implementation is almost same as `classifier for ANN`. the following small changes are made : 
	- changed final activation function of output layer from `sigmoid` to `none` as we are not doing binary classification but we are performing regression here.
	- While compiling ANN, we have used `loss` as `mean_squared_error` rather than `accuracy` (which was used in classification)