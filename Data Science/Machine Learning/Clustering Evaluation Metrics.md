**Title: Clustering Evaluation Metrics**
**Created: 13-03-2023**
**Tags:** #Clustering #MachineLearning #Metrics 


## Clustering Evaluation Metrics

Here are some differences between the clustering metrics you mentioned:

1. **Within-Cluster Sum of Squares (WCSS)**: WCSS is a measure of the sum of squared distances between each point and its assigned cluster centroid. It measures the compactness of the clusters, with lower values indicating tighter and more compact clusters. WCSS is often used in the Elbow Method to determine the optimal number of clusters.
    $$WCSS=\sum_{j=1}^{k}\sum_{i=1}^{n}||\textbf{x}_{i(j)} - \textbf{c}_{j}||^2$$

	where $\textbf{x}_i$ is the $i$-th data point, $\textbf{c}_{j(i)}$ is the centroid of the cluster to which $\textbf{x}_i$ belongs, and $j$ is the index of the cluster to which $\textbf{x}_i$ belongs.

2. **Silhouette Coefficient**: The Silhouette Coefficient measures the similarity of each point to its assigned cluster compared to other clusters. It ranges from -1 to 1, with higher values indicating better clustering. Positive values indicate that the point is closer to its assigned cluster than to other clusters, while negative values indicate the opposite. A value of 0 indicates that the point is equally close to two or more clusters.
	$$s(i)=\frac{b(i)-a(i)}{\max(a(i),b(i))}$$
	where $a(i)$ is the average distance between $\textbf{x}_i$ and all other data points in the same cluster, and $b(i)$ is the average distance between $\textbf{x}_i$ and all data points in the nearest neighboring cluster (i.e., the cluster with the smallest average distance).
	
3. **Calinski-Harabasz Index**: The Calinski-Harabasz Index is a ratio of the between-cluster variance to the within-cluster variance. It measures the separation between clusters, with higher values indicating better clustering. The index is sensitive to cluster size and tends to favor clusters that are large and well-separated.
	$$CH=\frac{B(k)}{(k-1)}\cdot\frac{N-k}{W(k)}$$
	where $k$ is the number of clusters, $N$ is the total number of data points, $B(k)$ is the between-cluster sum of squares (i.e., the sum of squared distances between the centroids of each cluster and the global centroid), and $W(k)$ is the within-cluster sum of squares (i.e., the sum of squared distances between each data point and its assigned cluster centroid).

4. **Davies-Bouldin Index**: The Davies-Bouldin Index measures the similarity between each cluster and its most similar cluster, taking into account both the within-cluster and between-cluster distances. It ranges from 0 to infinity, with lower values indicating better clustering. The index penalizes clusters that have high within-cluster variance and are close to other clusters with high within-cluster variance.
	$$DBI=\frac{1}{k}\sum_{i=1}^{k}\max_{j\neq i}\left(\frac{s_i+s_j}{d(\textbf{c}_i,\textbf{c}_j)}\right)$$
	where $k$ is the number of clusters, $s_i$ is the average distance between all data points in cluster $i$ and the centroid $\textbf{c}_i$, and $d(\textbf{c}_i,\textbf{c}_j)$ is the distance between the centroids of clusters $i$ and $j$.

5. **Bayesian Information Criterion (BIC)**: The BIC is a model selection criterion that balances the fit of the model to the data with the complexity of the model. It is calculated as the log-likelihood of the data given the model, minus a penalty term for the number of parameters in the model. In the context of clustering, the BIC can be used to select the optimal number of clusters by comparing the BIC values for different numbers of clusters and choosing the number that minimizes the BIC.
    $$BIC=-2\cdot\ln(L)+k\cdot\ln(N)$$
	where $L$ is the likelihood of the data given the model, $k$ is the number of parameters in the model, and $N$ is the total number of data points. The likelihood $L$ is typically calculated using a maximum likelihood estimator or Bayesian inference.

In summary, WCSS measures the compactness of the clusters, the Silhouette Coefficient measures the similarity of points to their assigned clusters, the Calinski-Harabasz Index measures the separation between clusters, the Davies-Bouldin Index measures the similarity between clusters, and the BIC is a model selection criterion that can be used to select the optimal number of clusters. Each metric has its own strengths and weaknesses, and the choice of which metric to use depends on the specific problem and the desired properties of the resulting clusters.

## Pros and Cons

Here are some potential pros and cons of the clustering evaluation metrics you mentioned:

1.  Within-Cluster Sum of Squares (WCSS):
	-   Pros: Simple and easy to calculate. Can help determine the optimal number of clusters.
	-   Cons: Can be biased towards selecting a larger number of clusters. Not a normalized metric.

2.  Silhouette Coefficient:
	-   Pros: Provides an indication of both cluster cohesion and separation. Can handle different types of distance metrics.
	-   Cons: May not work well with very large or very small clusters. Can be computationally expensive for large datasets.

3.  Calinski-Harabasz Index:
	-   Pros: Fast and easy to compute. Measures both separation and compactness.
	-   Cons: Can be sensitive to noise and outliers. May favor selecting a larger number of clusters.

4.  Davies-Bouldin Index:
	-   Pros: Sensitive to both cluster separation and compactness. Can handle clusters with different sizes and shapes.
	-   Cons: Computationally expensive for large datasets. Can be influenced by noisy or outlying clusters.

5.  Bayesian Information Criterion (BIC):
	-   Pros: Provides a probabilistic measure of model fit. Can help select the optimal number of clusters.
	-   Cons: Assumes the data follows a Gaussian distribution. Requires a prior distribution to be specified. Can be computationally expensive for large datasets.

It's important to keep in mind that no single clustering metric is perfect for every situation. The best metric will depend on the specific data and clustering algorithm being used, as well as the goals and constraints of the analysis. It's generally a good idea to use multiple metrics to evaluate clustering results and compare across them.

## Questions
1. **What is the elbow method?**
	The elbow method is a graphical tool used to determine the optimal number of clusters in a clustering algorithm. It involves plotting the values of the evaluation metric (e.g., within-cluster sum of squares) for different numbers of clusters and looking for a point on the plot where the improvement in the metric begins to level off, creating a "bend" or "elbow" shape in the plot. This point is considered the optimal number of clusters for the algorithm.

	The elbow method is not always definitive and may require human judgment in determining the optimal number of clusters. Additionally, it is important to note that the choice of evaluation metric, as well as the specific dataset and clustering algorithm, can affect the results of the elbow method. Therefore, it is generally recommended to use multiple evaluation metrics and perform sensitivity analyses to validate the optimal number of clusters suggested by the elbow method.

2. **Write code for Bayesian Information Criterion**

```python
def bic_score(X, labels):  
"""  
BIC score for the goodness of fit of clusters.  
This Python function is directly translated from the GoLang code made by the author of the paper.  
The original code is available here: https://github.com/bobhancock/goxmeans/blob/a78e909e374c6f97ddd04a239658c7c5b7365e5c/km.go#L778  
"""  
  
n_points = len(labels)  
n_clusters = len(set(labels))  
n_dimensions = X.shape[1]  
  
n_parameters = (n_clusters - 1) + (n_dimensions * n_clusters) + 1  
  
loglikelihood = 0  
for label_name in set(labels):  
X_cluster = X[labels == label_name]  
n_points_cluster = len(X_cluster)  
centroid = np.mean(X_cluster, axis=0)  
variance = np.sum((X_cluster - centroid) ** 2) / (len(X_cluster) - 1)  
loglikelihood += \  
n_points_cluster * np.log(n_points_cluster) \  
- n_points_cluster * np.log(n_points) \  
- n_points_cluster * n_dimensions / 2 * np.log(2 * math.pi * variance) \  
- (n_points_cluster - 1) / 2  
  
bic = loglikelihood - (n_parameters / 2) * np.log(n_points)  
  
return bic
```


## Related Notes

## References
* [Scikit learn Kmeans docs](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html)
* [Scikit learn silhouette_score docs](http://scikit-learn.org/stable/modules/generated/sklearn.metrics.silhouette_score.html#:~:text=The%20Silhouette%20Coefficient%20is%20calculated,max(a%2C%20b)%20.)
* [7 Evaluation Metrics for Clustering Algorithms](https://www.google.com/url?sa=i&url=https%3A%2F%2Ftowardsdatascience.com%2F7-evaluation-metrics-for-clustering-algorithms-bdc537ff54d2&psig=AOvVaw2W182c9jlK9btkfnA6ljYQ&ust=1678801652098000&source=images&cd=vfe&ved=2ahUKEwiliJ_Shdn9AhV3CLcAHSTpDd0Qr4kDegUIARCvAQ)
* [Calinski-Harabasz Index – Cluster Validity indices](https://www.geeksforgeeks.org/calinski-harabasz-index-cluster-validity-indices-set-3/)
* [Are You Still Using the Elbow Method?](https://towardsdatascience.com/are-you-still-using-the-elbow-method-5d271b3063bd)