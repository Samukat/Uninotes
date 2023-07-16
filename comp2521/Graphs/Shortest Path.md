# Shortest Path
Finding the shortest path through a [[Graphs|graph]].
The shortest path of a graph will be the solution found by a [[Graph traversal#Breadth-first search|BFS]] if the graph has uniform weights or is a non-[[Weighted Graphs#Weighted Graph|weighted graph]].

Shortest path is a path between two vertices on a weighted graph with non-negative weights.


## Implementation
>note: this implementation is best for c (or other low-level languages) *ONLY* 

Shortest paths from s to all other vertices:
- dist`[]` V-indexed array of cost of shortets path from s
- pred`[]` V-indexed array of predecessor in shortest path from s 

### Dijkstra's Algorithm
```c
dijkstraSSSP(G ,src):
	dist[]
	pred[]
	vSet // vertices whose shortest path from s is unknown
	initialise all dist[] to inf // or -1 e.g.
	dist[src] = 0
	initialise all pred[] to -1
	vSet = all vertices of G
	while vSet is not empty:
		find v in vSet with minimum dist[v]
		for each (v,w,weight) in edges(G):
			relax along (v,w,weight)
		vSet = vSet \ {w} // remvoe w from Vset
```

<p align="center">
<img src="https://upload.wikimedia.org/wikipedia/commons/5/57/Dijkstra_Animation.gif" 
 width=500px>
</p>

#### Relaxing the edge
replace higher value with lower value edge and change pred

#### Time complexity
- Every edge considered once => O(E). 
- Outer loop has O(V)
- 'find s in vSet with min distance' 

Time Complexity of Dijkstra's Algorithm is **O ( V 2 )** but with min-priority queue it drops down to O ( V + E l o g V )