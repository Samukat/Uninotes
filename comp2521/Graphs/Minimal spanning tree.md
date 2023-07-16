# Minimum Spanning Tree
**Spanning Tree (ST)** of a [[Graphs|graph]] G = (V, E):
- Contains all vertices (spanning)
- Contains no cycles (tree / [[Tree]])
- ST is a connected subgraph of G

**Minimum Spanning TREE (MST)** of a [[Graphs|graph]] G = (V, E):
- MST is a spanning tree of G
- Sum of edge weights is no larger than any other ST
<p align="center">
<img src="https://miro.medium.com/v2/resize:fit:1004/0*A9tQ2gjDUzAIvqZ0" 
 width=500px>
</p>


## Ways to find MST
Prims is better of dense, Kruskal better for sparse

### Kruskal's Algorithm
1. Start with empty MST
2. Consider edges in increasing weight order:
	1. add edge if it does not form a cycle in the MST
3. Repeat until V-1 edges area added

```c
KruskalMST(g):
	sort edges(G) by weight
	foe rach e in sortedEdgeList:
	MST = MST U {e} \\ add edge 
	if MST has a cycle:
		MST = MST \ {e} \\ drop edge
	is MST has n-1 edge:
		return MST
```

#### Cost 
- Sorting edge list is O(E*logE)
- at least V iterations over sorted edges
- Check if added forms cycle: O(V^2) ??? (Hayden says could be less, O(V))

Overall:
O($E\log(E)$) = O($E\log(V)$)
also for sparse graph could be O(V^2)

>see https://youtu.be/QUpq9vSJwSs?t=1945



### Prim's Algorithm
Used to compute an MST:
1. Start from any vertex v and empty MST
2. choose edge not in MST to add to MST; must be:
	-  connects a vertex in MST to vertex not in MST
	- minimal weight of all such edges
3. repeat until MST covers all vertices

<p align="center">
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/f7/Prim%27s_algorithm.svg/320px-Prim%27s_algorithm.svg.png" 
 width=50px>
</p>

#### Cost 
O($V^2$) or O($V * E$)


