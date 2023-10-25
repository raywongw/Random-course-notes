
[[COMP3230 L5 - Thread Abstraction and Concurrency|Previous Chapter]] [[COMP3230 L7 - Deadlock|Next Chapter]]

# Synchronization Tools

## Mutual Exclusion
- Mechanism to inform OS a thread enters a critical session

#### Lock
- locking a critical section
- data structure to indicate start and end of critical section
	- ask system to protect the data in the region
- either free or locked
- Need to avoid being preemptied when thread using critical section
	- Only available in kernel under privilege mode


#### Atomic Instructions
- Special atomic hardware instructions
- **Test and Set Instruction**
	- Test the old value while setting the variable to new value
	- Check if the 
- **Compare and swap**


### Condition Variables
- Data structure designed to support synchronization between threads


#### 

### Producer-Consumer Problem
- Bound-Biffer problem


- Synchronization requirement
	- Buffer pool is shared resource, producers and consumers need to use some method to coordinate the access to the pool
	- A producer must not overwrite a buffer when buffer pool is full
	- A consumer must not consume an empty buffer when buffer pool is empty
	- Mutual exclusion
	- Information must be consumed in FIFO order

#### Solution
- Wait for buffer pool becomes not full
- 