## Binary search on a list
- Examine the middle element
- For linked list, a pointer to middle element is needed



## Binary Search Tree
- Operations:
	- search
	- minimum
	- maximum
	- predecessor
	- successor
	- insert
	- delete
- Worst case: O(log(n)) if tree is balanced

- each node of a binary search tree contains:
	- key 
	- left (pointer)
	- right (pointer)
	- parent (pointer)

- If value in a node desired is smaller than current node, move to left of the node
- To list out all element in increasing order, [[Chapter 5 Tree#Preorder|Preorder]] can be used








## Randomly built BST



## Example
### 1. Given a binary treem give a algorithn to check whether it is a binary tree
- Given a root node, check the BST in left child node is smaller than root
- Method 1: Recursion
	- More extra space is used
	- Simpler program structure
- Method 2:


### 2. Given an array[0,n-1] if element in sorted orderm convert it to a binary search tree
- Node* createTree(A, starti, endi)
- Attempt to create a balanced BST
- 


### 3. Given a linked list of elements in sorted order, convert it to a balanced BST, Try to use as little memory as possible
- Use [[#2. Given an array[0,n-1] if element in sorted orderm convert it to a binary search tree|Q2 Method]], create an array and convert it to a BST



