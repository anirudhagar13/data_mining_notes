# Alternative measures:
- TPR/FPR can help not get fooled by a random classifier, when using other measures
- Given a classifier, it would have certain TPR and FPR
- Any Classifier could be made stricter in calling something positive, making FPR go down
- ROC curve can be constructed by defining looser and tigher thresholds for positivity by a classifier
- AUROC curve is **class imbalance invariant**, as only looking at success of positives and success of negatives separately, so only bothered by rates
- AUROC is a single metric, not necessarily the perfect metric
- As most of the time not using a range of classifier but only one instance of classifier

## Which classifier is better on ROC curve:
- In case if c2 better c1 in both TPR and FPR, then c2 >> c1
- But in real-life there would be variable costs associated with c2 and c1, thus it would also matter when deciding which model to deploy
- ROC curve can only be plotted for classifiers that outputs continuous valued outputs
- It might happen that ROC curves of two classifiers might cross each other, making each one better at certain regions

## Dealing with imbalanced classes - summary:
- *Depends on the context*
- None of the measures are perfect, depends on the situation
- Random classifiers can prove many of the methods wrong (for TPR and FPR would always be = 1)
- Given two classifiers, we can tell one thing for sure;
	- C1 has better TPR and FPR than C2, C1 is >> definetly better than C2 (provided they are measured on same dataset)
	- In other cases, either of the classifiers can be better, as would depend on imbalance in the samples
- F-scores should not be to compare two classifiers on two data sets with diff. class skew
- Cost/time tradeoff also plays a role in deciding which classifier is better
- Skew in dataset does not affect: **TPR**, **FPR** & **their ratio**. They remain same for each classifier. 
- Cannot just purely judge on basis of **TPR**, **FPR** (even though they are inaffected by skew), as large imbalance in dataset can also make small diff. in these measures look really bad (e.g. for a case of 100+ves and 100000-ves ground truth, a 0.1 diff in FPR would make a big diff.)

## Proper steps taken to make sure classification is accurate:
- Modify distribution such that **rare class is well-represented**
	- One way is to oversample rare classes and undersample majority class
- *KNN*, with right choice of K would also work well for case of imbalanced classes


# SVM:
- In middle of 90s, based on optimization framework
- They ruled till the advent of deep learning
- Current is third wave of neural networks (first were in 60s, second gen in 84 two layered)
- Similarly, there are different generations of SVM

## Simplest SVM:
- Linear hyperplane in a 2d space, plane in 3d, hyperplane in more (neural networks did this 1st through perceptrons)
- Earlier neural networks would have create anyone of multiple possible classifiers (planes)
- Even though there are many separators, one of them must be better than the others
- SVM Quantifies how one separator is better than the other, **by the margin**
- Widest the margin, better the model (model is not getting more complex, model is getting more tuned)

## Optimization I:
- Constrained optimization: Solved using laplace multiplier method:
	- i) Max the margin ii) Maintain constrains of f(x) = {1; wx + b > 1 && -1; wx + b < -1}
- Simplest solution as most problems are not linearly separable

## Optimization II:
- Adding penality for outliers
- Introduction of slack variables in the loss function; variables that are not on right side of boundary
- This brought in the concept of *regularization* in optimization
- L(w) = Margin + c * slack_variables (trade off is possible)
- Here, SVM reaches same power as logistic regression

## Optimization III (Non-linear SVM):
- Revolutionized SVM and made them relevant for many many years
- For cases where data point is not linearly separable
- Transforming features in a certain way can make them separable
- How to know which dimensional space to transform to:
	- Try all feature combinations and hope one of them would work well (But that can be very expensive)

#### Using mapping function (kernels)
- A function can be used to map data into different dimensions
- The optimization problem now becomes dual; computing parametrized function to convert to high dimension space

#### Kernel trick:
- Fixed functions that can be used to mapping in different dimensions:
	- Polynomial Kernel (xy + 1)^p
	- Radial Kernel
	- TanH based kernel
- Don't have to know mapping function
- Not all functions can be kernel

### SVM Summary:
- The learning problem here is convex optimization problem
- Greedy search by decision trees, local minima obtained by 
- Highly robust to noise (Like Decision trees and Naive bayes)
- Can handle redundant and irrelevant attributes very well
- Avoid overfitting by the use of margins
- User does need to provide kernel functions and cost functions - This is why 3rd gen of DL better
- Standard kernel function don't work well in many cases - 3rd gen NN learn these kernels
- Unable to handle missing values as require dimensions to construct hyperplanes
- Ordinal variables - SVM are affected with conversion, Decision Trees are not

# Ensemble methods
- Construct a collection of classifiers; final prediction made by combining results of all classifier

## Intuition:
- If all classifiers are independent (errors made by each are uncorrelated); ensemble error rate would be much less
- They work best with *unstable classifiers* (having high variance)

## How to construct ensemble methods:
- Manipulating traning set; selecting samples for each classifier
- Manipualting input features; randomly selected features for each level of random forest trees
- Manipulating class labels
- Manipualting learning algorithm; initializing diff. weights for the same model
