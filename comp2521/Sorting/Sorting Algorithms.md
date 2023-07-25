# Summary

|                | # compares |     |     | # swaps |     |     | # moves |     |     |
|----------------|-----------|-----|-----|--------|-----|-----|--------|-----|-----|
|                | min       | avg | max | min    | avg | max | min    | avg | max |
| Bubble Sort    | n         | n^2 | n^2 | n      | n   | n   | .      | .   | .   |
| Selection Sort | n^2       | n^2 | n^2 | n      | n   | n   | .      | .   | .   |
| Insertion Sort | n         | n^2 | n^2 | .      | .   | .   | n      | n^2 | n^2 |

# Bubble Sort
Moves through list pair-wise, swapping pairs in the wrong order. Repeats until list is sorted

<p align="center"> <img src='https://miro.medium.com/v2/resize:fit:1400/1*-qR66X2iwdcjhaqq10y9JQ.gif' width=400px> </p>

### Time complexity
- Worst case: O(n^2)
- Average case: O(n^2)
- Best case: O(n)
- [[Sorting#Adaptive sort|Adaptive sort]]: yes


### Code
```c
void bubbleSort(int a[], int lo, int hi) {
	int i, j, nswaps;
	for (i = lo; i < hi; i++) {
		nswaps = 0;
		for (j = hi; j > i; j--) {
			if (less(a[j], a[j-1])) {
				swap(a[j], a[j-1]);
				nswaps++;
			}
		}
		if (nswaps ==0) break;
	}
}
```

---

# Selection Sort
Selection sort finds smallest number through an iteration/move through and then moves it to the start

<p align="center"> <img src='https://www.codingconnect.net/wp-content/uploads/2016/09/Selection-Sort.gif' width=400px> </p>

### Time complexity
- Worst case: O(n^2)
- Average case: O(n^2)
- Best case: O(n^2)
- [[Sorting#Adaptive sort|Adaptive sort]]: No (best and worst case is the same)

### Code
```c
void selectionSort(int a[], int lo, int hi) {
	int i, j, min;
	for (i=lo; i < hi-1; i++) {
		min = i;
		for (j = i+1; j <= hi; j++) {
			if (less(a[j], a[min])) min = j;
		}
		swap(a[i], a[min]);
	}
}
```

---

# Insertion Sort
Takes the first element and assume that it is sorted; Take next item and insert into sorted section of array. Repeat until whole array is sorted

> If the array is very close to sorted then this is a very good choice; (not many swaps and is [[Sorting#Adaptive sort|Adaptive]] )
<p align="center"> <img src='https://i.pinimg.com/originals/92/b0/34/92b034385c440e08bc8551c97df0a2e3.gif' width=400px> </p>

### Time complexity
- Worst case: O(n^2)
- Average case: O(n^2)
- Best case: O(n)
- [[Sorting#Adaptive sort|Adaptive sort]]: yes

### Code
```c
void insertionSort(int a[], int lo, int hi) {
	int i, j, val;
	for (i = lo+1; i <= hi; i++) {
		val = a[i];
		for (j = i; j > lo; j--) {
			if (!less(val, a[j-1])) break;
			a[j] = a[j-1];
		}
		a[j] = val;
	}
}
```

--- 

# Merge Sort
The approach is recursive!
This sort also requires malloc-ing memory.

**Merge Sort Overview**
1. Split array into roughly two equal sized partitions *O(1)*
2. Recursively sort each of the partitions *O(log(n))*
3. Merge the two partitions into a new sorted array *O(n*log(n))*
This will take O(log(n)) time; as splitting in two


<p align="center"> 
<img src='https://upload.wikimedia.org/wikipedia/commons/thumb/c/cc/Merge-sort-example-300px.gif/220px-Merge-sort-example-300px.gif' width=300px>
<img src='https://www.programiz.com/sites/tutorial2program/files/merge-sort-example_0.png' width=300px> </p>

**Merging**
When combining two sorted arrays it is not O(n^2) (unlike unsorted), but O(N)
<p align="center"> <img src='https://i0.wp.com/blog.shahadmahmud.com/wp-content/uploads/2020/04/ms2.gif?resize=960%2C540&ssl=1' width=300px> </p>
When merging the split/divided array, the total time will be $$O(\log(n)) \times O(n) = O(n \log(n))$$
### Time complexity
- Best case: O(n*log(n))
- Average case: O(n*log(n))
- Worst case: O(n*log(n))
- [[Sorting#Adaptive sort|Adaptive sort]]: no

### Code 
```c
void mergesort(Item a[], int lo, int hi) {
	int mid = (lo + hi)/2;
	if (hi <= lo) return;
	mergesort(a, lo, mid);
	mergesort(a, mid+1, hi);
	merge(a, lo, mid, hi);
}
```

```c
void merge(Item a[], int lo, int mid, int hi) {
	int  i, j, k, nitems = hi - lo + 1;
	Item *tmp = malloc(nitems * sizeof(Item));
	
	i = lo; j = mid + 1; k = 0;
	// scan both segments, copying to tmp
	while (i <= mid && j <= hi) {
	    if (leq(a[i], a[j]))
	        tmp[k++] = a[i++];
	else
		tmp[k++] = a[j++];
	}
	
	// copy items from unfinished segment
	while (i <= mid) tmp[k++] = a[i++];
	while (j <= hi) tmp[k++] = a[j++];
	
	//copy tmp back to main array
	for (i = lo, k = 0; i <= hi; i++, k++)
	    a[i] = tmp[k];
	free(tmp);
}
```

---

# Quick Sort
This can be done recursively or with a stack.
Doesn't use as much memory (depending on implementation) as [[Sorting Algorithms#Merge Sort|Merge Sort]].
May not be [[Sorting#Stable sort|stable]], depending on implementation.

**Quick Sort Overview**
1. choose an item to be a 'pivot'
2. Re-arrange (partition) such that:
	1. All elements to the left of pivot are smaller then pivot
	2. All right are greater
3. (Recursively) sort each partition

|lo|i $\rightarrow$ |Unsorted < x| $x_{i}$ |Unsorted > x|$\leftarrow$ j|hi|
|-|-|-|-|-|-|-|

<p align="center"> 
<img src='https://upload.wikimedia.org/wikipedia/commons/9/9c/Quicksort-example.gif' width=300px>
<img src='https://lh3.googleusercontent.com/v2NFOwR9oxiuJhzL12LvC4Bii2mUmil-I1CL-uxyralpQ7PPBn7rb391CwktTSkWYr-IzJHKad6TObd3P43a1IB8yxS9eFO3i6bMQ6o2TJ-2gVFa-m31rWiiz2Pd1PvgEu7-7yM4_B2XZJ0KlQIDEQ8' width=300px> </p>


### Time complexity
- Best case: O(n*log(n)) 
	- Quicksort calls = O(log(n))
	- Partitioning = O(n)
- Worst case: O(n^2)
	- If pivot is chosen badly, i.e Quicksort calls = O(n)

#### Median of three improvement
Pick 3 numbers, then choose the median of the 3.
Good choices are *lo, med, hi*.



### Code
```c
void quicksort(Item a[], int lo, int hi) {
	if (hi <= lo) return;
	int i = partition(a, lo, hi);
	quicksort(a, lo, i-1);
	quicksort(a, i+1, hi);
}
 
int partition(Item a[], int lo, int hi) {
	Item v = a[lo];  // pivot
	int  i = lo+1, j = hi;
	for (;;) { //essentailly a while true
	    while (less(a[i],v) && i < j) i++;
	    while (less(v,a[j]) && j > i) j--;
	    if (i == j) break;
		swap(a,i,j);
	}
	j = less(a[i],v) ? i : i-1;
	swap(a,lo,j);
	return j;
}
```
