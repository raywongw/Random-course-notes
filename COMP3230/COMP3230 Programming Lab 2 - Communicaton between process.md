
 [[COMP3230 Programming Lab 3 - pThread|Next Lab]]

## Recap - Signal Handling
- OS determines how a process respond to a signal


## signal()
```C
sighandler_t signal(int signum, sighandler_t handler);
```

- setting up signal handler to handle a specific signal



## sigaction()
```C
int sigaction(int signum, const struct sigaction* act, struct sigaction* oldact);
```
- more flexible and powerful

Steps in setting handler:
1. Retrieve old sigaction structure for target signal
	- Current sigaction structure for SIGINT is saved
2. Modify sigaction struct to act with new value
	- Modify corresponding fields (what corresponding fields?)
3. Set new sigaction structure for this singal

## Pipes
- Mechanism for interprocess communication
	- Parent->child
	- child -> child
	- forking child(s)
- pipe is FIFO
- Parent creates the pipe for use


### Properties

Blocks process from writing to pipe till data can be written to it
- Can customize behaviour

Block process from reading from empty pipe till there is data
- Return 0 to the process when performing `read()`

SIGPIPE will be generated from writing to a closed pipe
- -1 to the `write()` at the same time

### Example - Linux Commands
```bash
cat demo-txt2.txt | grep process | wc-l
```
- [[#Pipes]] are used to transfer data to next process to be run
- 