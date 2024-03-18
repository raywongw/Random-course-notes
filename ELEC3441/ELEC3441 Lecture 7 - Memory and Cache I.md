
[[ELEC3441 Lecture 6 - Branch Prediction|Last Lecture]] [[ELEC3441 Lecture 8|Next Lecture]]


## CPU vs Memory
- Speed of Memory and CPU gap widens
- 



## Cache Operation
- from regfile to cache to memory to hard disk

## Memory Reference Patterns
![[Pasted image 20240314120319.png]]

- Properties to predict memory reference:
	- Temporal Locality
	- Spatial Locality
	



## Fully Associative Cache
- Cache tag with a offset
- can be stored in any location



## Direct Map Cache
- Memory address' value can only be stored in 1 possible location
	- k but of address for a 2^k line
- More than 1 memory address can be mapped to same cache location
	- Collision and eviction
- Often used in L1 cache
	- Simple and fast


## Set Associative Cache
- Reduce cache miss -> increase number of possible locations
- N-way set-associative cache -> N locations to store a data block








[[ELEC3441 Lecture 5 - Pipelining|Last Lecture]] [[ELEC3441 Lecture 7 - Memory and Cache I|Next Lecture]]