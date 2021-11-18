# Hierarchical Clustering

## **Intuition**

|What does Hierarchical Clustering do ?|
|---|
|![image](./assets/1.png)|

- ## Two types of hierarchical clustering : 
	- Agglomerative		*(Bottom-up Approach)*
		> Here we'll discuss more about `Agglomerative` approach.
	- Divisive		*(Top-Down Approach)*
	
- ## Agglomerative HC
	1. Make each data point a single-point cluster -> That forms N clusters
	2. Take the two closest data points and make them one cluster -> That forms N-1
	3. Take the two closest clusters and make them one cluster -> That forms N-2
		> Here, method of calculating the distance matters. *(like euclidean distance etc.)*
	4. Repeat *STEP 3* until there is only one cluster
	
	**FINISH**
	
|Euclidean Distance|
|---|
|![formula of euclidean distance](./assets/2.png)|

|Distance between clusters|
|---|
|![Different method for calculating distances b/w two clusters](./assets/3.png "Different method for calculating distances b/w two clusters")|

- Hierarchical clustering maintains the memory of how we formed the different clusters.

## **How do `Dendrograms` works?**

- Dandograms is a kind of memory of HC algorithms which memories how we formed the clusters.
- The height of the bar measures the dissimilarity b/w that two end-points.

- Steps to form Dendrograms : 

|Step 1|Step 2|Step 3|Step 4|Step 5|
|---|---|---|---|---|
|![](./assets/4.png "Making first cluster")|![](./assets/5.png "")|![](./assets/6.png "")|![](./assets/7.png "")|![](./assets/8.png "Making last cluster")|

|FINAL generated **Dendrogram**|
|---|
|![](./assets/9.png "Final Dendrogram")|

## Using Dendrograms