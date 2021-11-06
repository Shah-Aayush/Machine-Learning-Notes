# Evaluating Regression Model's Performance

## R Square 
	
- It tells how the model is fit to your data. *(Compared to average line drawn to the data)*

- Formula : 

	- <a href="https://www.codecogs.com/eqnedit.php?latex=\LARGE;{\color{Golden}SS_{res}=SUM((y_i-\hat{y_{i}})^2))}" target="_blank"><img src="https://latex.codecogs.com/png.latex?\LARGE;{\color{Golden}SS_{res}=SUM((y_i-\hat{y_{i}})^2))}" title="SS-residual formula" /></a>

	- <a href="https://www.codecogs.com/eqnedit.php?latex=\LARGE;{\color{Golden}SS_{tot}=SUM((y_i-y_{avg})^2))}" target="_blank"><img src="https://latex.codecogs.com/png.latex?\LARGE;{\color{Golden}SS_{tot}=SUM((y_i-y_{avg})^2))}" title="SS-total formula" /></a>

- => <a href="https://www.codecogs.com/eqnedit.php?latex=\LARGE;{\color{Golden}R^2=1-\frac{SS_{res}}{SS_{tot}}}" target="_blank"><img src="https://latex.codecogs.com/png.latex?\LARGE;{\color{Golden}R^2=1-\frac{SS_{res}}{SS_{tot}}}" title="R square formula" /></a>

- The closer the R<sup>2</sup> to one, the better. R<sup>2</sup> can be negative. So the lower the R<sup>2</sup>, the worsen the model is.
- We have to minimize SS<sup>res</sup>.
- SS<sup>res</sup> - Goodness of fit *(greater is beter)*.
- Here problem for multiple variable is that R square will never decrease. Using R square will not help us to determine whether the new added variable is helping our model or not.


## Adjusted R<sup>2</sup>

- <a href="https://www.codecogs.com/eqnedit.php?latex=\LARGE;{\color{Golden}Adj&space;R^2=1-(1-R^2)\frac{n-1}{n-p-1}}" target="_blank"><img src="https://latex.codecogs.com/png.latex?\LARGE;{\color{Golden}Adj&space;R^2=1-(1-R^2)\frac{n-1}{n-p-1}}" title="Adjusted R square formula" /></a>
	- p - number of regressors *(Number of independent variables)*
	- n - sample size
- So by this formula, adding more variables will decrease the R square unlike above formula.
- This will help us to determine whether the model is good or not.