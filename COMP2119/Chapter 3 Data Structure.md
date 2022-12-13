# Data Structure
Programming language usually provide some basic data types
- e.g. `int` that can operates with arithmetic operations


## Abstract data type
- Extends the concept of encapsulation to a more complicated data type
- which specifies the information we want to maintain with a collection of operations
- collections of variables, can be of different data types, 

### Common aggregate mechanisms
- Array
- Record Structure
- Pointer
	- Address to a variable

Methods to construct more complex [[#Abstract data type|ADTs]]

### Example: Plane
- An wallpaper program 
- ADT to represent drawing plane 
	- $n$ by $n$ pixels that each pixels is referred by a pair of numbers as co-ordinates
	- on or off state of the pixel

Consider operations like:```
```
	clear(P) # set all pixels in P to off
	state(P,i,j) # return state of that pixel at coordinate(i,j)
	plot(P,i,j) # et the pixel at coordinate(i,j) to on
```

would have several ways to implement an ADT given different case
- 2-d array for all data of an wallpaper
- linked list that stores only an 'on' pixel



## Set
- Collection of elements
- Each element is assinged to a `key`

Some of the operations: 
```python
init(S) # initialize a set S -> empty set
search(S,k) # return the element with key = k
insert(S,x) # insert element x to set S
delete(S,x) # delete element x from S
delete_key(S,k) # delete element with key k from set S
```
Comparing key values:
```python
muninum(S) # find the element in S with the smallest key value
maximum(S) # find the element in S with the largest key value
sort(S) # sort elements according to key values
```

IF set is an ordered set (aka [[#List|List]]):
```python
successor(S,x) # find element in S hoch is ordered next to x
predecessor(S,x) # find element in S hich is ordered in fromt of x
```

## List
- an ordered set of elements, e.g. `{a1,a2,a3,...,a(n-1),an}` has a size of n
- the position of `ai` is at `i`

worst case:
initialize: Θ(1), 
search element: Θ(n)

#### Implementation of List
##### - Array
##### - Linked List

memory|variable | target memory
--------|-------|---
87|a2|213
192|a5|0
213|a3|384
384|a4|192
1001|a1|87


Compare array and list:
- linked list is not good for find i-th element operation
- more appropriate if e need to rearrange items very often

- do not need to declare max size of list for linked list
- insertion and deletion ith linked lists require dynamic allocation and de-allocation of memory, which is expensive operation

- insert takes constant time O(const), but search may have Θ(n), n = len(array)


23/09/2022
## Stack
- a list that restricts insert and delete at one end only (top)
- a LIFO (Last in First Out) data structure
- operations as below:
```C++
top() // return top element

INIT(S) {S.tos = -1; }

push(S,x) { // insert at top of stack
	if (S.tos == max_cap -1)
		return(“Stack overflow!”);
	S.tos++;
	S.stack_array[S.tos] = x;
}
pop(S) { // return and delete top element
	if (S.tos == -1)
		return(“Stack underflow”);
	x = S.stack_array[S.tos];
	S.tos--;
	return(x);
}
```

|Order|Stack|
|-----|----|
| | |
|what top() returns |102
| |830|
||492|
|Bottomost element|849|

### Array implementation of Stack
- Can avoid using pointer and dynamic memory management
- consumes more memory since Array cannot change length (allication the array to a new longer array is an alternative)
	- if `size` is set too large, space is wasted
	- if `size` is set too small, stack overflow happens
- More simple and efficient if have known size stack

### Singly linked-list implementation of Stack
- Better memory management
- Modifications are done at end of linked-list, so there may be more time needed
- If `stackSize` is unknon, use linked list


## Queue
- Insert is done at tail, while delete is performed at head.
- Basic operations:
```python
enqueue(Q,x) # add element x to the tail of Q
dequeue(Q) # return and remove element from the head of Q
```

### Doubly linked-list implementation of Queue
- Procedures of enqueue():
	- add a new tail node
	- point tail from `NULL` to new node

- Procedures of dequeue():
	- make the node after head node as head
	- point head.next().last() to NULL
	- point head.next()to NULL
	- remove head


### Array implementation of Queue
- 2 indices is required, head and tail
```C++
struct Queue {
	int head;
	int tail;
	int length;
	element queue_array[max_cap]; 
}


INIT(q) {
	q.head = 1;
	q.tail = q.length = 0;
}

enqueue(q,x){
	if (q.length == max_cap)
		return(“Queue overflow”);
	tail = (tail + 1) mod max_cap;
	q.queue_array[tail] = x;
	q.length ++;
}

dequeue(q){
	if (q.length == 0)
		return(“Queue underflow”);
	x = q.queue_array[head];
	head = (head + 1) mod maxcap;
	q.length --;
	return(x);
}
```


30/09/2022
## Graph
- set of vertices and set of connections among vertices
- An mathematical object
- Represents relationships beteen objects
- Connections can be directed or undirected

### Representation of an undirected graph
#### Adjacency matrix (2-dimension array)
- When entry`[i,j]` is set to 1, there is connection
-  Space efficiency of Adjacency Matrix: O($V^2$)
- More efficient for operations to see if 2 vertices are connected
Example:
| |0|1|2|3|4|5|6|7|
|-|-|-|-|-|-|-|-|-|
|0|0|0|0|0|0|0|0|1|
|1|0|0|1|0|0|0|0|0|
|2|0|1|0|0|0|0|0|1|
|3|0|0|1|0|0|0|1|0|
|4|0|0|0|0|0|1|1|0|
|5|0|0|0|0|1|0|1|0|
|6|0|0|0|1|1|1|0|1|
|7|1|0|1|0|0|0|1|0|

#### Adjacency lists (Array of linked lists)
- Keep a linked list for each vertex v
- Space efficiency of Adjacency list: O($V+E$)
- More efficient for operations that required to process all edge of the graphs

Example

	0 --> 7
	1 --> 2
	2 --> 3 --> 1 --> 7
	3 --> 2 --> 6
	4 --> 5 --> 6
	5 --> 4 --> 6
	6 --> 3 --> 4 --> 5 --> 7
	7 --> 0 --> 6 --> 2


#### Breadth-first Search
- Start with vertex k
- Visit other vertex that is directly linked to k first
- then visit other vertex that is directly linked to the vertex that is linked to k

First implement:
```C++
BFS(k,n) { /* k = starting vertex; n = number of vertices in the graph */
	Queue Q; /* declare a queue Q */
	bit visited[n]; /* declare a bit vector visited */
	INIT(Q); visited[0..n-1] = all 0’s;
	Q.Enqueue(k);
	while (!empty(Q)) {
		i= Q.Dequeue();
		if (!visited[i]) {
			visited[i] = 1; output(i);
			for each neighbor j of i
				if (!visited[j]) Q.Enqueue(j);}}}
```

Second implement:
```Pseudocode
Data structures: Queue (FIFO) Q+ an array:
	Visited[1..n]: indicates whether a node was put into Q at some point.
Initialization: Visited[i] := false for vertices i; Init(Q);
	Q.Enqueue(k); Visited[k] := true; Output(k); (start at k)
While Qis not empty
	v:= Q.Dequeue();
	For each vertex w in the adjacent list of v,
		if (!Visited[w]) then {
			Q.Enqueue(w); Visited[w] := true; Output(w);
		}
```


Replacing Queue ith Stack:
```C++
Search(k,n) { /* k = start; n = number of vertices in the graph */
	Stack S; /* declare a stack S */
	bit visited[n]; /* declare a bit vector visited */
	INIT(S); visited[0..n-1] = all 0’s;
	S.Push(k);
	while (!empty(S)) {
		i= S.Pop();
		if (!visited[i]) {
			visited[i] = 1; Output(i); Function(i);
			for each neighbor j of i
				if (!visited[j]) S.Push(j);}}}
```


#### Memory usage:
- find the peak memory usage in this program

