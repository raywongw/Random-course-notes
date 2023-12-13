
[[COMP3230 Programming Lab 3 - pThread|Previous Lab]] [[COMP3230 Programming Lab 5|Next Lab]]
## pThread condition variables

### Creation
```C
// Static
pthread_cond_t cond= PTHREAD_COND_INITIALIZER;
// Dynamic
pthread_cond_init(&cond, NULL/*Pass the status here*/);
```

- Declared and initialized before used

### Destruction
```C
pthread_cond_destroy(&cond);
```
- Destroy the condition variable


### Waiting for the Condition Variable
```C
int pthread_cond_wait(pthread_cond_t *cond, othread_mutex_t *lock);
```
- Avoids race condition

- Blocks calling thread until specified consition is reach

- Called after mlock is locked by calling thread
- System release mlock while getting thread to sleep


### Signaling
```C
// Signal one thread
int pthread_cond_signal(pthread_cond_t*CV);
// Signal all thread
int pthread_cond_broadcast(pthread_cond_t* CV);
```
- Single thread singal should be called by a thread that acquired the lock and unlock the lock after calling


## POSIX Semaphores
```C
#include <semaphore.h>
```
- include **semaphore.h** to use semaphores
- General data structure as `sem_t`
- To control access 

### Initialize and Destroy a semaphore
```C
int sem_init(sem_t* sem, int pshared, unsigned int value);
```
- sem as a pointer to the semaphore object
- pshared to indicate if the semaphore is local to the process
- value as the initial value


### sem_wait()
- Ask the process to wait on a semaphore
```C
int sem_wait(sem_t *sem);
```
- Textbook view: The calling thread will not return from call if the value in semaphore is below 0
- Linux implementation: semaphore's value will not be below zero for whatever reason
	- sem_wait decrements the semaphore if it is above 0 and returns 0
	- sem_wait call is block if semaphore is 0 until it can perform sem_wait or a interrupt created by signal handler

### sem_post()
- Increment the value of semaphore