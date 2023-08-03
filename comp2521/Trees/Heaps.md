# Heaps
Heaps are not related to memory-heaps.
Heaps are [[Tree]] like structures, similar to [[Binary Search Trees]].
They are very useful for [[Priority Queue]].

### Properties
Heaps are not trees, but can be conceptually considered as a dense tree where:
- Tree maintains order with higher elements at top
- Items on right are larger, Items on left are smaller (not all the time)
- Adding item starts up lower-most, right-most leaf, which then move up
- items are always deleted by removing root (top priority)
- Since heaps are dense trees, depth = floor(log(2N)) + 1

Often implemented using arrays where index 0 is empty, and elements begin at index 1
    - Left child of item at index i is located at 2i
    - Right child of item at index i is located at 2i+1
    - Parent of item at index i is located at i/2

> note: index 0 is empty to ensure that the math still works (i.e. otherwise `2*0 = 0`)


### Inserting 
This is a O(log(n)) operation.
1. Add new element at next available position (bottom row)
	- This may break heap rule - Larger items are at top
2. Reorganise elements along path to root by value to restore heap order
	- Swap with value higher, until It is smaller then above

see [[Heaps#Code#Inserting]]

### Deleting 
This is a O(log(n)) operation.
1. Replace root element by bottom right element
2. Remove bottom right element
3. Reorganise elements along path from root to restore heap order
<p align="center"> <img src='https://lh4.googleusercontent.com/drCrkgnpT8JUlHeGXsbKXy32K1Q7ljDgwKAQlKFqSySi24LI-vdcm7dMWCneEHocP-e0WsXKZ9NZmrVI-mDEjaDa-0EHP99nSxGujCjCJnRBXLEXVF3rRLsKznM1bHfMKOIUzJ5DksA6gqA9lmz0JZc' width=400px> </p>
see [[Heaps#Code#Deleting]]

### Example
Heap tree:
<p align="center"> <img src='https://lh5.googleusercontent.com/0u62gjZ5UU7dM5_ZVe-WF-nmZ9HXZ0Mdh582k9hj6aRJItrt7UPlyvg9oIFa3p3AHLVedaIvvN1v91ksx40-wFsB3YptkEr3tbI-nVpS70FcwUVhUzcMuoVSsHyJDfYMI1-_JBBoT3_oBCIF-VD15tI' width=400px> </p>
The array for this tree would be:

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|----|
|   | z | t | s | d | k | m | j | a | b | h  |
Therefore: 
- left item of $t$ = $[2*2]$ = $[4]$ = $d$
- Right item of $t$ = $[2*2 + 1]$ = $[5]$ = $k$
- parent item of $k$ = $[5/2]$ = $[2]$ = $t$


### Code 
#### Structure
```c
typedef struct HeapRep {
	Item *items;  // array of Items
	int  nitems;  // #items in array
	int  nslots;  // #elements in array
} HeapRep;

typedef HeapRep *Heap;

Heap newHeap(int N) {
	Heap new = malloc(sizeof(HeapRep));
	Item *a = malloc((N+1)*sizeof(Item));
	assert(new != NULL && a != NULL);
	new->items = a;   // no initialisation needed
	new->nitems = 0;  // counter and index
	new->nslots = N;  // index range 1..N
	return new;
}
```

#### Inserting 
```c	
void HeapInsert(Heap h, Item it) {
	// is there space in the array?
	assert(h->nitems < h->nslots);
	h->nitems++;
	// add new item at end of array
	h->items[h->nitems] = it;
	// move new item to its correct place
	fixUp(h->items, h->nitems);
}
 
// force value at a[i] into correct position
void fixUp(Item a[], int i) {
	while (i > 1 && less(a[i/2], a[i])) {
		swap(a, i, i/2);
	    i = i / 2;  // integer division
	}
}

void swap(Item a[], int i, int j) {
	Item tmp = a[i];
	a[i] = a[j];
	a[j] = tmp;
}
```

#### Deleting
```c
Item HeapDelete(Heap h) {
	Item top = h->items[1];
	// overwrite first by last
	h->items[1] = h->items[h->nitems];
	h->nitems--;
	// move new root to correct position
	fixDown(h->items, 1, h->nitems);
	return top;
}
 
// force value at a[i] into correct position
// note that N gives max index *and* # items
void fixDown(Item a[], int i, int N) {
	while (2 * i <= N) {
	    // compute address of left child
	    int j = 2 * i;
	    // choose larger of two children
	    if (j < N && less(a[j], a[j+1])) j++;
	    if (!less(a[i], a[j])) break;
	    swap(a, i, j);
	    // move one level down the heap
	    i = j;
   }
}
```


### Heap Sort
Create and add all elements to the heap;
Take all elements out.

This is O(n*log(n))