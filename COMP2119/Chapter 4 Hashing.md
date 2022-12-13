# Chapter 4 Hashing

## Dictionary ADT
Structure: (key, value)
- phonebook 
- 3 operations: `INSERT`, `DELETE`, `SEARCH`

#### Insert for dictionary
- add a `key`, `value` pair to the dictionary
- O(1) time needed

#### Delete for dictionary
- Can be deleting a key and value pair
- O(n) for search operation

#### Search for dictionary




### Implementation by Linked List
- not very efficient for searching, O(n) time is needed



## Hashing
- forming compartments and fill in
- $h: K \to [0,1,2,...,m-1]$

### Example 1 in hashing
- Keep record of students in a class
- Use an hash table ith 3000 entries `T[0...299]` to store records of students by: 
h(U.No.) = (U.No.) mod 300
-  h("BEN") = ($66(128)^2 + 69(128)^2 + 78$ ) mod 300=54

### Problems in hashing
##### Hash Collision
- when 2 keys have a same hash value
- Handling collision:
	- Use better hash function
	- Use collision resolution strategy


#### Chaining (Open hashing)
- Implement a linked list when there is same key that have same hash


Implementation by singly linked list
- less space used for a pointer

Implementation by doubly linked list



##### Analysis of chaining
##### load factor(a)
- a = (no of element)/(no of slots)


##### *assuming the hash table is distributed uniformly*
- Insertion 
	- takes O(1)
- Deletion 
	- takes O(1) if doubly linked list is used, otherise same as searching
- Searching
	- Unsuccessful search: O(1+a)
	- Successful search: O(1+a)
	- there is a 1 in [[Chapter 2 Algorithms#Big O identifies an algorithm with growing complexity|Big O notation]] because the expected length is $1 + \frac{n-1}{m}$




## Hash functions
### Good hash function
- easy to compute (efficient)
- use all of the information on keys
- satisfy the assumption of simple uniform hashing
- 
### Division method
- $h(k) = k \text{ mod } m$
- where k is key and table size is m
- a good value of table size is a prime
- 


## Open addrssing
- aka closed hashing
- Avoids pointers when compared to [[#Chaining (Open hashing)|Open hashing]]
	- saves time from allocating pointers
	- saves space by not using pointers
	- larger number of slots are available by closed hashing
	- n element with each element takes 10 byte
	- Chaining:
		- `n` elements are stored in a table of `m`
		- Take load factor $\frac{n}{m}$ = 3
		- Pointer size is 4
		- An array would have 4 * m size

- A rehashing may have to be done in order to get the [[#load factor]] < 0.5
- Solution: reconstruct a larger hash table to lower load factor



- Code implementation of Open addressing
```C++
open_adress_hash_insert(T,x){
	i = 0; /* collision count*/
	k = x.key
	do {
		j = hash(k,i);
		if (T[j].key == NULL){
			copy x to T[j];
			return;
		else
			i++;
	} while (i < m);
	return("hash table overflow!")

}

open_address_hash_search(T,k){
	i = 0;
	do {
		j = hash(k,i);
		if (T[j].key == k)
			return j;
		i++;
	} while ((T[j].key != NIL) && (i < m))
	return("Not found!");
}

open_address_hash_search(T,k){
	i = 0;
	do {
		j = hash(k,i);
		if (T[j].key == k)
			T[j].key = NULL;
		i++;
	} while ((T[j].key != NIL) && (i < m))
	return("Not found!");
}
```




## Load Factor
- For [[#Chaining]], it can be greater than 1
- For [[#open addressing]], it should be < 1, preferably < 0.5


## Ways to resolve collision
### Linear probing
- $h(k,i) = h_1(k) + i \text{ mod }m $
- By linearlly increment/decrement the hash key of each element to be inserted

Problem caused:
#### Primary clustering
- When block of consecutives ccupied slots occur
- By [[#Linear probing]], more attempt would be used
	- Results in a large cluster of hash function

#### Quadratic probing
- $h(k,i) = h_1(k) + i^2 \text{ mod }m$
- An attempt made to eliminate the [[#Primary clustering|problem]] occured in [[#Linear probing]]

Problem caused:
#### Secondary clustering
- The probe sequence would not span through whole table
- Only m probe sequence, therefore there would also be a cluster

#### Double hashing
- utilizes 2 hash functons to define a probe sequence
- - Very unlikely to causes clustering
- $h(k,i) = (h_1(k) + i(h_2(k))) \text{ mod } m$
- $h_1(k)$ determines the initial slot
- $h_2(k)$ determines the incrementation for next probe
	- it should never get a number to 0(would result in a endless loop
	- the result should be a relative prime to m
		- set m as a prime and $h_2(k) < m$
 







