
[[COMP3230 Programming Lab 2 - Communicaton between process|Previous Lab]] [[COMP3230 Programming Lab 4 - Synchronization Tools|Next Lab]]

# Thread
- share same pid as main thread
- 



## Precaution when using pThread
- Include pThread header file
```C
#include <pthread.h>
```
- Compile with pthread flag
```bash
gcc prog.c -pthread -o prog
```

## Create a thread
```C
// function for theread to compute
void *func1(void *arg){
	intx = *((int*)arg);
	printf("The integer passed in is%d\n", x);
	printf("Thread: Process id is %d\n", (int)getpid());
	pthread_exit(NULL);
}

// thread creation
pthread_t thread;
pthread_create(&thread_id, NULL, func1,(void*)&x);

```
- use `pThread_create()
	- first argument: Address of thread
	- Second argument: Attribute of pThread
	- Third argument: Function to be passed
	- Fourth and further: Arguments to be parsed


## Get return values from pThread
```C
int * ret_ptr;

// get return value
pthread_join(thread_id, (void **)&ret_ptr);
```
- pass the address of the pointer into second argument

## Thread Management Function
```C
pThread_self(void);
```
- Returns the currently executing thread's handle

```C
int pthread_equal(pthread_t t1, pthread_t t2);
```
- Return 0 when two are not equal
- Return non zero value if equal

### Get thread id
```C
// All platforms
(int) pthread_self();
// Linux-Specific thread id
(int)syscall(SYS_gettid);
```



## Cancellation
- When the thread is not needed anymore
```C
int pthread_cancel(pthread_t thread);
```
- Sends cancellation request to thread
- The target thread can **ignore**, **handle it**, or wait till a cancellation point

**Setting cancellation state for thread**
```C
int pthread_setcancelstate(int state, int* oldstate);
```
- Can be set tp (1)PTHREAD_CANCEL_DISABLE or (2)PTHREAD_CANCEL_ENABLE <- default


##### Cancellation point
- A location in code that thread cancels
- Most system calls results so

## pThread Lock
- Mutex variable
```C
pthread_mutex_t lock;
```
##### Initializing mutex lock
```C
// Static
pthread_mutex_t lock = PTHREAD_MUTEX_INITIALIZER;
// Dynamic
pthread_mutex_init(&lock, NULL);
```
- For Dynamic way, second argument is the attribute of lock


##### Lock and Unlock
```C
int pthread_mutex_lock(&lock);
int pthread_mutex_unlock(&lock);
```
- When lock is free and a thread perform lock
	- lock becomes locked
	- thread can access critical section
- When lock is locked
	- Block the calling thread from locking until unlocked
	- Thread will wait until the mutex is unlocked
