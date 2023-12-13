
[[COMP3230 L11 - Finding Free Page Frame|Previous Chapter]] [[COMP3230 L13 - File System Implementation|Next Chapter]]

## Secondary Storage
- Random-access storage


## File Systems

- File Management: Provide services to user and apps
- Storage Management: Allocate space for files
- File Integrity: Guarantee file in data are valid
- Security: Data in file should have strict access control




## Directory
- A file of mapping to valid files under it
- 
### Directory Structure
- Hierachically Structured File System
	- Directories within directories
	- Starts with root directory `/`
	- absolute path as full name of the file
		- e.g. `/home/ray/testing.txt`
	- relative path as shorter name, with current working directory as 
		- e.g. `testing.txt`
#### Link
- mechanism to link 2 directory entry to a file in other directory
-


##### Hard Link
- Map a directory entry with same low-level id of original file
- Remove the directory entry will not delete the original file

**Limitations**
- Cannot hard link to directory
- Cannot create hard link to files in other disk


##### Symbolic Link
- 