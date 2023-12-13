
[[COMP3230 L3 - Virtualizing the CPU|Previous Chapter]] [[COMP3230 L5 - Thread Abstraction and Concurrency|Next Chapter]]
# Process Scheduling
- Selection of next process or thread to be serviced by processor

Policy influences the following:
- QoS provided to users
	- better performance and user satisfaction
- Effective resources usage
	- Minimizing process switching 
	- Better scheduling decision impacts efficient use of CPU
- System performance
	- Maximize number of processes completed per unit time

## Scheduling Levels
### High Level/Long Term Scheduling
- Creating processes
- Control number of processes in system at one time
### Intermediate Level/Medium Term Scheduling
- Which process should be allowed to be completed by processor
- Control swapping process in and out
- Respond to fluctuations in system load
### Low Level/Short Term Scheduling
- Choosing the next process for a certain processor
- Assigning the processor to the process

## Scheduling Terms and Concepts
### CPU-Bound process
- Process tends to use all the processor time allocated
- Process run faster if CPU is faster
### I/O Bound process
- Process tends to use very few CPU usage while generating I/O request
- Process run faster if I/O subsystem is faster
### Turnaround Time
- Time required to execute a process from submission to complete service
- To be minimized for enhanced system performance

### Waiting Time
- Time of a process waiting in ready queue
- Turnaround time - CPU time 

### Response time
- Time required from process arrived to system to system process the process
- Performance metric of interactive task
- To be minimized

### Throughput
- Average number of process complete execution per time
- To be maximized

### Fairness
- Equality of processes



## Scheduling Algorithm

### Workload Assumptios
- All process only uses CPU and No I/O
- Jobs with I/O is counted as a CPU Burst
- Duration of runtime of each process is known

### Algorithm Evaluation
- Evaluate the performance of algorithm with pre-determined workload


### First-in-First-out Scheduling (FIFO)
- First Come First Serve
- Process are handled according to arrival time
- non-preemptive


**Advantages**
- Fair to all processes
- Easy to implement

**Disadvantages**
- Short process waits longer if they are behind CPU-bound process
- Interactive process takes longer to execute
	- Less repponsive


### Shortest-Job-First Scheduling (SJF)
- Short-Process-First
- Process with shortest CPU burst is selected to run next
- non-preemptive


**Advantages**
- Lower average wait time than FIFO
	- Reduces queue of waiting processes
	- Better in terms of average wait time

**Disadvantages**
- Short jobs have to wait for a running CPU-bound job
	- Slow response time

- Starvation of long process
	- Longer process have to wait for all short process
	- Higher variance in wait times


### Highest-Response-Ratio-Next Scheduling (HRRN)
- non-preemptive
- Priority on predicted service time and time waited
- $\text{priority} = \frac{\text{Time waited} + \text{Service Time}}{\text{Service Time}}$
- Shorter process are favored for scheduling
- Aging effect
	- Prevent indefinite postponing process


**Advantages**
1. HRRN Scheduling algorithm generally gives better performance than the Shortest Job First (SJF) Scheduling
2. It not only favors the shorter jobs but also limits the waiting time of longer jobs
3. It improves upon SPF scheduling and prevents indefinite postponement

**Disadvantages**
1. The on-ground implementation of HRRN scheduling is not possible as it is not possible to know the burst time of every job in advance
2. In this scheduling, there may occur overload on the CPU
3. It does not support an external priority system


### Shortest Time-To-Completion First Scheduling (STCF)
- Preemptive version of [[#Shortest-Job-First Scheduling (SJF)|SJF Scheduling]]
	- Process may be interrupted and switched to other process

**Procedure**
1. New process arrive and another process is running
2. Scheduler check the remaining time for current process to complete
3. Compares the time with new process's processing time
4. Choose to run the one with shortest run-time-to-completion
	- If 2 process in queue have same run-time-to-completion
		- random choose one
		- Choose one that waits longer in queue


**Advantages**
- Low waiting time
- Low turnaround time
- Low response time

**Disadvantages**
- large variation in waiting time
	- long process may have to wait much longer than in [[#Shortest-Job-First Scheduling (SJF)|SJF Scheduling]]
- Not always optimal
	- Short incoming process preempt running process that is near completion
	- More context switch -> affect performance


### Round-Robin Scheduling (RR)
- preemptive
	- Time interrupt
- Keep process in ready FIFO
- Process run for a limited amount of time and switch to next process
	- Current process is placed at end of ready queue

**Advantages**
- Fair
- Low average response time
	- Interactive processes are switched and can be completed in a short time

**Disadvantages**
- High turnaround time
	- Process are constantly switching

##### Time quantum
- Unit time for each process to be switched
	- Usually 100ms and around 10ms to 200ms

- Large quantum size
	- Process run longer
	- Less context switch
	- Degenerates to FIFO
- Small quantum sizze
	- More context switch time than running process
- Sweet spot
	- Long enough for interactive process to finish
	- Long process still get majority of process time
- 


### Multi-level Feedback Queue Scheduling (MLFQ)
- Different queue with different priority level
- Scheduler choose a lower priority queue process only if higher priority queue is empty
- [[#Round-Robin Scheduling (RR)|Round-robin]] for process at same level
   
#### Priority of process
- Dynamic priority is used
	- based on time, behaviour prediction
- New submitted processes enter the highest priority queue
- If a process uses up its quantum, it is preempted and positioned at the end of the next lower level queue
	- Long processes repeatedly descend into lower priority level
- If a process relinquishes the CPU before quantum expires, it stays at the same priority level
	- We don’t want to penalize interactive job and keep them at the same priority level

#### Deficiency
- Process in lower queue can be in starvation
	- Too many interactive process
	- Issue for priority based scheduling
- Misbehaved process can steal CPU time
	- Making the scheduler thinks this process is a short job by relinquishes CPU before time quantum expiration
- Process may become I/O Bound from CPU Bound
	- Cannot be treated as interactive process due to previous execution

#### Adjustment
- Starvation
	- Periodically boost priority of process in system
	- Long process gets a chance to run
	- I/O Process turned from CPU-Bound process can be treated correctly
- Different time quantum length
	- Scheduler increases process quantum size for lower queue
	- $2^{k-i}$ where i is number of queue and i is current level
- Unfair usage by misbehaved process
	- Memorise process behaviour at each level
	- process demoted when used up CPU time at given level

### Multi-level Feedback Queue
- Responds to change of behaviour of environment
	- Process moved to different queue if they switched from interactive and batch behaviour
- Increased scheduler sensitivity but incur more overhead


### Fair Share Scheduling
- Previous scheduling policies applied to individual process
- Scheduling decisions based on process groups
	- User assign a weighting that indicates their share of system resource
	- FSS monitor resource usage to maintain the fraction allocated in fair share


### Lottery Scheduling
- Random allocation to achieve fair share
	- Resource consumption rate proportional to relative shares allocated
- Lottery tickets are distributed to all process
	- Basis of fair share CPU time
- Ticket chosen at random during scheduling
- Important process have higher chance as they are given more tickets
- A process will get $t \cdot \text{fraction of tickets}$ second of time given t is large

### Multiprocessor scheduling

#### Single-queue Scheduling
##### Deficiency
- Poor scalability


#### Multi-queue Scheduling
- One scheduling queue per core
	- On random basis/workload/nature of process



Pros
- Less concurrency issue
- Cache affinity
Cons
- Load imbalance
	- Some queue may have less job than other queue
	- Solution: Migration of jobs by work stealing
		- A queue with less jobs seeks the length of jobs from other queue
		- steal one or more job from that queue


### Case: Linux Scheduler
- Preemptive and priority-based algorithm
- 2 queues: Real-time level and no real-time level
- Real-time priority: 1(low) to 99(high)
	- SCHED_FIFO: Runs until it exits, sleeps, blocked or preemptied by another newly arrived higher priority process
	- SCHED_RR: RR scheme on real-time process with same priority
	- Real time process cannot postpone other normal processes indefinitely
		- normal users cannot create real time process


#### Completely Fair Scheduler
- non-real-time class from kernel 2.6.23 and after
	- Does not label a process
	- Ensure all process are treated the same
	- Maintain fairness in providing processor time to tasks
- Fairness
	- Divide CPU resource fairly by available runnable process
	- each process gets a fair fraction of CPU time based on number of process
	- Process with higher weighting factor receives larger proportion of CPU time
