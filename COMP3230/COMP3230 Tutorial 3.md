Question 1 (2006/07 Assignment)
Suppose the page table for the process currently executing on the processor looks like the following. All
numbers are decimal, everything is numbered starting from zero, and all addresses are memory byte
addresses. The page size is 1024 bytes.

| Virtual page | Valid bit | Reference bit | Modify bit | Page frame number |
| ------------ | --------- | ------------- | ---------- | ----------------- |
| 0            | 1         | 1             | 0          | 4                 |
| 1            | 1         | 1             | 1          | 7                 |
| 2            | 0         | 0             | 0          | -                 |
| 3            | 1         | 0             | 0          | 2                 |
| 4            | 0         | 0             | 0          | -                 |
| 5            | 1         | 0             | 1          | 0                  |

What physical address, if any, would each of the following virtual addresses correspond to? (Do not try
to handle any page faults, if any)
i) 1052
To binary:
0100 0001 1100

offset ->11100_2 -> 28

floor(1052/1024) -> VPN
Get PFN -> 7
Physical address: 7 x 1024 + offset(28)


ii) 2221



iii) 5499
To binary




## Question 2
Given a system that uses 12-bit addresses and pages of size 32 bytes. Assume each page table entry is 2 bytes.


a) If a single linear page table is used, how many frames are needed for the page table?


b) If multi-level page table is used, how many levels of tables and what should be the logical address format?
8 frame for whole linear page table
divide whole linear page table to 8 pieces
each piece have 32 byte/2byte

c) Consider a system is using the above multi-level scheme. The contents of some of the physical page frames are shown below. Each frame has 32 bytes and the bytes are order from left to right and bottom to top. The number appears on the bottom-left of each frame is the page frame number.





## Question 3 (2000/01 Examination)
A computer whose processes have 1024 pages in their address spaces keeps its page tables in memory. The overhead required for reading a word from the page table is 100 ns. To reduce this overhead, the computer has an associative memory, which holds 32 registers, and can do a look up in 20 ns. What hit ratio is needed to reduce the mean overhead to 40 ns.

- Associative Memory -> TLB: 32 register
	- 20ns lookup time (TLB Hit time)
- Main memory -> 100ns
	- TLB miss time

Solution
Let X be the hit rate
$X \cdot 20\% + (1-X) \cdot (20+100+20) = 40ns$
for miss, 20ns for lookup TLB, 100ns for lookup main mem, 20ns for TLB lookup



## Question 4 (2007/08 Examination)
In a paged-segmented system, a virtual address consists of 40 bits of which 14 bits give the displacement, 12 bits are a segment number and 14 bits are a page number. Calculate:

What is page-segmented system



Given:
- Virtual addr: 40 bit
- 14 bit displacement
- 12 bit segment number
- 14 bit page number


i) page size
2^14 = 16KiB


ii) maximum segment size
2^(40-12) = 2^28 = 256 MiB

iii) maximum number of segments


iv) maximum number of pages.



## Question 5 (2002/03 Examination) 
Consider a memory system with 5 frames, initially empty. Pages are numbered between 1 to 10. Suppose the clock page algorithm is used to control frame allocation. Show the events that occur when pages are requested in the following order:
1 2 1 3 4 5 6 2 3 7 8 7 2 9 10

1: miss


if full: 
if use bit is 0: replace and change new page use bit to 1
if use bit is 1: move pointer and set previous use bit to 0
