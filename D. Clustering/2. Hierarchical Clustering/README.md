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

- We have to set Distance/Dissimilarity Threshold on Euclidean Distance axis. 
	> The number of vertical lines crosses the threshold line *(Horizontal line)* is equal to the number of cluster at the current threshold we have.
	> Here we have `2` clusters.
	
|2 clusters|4 clusters|6 clusters|
|---|---|---|
|![](./assets/10.png "2 clusters")|![](./assets/11.png "4 clusters")|![](./assets/12.png "6 clusters")|

- As if we are using `ELBOW` method in k-means clustering, to find optimal numbers of clusters, here are using this method to find *Optimal Number Of Clusters*

|Largest distance = optimal number of clusters = 2|
|---|
|![](./assets/13.png "Here, optimal number of clusters is 2")|

|Another Example|
|---|
|![](./assets/14.png "Here, optimal number of clusters is 3")|