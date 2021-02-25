# Basic Association Analysis:
- Classification / Supervised learning - covered in pattern recognition, stats, ml classes
- association analysis is exclusive to data mining class - Unsupervised learning
- Given a set of transactions, find rules that predict occurrence of one object given another object
- Dataset is of type **Market-basket** data, but association rules do apply to other datasets
- Association rules imply *co-occurrence* and not *causality*

## Market-Basket dataset:
- Consists of asymmetric binary variable (does not consider absence of an item while calculating similarity)
- 1 (presence) is more important than the 0 (absence)
- Beer & Diaper story: By people heading home in the evening
- Some patterns are intuitive, while others require data analysis
- Utilities, can have discount on one and premium surcharges on the other

## Definitions:
- *Frequent Itemset:* Collection of more than one items (k-itemset has k items in it)
- *Support Count:* Frequency of occurrence of an itemset
- *Support:* Fraction of transactions that contains the itemset
- *Frequent Itemset:* Itemsets with support above *minsup* threshold
- *Association Rule:* X->Y (X implies Y) [never have same items on both sides]
- *Support for rule:* Fraction of transactions that contains both X & Y
- *Confidence for rule:* How often items in Y appear in transaction that contain X i.e. 
	[sup(X & Y) / sup(X)]

## Goal:
- Given a set of Transactions, find all association rules that have:
	- support > minsup | confidence > minconf
- Brute Force approach is **Computationally prohibitive**
- This is an exponential space for rules

## Mining association rules
- Separate support and confidence calculations (as rules from same itemset would have same support but different confidence)
- Two set approach:
	- Getting frequent itemsets
		- 2^d possible itemsets (all possible subsets)
	- Generating high confidence rules from frequent itemset

## Brute Force:
- Each itemset in the transactions is a *candidate* for frequent itemset
- Complexity to calculate support is O(NMw) [N: Transaction, M: Candidate itemsets, w: width of itemsets]
- Optimizations on every front

## Reduce the number of candidates:
- **Apriori** principle to reduce the exponential itemsets: states that if an itemset is frequent, then it's subsets are also frequent
- This is called *anti-monotone* property of support
- Thus, can prune supersets using Apriori

## Apriori principle:
- Don't have to look at supersets (don't have to next layer of lattice if subset support is not above threshold)

## Apriori Algorithm:
- Read from slides

## Candidate generation methods (Read from elsewhere):
- F_{k-1} x F_{k-1} method
- Alternate F_{k-1} x F_{k-1} method



