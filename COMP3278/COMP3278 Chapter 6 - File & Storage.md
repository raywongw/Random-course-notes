
[[COMP3278 Chapter 5 - Relational Database Design|Last Chapter]] [[COMP3278 Chapter 7 - Indexing |Next Chapter]]

### Storage Media

##### **CPU Cache**
- extremely fast memory
- volatile
- manage computer system hardware
- noticing cache effects when designing query processing data structure and algorithm


##### **Main Memory**
- Volatile
- Fast access (in nanoseconds)
- Too small to store entire database


##### **Magnetic Disk**
- Non-volatile
- Long-term storage of data
- Much slower access time

###### Read-Write Heads
- very close to platters
- read and write data to the disk
###### Platters
- 2 surfaces covered with magnetic material
- divided into circular tracks
- ~50,000 to 100,000 tracks per platter
###### Sectors
- Smallest unit of data
- located in tracks
- typically 512 bytes per sector

###### Ways to read/write data
- Seek
	- Position the head onto the right track
- Rotation
	- Spint he disk to locate to the start of data


##### Access time
- Time between request and start of data transfer

###### Seek time
- Time required to move arm to correct track
- around 2 to 30 ms

###### Rotational latency
- Time required to rotate the platter until the required sector os under disk head
- around 4 to 11 ms per rotation

##### Data transfer rate
- rate of data retrieved from or to disk
- 25 to 300 MBps
- bounded by disk controller;s processing speed


##### Data block
- Data transfer unit between disk and memory
- size of multiple sectors (4kb to 16kb)
- whole block is transferred when that block contains the item needed


##### IO operation
- Time required to read/write a block
- Seek time + rotational delay + transfer time
- Efficiency: 
	- Time required to move data dominates the cost of proessing query








##### Magnetic Tape
- usually commercial use
- offline backup and archive
- Non-volatile
- Slow and only sequential access


##### Optical disk
- Non-volatile
- Slower read speed
- Wrote once, read many


##### Flash Memory
- Non-volatile
- Read Write: in terms of page, typically 4kb
- Limited program/erase lifetime


### Storage hierarchy

- Put all data on disks
	- Data must be maintained after power failure
	- Storage capacity must be big enough for all data
- Use memory for temporary storage and manipulation of data during queries
	- Selected data are transferred to memory for fast processing
	- Updates are first performed in memory and later written back to disk
- Backup data on tertiary storage
	- Periodically backup the contents of DB on tapes

CPU Cache -> Main memory -> Magnetic Disks -> Magnetic Tape



### Reliability and efficiency

Reliability
- Hard disks may fail, but we don’t want to lost our data.
Efficiency
- Disks are slow compare with the speed of CPU
Solutions
- Mirroring
- Data striping
- Error correction schemes

##### Disk failure
**Mean time to failure (MTTF)**
- Avg time the disk is expected to run without failure

**Mean tome to data loss**
- depends on MTTF and how disk organized


##### Mirroring
- Store a redundant copy on other disk
	- longer Mean time to data loss
- Efficiency
	- read requests rate is doubled
	- Speed of each read is same as single disk system


##### Data striping
- Partition data to several disk
- Data can be read in parallel
	- Faster read

##### Parity check
- Spread the data block to different disk
- Make an extra bit to check for parity
- Even if a disk is lost, it can be recovered quickly


##### RAID
- aka redundant array of independent disk
- more reliability but more expensive
- various level of striping, mirroring and error correction strategy

###### RAID 5
- giving a parity bit to different disk
- one disk fail, other disk can quickly recover data from it





### File organization
- Database store records in file
- Large scade DBMS does not store data on OS
	- allocate a large operating system file
	- store all relations and data to the one file

###### Blocks
- fixed length storage of file
- units of storage and data transfer

- may contain several records
- Assume no record is larger than block

**Fixed length block**
- Store a number of record to a block

**Variable-length record**
- Storages of multiple record type in same block
- record type allow variable length for one or more field

**Slotted page structure**
- Header
	- number of attribute
	- Size of each attribute
- free space
	- buffer for a block
- Records
	- different records for attributes


**Free List**
- When a deleted record



###### Heap File
- No ordering, can be at anywhere
	- Simple
	- Hard to search


###### Sequential FIle
- Sequential order based on value of search key
- efficient processing of records in sorted order

###### Hashing
- fixed hash functions
- Most DBMS choose primary key
- maybe be pointers, fixed length or variable length


###### Multitable clustering
- put more than 2 related relation in a same file
	- achieve faster join

- e.g. Department(deptID, name, budget) and Lecturer(lecturerID, name, deptID, salary)
- the table is pre computed by putting dept tuple, followed by lecturer tuples of same deptID
- 



### Buffer
- DBMS seeks to minimize the number of blocks transfers between disks and memory


Buffer
- Portion of memory available to store copies of disk blocks.
Buffer Manager
- program responsible for allocating buffer space in main memory and moving blocks between disk and memory (so that disk I/O is minimized)


