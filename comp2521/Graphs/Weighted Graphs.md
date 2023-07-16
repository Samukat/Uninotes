## Directed Graphs (Digraphs)
A [[Graphs|graph]] where where edges have a sense of direction such that: $$v \rightarrow w \ne w \rightarrow v \text{.}$$
<img src="https://i.imgur.com/JWL96oK.png" width=300px>

#### Digraph Properties
- Directed path, Directed cycle ([[Graphs#Terminology|see]])
- **Degree** of a vertex:
	- Outdegree: deg(v) = number of edges of (v, `_`)
	- Indegree: deg<sup>-1</sup>(v) = number of edges of (`_`,v)
- **Reachability**: w is reachable from v with directed oath
- **Strong connectivity**: Same as [[Graphs#Terminology|connectivity]] but with direction
- **Directed acyclic graph**: contains no directed cycles

#### Representation
Very similar to [[Graph Representation]] of undirected graphs ![](https://lh4.googleusercontent.com/39Kfc32nVwDIUuxKsH_RfDcvE5SvivdDvBPRlBtCrt8sWnny0rCrS3y0wwjdpoWNH5w8dxyJZx8wiseM0EEibaGAFHGLGU_CmfWsW__yj4lCCEtf3KbeSKfPpKZo0DBuSEtNrUfhDwr6clXtYuouM-A)
> adjacency Matrix now has other half used


#### Traversing
The same as [[Graph traversal]].

--- 

## Weighted Graph
Weighted [[Graphs|graphs]] are similar, however, edges have a sense of COST / WEIGHT.
Each edge is now (s, t, w) instead of (s, t).

#### Problems
1. Cheapest way to connect all vertices ([[Minimal spanning tree]], but ***NOT*** a [[Graph Algorithms#Paths & Circuits|Hamiltonian/Euler Path]])
2. Cheapest way to get from A to B (shortest path problem)

#### Representation
###### [[Graph Representation#Adjacency Matrix|Adjacency Matrix]]:
All points are now a weight (instead of 1 or 0s) in the matrix,
![](https://lh6.googleusercontent.com/j_FsGRIOI1LGoQ3FsMAwY_KV4hoUcO10ZEOY3cTeaBhmb7bkBShO_HKirqEhjjOXyO-e7cUMVbr641UpliXrDzzKey-MU_0MgbY5jPyNs7dNk3eSQnlWeGudEUEmwmL81NDceSteF4FSSR15_G61yN4)

###### [[Graph Representation#Adjacency List|Adjacency List]]:
All points are now have a weight,
```c
struct Link {
	int vertex;
	int weight;
	Link *next;
}
```

![](https://lh5.googleusercontent.com/3q-X0MH08mGKj4rqQEGPK0lmfKNLd_HHwepp8_Gd_QPC511V1B5Cl94PblQLSA2_a5cxD0UANG1bamBmSxp1HBDUq7-7OOVNikBFX8vZ7vaxlhStIkFdUpMFLl4OvDUu_Wt8WnoDzueIFfbfzYfgIcU)

###### [[Graph Representation#Array of edges|Edge List]]:
**![](https://lh6.googleusercontent.com/Jn540Ssl3DFIQ6WOFXA0iBIaREBvKGfWBmnF3QZPsJKEh5l3P2-7VsFTUdW3N7hFyz3XK4aHa5yxB2kvunwnwfLezYZ9BXmKx_XVuNthZ7sIvWBNDpyEHNJVFcmz2812tXBqHSBJ3ZjH2XxS7lXsZEE)**