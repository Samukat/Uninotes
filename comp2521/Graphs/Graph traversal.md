Graph Traversal is the systematic exploration of a [[Graphs]] via the [[Graphs#Structure|edges]]

There are 3 main topics we will focus on relating to traversal:

- Traverse for item searching
- Traverse for path finding (Find value and record how to get there)
- Traverse Fully (All [[Graphs#Structure|vertices]]) ^704dc6

The two main methods are **Depth-first search** (iterative and recursive solutions) where we go deep and **Breadth-first search** (iterative solutions) where we go wide

## Breadth-first search
Traversing by expanding out equally from a node (expanding).

- You record a 'visited' array to keep track of what has already been searched
    - The visited array contains the parent node of each node (the first parent node when traversing -> enables smallest path to be found) (Also can be in a predecessor array)
    - Visited array can also just be Booleans, but this is only if all we care about is searching
- Uses a Queue (iterative) to traverse

#### Pseudo code
```c
bfs(g, src):
	**Inputs:** graph g
	        starting vertex src
	
	create visited and predecessor arrays
	create queue and enqueue src

	mark src as visited
	**while** the queue is not empty:
		dequeue v
		
		**for** all edges (v, w) where w has not been visited:
			mark w as visited
			set predecessor of w to v
			enqueue w
```

A standard BFS will generate the smallest path, assuming each edge has the same weight (cost)!
**![](https://lh6.googleusercontent.com/FeXF_XOJ0_xlSyvIsBGZZMTF5M-0Mj79rv1YLPatpHQzNrIGlp74BiVFg7dDh40wwlniyVdilo4eazoKeAREPubt_7qkoYOZsul4-B_plkY8l_ACrVQeHAlsHN_V0ASj0nf-UvoZRFS0MLNYZS0CK94)**

#### Cost Analysis
For [[Graph Representation|adjacency list]] representation:
- Each vertex visited at most once: Cost = O(V)
- Visit all edges incident on visited vertices: Cost = O(E)
- BFS: O(V + E) (adjacency list)

---
## Depth-first search
Traversing with DFS is about going as deep as possible until you reach a dead end, and the unwinding back through nodes until there is another branch to take.
- Common way is to go to the next lowest vertex

##### Iterative Solution
- Iterative DFS uses a stack instead of queue
    - In a stack we insert in one direction, and take off in the other direction
    - Add nodes to stack in highest to lowest order (if we are going to next smallest number)

##### Recursive Solution
This is for [[Graph traversal#^704dc6|full traversal]]
```c
visited = {} 
depthFirst(G,v):
	visited = visited ∪ {v} 
	for all (v,w) ∈ edges(G):
		if w ∉ visited: 
			depthFirst(G,w)
```


#### Cost Analysis
For [[Graph Representation#Adjacency Matrix|adjacency list]] list:
- Each vertex visited at most once: Cost = O(V)
- Visit all edges incident on visited vertices: Cost = O(E)
- BFS: O(V + E) (adjacency list)
- A full traversal of a tree is essentially using BFS or DFS to find a spanning tree -> may not be minimal
- All the code is on the course website!
