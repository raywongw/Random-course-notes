
[[COMP3278 Chapter 6 - File & Storage|Last Chapter]] [[COMP3278 Chapter 8 - Collaboration Filtering|Next Chapter]]

### Basic Concepts
- Indexing
	- Speed up access to desired data
	- Usually much smaller than original file
- Search Key
	- (Set of) Attribute to be used to look up records


### Indices
- Classified as Primary index and Secondary Index

##### Primary Index
- Its search key defines sequential order of file
- ony be able to sort in one order

##### Ordered Indices
- Keys are sorted in index
- e.g. [[#B+ Tree]], indexed-sequential file


##### Hash Indices
- keys are distributed over different buckets by hash function
- e.g. extendable hash index


##### Index evaluation factors
- Access types
	- type of access supported efficiently
- Access time
- Insertion/Deletion time
- Space Overhead



### B+ Tree
- Widely used in DBMS
- All path from root to leaf are same length
- Efficient processing of queries like `SELECT * FROM R WHERE R.A = 3`

- Compared to BST
	- Size of node = 1 block (more than 1 key)
	- Low height
	- Balanced


#### Properties
##### Node in B+ Tree
- has n-1 search key values, n pointers
- keys in sorted order


##### Leaf Node in B+ Tree
- at least $\lceil \frac{(n-1)}{2}\rceil$ and at most n-1 key values, n as no. of pointers
- last pointer for chaining the leaf nodes in search-key order

##### Non-Leaf Node in B+ Tree
- at least $\lceil \frac{n}{2} \rceil$ and at most n pointers
- left pointer to node must contain smaller key value than itself
- right pointer to node must contain larger or equal key value than itself


#### Searching in B+ Tree
- Useful for range search

###### Procedures
- Traverse from root node to leaf node
	- get first value in root node
	- if it is greater than value in last slot, goto to node that last pointer point to
- Traverse from current leaf node to right if target not in current node


#### Number of disk block access
1. determine the type of search
- Calculate the depth of tree
	- Usually at $\log_{\text{number of }}$