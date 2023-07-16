## Cycle Checking 
A [[Graphs|graph]] has a [[Graphs#Terminology|cycle]] if, at any point in the graph (ALL):
- is has a path length > 2
- start vertex = end vertex; where
- edges aren't used more then once

#### Code:
DFS on all vertexes
```c
bool dfsCycleCheck(Graph g, Vertex v, Vertex u) {
   visited[v] = true;
   for (Vertex w = 0; w < g->nV; w++) {
      if (adjacent(g, v, w)) {
         if (!visited[w]) {
            if (dfsCycleCheck(g, w, v))
               return true;
         }
         else if (w != u)
            return true;
      }
   }
   
   return false;
}

```

- Looping over all possible vertex combinations:
```c
Vertex *visited;
bool hasCycle(Graph g, Vertex s) {
   bool result = false;
   visited = calloc(g->nV,sizeof(int));

   for (int v = 0; v < g->nV; v++) {
      for (int i = 0; i < g->nV; i++)
         visited[i] = -1;
      if (dfsCycleCheck(g, v, v)) {
         result = true;
         break;
      }
   }

   free(visited);
   return result;
}
```

---

## Connected Components
For a given [[Graphs|graph]] how many subgraphs may there be?

Solution:
- Create a `componentOf[]` array, where each index refers to a vertex, and the value at that index refers to which graph it's in.

<img src="https://lh4.googleusercontent.com/0LZA3orRMc3aYH6i36GSZl4Tme1YpLkTG6rXgGrENe9T15qovBQbPQCFOaw9Gw5A_ihBGCm_fd94DxPdkOF2WiKbOMoIZ_nnNhld8MyciXou00h7JaUQGM_9dYSHk3FTjGKRH1hHHoUlPoXtmcmfJyA" width=600px>

#### Code 
You could do this code with BFS or DFS (However, DFS you can do with recursion)
```c++
components(G):  
  for all vertices v ∈ G:
    componentOf[v] = -1
  compID = 0  // component ID
  for all vertices v ∈ G:
    if componentOf[v] == -1:
      dfsComponent(G, v, compID)
      compID = compID + 1
      
dfsComponent(G, v, id):
  componentOf[v] = id
  for each (v,w) ∈ edges(G):
    if componentOf[w] == -1:
      dfsComponent(G, w, id)
```

---

# Paths & Circuits
## Hamiltonian Path & Circuit 
- **Hamiltonian Path:** A [[Graphs#Terminology|path]] connecting two vertices that includes every vertex ***exactly*** once
- **Hamiltonian Circuit:** Hamiltonian Path where starting vertex = ending vertex


#### Approach
- Generate all possible simple paths (e.g. DFS)
- Keep counter of vertices visited in current path
- Stop when find a path containing V vertices

essentially DFS but keep track of path lengths

#### Code
```c
hasHamiltonianPath(G, src, dest):
	visited[]
	for all verticies v in G:
		visited[v] = false
	return hamiltonR(g, src, dest, #vertices(G) - 1)
```

```c
hamiltonR(G,v,dest,d):
	if v = dest:
		return d == 0;
	else:
		visited[v] = true
		for each (v,w) in edges(G) where not visited[w]:
			if hamiltonR(G, w ,dest, d-1):
				return true
	visited[v] = false
	return false
```

#### Time complexity
Worst case; O((V-1)!)
- as there are V-1 paths to be explored
- This is a [[P, NP#Hard Problems|hard problem]] to solve


## Euler Path & Circuit 
Essentially same as [[Graph Algorithms#Hamiltonian Path & Circuit|Hamiltonian Path & Circuit]] but with edges
- **Euler Path:** [[Graphs#Terminology|path]] connecting two vertices that includes every edge exactly once
	- A graph has a Euler path (non-circuit) if and only if it is connected and exactly two vertices had odd degree
- **Euler Circuit**: Euler Path where starting vertex = ending vertex

> A graph has a Euler circuit if and only if it is connected and all vertices have even degree (number of connections on a node)
> A graph has a Euler path iff it is connected and has exactly two vertices with an odd degree



