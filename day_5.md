# Decision Trees Continued

## Advantages:
- Relatively cheap to construct
- Very fast inferencing time
- Can easily handle irrelevant and redundant attributes
- Robust to noise
- Interpretable
- Can handle any kind of attributes (Gini-Index can be calculated for any kind)
- Even scale of attributes can be different (Gini-index calculation is scale invariant)

## Handling interactions between attributes in a Decision tree:
- Exclusive OR problem - Cannot be handled by 1st gen Neural networks 
- Just one cut in above problem (using one attribute for separation), would lead to equal distribution of classes (Gini-index = highest and Entropy = appx. 1)
- Z as uniform noise: no matter where cut along z-axis, distribution remains same
	- When using such variables for cut initially, information is lost as lesser variables in successor
	- Thus, cutting on noise variables initially leads to bad performance as lesser information remains as we go down

- Cuts in decision trees are only vertical or horizontal (no diagonals possible): *Downside of single attribute based decision boundary*

## Overfitting in Decision Trees:
- Objective in classification setting: Training set -> Using learning algo to Learn model -> Apply model for deduction -> predict on test set
- Labelled data is the training set
- During training, can only see errors on labelled data, but objective is to get low error on data not seen by the model.
- *Test error* is an approximation of *Generalization error*.
- Test error obtained by hiding a portion of labelled dataset to get test error, which would an estimate of the generalization error.
- As number of nodes increases, train error decreases drastically
- **Overfitting**: Training error small, testing error large
- **Underfitting**: Training error & Test error are large
- Bigger training set, effects of overfitting are less (i.e. Less diff in training and test error of overfitted models)
- More choices of attributes: More probability of being correct
- More data samples: less likely to fake being a good model by accident or randomness

## Conclusion:
- Overfitting is when creating more complex decision tree than required
- Training error cannot give any way a good estimation of generalization error
- We need ways to estimate generalization error, to see if model is overfitting or not

## Model selection:
- As model complexity increases, the training error would keep on going down, but as some point the generalization error will start increasing (point where model becomes overfit)
- No way of identifying this point, unless we estimate generalization error thorugh test error

## Incorporate model complexity inside training process to estimate generalization error:
- Generalization error = Training error + (alpha * Model_complexity)
- Intuition as more complex model give higher generalization error
- Puts a check on model becoming too complex

## Estimating complexity of decision trees (Pessimistic Error Estimate):
- err_gen(T) = err(T) + omega * (num of leaves [k]) / N_train (total number of training records)
- Would prevent tree from getting too big
- If omega=0, would keep building tree bigger and bigger till err(T) = 0
- omega figured out using validation set 
- **Resubstitution estimate (Optimistic error estimate)**; when training error used as estimate for generalization error i.e. omega=0

## Notion of model complexity
- Using number of leaves as measure of model complexity in decision trees is very adhoc
- A more universal and systematic way is using Minimum Description Length (MDL)
- Sending model to recreate targets at the other side of the tree
- Cost(Model, Data) = Cost(Data | Model) + alpha * Cost(Model)
