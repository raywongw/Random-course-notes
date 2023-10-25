
[[COMP3230 L4 - Process Scheduling|Previous Chapter]] [[COMP3230 L6 - Synchronization Tools|Next Chapter]]
## Threads
### Thread of execution
- Sequence of instructions to perform a task
- traditional process -> process with a thread


### Multithread process
- Process with multiple thread of execution
	- Multiple sequence of instructions that can execute concurrently
- Threads are entities in a process
- Shared address space for threads to work with
- threads has its own registers and stack to work with different instructions
- 


### Concurrency Issue
- Uncontrolled Scheduling
	- Cannot predict when a thread executes
- Race condition
	- Several thread access shared data item
	- Output depends on when threads executes sequence
####