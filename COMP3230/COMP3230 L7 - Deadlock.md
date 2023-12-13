
[[COMP3230 L6 - Synchronization Tools|Previous Chapter]] [[COMP3230 L8 - Process Address Space|Next Chapter]]

# Deadlock

55

- Each thread are holding the system resources that the other thread want, and cannot release
# Deadlock
- Each thread are holding the system resources that the other thread want, and cannot release 

## How They Occur



## Dining Philosophers
- 5 philisopher sit around a table, thinking and eating spaghetti
- 5 forks are provided
- Eating spaghetti requires adjacent forks to perform
- How to handle problem such that no philosopher is at starve
- No need to worry how long think and eat will happen



## Necessary condition for deadlock
- Any of the condition is not met then deadlock cannot occur

#### Mutual Exclusion condition
- Allow only a thread to have exclusive access to a resource

#### Wait-for condition (Hold and wait)
- Thread may hold some resource that other thread wants

#### No preemption condition
- No resource can be forced to be removed from a thread

#### Circular-wait condition
- Two or more threads are locked in a chain




## Deadlock Prevention
- Use restrictive policy in allocation of resources

#### Prevent Circular-wait condition
- Imposes a total ordering of resources types
- Threads must acquire resources in increasing order


##### Disadvantage
- Poor resource utiliation
	- resources are forced to hold resource of smaller label


#### Prevent hold-and-wait condition
- Thread gets all needed resource at once

##### Disadvantage
- Poor resource utilization
- Possible starvation

#### Mutual Exclusion condition
- Sharable resource
	- most sharable resource does not support this

#### Deny no-preemption condition
- Process is holding some resource and request other resource
- The targeted resource is not available to them
- The thread must release all resources
- Thread only start only if it regain ALL required resource

##### Disadvantages
- Chance of starvation
	- Other threads continuously holding any one of the resource
- Substantial overhead
	- Process may lose progress of work/ undo all work before release


## Deadlock Avoidance
- System tries to avoid deadlock
- Global knowledge on resource requirement needed

#### Avoidance by scheduling
- Schedule threads by resource usage
- Thread of same needs of resource will be scheduled at same CPU core
	- To avoid deadlock by these threads

##### Disadvantage
- Resources not fully utilized
	- Some CPU may not be fully utilized
- Conservative approach

#### Banker's Algorithm
- System only give additional resource if giving resource would not result in unsafe state
- Checking if remaining resource can be allocated feasibly
	- leads to successful termination of processes

Weakness
- Need to know what resources does each thread/process require

|                | max() | loan()    | claim() |
| -------------- | ----- | --------- | ------- |
| T1             | 4     | 1         | 3       |
| T2             | 6     | 4         | 2       |
| T3             | 8     | 5         | 3       |
| Total resource | 12    | Available | 2       |

- max(): Declared maximum usage
- loan(): Current usage
- claim(): Future requests



## Detection & Recovery
1. Allow deadlock to occur
2. System take action periodically to check if deadlock happened
	- If circular wait exists
	- Identify proces sand resources involved
3. Recover from deadlock
	- Some process will become victims
		- 
	1. Abort all deadlock process
	2. Abort process by process
		- Check if deadlock cycle is eliminated
