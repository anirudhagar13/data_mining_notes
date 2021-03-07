## Rule Generation:
- Find frequent itemsets using support threshold
- Then find all rules that could formed from such frequent item set
- Each rule would have some confidence, choosing the ones with **high confidence**.
- For itemset = k; candidate rules = 2^k - 2
- Confidence does not have **anti-monotone** property in comparing different frequent itemsets(as we cannot tell what would happen to the ratio)
- But for same confidence of rules generated from same itemset (same numerator), we can find anti-monotone property in confidence.
- In lattice graph of confidence, if any node confidence is below threshold; prune all it's children (Apriori Algorithm).
- Sometimes frequent itemsets by themselves are useful and not required to generate any inference rules.

## Algorithms and Complexity of Association analysis:
- Factors affecting complexity of Apriori:
	- Choice of support threshold (Increasing threshold would make the complexity go down)
	- Finding all itemsets at the base are always exponential - Dimensionality (number of items) of dataset 
		- Most space required in memory and disk, for more items
		- run time increases exponentially
	- Number of transactions (Size of the database) 
		- run time increases linearly
	- Average transaction width 
		- average number of items in the transaction
		- puts limit on length of the frequent item sets
		- can exponentially increase runtime
		- width of transaction << total no of items - then only matrix is sparse and support based pruning works effectively
			- Does not satisfy in use cases such as Gene-expression - but people have figured out association framework for such use cases

## Compact representation of frequent itemsets:
- *Maximal Frequent itemset:* an itemset is maximal frequent if it is frequent and none of it's immediate supersets are frequent
- Using maximal frequent itemsets, we can generate all frequent itemsets as it's possible subsets
	- e.g. If E, F, and {E, F} are frequent, then maximal frequent itemset would be {E,F} as frequent itemsets can be derived from this maximal frequent itemset
- Some algorithms try to directly find the maximal itemsets - helps in datasets that are not very sparse

## Closed Itemset:
- Build compact representation of dataset in such a way; without having the notion of support threshold
- Closed itemset is an itemset for which none of it's immediate supersets have the same support as the itemset itself.
- In a dataset with items {A, B, C, D}, considering itemset {B, D}, it's immediate supersets are {A, B, D} & {B, C, D}. 
- If both of these have support < {B, D}, then only {B, D} is closed itemset. If even one has equal support, then {B, D} would not be a closed itemset. 
- Anyways, the apriori would prevent supersets to have support > support of subsets
- Using closed itemsets, we can find support of any other itemsets very fastly.
- If an itemset is maximal, it is automatically closed itemset also. 
- In datasets that seem to have blocks (subsets) - then closed itemset really helps a lot
- Then only need to visit transactions of closed itemset

## Maximal vs Closed Itemsets
- Closed Itemset < 2^d (If data has lot of blocks / structure into it)
	- Out of above some are frequent itemsets: depends on support threshold
- Out of the Frequent itemsets, some of them would be maximal and those would be closed as well
- The amount of frequent itemsets changes with change in support threshold, but amount of closed itemsets remains same and depends on structure of data.  






