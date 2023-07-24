# Summary

**![](https://lh3.googleusercontent.com/D8csDeu74cGyVDn7P1Eveo2uqrA1T1u9zzd4Kdadd5A0jiT9hNvLE8BtvQBrB5Jp0-C_1nl0lBq5QUvA3oCm3lCmCsSuOfRjtUAH0dHH7dnVuaTT9-NocbKLRfk1xOrlEBA7AI5fcpOSe7iEd9n28Co)**


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


# Merge Sort
The approach is recursive!

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
- Worst case: O(n*log(n))
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