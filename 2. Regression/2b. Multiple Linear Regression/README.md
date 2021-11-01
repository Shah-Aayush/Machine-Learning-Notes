# Multiple Linear Regression



---

- **Dummy Variables** : Data in column `States` are categorical values so we have to assign dummy variables to that column. 
	- We can create number of columns equal to the number of unique values in this categorical `States` column. Suppose if there are two unique values `New York` and `California` then we can create two columns `New York` and `California`. in which if the `States` says `New York`, we can put `1` in new york and 0 in california columns. 
	- We don't need to include `States` column now as we have converted that column's data in two new columns. also if we not include one of the column from this two columns, it is okay as if we say 1 in new york it means there is no california and 0 in new york is there is california so including only 1 column among this two will be fine.
	- Not including one column will not make our model *BIAS* as it has default state as california if we include new york  and not include california column.
	- Including both columns will basically a duplicating a variable. Including all dummy variables can cause a *Dummy Variable Trap*.
	- During Building a model always omit *One* Dummy variable.
	
- **Statistical Significance** : Statistical significance is a determination made by an analyst that the results in the data are not explainable by chance alone. Statistical hypothesis testing is the method by which the analyst makes this determination. This test provides a p-value, which is the probability of observing results as extreme as those in the data, assuming the results are truly due to chance alone. A p-value of 5% or lower is often considered to be statistically significant.
	[Read more...](https://www.investopedia.com/terms/s/statistically_significant.asp)

- **Building a Model**
	5 methods  of building models : 
		1. All-in
		2. Backward Elimination
		3. Forward Selection
		4. Bidirectional Elimination
		5. Score Comparison

	> `Stepwise Regression` includes : `Backward Elimination`, `Forward Selection`, `Bidirectional Elimination`. 
	> Sometimes it is also refers to `Bidirectional Elimination` only.
	
	- `All-in` cases : 
		- Prior knowledge
		- You have to 
		- Preparing for Backward Elimination
	
	- `Backward Elimination` :
		1. Select a significance level to stay in the model (e.g SL = 0.05) *{Here `SL` means Significance Levels}*
		2. Fit the full model with all possible predictors
		3. Consider the predictor with the `highest P-value`. if `P > SL`, go to step 4 otherwise go to *FINISH*
		4. Remove the predictor
		5. Fit model without this variable. 
			- Then we have to Rebuild the model/Refit the model
			- Coefficient and constants will be different then if we remove one variable.
			- Go back to step 3. and check for new p-values.
			
		FINISH : Your model is ready.
	
	- `Forward Selection` : 
		1. Select a significance level to enter the model (e.g. SL = 0.05)
		2. Fit all simple regression models y ~ x<sub>n</sub>. Select the one with the lowest P-value.
		3. Keep this variable and fit all possible models with one extra predictor added to the one(s) you already have.
		4. Consider the predictor with the lowest P-value. If `P < SL`, go to step 3, otherwise go to FINISH.
		
		FINISH : Keep the previous model.
		
	- `Bidirectional Elimination` :
		1. Select a significance level to enter and to stay in the model. e.g. SLENTER = 0.05, SLSTAY = 0.05
		2. Perform the next step of `Forward Selection` *(New variables must have P < SLENTER to enter)*
		3. Perform all steps of `Backward Elimination` *(Old variables must have P < SLSTAY to stay)*
		4. No new variables can enter and no old variables can exit.
		
		FINISH : Your model is ready.
		
	- `All Possible Models` : 
		1. Select a criterion  of  goodness of fit *(e.g. Akaike criterion)*
		2. Construct all possible regression Models : 2<sup>N</sup>-1 total combinations
		3. Select the one with the best criterion.
		
		FINISH : Your model is ready.
		
---

- ### `50_Startups.csv` : 

	|R&D Spend|Administration|Marketing Spend|State     |Profit   |
	|---------|--------------|---------------|----------|---------|
	|165349.2 |136897.8      |471784.1       |New York  |192261.83|
	|162597.7 |151377.59     |443898.53      |California|191792.06|
	|153441.51|101145.55     |407934.54      |Florida   |191050.39|
	|144372.41|118671.85     |383199.62      |New York  |182901.99|
	|142107.34|91391.77      |366168.42      |Florida   |166187.94|
	|131876.9 |99814.71      |362861.36      |New York  |156991.12|
	|134615.46|147198.87     |127716.82      |California|156122.51|
	|130298.13|145530.06     |323876.68      |Florida   |155752.6 |
	|120542.52|148718.95     |311613.29      |New York  |152211.77|
	|123334.88|108679.17     |304981.62      |California|149759.96|
	|101913.08|110594.11     |229160.95      |Florida   |146121.95|
	|100671.96|91790.61      |249744.55      |California|144259.4 |
	|93863.75 |127320.38     |249839.44      |Florida   |141585.52|
	|91992.39 |135495.07     |252664.93      |California|134307.35|
	|119943.24|156547.42     |256512.92      |Florida   |132602.65|
	|114523.61|122616.84     |261776.23      |New York  |129917.04|
	|78013.11 |121597.55     |264346.06      |California|126992.93|
	|94657.16 |145077.58     |282574.31      |New York  |125370.37|
	|91749.16 |114175.79     |294919.57      |Florida   |124266.9 |
	|86419.7  |153514.11     |0              |New York  |122776.86|
	|76253.86 |113867.3      |298664.47      |California|118474.03|
	|78389.47 |153773.43     |299737.29      |New York  |111313.02|
	|73994.56 |122782.75     |303319.26      |Florida   |110352.25|
	|67532.53 |105751.03     |304768.73      |Florida   |108733.99|
	|77044.01 |99281.34      |140574.81      |New York  |108552.04|
	|64664.71 |139553.16     |137962.62      |California|107404.34|
	|75328.87 |144135.98     |134050.07      |Florida   |105733.54|
	|72107.6  |127864.55     |353183.81      |New York  |105008.31|
	|66051.52 |182645.56     |118148.2       |Florida   |103282.38|
	|65605.48 |153032.06     |107138.38      |New York  |101004.64|
	|61994.48 |115641.28     |91131.24       |Florida   |99937.59 |
	|61136.38 |152701.92     |88218.23       |New York  |97483.56 |
	|63408.86 |129219.61     |46085.25       |California|97427.84 |
	|55493.95 |103057.49     |214634.81      |Florida   |96778.92 |
	|46426.07 |157693.92     |210797.67      |California|96712.8  |
	|46014.02 |85047.44      |205517.64      |New York  |96479.51 |
	|28663.76 |127056.21     |201126.82      |Florida   |90708.19 |
	|44069.95 |51283.14      |197029.42      |California|89949.14 |
	|20229.59 |65947.93      |185265.1       |New York  |81229.06 |
	|38558.51 |82982.09      |174999.3       |California|81005.76 |
	|28754.33 |118546.05     |172795.67      |California|78239.91 |
	|27892.92 |84710.77      |164470.71      |Florida   |77798.83 |
	|23640.93 |96189.63      |148001.11      |California|71498.49 |
	|15505.73 |127382.3      |35534.17       |New York  |69758.98 |
	|22177.74 |154806.14     |28334.72       |California|65200.33 |
	|1000.23  |124153.04     |1903.93        |New York  |64926.08 |
	|1315.46  |115816.21     |297114.46      |Florida   |49490.75 |
	|0        |135426.92     |0              |California|42559.73 |
	|542.05   |51743.15      |0              |New York  |35673.41 |
	|0        |116983.8      |45173.06       |California|14681.4  |