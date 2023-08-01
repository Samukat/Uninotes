# Hashing
Hashing is the process of transforming any given key or a string of characters into another value.
Key Space: The max amount of key-value pairs

### Issues:
- Collisions 
- Can't expand array - this is due to the has function relying on the size of the array in mod.
- Items are stored in *effectively* random order

---

## Ordered & Associative containers
**Ordered Containers**:
- have order between elements, and (typically) each element has a meaningful *index* that denotes that order
- e.g. Linked list, array, trees

**Associative containers**:
- Map "keys" to various values, and items in associative containers have no sense of order.
- *Keys* are usually strings

---

## Hashing Process
We will make a hashing function that allows us to run code like the following:
```c
dict[h('key')] = 'value'
```
Where $h$ converts our string to a number.

To use arbitrary values as keys:
- set of Key (strings) values, each key identifies one Item 
- an array (of size N) to store Items 
- A hash function $h()$
	- Requirement: if (x == y) then h(x) == h(y)
	- requirement: h(x) always returns same value for given x
- Issue: if amount of keys > N then there will most likely be double ups. This also mean that there can be doubles sometimes.

---

## Hash Collisions
Approaches:
- Chaining:
	allows $\alpha > 1$, easy to implement
- Linear probing:
	Fast if $\alpha \ll 1$, complex deletion
- Double hashing:
	Faster then linear probing, esp for $\alpha \cong 1$


### Separate Chaining:
Solves collisions by allowing multiple items per array entry. All items with the same hash() value get added to [[Linked List]] style structure. 
This is the only way to deal with M > N

##### Cost
This could remove efficiency as linked list is O(n). Could reduce hash map to O(n). 

Load a = M/N (N is slots, M is items)
- Average list length: L = M/N (N is slots, M is items)
- Best is all same L
- Worst is all same slot, 1 list of M
- If good hash (Best L), Complexity = O(M/N/2) <- average case


### Linear Probing
In linear probing, the hash table is searched sequentially that starts from the original location of the hash. If in case the location that we get is already occupied, then we check for the next location.

As Load a (Load a = M/N) approaches 1, performance gets worse

**Deleting**:
Cant have nulls, therefore, when removing:
Remove all following values then re-add values


#### Double Hashing
**h(key, i) = (firstHashfunction(key) + i * secondHashFunction(key)) % tableSize**.
increases the amounts of nulls between hash(key) duplicates --> improves performance 



---

## Hash Functions

The hash function is as follows;
```c
int hash(Key key, int N) {
   int val = convert key to 32-bit int;
   return val % N;
}
```
> Clearly collisions can happen as N will (almost always) be less then the domain space

#### Example hash function
```c	
int hash(char *key, int N) {
	int h = 0, a = 31415, b = 21783;
	char *c;
	for (c = key; *c != '\0'; c++) {
	    a = a*b % (N-1);
	    h = (a * h + *c) % N;
	}
	return h;
}
```



