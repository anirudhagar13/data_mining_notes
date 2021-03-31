## Limitations of hierarchical clustering:
- Kmeans can work with noise, but is very sensitive to outliers as they can distort centroids
- Kmeans, make sure to remove extreme outliers
- Hierarchical clustering, outliers would appear at the first level so outlier is not much an issue
- Each algorithm has it's niche (thus, need to know when to apply them)

## Density based clustering:
- Younger algorithm (25 years old)
- It's a niche area (a sub-discipline on it's own)
- This is not very general, like hierarchical or KMeans, was used mostly in the context of spatial data
- Distance between points: euclidean
- Clusters are regions of high density, separated from other high density regions through regions of low density
- The need not necessarily assign every point to a cluster
- Automatically handles outliers so do not need to worry about them, unlike KMeans and Min

## DBScan concepts:
- Define notion of density
- Draw a circle of certain radius (Eps), count the number of points in the circle
- We need (Eps) and threshold of points to call it *high density*.
- Core point is one whose circle has threshold number of points inside it's circle
- Border point (low density regions) is neighbor of core point (within high density regions)
    - If circle of point contains core point, but not enough number of point, then it is border point
- Noise points are points neither border, nor core
    - Circle of noise points neither have core points, nor min. number of points
- Kmeans defined by prototype based clustering / centroids
- DBScan on the other hand are defined by high density regions, not any concept of prototype / centroid

## DBScan algorithm:
- Label core, border and noise points
- Remove noise points
- Form clusters out of connected core points
- Assign border points to it's nearest cluster

## DBScan works well:
- Can handle clusters of different shapes and sizes
- It is resistant to noise (as removes noisy points) (Big difference between Min and DBScan)
- Ignores small clusters made by outliers

## DBScan does not work well:
- Different clusters with different densities cannot be detected (all clusters would have similar densities due to threshold); thus clusters might be merged or some clusters might be removed as noise

## Determining hyperparameters (MinPts, Eps):
- Fix a MinPts (changing this changes shape of curve)
- Plot Eps vs Number of points lost to being noise () 
- Good curve should have a sharp edge

# Cluster validity:
- For supervised learning, it is very easy (various metrics comparing to ground truth)
- Clusters would be found in random data as well
- **Cluster tendency**: Does the data have tendency to cluster
- **External verification**: Compare to know results
- Measures are two types: i. Supervised (external labels available only for test set)
- **Cohesion**: How close are points in the cluster (Sum of squares; euclidean)
- **Cluster separation**: Difference between clusters

## Using Unsupervised measures: 
- Cohesion 
- Separation
- Silhouette coefficient; How strong belongs to a cluster it has been assigned to compared to other clusters it could have been assigned to.
    - b = min(avg distance of points in other clusters)
    - a = avg. distance to points in it's own cluster
    - s = (b-a) / max(a,b)
    - s in {0,1}; the closer to 1, the better
    - Silhouette coefficient would be 0 for points on border of two touching clusters
    - Average silhouette coefficient of all clusters helps with cluster validity 

## Using Correlation:
- Find clusters and put points in one cluster together, then
- Construct similarity matrix, and compare with ideal case
- Ideally, diagonal box would have high similarity and non-diagonal would have low density
- If clusters are arbitrary size and shape, then visualization would not be effective

## Determine the number of clusters:
- As K increases, SSE decreases (K=n; SSE=0)
- Look for **knee** of the curve, to determine the K
- If clusters of diff. sizes and shapes, clusters would not be that crisp

## Supervised Measures:
- Can use labels to get entropy and purity

