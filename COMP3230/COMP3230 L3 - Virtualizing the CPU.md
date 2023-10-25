
[[COMP3230 L2 - Process Abstraction|Previous Chapter]] [[COMP3230 L4 - Process Scheduling|Next Chapter]]
### Process Control
- System calls for restricted operations
- Virtualizing CPU
	- Provide illusion of many CPUs


### System Calls
- Process voluntarily release CPU
- Allow kernel to carefully expost ceratin key services to aplications
	- Most OS has a few hundred
- Accessed via High-level API
	- e.g. Windows API for Windows, POSIX API for POSIX-based Systems (UNIX, Linux, macOS)
- Caller only need knowledge on standard API to invoke System Call and values returned
	- Details of OS will not be exposed to programmer
	- Same API provided by different OS platforms
		- Dev does not need to develop different OS-specific platforms


#### Implementation of System Calls
- Library call has a special machine instruction that cause trap
- transfer control to kernel

### Interrupts
- Process involuntarily release CPU

### Context Switching
- Provide illusion that a process has its own CPU
- Run a process and stop it to run another

Crux
- How to transparently and temporarily stop a process and resume
- How OS regain control of CPU


#### Implementation of Context Switch
- Remove a process from running to other state
1. Save context of current running process before stopping it
2. Restore the context of process to be started before resuming

##### Mode Switch
1. Switch from user mode to kernel mode
2. Kernel execute "On behalf of current interrupted process"
3. Process's content can still be accessed in [[COMP3230 L2 - Process Abstraction#Address Space|address space]]
4. Upon exiting kernel, process may resume
	- The process may have to be switched to ready mode


##### Context Switch
- Switching from process to to other process
- Essential feature for Multiprogramming and time-sharing systems
1. Kernel suspends progression of current process and stores context
	- Save the current process's execution context to its kernel stack
	- Save the current process's kernel stack and memory to its [[COMP3230 L2 - Process Abstraction#Process Control Block|PCB]]
	- Change the current process's state in [[COMP3230 L2 - Process Abstraction#Process Control Block|PCB]] to appropriate status
2. Retrieves context of another process and restores it to CPU
	- Scheduler select a ready process according to scheduling policy
	- Load the selected process's kernel stack and memory from [[COMP3230 L2 - Process Abstraction#Process Control Block|PCB]]
	- Load the selected process's execution context from kernel stack
	- Update the selected process's state
3. resumes execution of another process

- OS must minimize time required for context switching
	- Reduce time for execution process



###  Ways to regain control of CPU

#### Passive approach
- Waits for a process to make system calls or illegal operation
- Process may get into a inf loop and never makes a system call

#### Active approach
- Requires hardware support
- A timed device generate interrupt periodically
- OS handles interrupt 