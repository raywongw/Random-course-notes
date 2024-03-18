
[[COMP3323 Chapter 1 - Introduction|Last Chapter]] [[COMP3323 Chapter 3 - Spatial Data Management|Next Chapter]]

### Basic Structure of Relational Database
- sets 


### Relation Schema
- A1, A2, ..., An are attributes, then R = (A1, A2, ... , An) is a relation schema

### Relation Instance
- Values of a relation specified by table

### Database
- multiple inter-related relations in a database


### Query Language
- Language that user request information from database
- Category of query language
	- Procedural
	- non-procedural
		- SQL
- "Pure" languages
	- Relational Algebra
	- Relational Calculus


### SQL
- based on set and relational operations
- Result of SQL Query is a multiset of tuples


### Storage Hierarchy
- Primary Storage
	- Fast and Volatile
	- RAM, Cache
- Secondary Storage
	- Not as fast, non volatile
	- Flash Memory, Magnetic Disk
- Tertiary Storage
	- Slowest, non vlatile
	- Magnetic Tape, Optical Storage
- Cloud Storage
	- Cheapest option
	- Backup in a remote location
	- AWS EC2

### Magnetic Disks
- RW head very close to the platter
- Sector -> Track -> Cylinder
- Performance Measure
	- Access Time: Time taken from read/write command issued to data transfer begin
		- Avg: 1/2 worst case seek time, around 4-10ms
	- Data Transfer Rate: Rate that data is retrieved/stored to disk
		- 4-8MB per second

### Storage Access
- Database File is partitioned to blocks
	- Around 4kb to 16 kb








### Indexing
- To keep track of record with a small index file
- Smaller size to be computed
	- Smaller compute cost(Query in number of index blocks + blocks containing query result)
- 
- Binary search -> cost reduced to O(log_2(No. of blocks in index file))
- f-way search -> cost further reduced to O(log_f(No. of blocks in index file))


- New data structure
	- Objective: Support insert/deletion and give faster search
	- Solution: B+ Tree
	- 

#### Indexing mechanism
- To speed up access to desired data
- Search Key
	- Attribute(s) to lookup records in file
- Index file has records in (Search Key|Pointer to Block)
- Basic Kind of Indices
	- Ordered Indices: keys in sorted order
	- Hash Indices: keys distributed across buckets by hash function


### What is a good index
- Access types supported by index efficiently
	- Records with specified value
	- Records in a certain range
		- B+ Tree can better support range query
- Access Time ->**Query response Time**
- Insertion Time -> **data record insertion time**
- Deletion time -> **data record deletion time**
- Space overhead -> **size of the index file**



### Classification of Index
- Ordered Index
	- Primary Index
		- Search Key has same order as sequential file
	- Secondary Index
		- search key has different order as sequential file
- By Density
	- Dense Index
		- Records appear for all search-key value in file
	- Sparse Index
		- Records appear for some search-key value in file
		- Records not appear must be in previous
		- Cannot be applied to secondary index as there is information loss
			- if some entries in secondary index is removed, since it is not in order as sequential file, the information we want would not be able to retrieved by the order of secondary sparse index
			- useless index


### Multilevel Index
- Objective: Reduce disk access to minimum
- Outer index: sparse index on 1st level index file
- Inner index: 1st level index file
- Inserting 

#### [[COMP3278 Chapter 7 - Indexing#B+ Tree|B+ Tree]]
- Disk-based tree
- design to keep tree balanced
- Logarithmic time insertion/deletion
##### Node in B+ Tree
- has n-1 search key values, n pointers
- keys in sorted order

##### Non-Leaf Node in B+ Tree
- at least $\lceil \frac{n}{2} \rceil$ and at most n pointers
	-  $\lceil \frac{n}{2} \rceil$ -> the minimum fan-out/degree
		- 
- left pointer to node must contain smaller key value than itself
- right pointer to node must contain larger or equal key value than itself

##### Leaf Node in B+ Tree
- at least $\lceil \frac{(n-1)}{2}\rceil$ and at most n-1 key values, n as no. of pointers
- last pointer for chaining the leaf nodes in search-key order

#### Queries on B+ Trees

- Start with root node
- Examine each key in node
- goto to next level...
- get to leaf node and get record
##### Range Query
- Search for node with value between k and m
- Goto to node with value k
- then use pointers of leaf node to get to node contains n

##### Comparison with Binary Tree
- Problem sin binary tree
	- Small fan-out
		- One node has 2 children only
		- Tall tree -> more I/O
	- Bad Space Utilization
		- One disk page with 2 entry
		- B+ Tree has at least 50% full, more item is packed

Complexity
- $\log_{\lceil\frac{s}{2}\rceil}n$
- better than binary tree as binary tree has log_2 only

#### Insertion in B+ Tree
- Find leaf node which the record should be inserted
- If search key is in there
	- pointer is added to file
	- more pointer is associated with search key value
- If search key not there
	- add record to main file
	- if room in leaf node: insert and done
	- if not: split node
		- hold first  $\lceil \frac{n}{2} \rceil$ search-key value + pointer pair, move other to new node
		- Move first key-pointer pair to parent node
		- Check if parent is full again
		- Worst case: increase height of tree by 1


#### Deletion in B+ Tree

First way
- Search for the record to be deleted
- delete it from relation file
- If node has too few entries
	- Merge 2 nodes to a node
	- Remove pointer from parent

Second way (sibiling cannot be fitted)
- Redistribute pointer between node and sibiling
	- both have more than min number of entries
	- Update corresponding search-key value in parent node


### Static Hashing
- **Bucket**: Storage unit with one or more records.
- **Hash File Organization**: Method to get a record's bucket using a hash function and search-key.
- **Hash Function**: Maps all search-key values to bucket addresses. Used for record access, insertion, deletion.
- **Collision**: Occurs when different search-key values map to the same bucket. Requires sequential bucket search to locate a record.


### Hash Functions

- **Worst Case**: All search-key values map to the same bucket
	- access time proportional to number of search-key values in the file
- **Ideal Hash Function**: Uniform and random.
	- Uniform: each bucket is assigned the same number of search-key values from all possible values
	- Random: each bucket has the same number of records assigned irrespective of the actual distribution of search-key values
- **Typical Hash Functions**: Perform computation on the internal binary representation of the search-key. For example, for a string search-key, the binary representations of all characters in the string could be added and the sum modulo the number of buckets could be returned.

### Handling of Bucket Overflows

- **Bucket Overflow**: Occur due to insufficient buckets / skew in distribution of records. 
	- Skew can occur due to multiple records having the same search-key value
		- the chosen hash function producing a non-uniform distribution of key values
- **Solution**: Handle by using overflow buckets


[[COMP3323 Chapter 1 - Introduction|Last Chapter]] [[COMP3323 Chapter 3 - Spatial Data Management|Next Chapter]]



