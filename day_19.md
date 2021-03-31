# Advance Clustering:
- Prototype based: KMeans
    - Center is representative
    - Define as objective to minimize
- Density based: DBScan
    - Cluster represents regions of high density
- Graph based: Hierarchical (Shared Nearest Neighbor)
    - Produced dendograms
    - Group average, single-link to bring clusters together
    - Chameleon: a generalized 
    - Jarvis Patrick, SNN
- Mostly based on proximity metrics

## Prototype based methods:

### Fuzzy c-means:
- Hard/crisp clustering (each data point assigned to only one cluster): KMeans
- Soft/fuzzy clustering (data point can be assigned to multiple clusters)
- In KMeans, we optimize SSE
- An additional weight is added to each point, corresponding to each cluster the point can belong to
- Initial cluster centers, assign weight to each cluster with weight inversely proportional to distance to the cluster center
- Weight mean taken to compute new cluster centers, and then above steps are repeated
- Trying to optimize the SSE
- All weights for each point has to add up to 1
- SSE vs w_x1 plot (SSE only optimized when point assigned to the closest cluster)
- Instead raise to the power w_x1^p; p=1 (means most optimized is only K-means)
- If p>1; SSE is optimized, even though point might be assigned to multiple clusters (different from K-means)
- SSE would be reduced in successive iterations
- If p is large (weights become similar for all cluster - fuzzify factor)
- If p is small 1 (only one weight becomes very large = 1)
- P value is obtained through heuristics, not any analytical solution
- Image segmentation are great use cases of fuzzy c-means (Kmeans does not work that well in this case)

### Expectation / Maximization algorithm (Clustering using mixture of models):
- EM is based on probabilistic framework 
- K-means is a special case of EM algorithm
- EM assigns each a point a certain probability (different from weights) of belonging to each of the clusters
- Kmeans requires (centers, distance/proximity)
- Each cluster represented as parameters of probabilistic model in the mixture
- Each of point can be assigned to be belonging to any of the probabilistic distribution among the mixture
- For crisp clustering, assign to distribution with highest probability, else can keep it fuzzy
- Assume that we know n of the n-number of mixture models

### EM algorithm:
- Initialize the parameters for the distribution of mixtures
- For Each point compute the probability of it belonging to a distribution
- Use these probabilities to re-calibrate the parameters and repeat
- Can use random initialization, can get stuck into local minima
- Find expectation of a point P(C_j|x_i) [posterior] belonging to cluster, use probability to find new params with highest likelihood P(x_i|C_j)
- In Fuzzy c-means: center is dark, edge is light (higher weight more dark point is)
- In EM: both center and edge are dark

### Advantages / Disadvantages:
- Can find Dense and sparse clusters
- Can even detect clusters half way into other clusters
- Convergence can be slow, guarantees only local minima
- Have to make a lot of assumptions

## Self-organizing Maps:
- Like K-Means have fixed number of clusters, and concept of centroids
- Also organizes clusters in a spatial map (preferably in a grid) - provided by the user 
- Not only update one centroid, but other centroids based on their spatial proximity
- Derived from both Kmeans and Fuzzy-c means (fuzziness structure defined by the user)
- Helps tell how clusters are correlated with each other
 

