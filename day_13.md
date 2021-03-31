## Pattern Evaluation:
- Association rule mining  can create a lot of rules
- Can measure *Interestingness* of rules through certain metrics
- Such measures can then be used to rank/prune the rules

## Computing Interestingness:
- Can convert market basket data of two variables into a contingency matrix
- f_11, f_00, f_10, f_01 (only f_11 needs to be computed directly)
- Rest three can be computed from supp(X), supp(Y) and N (Total transactions)
- Tea -> Coffee rule is P(Coffee|Tea); association rules only considers presence of items
- Thus, cannot use *confidence* directly to assess the Interestingness of a rule
- As per Larry page and Sergey Brin's paper: Confidence is a bad metric to rate association rule using an example of Tea and Coffee.
- Confidence(X|Y) should be high but it should be > Support(Y) to make sense
- Confidence by itself is not a good measure from the above discussion

## Criterion:
- Confidence(X->Y) = Support(Y)
	- P(Y|X) = P(Y) means X, Y are independent
	- Thus, P(X,Y) > P(X) x P(Y) means +ve correlation
	- P(X,Y) < P(X) x P(Y) means -ve correlation
	- This is directional i.e. P(X->Y) != P(Y->X)
- Interest: P(X,Y)/P(X)P(Y)
	- =1 means independence
	- >1 means +ve correlation
	- <1 means -ve correlation
	- This is non-directional
- No measure is better than the other (Interest widely disagrees with correlation)

## Which measure to use given the dataset?
- Depends on the property of dataset

### Inversion:
- Also depends on representation (1 - presence in market basket data, 
for comparing students answers True/False 1,0 does not matter so inversion doesn't matter)
- Correlation is inversion invariant (not useful if 1s and 0s have difference significance like the market basket dataset)
- Cosine/IS is inversion variant (changes if 1s and 0s are inverted)
	- This would not work if 1s and 0s inversion is fine like the students answers

### Null addition:
- Transaction which don't have A or B
- Cosine, Jaccard, Confidence are invariant to this
- Correlation, Interest/Lift, Odds ratio are variant to this

### Scaling:
- If sample-size is increased for each category separately, the metric should not change
- Only odds-ratio has this property i.e. invariant to changing ratios between categories
- odds ratio: a * d/b * c if a|b//d|c is the contingency matrix

## Simpson's paradox:
- On different strata of the population A better than B, but overall B is better than A
- This is called *compounding factor*, truth might be occluded by smaller details
- Compounding factor can lead to wrong information

## Skewed distribution:
- Many datasets have skewed distributions for support (very frequent items like bread vs very infrequent items like shoelace)
- Few items with high support / Many items with low support
- High support threshold: eliminates most of the items
- Low support threshold: includes a lot of items, choking the system
	- Would lead to low-frequent items being co-occur with high-frequent items e.g. (cavear, milk)
- Cross-support is used to tackle this problem
