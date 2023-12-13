
## Q1: Explain why delete hard link need update inode while soft link does not

- Soft link is a file containing the pathname of another file
	- Delete the soft link only delete the linking, original file would not be touched
- Hard link is a directory entry point to physical address of the file
	- Delete the hard link



## Q2: 12 direct block pointer, 1 singly, double, triple block pointer, System block size and disk sector both 8KiB, Disk Block pointer is 32 bit, 8 bits for identify physical disk and 24 bit to refer the physical block


### 1. Max file size supported by system
- Total number of blocks -> 12

- Indirect ptr:
	- 8 KiB(system block size?) divide by ( 4 byte for each disk block pointer) = 2048 bytes
- Double ptr:
	- Single ptr^2 = 4,194,304 bytes
- Triple ptr:
	- Single ptr^3
- Total
	- (12 + 2048 + 2048^2 + 2048^3) x 8KiB(disk block?) = 64TiB


### 2. Max file system partition size
- 24 bit for identify blocks within a partition of disk
	- 2^24 * ?? = 128 GiB



### 3. only inode loaded, find number of disk access to load byte location at logical pos 13,423,956
- see which block ptr access can cover that
- in this case-> indirect ptr covers 16MiB
- therefore 2 x 1(indirect ptr) disk access needed



## Q3. file of 100 data block by linked list, 1 data block per disk block, File inode and dir loaded to main mem, System has data block bitmap cached in main mem

### 1. Number of disk block access needed to read file block 24
- 24 disk access
	- Linked list -> linear time


### 2. Number of disk access to read
- 100 read disk access + 1 write access to 101th block + 1 write access to 100th block to update link





## Q4: Number of disk ops needed to fetch inode of `/user/home/course/c0230a/lecture.txt`

Assumptions: inode for `/` is a main mem

Tldr: find disk block -> read inode -> ... -> inode ( 2x directory depth)
1. Through root dir, system locate and read the directory disk block and search for /user
2. Disk read to obtain inode of `/user` to get directory disk block for it
3. Disk read for directory block of `/user`, find inode for `/user/home`





## Q5: Min block size such that bitmap is less than 0.1% of total disk space


Assume system has X byte storage space, system block size of D bits
- Size of bitmap: X/8D bytes
- Percentage = 0.1% = 1/8D = 1/1000, D = 125 Byte