## Classification errors;
- Training errors: errors on train sets
- Test errors: errors on test set
- Generalization errors: errors on random samples from same distribution
- Generalization error becomes high for very complex models
- How complex a decision tree is: How many nodes decision trees have, how many attributes being using to build 
- *Read pruning from the book*
- Trainset: to build models
- Validation set: for configuring parameters, thus it has been used in any aspect of construction of the model (selection of model parameters).
- Thus, model is biased towards validation set, even though it is also unseen data. 
- Thus, we require generalization error on completely unseen data.

## Data parts:
- Train set (building model) | Validation set (for selection of right hyperparams) | Test set to report the model performance as generalization error
- More data there is, more **robustness** the model will achieve.
- Model complexity can be choosen, amount of label dataset cannot be chosen
- Ample amount of data (never the case): no worries
- Small amount of data: difficult scenario

## Working with small dataset:
- Assume we already figured out algo, that tries models of diff. complexities and chooses best among them
- Option1 (**HoldOut**):
	- Split for training and model selection
	- Other split for testing model
	- Random subsampling (try over multiple runs)
	- Not good when data amount is very low
- Option2 (**Cross Validation**):
	- Split data into K parts in each run
	- One split reserved for testing and other splits for training in each run
	- repeat for all runs till test split covers entire dataset.
	- Training set data is itself used for building and model selection
	- Of two types (*K-fold*, *Leave one out*)
	- Better idea to create these folds using stratified sampling, else performance is not as good

# Chapter 4:
- Models built on probabilistic theorum

## Bayesian Classifiers:
- Serves as basis for more complex frameworks
- P(Y|X) = P(Y,X) / P(X)
- Always need to find out P(Y|X1, X2, .... Xd). Can this be estimated from the data?
	- Only possible if there are lot of samples such that all combinations (exponential) are present in the data
- Can be written using Bayes theorum:
	- P(Y|X1, X2, .... Xd) = [ P(X1, X2, .... Xd|Y) * P(Y) ] / P(X1, X2, .... Xd)
	- Bottom does not matter as remains same for all Ys (classes) - Normalization factor
		- Know apriori property of each class - P(Y) 
		- Generative models to create samples of each class - P(X1, X2, .... Xd|Y)
	- Apriori property can be easily estimated from the data given
	- Training samples would never be big enough to completely estimate - P(X1, X2, .... Xd|Y)
		- Thus, we need to assume **conditional independence**
			- P(X|YZ) if X & Y are conditionally independent = P(X|Z)
		- Thus, from above assumption we can write as;
			- P(X1, X2, .... Xd|Yj) = P(X1|Yj)P(X2|Yj)...P(Xd|Yj)...
			- Thus, do not need exponential combinations are now.
			- If conditional independence assumption not correct, this doesnt not stand
			- Here above; Sum of P(X1_values|Yj) = 1

## Advantages of Naive Bayes:
- If no attributes available, still have priori of classes
- Bayesian frameworks shine best in the absence of information around instances

## Demerits of Naive Bayes classifier:
- Assumption of the independence of the class attributes
- P(Xn|Y1) = 0 makes contribution from all other attributes = 0 (loss of information)
- Sometimes even P(X|Y1) & P(X|Y2) both can be zero; can be prevented by not letting probability to become zero (by adding epsilon - a very small number)

### Another solution for Naive Bayes zero issue:
- original: P(Xi | y) = n_c / n
- Issues happends when n_c = 0 (for any class)
- If n_c becomes zero for both conflicting classes - Breaks Naive bayes ability to make a decision
- **Laplace estimate** and **m-estimate** are solutions to the above problem.
