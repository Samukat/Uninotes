Graph representations are way of storing and using [[Graphs]] in code. 

![](https://lh4.googleusercontent.com/dhHEDDHZZAV-Aas_6WnNmwbOcheySau_70JkXiyGbdNaDwdZ2Suu-GZ4HFyF9uEch8-b2FAe7ZS2enhOLEa0WQJCZQZ3yML_Jo67FYL6BUkh5nm-zFtcmDJL4cFkK1iYkYZExiKCrWlv8vIjU0fxMNk)

---

## Array of edges
Stores as an array of E. This is space efficient. 
Adding/deleting/lookup is mildly complex

E.g. `[(1,2), (3,5).....]`
<img src="https://lh5.googleusercontent.com/1CnDtCnib0sHgmiCHApHRyr8bpaOvdJ42O8jyGy-1OdywUgICcB9qmPNKYv7pk-ObHDrSM16h9AngCh0YWiv5I1XgZaPJEdGwPDcdv487LCXlkfmFbMBT880ZpjAX9OscSTqzLoPkjs8VSz779IMgPI" alt="Image" width="400px" />

#### Complexity 
Storage: O(E)
Operations: O(E) 

Time complexity:
    - Initialisation: O(1)
    - Insert edge: O(E)
    - Delete edge:  O(E)
    - Find edge: O(log(E)) (if edges maintained in order)

```c
typedef struct GraphRep {
  Edge *edges; // array of edges
  int nV;      // #vertices (numbered 0..nV-1)
  int nE;      // #edges
  int n;       // size of edge array
} GraphRep;
```

---

## Adjacency Matrix
A 2d representation of all the edges in the graph.
- Easy to implement
- Relatively fast (Insert/del edge: O(1))
- Space inefficient: O(V^2) for [[Graphs#Properties of graphs|sparse graphs]]
	- 0's in matrix aren't useful to store
- For [[Graphs#Terminology|undirected graphs]], the table is a mirror about the diagonal
	- Double up on data storage for no reason.


#### Pseudo code / Structure
```c 
typedef struct GraphRep {
	int **edges;  // adjacency matrix
	int nV;       // #vertices
	int nE;       // #edges
}
```
<p align="center">
<img src="https://lh3.googleusercontent.com/wu_u5a6Xa8cp57wo0abvG0x3HXl3riH5HcipBsn63U2ojkCBVEh7NbLplicaJroz6Bkd47xvVfvZO5v-ikWL-I5utDWEnYM7w6KTEUNE3AHPsgnD5oV6wxEhrZ0_vSfAvhhWKVeRweEqkZHcO1KiwTU" 
	alt="Image" width="400px" />
</p>

#### Complexity
Insert/del edge: O(1)
space inefficient: O(V^2)

---

## Adjacency List
- Every item points to a [[Linked List]]


#### Pseudo code / Structure
```c
typedef struct GraphRep { 
	Node **edges; 
	int nV; 
	int nE; 
} GraphRep; 

typedef struct Node { 
	Vertex v; 
	struct node *next; 
} Node;
```

<p align="center">
<img src="https://lh6.googleusercontent.com/WABBH1T-_vpsMcxPJ-Bij1pelhLe8c9Xd0og0rOk12lA53zcVhTZXXtOedQtGqOc7yo-QALH8kXhuYLMds_YAQ7mRbMnNTcDuUF2W6msI3_HjMvl-v-LuCOwNnCi4sGMhOdmRhRaIU0tXP8VAuSbpD4" alt="Image" width="500px" />
</p>
#### Complexity
Time complexity:
    - Initialisation: O(V)
    - Insert edge: O(1)
    - Delete edge: O(E)