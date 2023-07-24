# Sorting

Can be applied to collections of items that are sortable.

**Reasons**
- Helps with speed for searching 
- Help arranging data


## The sorting problem
Arrange items in array slice `a[lo..hi]` into sorted order, where:

**Pre-conditions:**
- lo, hi are valid indexes (i.e. 0 <= lo < hi <= N-1)
- `a[lo..hi]` contains defined values of type *Item*
**Post-conditions:**
- `a[lo..hi]` contains the same set of values as before the sort
- for each **i** in lo..hi-1, `a[i] `$\le$`a[i+1]`

Each *item* contains a *key*, which determines the order of the sort.


## Properties
#### Stable sort
Maintains order for duplicates,
- given that x == y, if **x** precedes[^1] **y** in unsorted, then it will precede in sorted list

#### Adaptive sort
Performance is affected by actual values of items
- Best, average and worse case performance differs  
- E.g. [[Sorting Algorithms#Bubble Sort|Bubble Sort]]


## Sorting Complexity
Mainly, for sorting we focus on:
- Random order
- Sorted order
- Reverse order

Trying to optimise:
- Amount of comparisons
- Number of swaps




[^1]: The item is earlier in the array