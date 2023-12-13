
[[COMP3230 L10 - Translation-Lookaside Buffer and Hierarchical Tables|Previous Chapter]] [[COMP3230 L12 - File and Directories|Next Chapter]]

### Not enough Physical Address Memory
- Process' address space is large
	- 48-bit -> 256 TB
- Limited Physical Memory


## Swap Space
- A space in disk to swap physical memory from and to it
- Store process' memory
- not managed by file management
- located at consecutive blocks to enhance disk r/w performance
	- no need to search on whole disk for the process' memory

## Page Fault
- A type of exception
- Happens when processor founds that the page is valid but not on memory
Procedure for handling page fault
1. OS' page-fault handler then proceeds to get disk address from [[COMP3230 L9 - Segmentation and Paging#Page Table Entry|Page Table Entry]]
2. Go to disk address of page in [[#Swap Space]]
3. Issue a I/O request to move the page to memory
4. OS place current process in blocked state, performs context switch to move to other ready proccess
5. After I/O finished, OS update page frame number(index of L10 PTE) and present bit of [[COMP3230 L9 - Segmentation and Paging#Page Table Entry|Page Table Entry]]
6. Unblock process and let process to retry
	- Causes a TLB miss -> 

## Page Replacement policy
- Ways for OS to choose which virtual page to be moved to disk space
- 
## Ways to replace page

### Optimal Replacement
- Replace the old page that will be accesed in the farthest time in future

**Advantage**
- Fewest page fault

**Disadvantage**
- Cannot predict future


### First-In-First-Out Replacement
- Kick the oldest page in system


**Advantage**
- Easy to implement
- Very few extra processing time(overhead)

**Disadvantage**
- May replace the oldest page which is used heavily
- Not practical for real-life system




### Least-Recently-Used Replacement
- Kick the page that is not referenced for longest time


**Advantage**
- Better performance than FIFO
	- Leave most used page in memory
- 

**Disadvantage**
- Increased overhead
	- Need to maintain timing of all page
	- OS scans all time fields of page to find a least recently used page
### Least-Frequently-Used Replacement
- Kick the page that is least frequently used
- If 2 page are same, kick the older page


**Advantage**
- Keeps frequently accesse page in memory

**Disadvantage**
- Freuqently used page in past may be kept in memory
- Additional counter needed for each page


### Approximating LRU
- Use a reference bit to indicate if a page is recently referenced
- System have to clear the bit periodically
	- Eventually all page will be used if not
- Bit is set to 1 by hardware, OS have to clear that on some time


### Clock Replacement
- Similar to [[#Least-Recently-Used Replacement|LRU Replacement]]
- Pointer to point to oldest virtual page
- If the use bit is 0, replace this page

**Advantages**
- Simple and efficient to implement
- Balances between LRU and FIFO algorithms
- Gives “second chance” to pages in use

**Disadvantages**
- May not provide optimal solution
- Requires overhead to maintain “second chance” bit
- Can lead to more page faults








## Summary
- Virtual Memory system gives an illusion to the process that it has large amount of main memory to store the process’s address space
- In real life, physical memory is scare resource; OS makes use of slower, larger disks to support the virtualization of memory
- When the CPU tries to access a virtual page that is not in physical memory, OS will be invoked to handle this; it is responsible to load the page from swap space to main memory
- If the system does not have enough free physical memory, OS needs to make the decision in selecting some pages to swap out
- Page replacement policy is critical to system performance; a wrong decision will induce more page fault 
- Realistic replacement policies make use of past accessing history to guide the OS in selecting suitable pages for eviction
- LRU and LFU are performing better than others; however, they are more complicated and have higher implementation overhead
-  Thrashing will be appeared if the system is oversubscribed with too many running processes
