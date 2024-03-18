
[[COMP3323 Chapter 3 - Spatial Data Management|Last Chapter]] [[COMP3323 Chapter 5 - Ranking and Top-k Queries|Next Chapter]]

## Spatial Networks
- Geographic Data
	- Streets, Routes
- Search for shortest path
- Spatial query over spatial networks
- Ways to index spatial network

### Challenges
- Euclidean distance does not apply
	- R-Tree no longer useful
- Graph cannot be flattened to one-dimensional space
	- New ways to store and index these graphs
- Different graph properties
	- Directed/Undirected
	- Length, Time
### Network Distance
- Shortest path distance instead of Euclidean distance


## Modelling Spatial Networks
- Adjacency Matrix
	- Only applicable for dense graphs
	- Easier to check if node A and node B have direct edge
	- Have more unused space
- Adjacency List
	- More favourable for sparse spatial networks
	- More applicable for spatial networks
		- Most spatial networks are sparse

## Storing
Use B+ Tree on top of partition



## Shortest Path Computation

### Dijkstra's Algorithm
Explore graph around and get to target




### A* Algorithm
- Dijkstra's Algorithm but with directing search
	- Search favours nodes nearer to T rather than away from T
	- Compute the path distance + euclidean distance of current node to target
	- Choose shortest overall distance from [[COMP2119 Chapter 9 - Sorting I#Priority Queue|prioq]] to explore

### Bi-directional search
- Search from source and target
- 2 [[COMP2119 Chapter 9 - Sorting I#Priority Queue|prioq]] needed

[[COMP3323 Chapter 3 - Spatial Data Management|Last Chapter]] [[COMP3323 Chapter 5 - Ranking and Top-k Queries|Next Chapter]]