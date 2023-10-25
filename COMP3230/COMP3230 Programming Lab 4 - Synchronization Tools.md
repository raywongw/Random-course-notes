
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