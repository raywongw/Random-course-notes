
## Q1

**i) Two processes share the variable I. Process A increments it 10 times. Process B decrements it 25 times. The initial value of I is 0. Process A and B run concurrently, without using any critical sections. Which of the following statements is true?**


A. The final value of I will be –15.
- Race condition, would not be always true

B. The final value of I can be any integer.
- False, there is a specified range

C. The final value of I will be an integer between –25 and 10, inclusive.
- Correct Answer

D. The final value of I will not be 0.
- Not always correct

E. The final value of I can be as small as –20 or as large as 5, but will not fall outside this range.
- False, can be -25 or 10



**II. Which of the following is NOT a requirement for mutual exclusion?**
A. A process that halts in its non-critical section must do so without interfering with other processes


B. A process must not be delayed access to a critical section when there is no other process using it
- Requirement, a process should not stop other process

C. Only one process at a time is allowed in the critical section for a resource
- A requirement to perform mutual exclusion

D. A process remains inside its critical section as long as it requires
- Requirement, You process the information as fast as possible and prevent othrer process from waiting for it

E. No assumptions are made about relative process speeds or number of processes
- Requirement
- When design a solution to concurrent problem
	- Number of execution logic does not need to be cared




**III. True or False: Thread Joining is only used by main thread to wait for and synchronize with its child threads.**
- False
	- Use of pThread_join is most of the time by master thread
	- But it is not limited to other thread to perform synchronization
		- Wait for a thread to perform specific task


**IV. An unsafe state implies ________.**
A. the existence of deadlock
- There is a deadlock **at future**, just don't know when

B. that deadlock will eventually occur


C. that some unfortunate sequence of events might lead to a deadlock
- True

D. none of the above



### Question 2 
**Consider the following code fragment that implements a solution to the mutual exclusion problem for two threads on a single processor (single core only) machine. Argue for its correctness or show a case in which it fails.**
```C
bool t1Inside = false;
bool t2Inside = false;
// T1
while (1) {
/* attempt to enter critical section */
	disable_interrupt();
	while (t2Inside);
		t1Inside = true;
		enable_interrupt();
		//now in critical section
		//exit the critical section
	t1Inside = false;
	}
}

// T2
while (1){
	/* attempt to enter critical section */
	disable_interrupt();
	while (t1Inside);
		t2Inside = true;
		enable_interrupt();
		//now in critical section
		//exit the critical section
		t2Inside = false;
}
```

- The solution may result in deadlock

- T1 enters critical section first
	- t1inside = True
- The critical section is not protected by interrupt
	- May be descheduled when processing critical section




## Question 3
**Consider the following C-like code, which is a solution to the Producer-Consumer problem by using general semaphores.**

```C
buffer[sizeofbufer]; 
semaphore semMutex, notFULL, notEMPTY;
semaphore_init(semMutex, 1); 
semaphore_init(notFULL, sizeofbuffer); // count the available slots in pool
semaphore_init(notEMPTY, 0);           // count the number of tasks in pool

Producer(){
	while (1){
		d = generating_data();
		P(notFULL);  // 1
		P(semMutex); // 2
		append(d, buffer); 
		V(semMutex); // 3
		V(notEMPTY); // 4
		remaining_work();
	}
}

Consumer(){
	while (1){
		P(notEMPTY); // 1
		P(semMutex); // 2
		d = take(buffer);
		V(semMutex); // 3
		V(notFULL);  // 4
		consume_data(d);
		remaining_work();
	}
}
```

i. Swap (1) and (2) in the Producer’s program;
- Causes deadlock
	- Producer holds mutex lock and wait for buffer to be not full
	- Consumer cannot acquire lock and consume data to free buffer spaces

ii. Swap (5) and (6) in the Consumer’s program;
- Causes deadlock
	- Consumer holds mutex lock and wait for buffer to be not empty
	- Producer cannot acquire lock and generate data

iii. Swap (3) and (4) in the Producer’s program;
- No affection
	- Producer perform sem_post of data to buffer before release lock
	- Consumer can acquire lock and release buffer

iv. Swap (7) and (8) in the Consumer’s program.
	Same as iii



## Question 4 
from (2000/01 Examination)
In a fee and salary payment system in HKU Finance Office, there are **hundreds of identical processes** that work as follows. 
Each process reads in an account of fee, the account to be credited, and the account to be debited. Then it locks both accounts and transfers the money, releasing the lock when done. However there is a danger especially with many processes running in parallel that having locked account x it will be unable to lock y because y has been locked by a process now waiting for x (the common deadlock situation). Propose a scheme that avoids deadlocks where you are not allowed to release an account record until the transactions have been completed. Show that your scheme work.

#### Breakdown
- Many concurrent updates

#### Proposed solution
- Deny wait-for condition or circular-wait condition
- Total ordering principle is used to restrict account acquisition order
	- Reason: We can uniquely identify account
	- 



## Question 5 (2006/07 Examination)
Assume a system with four resource types (A, B, C, and D) and five processes (p0, p1, p2, p3, and p4). There are multiple units of each type of resources. 
Is the state of the system safe with the following resource allocation information? Explain your answer. 
If the system is safe, show how all processes could complete their execution successfully. 
If the system is unsafe, show how deadlock might occur.
Total Resources

| A   | B   | C   | D   |
| --- | --- | --- | --- |
| 6   | 4   | 4   | 2   |

Maximum Claim

| Process | A   | B   | C   | D   |
| ------- | --- | --- | --- | --- |
| p0      | 3   | 2   | 1   | 1   |
| p1      | 1   | 2   | 0   | 2   |
| p2      | 1   | 1   | 2   | 0   |
| p3      | 3   | 2   | 1   | 0   |
| p4      | 2   | 1   | 0   | 1    |

Current loan

| Process | A   | B   | C   | D   |
| ------- | --- | --- | --- | --- |
| p0      | 2   | 0   | 1   | 0   |
| p1      | 1   | 1   | 0   | 0   |
| p2      | 1   | 1   | 0   | 0   |
| p3      | 1   | 0   | 1   | 0   |
| p4      | 0   | 1   | 0   | 1   | 


### Solution
- Get future claim table

| Process   | A   | B   | C   | D   |
| --------- | --- | --- | --- | --- |
| p0        | 1   | 2   | 0   | 1   |
| p1        | 0   | 1   | 0   | 2   |
| p2        | 0   | 0   | 2   | 0   |
| p3        | 2   | 2   | 0   | 0   |
| p4        | 2   | 0   | 0   | 0   |
| Available | 1   | 1   | 2   | 1   |

First state: p2 can be completed
After p2:

| Process      | A   | B   | C   | D   |
| ------------ | --- | --- | --- | --- |
| p0           | 1   | 2   | 0   | 1   |
| p1           | 0   | 1   | 0   | 2   |
| p2(finished) | -   | -   | -   | -   |
| p3           | 2   | 2   | 0   | 0   |
| p4           | 2   | 0   | 0   | 0   |
| Available    | 2   | 2   | 2   | 1   |

Second step: p0, p3, p4 can complete
choose one that allow max amount of process to be complete after this
p0 can release resource D to p1 -> allocate resource to p0