
[[COMP3230 L12 - File and Directories|Previous Chapter]]

## Management of Files and Storages
- some way is needed to store the metadata of files on disk
- Types of on-disk structure for file systems to organize data

### Superblock
- some disk block store content of whole disk
- Windows equivalent: Master File Table

Contains
- File System Identifier
- Number of inodes and data blocks available in the filesystem
- Location of inode table, inode bitmap and data block bitmap
- Info of inode of root directory
- 

 
 
### Inode table
- Array of File Control Block
-



## Caching and Buffering
- Case: Open a file at `/home/ray/testing.txt` without touching its content
- Each file open take 2 read operation for each level in directory hierachy
	- 2 read for `/`, `/home`, `/home/ray` and 1 read for inode of `testing.txt`
- Important blocks are cached at physical memory
	- Frequently used blocks?
	- first time opening a file requires a lot of I/O
	- File opening onwards results in cache hit -> require no IO


## Access Control and Protection
- Each user is assigned a Unique User ID and Group ID(if applicable)
- Make access dependent on identity of user
	- Each file has associated access control list (read, write, execute)
	- 3 class of users: Owner, Group, Public (rwxrwxrwx)
	- 3 access control as a unsigned number (eg `chmod 700` results in only owner has all access to this file)
	- can be stored in inode for security and efficiency

## Integrity Protection
- System crash -> inconsistency in files and filesystem
	- System fails during file creation/writing leads to inconsistency in a file
- Solution
	- Routine Backup
		- Duplicate superblock to save as backup
		- Whole disk physical backup by `dd`
		- Logical backups
	- Consistency Checking
		- Compare data in directory and try to fix the inconsistency in files and filesystem
		- Windows: `chkdsk`
		- Linux: `fsck`
			- Check superblock to find suspected corruption
			- scan inodes state
			- scan inodes direct and indirect block pointers to build correct free block bitmap
			- scan all inodes to build the Free inode bitmap


## Journaling File Systems
- Example: NTFS, ext3 and ext4
- Log all file system operations to ensure system integrity
	- Each update is logged as transaction and labelled by a number
	- Once written to log -> transaction committed
- Open a file and append data block to end of file
	- Log inode to be replaced
- If transaction is incomplete -> revert changes