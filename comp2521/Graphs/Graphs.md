### Structure
A Graph G = (V, E) is a general data structure that consists o
- V: A set of vertices (collection of items)
- E: A set of edges (relationship between items) 

They may contain cycles, and there is no implicit order of items

<p align="center">
<img src="https://lh3.googleusercontent.com/3Qt1lUZzDfUCsd3O4s0Tx-TFIWKUtiW-0Wm26MY2IxPpKGX6DaauXdGY5CGH51Tew5Tt1CXZn28SJ4k0GVMeswiM5leUcHQoLpk7QXOMZXOCsYDKo-GvHdEtIT_QlgxkFnSOnu_4xa14gai_xeZkmMo" 
 width=400px>
</p>
### types
- A [[Tree]] is a type of graph with no cycles (vertices = nodes, edges = children), all nodes only have 1 child.
	- **Spanning Tree**  containing all vertices
- A [[Linked List]] is a type of graph(vertices = nodes, edges = next links), all nodes only have 1 next.
- **Clique**: complete subgraph

<p align="center">
<img src="https://lh6.googleusercontent.com/idXV_5XhajYX_Vx3_VMDIX9DF55n9YBBBl8NBbubTfvcWaCu5fpaSHfE_PSFh9QuNm7qTKhUZp5Xrgbkf8kYYIyCnS8Zy0uRAByq454gq7zWi4-BF2_5YLpdS3iCzbJtKk4lCup9XvQ4tdu79yAYupM" 
 width=400px>
</p>


### Terminology
- **Path**: Sequence of vertices where each vertex has an edge to it's predecessor
- **Cycle**: A path where the last vertex in the path is the same as the first vertex (see [[Graph Algorithms#Cycle Checking|cycle]])
- **Length of path**: Number of edges in it
- **Connected Graph**: There is a path from each vertex to every other vertex
- **Complete graph**: There is an edge from each vertex to every other vertex

An undirected graphs are graphs whose edge do not have a direction. Likewise directed graph's edges have direction. See [[Weighted Graphs#Directed Graphs (Digraphs)|Directed Graphs (Digraphs)]]

<p align="center">
<img src="https://lukakerr.github.io/assets/img/2521/graph2.png" 
 width=400px>
</p>
### Properties of graphs:  
A graph with V vertices has at most V(V-1)/2 edges 
- E < V^2 always (hayden), this is because v can have at most (V-1) edges 

The ratio Edges:Vertices (E:V):
- If E is closer to V^2, the graph is dense
- If E is closer to V the graph is sparse


[[Graph Representation]]


