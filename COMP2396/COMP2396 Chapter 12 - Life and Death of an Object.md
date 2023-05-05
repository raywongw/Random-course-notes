
[[COMP2396 Chapter 11 - Network and Multi-threading|Last Chapter]] [[COMP2396 Chapter 13 - Exception Handling|Next Chapter]]

#### Stack
- Scratch space for storing execution threads
- Last in First out
- Local variable in stack

#### Heap
- Object's location
	- All class inherit from Object will be in heap
	- Instance variables of objects also
- Dynamically allocated
- Garbage-collecting heap
	- Objects not used will be 


#### Role of Superclass Constructor
- all inherited superclass will be constructed upon creation of a subclass
	- e.g. Object -> Animal -> Mammal -> Human
	- Sequence of creating human: Object -> Animal -> Mammal -> Human