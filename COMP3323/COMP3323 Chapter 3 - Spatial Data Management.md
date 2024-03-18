
[[COMP3323 Chapter 2 - Database Review, Database Design and Queries|Last Chapter]] [[COMP3323 Chapter 4 - Spatial Networks|Next Chapter]]

## Location Data
- More and more check in service usage

## Online Maps
- Identify location
- Provide routes to destination


## Location-based Services
- Map services able to locate users
- Navigate users to destination
- Company can send SMS to subscribers when they are near their store
- Application suggest content based on location/places nearby

## Location Tracking
- Companies can monitor their parcels location
- Bus companies can publish arrival information to users


## Traffic Data Analysis
- Loop detectors to capture real-time traffic information
- Different data source from different companies and departments
- Can predict traffic condition and enhance quality for suggested route

## Spatial Databases
- PostgreSQL with PostGIS
- Neo4J-spatial
- HadoopGIS
- Ingres
- GeoMesa


## Spatial Data Management
- Manages large collections of multidimensional object
	- Usually 2D/3D
- Spatial object contains at least a spatial attribute which describe locations
- Spatial relation


## Spatial Data
- Spatial object have extent/points to bound them
- e.g. rivers/forests/buildings/districts

- Ways to represent objects
	- Vector representation
		- Approximation by geometric object
		- e.g. Polygon, poly-lines
	- Raster representation
		- Divide space by fine grid
		- Approximate object by set of pixels

- In many applications
	- Geographical Information System
	- Segmented Images
		- Objects in X-Rays
	- Components of CAD constructs/VLSI circuits
	- Stars on Sky


## Spatial Relationships
- Associate 2 objects according to their relative location and extent in space

Can be classified into
- Topological relationship
- Distance relationship
- Directional relationship
	- which can be combined


### Topological Relationship
- Characterized by space that it occupies
	- Finite set of pixels
- Each object has boundary and interior
	- Boundary: Set of pixels that object occupies, adjacent to at least a pixel not occupied by object
	- Interior: Set of pixels occupied by object, not part of boundary
- Some object may not have interior
- Defined by a set of relations
	- disjoint(o1, o2): if o1 and o2 does not have overlap
	- intersect(o1, o2): if o1 and o2 have overlap
	- equals(o1, o2): o1 and o2 are same
	- inside(o1, o2): o1 is inside o2
	- contains(o1, o2) o2 contains o1
	- adjacent(o1, o2): o1 is beside o2


### Distance Relationships
- Associate 2 objects based on geometric distance
- Usually Euclidean distance
- Abstracted to human mind
	- use human unit
	- e.g. 100m, 10km, 21.7km


### Directional Relationship
- Associate 2 objects based on relative orientation according to global reference system
- Expressed in direction or degrees
	- 123 deg/ Southeast


## Spatial Queries
- Applied to one/more spatial relation
- Retrieve object that satisfy some spatial relationship
	- Nearest city to my current location
	- All hotels and restaurants that are within 100m distance from each other

- Range Query
	- Find all city in a certain region
- Nearest Neighbour Query
	- Find city closest to a building
- Spatial Join
	- Pairs of rivers and cities that intersect


## What is special about spacial
- Dimensionality
	- No total ordering of objects in multidimensional space which preserve spatial proximity
- Complex Spatial Extent
	- Adds complexity of object clustering to disk pages imposed by domensionality
- No standard def of special operations and algebra
- Relational indices and query processign methods not really applicable to spatial data
	- New spatial access methods needed for spatial data


## Two-step Spatial Query Processing
- Approximated by minimum bounding rectangle

Processing spatial query:
1. Filter Step: MBR is tested against query predicate
2. Refinement Step: Exact geometry of objects that pass filter step is tested for qualification

#### Example: Find objects intersect with Query window W
- Enclose all objects in Minimum Bounding Rectangle
- Find rectangles that intersect with W
- Check if any points in object is in W
	- if so, include it in result

## Spatial Access Methods
- Hard to index spatial data
	- No dynamic access methods with good worst case
- Aims to minimized expected cost
- Early SAM index multidimensional point


### Point Access Methods
- Divide space to disjoint partition and index points
	- e.g. grid file

- not effective for extended object
	- Objects may clipped to several parts
		- data redundancy
		- affects performance
	- Solution: allow some MBR to have minimum overlap


## R-Tree
- Group Object MBRs at a hierachical level
	- One larger rectangles in other smaller rectangles that enclose several MBR
	- (Object MBR, pointer to child node) as non-leaf node
	- (Object MBR, object id) as leaf node
- Smaller rectangles have to be fully in larger rectangle to be the child node

- Balanced Tree
	- Equal depth

- Not tightly packed
	- Easy to insert/delete
	- Less time to re compute the rectangles
- Higher dimension rectangles: Hyper-dimension triangle
- Dimensionality reduction

### Range Query with R-Tree
- if n is not leaf node


## R*-Tree
- Better quality [[#R-Tree]]
	- smaller MBR
		- Lesser dead space
		- Enhance query performance
	- smaller overlap
		- Lessen number of node traversed
	- square-like node
		- Lessen margin-to-area ratio
		- Less dead space
	- more packed node
		- Less dead space

- Margin minimalization
	- Try to pack objects to square-like MBRs
		- 

## Bulk-loading R-Tree
- Loading rectangles to tree with fast algorithm
    - sorting or hash-based
Dumb way
- insert from empty tree without order
    - tree nodes are not as full as possible
### X-Sorting
- Each object is a point
- nodes are bulk-loaded
- Sort by one axis
- Objects are assumed to static -> no insertion/deletion -> no need to leave space for new object

Disadvantages
- biased to one axis
- one axis may be close but far from other axis
    - MBR have large margin


### Hilbert Sorting
- Make a space-filling curve
- insert the nodes one by one according to theline

### Sort-tile-recursive
- Sort one axis, then the other
- Usually the best structure compared to other methods


## Spatial Query Processing

### Spatial selection
- Given a window, find the objects that is in the window
- Start with largest MBR


### Nearest Neighbour Search
- Find the nearest neighbour from a query point
- Closeness: Shortest euclidean distance
- Distance of MBR is usually smaller than actual distance

Generalized problem
- find k nearest neighbour (k-NN) of a point


### Distance measured between MBR
- Object MBR distance is the minimum object distance
- Use distance between query point and larger MBR for minimum distance between 

### DFS for Nearest Neighbour with R-Tree
- function dff_nn(object q, Node n, object o_nn)
    - q as query point/object
    - n as root
    - o_nn start as imaginary object, dist(q, o_nn) = $inf$
- start with node n
    - if n is leaf node then search for each mbr in n
    - if not compute the distance between larger mbr to smaller MBR


### Best-First Nearest Neighbour Search
- More efficient algorithm
- aka Greedy approach
- Requires more memory
	- To store entries that have not been added to queue
- Utilizes [[COMP2119 Chapter 9 - Sorting I#Priority Queue|priority queue]] to organize seen entries
	- prioritize next node to be visit

1. Initialize all vertices as unvisited.
2. Select an arbitrary vertex, set it as the current vertex u. Mark u as visited.
3. Find out the shortest edge (using some heuristic or cost function) connecting the current vertex u and an unvisited vertex v.
4. Set v as the current vertex u. Mark v as visited.
5. If all the vertices in the domain are visited, then terminate. Else, go to step 3.


## Spatial Joins

Let R, S be 2 spatial relation, $\theta$ be a spatial relation
$$\{(\mathsf{r},{\mathsf{s}})\colon\mathsf{r\in R,\ s\in S,\ r\ \theta\ s\ i s\ t r u e}\}$$
Example:
- Semi-join: Find the cities that intersect a river
- Similarity join: Find pairs of hotels, restaurants close to each other (with distance smaller than 100m)
- Closest pairs: Find the closest pair of hotels, restaurants
- All-NN: For each hotel find the nearest restaurant
- Iceberg distance join: Find hotels close to at least 10 restaurants

Problem:
- More expensive than selection
- How can the filter be applied


### R-Tree Join
- Find 2 R-Trees' intersection node
- Look at larger MBR first
- Check if any sub-elements (object eventually) intersect with each other
	- refinement and filter

- Problem: Cost is high to work with 2 MBR
	- Compute MxN pairs, m = number of rectangle in tree1 and n = number of rectangle in tree2

- Cannot be used for non-indexed input
	- on the fly R-Tree

**Optimization for R-Tree Join**
- Try to reduce the computation time

#### Space restriction
- if entry i not in both large MBR
	- prune
- compute much less MBRs in both R-Tree
- Cost: $O(M) + O(N)$


#### Plane Sweep
- Sort entries by a axis
- Sweep through the axis to find ones that intersect
- Cost: ${\mathrm{O}}(({\mathrm{N}}+{\mathrm{M}})\cdot{\mathrm{log}}({\mathrm{max}}({\mathrm{N}},{\mathrm{M}}))+{\mathrm{k}})$

### Single-index methods
- Indexed Nested loops

- Seeded tree join and bulkload and match
	- build a rough R-Tree


### Comparison between different join algorithms
- Better to use R-Tree
- Single index method is also ok
- No conclusion on non-indexed data


## Multi-step join processing
1. Find MBR pairs that intersect
2. Compare with detailed approximation to check if 2 object overlap
	- Convex hull
		- rubber band like approximation
	- Maximum enclosed triangle
		- guaranteed to be overlap
3. Perform refinement step if still join predicate inconclusive


[[COMP3323 Chapter 2 - Database Review, Database Design and Queries|Last Chapter]] [[COMP3323 Chapter 4 - Spatial Networks|Next Chapter]]