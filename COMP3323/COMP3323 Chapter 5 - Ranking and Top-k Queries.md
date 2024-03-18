
[[COMP3323 Chapter 4 - Spatial Networks|Last Chapter]] [[COMP3323 Chapter 6 - Big Text Data|Next Chapter]]

## Recommendation System
- Try to use data to recommend similar items
- Better algorithm is needed to better meet user's favor
	- increase purchases and revenue

## Multidimensional Data
- Has different attributes
	- e.g. Tuples of data 
- Each feature as a dimension


**Data Warehouse**
- Fact table
	- Managing data that is interlinked

**Spatial Data**
- Location dimension

**Text Documents**
- Term frequency
- Similar to [[COMP3278 Chapter 9 - Processing big data with MapReduce#Term Frequency - Inverse Document Frequency|tf.idf]]


## Attribute Types
- **Ordinal**: Can be sorted easily
- **Nominal Categorical**: Cannot be sorted
- **Binary**: Only 2 options

- Creating basic query based on above data

## Basic Queries
- **Range selection query**: Returns records of a certain range
	- Can be multidimensional range
- **Distance Query**: Returns records within a certain distance from referenced record
	- Finding similar image in database by vector comparison
	- Similarity Search
- **Nearest Neighbour Query**: Find most similar items by distance
	- Apple Photos: Find similar faces


## Top-k Query
- Find k object with highest combined score by an aggregation function f
- Example: Find k best restaurant
	- Table: (Price, Quality, Location)
	- Function: sum(-price, quality, -dist(location, own location))
	- Attribute value are normalized
		- All values in [0,1]
		- able to treat all attributes equal and not favoring some attributes
	- 

### Variants
- Standalone query in a more complex query plan
- Incremental retrieval of object with highest score
- 


### Evaluation
- Most solutions assumes factors are distributive and monotone


### 1D Ordering and Merging List
Use a f to compute the score for each attribute -> get final rank of each object

**Advantages**
- Can be applied on any subset of inputs (arbitrary subspace)
- appropriate for distributed data
- appropriate for top-k joins
- easy to understand and implement
**Drawbacks**
- slower than index-based methods
- require inputs to be sorted


#### Threshold Algorithm
- Iteratively retrieves object and atomic score from ranked input
- Can also read a random object in a certain rank
	- May be expensive
- Fetch the F-score (cumulative score based on all factors) of a object


**Procedure**
- Fetch T, aka max(F-score) by f(1st elem for each rank)
- Fetch the top-1 score 
	- if top-1 score < max(F-score), iterate T to next rank
	- if top-1 score >= max(F-score), increment counter

**Problem**
- Time wasted on finding element if no random access
- Space wasted on building a tree for quick search



#### No-Random Access Algorithm
- Quickly find top-k item without random access


**Procedure**
- Build a tuple (upper bound, lower bound) of n item
- have to keep to know which attribute of a item has been accessed?
- Build a prioq Q to store k object with largest lower-bound f-score

- For each rank in all ranks
	- Calculate upper bound and lower bound f-score of each object
	- Compare if min(lower bound f-score of object in Q) is smaller or equal max(upper bound f-score of object not in Q)

#### Lattice-based Rank Aggregation
- More efficient than [[#No-Random Access Algorithm|NRA]]
	- Avoid updating some bounds

**Observation on NRA**
- Upper bound is not useful
	- No need to update and make comparison with upper bound in this phase
- while max(lower bound f-score of unseen object) < min(upper bound f-score of seen object), all object can be in top-k result
- No unseen object can be in top-k when t >= T


**Procedures**

Let t be max(lower bound f-score of unseen object)
Let T be min(upper bound f-score of seen object)


Growing Phase
While (t<T)
- Iteratively retrieve objects and their atomic scores from the ranked inputs in a round-robin fashion.
- Update lower bound (fx_lb) for each newly accessed object x.
- Update Wk (the set of the k objects with the largest f lb) and compute t from it.
- Update T from the last atomic scores seen at each input.

Shrinking Phase
- Accessed objects that have not been seen during the growing phase are immediately pruned (observation 3)
- Instead of explicitly maintaining fx_ub for each candidate x, LARA reduces the computations by distributing the candidates using a lattice.

Lattice
- Base: Null
- First Layer: each attribute has 

### Issues in Top-k Rank Aggregation
- Need index for data/Pre-compute some info
	- Time-Space Tradeoff


### Index/View based solution


### Multi-dimensional index search
- A aggregate function to convert spatial object to a f-score
- measure f-score of mbr by a lower/higher bound -> decide which mbr to cover first
- 

[[COMP3323 Chapter 4 - Spatial Networks|Last Chapter]] [[COMP3323 Chapter 6 - Big Text Data|Next Chapter]]

