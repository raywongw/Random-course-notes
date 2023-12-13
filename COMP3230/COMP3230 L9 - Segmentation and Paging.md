
[[COMP3230 L8 - Process Address Space|Previous Chapter]] [[COMP3230 L10 - Translation-Lookaside Buffer and Hierarchical Tables|Next Chapter]]

## Segnemtnation
- Block of contiguius virtual address of a certain length in a process' address space

## Table Entry of Segment Table
Simplified Look

| Base | Bounds | Available Space | G              | R        | W         | E           | V         |
| ---- | ------ | --------------- | -------------- | -------- | --------- | ----------- | --------- |
|      |        |                 | Grow Direction | Read Bit | Write Bit | Execute Bit | Valid Bit |

- Protection Bit
	- Read/Write/Execute Bit
	- Segmentation fault raised if process try to write a read-only segment
- Grow Bit
	- Direction of which the segment can grow
	- Heap go upwards, stack go downwards
- Valid Bit
	- Valid bit should be set to false if 


## External Fragmentation
- Issue occur when allocating memory to segments of different size
- Memory becomes full of process, in between there is a lot of small spaces
	- not enough to hold a small process, but enough to hold some when add up

### Ways to tackle external fragmentation
- Coalescing
	- Attempt to combine free blocks to a large one'
- Compaction
	- Relocating 



## Manage Free Space
- Allocating physical memory for process in segment form while knowing where are free spaces
- Easy approach: free-list
	- Reference to free memory space
	- e.g. linked list with each node containing memory address and spaces available

### Free Space Allocation Strategy
#### Best Fit
- Search the free list and place the segment



## Address Translation
- Each process has its own page table
	- Address translation information of all virtual page of process
- 32-bit address space has $\frac{2^{32}}{2^{12}} = 2^{20}$ virtual pages

- Find out which virtual page that this virtual address is in
- Top left p-bits: Virtual page number
- Remaining bit: offset memory location relative to start of address

## Page Table Entry
- aka PTE


| Page Number | Free Space | Reference Bit (R) | Dirty Bit (D) | Present Bit (P) | R   | W   | E   | Valid Bit (V) |
| ----------- | ---------- | ----------------- | ------------- | --------------- | --- | --- | --- | ------------- |
|             |            |                   |               |                 |     |     |     |               |


### Dirty Bit
- Indicate if the virtual page is modified since it brought into memory