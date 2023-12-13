
[[COMP3230 L9 - Segmentation and Paging|Previous Chapter]] [[COMP3230 L11 - Finding Free Page Frame|Next Chapter]]
## Make Transition Faster
- Hardware Support -> TLB
	- High speed cache in MMU
	- Recent/frequently used virtual-to-physical address translation mappings are cached in TLB
- Good performance in address translation
	- Temporal locality
		- 
	- Spatial locality
		-  e


## Address Translation with Hardware-managed TLB
![[Pasted image 20231114115003.png]]
Lucky path: TLB Hit
- Able to access physical memory

Unlucky path: TLB Miss
- MMU then access the process's page table for content
- Get page frame number


## TLB Issues
- All mappings in TLB only relavant to current running processes
- Can TLB be shared with other process
	- Yes
		- How MMU identify set of TLB entries relaxant to current running process
	- No
		- CPU have to flush TLB during context switch
		- Some TLB misses will be experienced by the newly switched process
- Large TLB are costly
	- Usually with $2^{5-7}$ entries
- Which TLB entry to kick if it is full
	- Lease Recently Used Policy


## Make Smaller Page Table
- Page Table used too much physical memory
	- 32 bit system with 4KiB page size -> 4MiB page table
	- Increase page size to 16KiB -> 1 MiB page table
		- High chance of internal fragmentation
		- Longer page loading time
- How to make page table smaller
	- Not all PTE refer to valid virtual pages


### Multi Level Page Table
- Chop page table to multiple page sized unit -> split to page frames
	- Each unit is a part of stored in one page frame
- Only allocate page frames with entries toa smaller page table
- Add a page directory for valid "smaller" page table
	- n page directory for n page table segment
	- Valid bit and the page frame number to derive the location

##### Performance penalty
- Save memory yet more time to process
	- Time-Space Trade-off
- TLB Miss require 2 extra memory access to get right translation information
	- Access page directory to get physical address of specific page frame
	- Access specific page frame to find 
	- TLB hit is usually >80%


##### Real World Case: IA-32e
- 48 bit memory address- Number of PTEs = 36 bits
- Number of page frame: $\frac{2^{36}}{2^9} = 2^{27}$ page directory table
- Number of Page Table Entry in each page frame: $\frac{2^{27}}{2^9} = $

### Inverted Page Table
- Only in high end systems
- 