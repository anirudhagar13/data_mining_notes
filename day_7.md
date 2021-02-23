# Classification: Alternative Techniques:
## Rule-based classifier:
- Easy to interpret
- Coverage of rule: Fraction of records that satisfy antecedent of the rule.
- What happens when an instance triggers / satisfies multiple rules:
	- R4: (A=a1) ^ (B=b1)
- What happends when an instance does not trigger any rule:
	- Never faced such situation in decision trees

## Strategy of creating rules:
- Rules should be mutually exclusive (No instance fires more than one rule)
- Rules should be exhaustive (No instance is left out, not being covered by rules)
- Thus, each record is covered by atmost and atleast one rule
	- Decision trees have such values as each record goes to one leaf only
	- Every instance starts at root node (thus, covered by one rule atleast)
- Rule-based paradigm is much more general than decision trees though
- Rules should be more flexible: Not exhaustive and not mutually exclusive

## How to handle triggering multiple rules:
- Define hierarchy for rules (Ordered rule set)
- Use voting schema for unordered rule set (not much used - except for ensemble models)

## Tackle rules not being exhaustive:
- Define a default rule / behavior (Cover everything not covered by other rules)
- Prevents rule-based system to not be very large
- If have imbalanced classes, use larger class as the *default class*.
- For orderd set: `One knowledge is true, only if previous knowledge do not apply.`

## Class-based ordering:
- Build rules for all the classes, thus no ordering required
- Even if multiple rules fired, it would belong to the same class
- Classes are arranged in hierarchy though, and for last class no rules required, as becomes
default class.
- This paradigm works very well for imbalanced class, by creating rules for smaller class first
- Decision trees entropy for minority class is low, hence might get lost, but not here.
- One of the advantages of rule-based system is to **handle imbalanced class dataset**.

## Building classification rules:
- Direct method: RIPPER (extract rules from data)
- Indirect method: Extract rules from other classification techniques like decision trees

## Direct method for building rules:
- Start from empty rule
- Build one condition at a time (like building decision trees)
- Remove training records covered by the rule
- Repeat process until all records covered under the rules
- The above method is also called **Sequential Covering**.

## Rule evaluation
- In general to specific approach (RIPPER method)
- We use *Foil's Information Gain* to add rules one by one
- First build rules for c0 vs rest, then c1 vs rest (thus it works for the case of multiple classes)
- Techniques like pruning, validation set, or MDL used for model pruning and preventing overfitting.

## Advantages / Disadvantages of rules based classifier:
- Performance comparable to decision trees
- Easy to interpret
- Can handle redundant and irrelevant attributes
- Cannot addrees interacting attributes
- Are better suited to tackle imbalanced class problems
- Harder to handle conditions when missing values in test set

# K-Nearest Neighbors
- Also called **Lazy-classifiers**
- Look for nearest labels in training set, look at their class labels
- Use class labels of neighbors as their own class label
- *If walks like a duck, acts like a duck -> then it is a duck*

## Building model:
- Requies a proximity metric / distance / similarity metric
	- One is eucledian distance
	- With documents or market-basket data: Cosine is better than correlation or eucledian
	- Thus, would depend on the usecase
- Requies a labeled data (supervised learning)
- How many neighbors should I look at (*Choose K to be odd to get a majority*)
- How to use labels of neighbors to choose my label:-
	- (*Choose the majority*)
	- Weight the vote (more weight to nearer neighbors = 1/d^2)

## Data preprocessing is required:
- height, weight and income have different ranges
- Need to **normalizing** these variables

## Choosing the value of K:
- K-small: Sensitive to noise (overfitting)
- K-large: Includes neighbors of other classes (underfitting)
- Use validation set to figure out the value of hyperparameter K

## How to handled missing values in training and test sets KNN:
- KNN will breakdown even if values missing in either set
- Using subsset of attributes to compute proximity would be non-comparable, thus would not be valid to be used.

## Irrelevant / redundant attributes in KNN:
- Suceptible to irrelevant attributes
- Gini-index in decision trees handles them properly
- Irrelevant attributes add noise to the proximity measure

## Handling attributes that are interacting:
- It doesn't matter, as it's the job of distance function to find this metric
- The interaction is abstracted within the distance function for KNN

## Drawback of KNN:
- Very slow (Compute similarity with every sample of labeled dataset to assign a label)
