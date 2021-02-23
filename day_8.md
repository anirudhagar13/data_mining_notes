# Classification: Alternative Techniques:

## Imbalanced Class problem:
- Distribution of classes in training samples is skewed
- e.g.: Credit card fradulent transactions are outliers, Intrusion detection happens very rarely over the intern

## Confusion Matrix:
- Actual class vs Predicted class
-    (Predicted)
|--------------------|
|	  | Yes   |  No  |
|--------------------|
| Yes |	 TP   |  FN  |   (Actual)
|--------------------|
| No  |  FP   |  TN  |
|--------------------|

- Accuracy: (TP + TN) / ALL
- Error Rate: (FP + FN) / ALL

## Issues with accuracy:
- Accuracy for imbalanced class would be good (although would not be true)
- A model just predicting all towards the most popular class would give good accuracy, but would be wrong

## Alternative measures (Used in IR)
- [TP: a, FN: b, FP: c, TN: d]
- Precision: a / (a+c) : [Of the documents that came back, how many were relevant. **How precise was the retrieval**]
- Recall: a / (a+b) : [How many of relevant documents were returned]
- Since both have to be good, still average of both would not work
- Getting either of them to be high is easy
- F-1: 2pr/(p + r) [Deviates towards the smaller one]
- Focus always on one class (smaller class usually) and it's presence gives Precision, Recall, F-1
- In multi-class scenario, it is one vs all
- F-1 works much better than in case of class imbalance
- F-1 cannot make any statements about it

## How to compare classifiers:
- Higher F-measure is better, but **context is required as data can be skewed**
- To use F-measure to compare two classifiers make sure: **skew of classes in both cases is same**
- A classifier once built and finalised, 
- Recall: what fraction of positive class would be catched by the classifier
- False positive rate: How many times does the classifier makes mistakes in picking as positives

## Metrics:
- Precision: Also called *Positive predictive value*
- Recall: Also called *Senstivity* or *TP rate*
- Specificity: *TN rate* i.e. TN / TN + FP
- FP Rate = 1 - specificity
- FN Rate = 1 - senstivity
- Most two important metrics are: TPR should be high, FPR should be low
- TPR / FPR can help detect a better classifier, even in face of skew
- TPR / FPR = 1 would mean random classifier
- F-1 measure is *garbage* and cannot tell anything 

## Not having black-white classifiers:
- Instead generate probabilities for classes

## ROC:
- *Receiver Operating Characteristic*
- Plots TPR vs FPR
- Diagonal classifier in ROC has same TPR / FPR, thus it is random
- A random classifier can have any value for TPR / FPR and lie on diagonal
- Ideally, we want Y-axis in ROC curve as ideal classifier (1: TPR; 0: FPR)
- For a good classifier, should be above blue diagonal line in ROC curve
- AUROC for random = 0.5 and for perfect classifier = 1 (for good classifier should be close to 1)

## Convert the classifier:
- Output Continious values outputs
- We have fraction of classes at nodes
- Define threshold on leaves such that the AUROC for decision trees is higher
