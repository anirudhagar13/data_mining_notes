# Chapter 3 (Classification)
- Supervised Machine Learning
- Use labelled data to prepare models and perform classification using Big Data
- Each record is a tuple (attribute set [x], class attribute [y])
- y: response, dependent variable (Here binary, but generally can be not-binary)
- Training set also called *Labeled set* -> Learn a model (Using learning algorithm)
- Then, we can apply model on data for which we don't have class labels
- Bayesian Belief Networks 80s; SVM 90s; multiple waves of Neural networks (65s, 85s, 10s, 15s)
- DNNs are state of the art (data hungry)
- Ensemble methods: Use a collection of classifiers

## Decision Trees:
- Can exist multiple trees, but should work well on unseen data
- Tree has to be generalised as well as work well on training data (low bias and low variance)
- Decision Tree Induction: 
	- Hunt's algorithm (earliest)
	- CART (based on regression trees)
	- ID3, C4.5
	- More recently 90s for large datasets (SLIQ, SPRINT) - for scalable
- Hunt's algorithm:
	- It's a recursive procedure
	- Given a set of records, if all belong to same class, no needs for decision tree and arive at the leaf
	- If records belong to more than one class, split records using one of the attributes
	- Repeat process, until run out of attributes, or reach a point where classes in set of records become same
- Default label based on ratio of class labels in the sample obtained from population
- Use one attribute (Home Owner), in both branches not repeat the process

### How to choose the right attribute and how to choose for non-binary target:
- Can have exponential number of trees
- How to find the optimal decision trees (question being asked in 75s) - NP hard
- Go for **greedy approach**, things that look good locally

### How should training records split:
- Nominal attributes: Multi-way splits (for each value), Binary split (all possible subsets)
- Ordinal attributes: Multi-way splits (for each value), Binary split (all possible subsets - pruned through maintaining the order)
- Continuous attributes: Binary split (Using a threshold), Multiway splits (multiple thresholds / grouping)
- Split such a way that nodes are purest (all records belonging to one class)
- Notion of how good a node is, also collectively how good all nodes are post-split

#### Node Impurity:
- **Gini Index:** Highest impurity (.5; means equal distribution for two class), Lowest impurity (0; for pure node). = 1 - sum (fraction of all classes)^2
- Highest impurity (1 - 1/c) i.e when distribution is exactly equal i.e. the attributes did not contribute anything.
- **Gini split**: add gini index of each node weighted by records they contain (weighted impurity of all nodes)
- If Gini split almost equal for two options, go for one which has lesser successors. 
- Now, it is ideal to go for binary split
- **Entropy:**
- *Misclassification error* is not good a metric, although has same properties but can have false positives. Misclassification error not a very good representation for the node impurity. 
- Measure impurity before and after split, choose attribute that gives highest gain in the purity measure.
- Gain = Previous purity - Combined purity measure (weighted by number of records)
- These days split are only binary, earlier the concept of smaller number of successors with same gain was introduced.

#### Working with continuous attributes (Computing Gini Index):
- Sort the data records that is continuous
- Choose split values in the middle of data records to create contingency matrix
- Can just shift tables and calculate new tables just by including the change

#### Gain Ratio:
- Gain ratio = Gain_split / split_info (to penalize more number of successors)
- Split info very high if splititng into many successors that are very large 
- Missclassification error not good a metric for impureity measure  

#### Advantages:
- Computationally cheap to construct
- DL and SVM can take a long time, runtime for decision trees is linear once data is sorted
- Very fast inference time
- Can automatically weight that attributes, thus don't need to normalise the data
- Highly interpretable, compared with black box DL models and complicated kernels
- Robust to noise (low variance) - when overfitting is avoided (using random forest)

#### Disadvantages: 
- Does not deal with scnearios of interacting attributes, where multiple attributes come together to separate classes from each other.
