### 1-dimensional structure
- Each element is followed by exactly one element, except for the last which has none
- Example:
	- Linked list
	- Stack
	- Queue

### Multi-dimensional structure
- Each element can be followed by more than 1 element

### Tree
- a [[#Multi-dimensional structure]] 
- There is a node called root
- unordered
- If there is no root node its called a null tree
 - No. of edged in a tree with `n` nodes: `n-1`

#### Leaf node
- a node in the tree that has no child node

#### Internal node
- a node that is not [[#Leaf node]] or 

#### Ancestor-descendant path
- `n1`,`n2`,...`nk` is a sequence of node in a tree
- `ni` is the parent of `ni+1`, for 1<= i < k

#### Implementation of tree with fixed amount of child
```C++
struct tree_node { 
	element ele; 
	tree_node *child[4];
}```

#### Implementation of tree with unknown amount of child
- left branch as child branch
- right branch as sibiling
```C++
struct tree_node { 
	element ele;
	tree_node *lc; 
	tree_node *rs;
}```

#### Traversing a tree
- 3 visiting order: [[#Inorder]], [[#Postorder]], [[#Preorder]]
- Complexity: O(n)

##### Preorder
- Time: O(n)
- Memory: O(d) where d is the depth of a tree
- Usage: traversing a directory
- Code implementation
```C++
PREORDER (n) {
	if (n == NULL) return;
		visit n;
	/* suppose n has k subtrees: T1, T2, ..., Tk */ 
	/* ordered from left to right */
	for i = 1 to k
		/* i.e., from left to right */
		PREORDER (T_i); 
}
```


##### Postorder
- aka Depth first search
- Time: O(n)
- Memory: O(d) where d is the depth of tree
- Usage: remove a directory

- Code implementation:
```C++
POSTORDER (n) {
	if (n == NULL) return; 
	for i = 1 to k
		POSTORDER (T_i); visit n;
}
```

##### Inorder
- Time:O(n)
- Memory:O()


- Code implementation:
```C++
INORDER (n) {
	// for binary trees only
	if (n== NULL) return; 
	INORDER(left subtree); visit n;
	INORDER(right subtree);
}```




#### Binary Tree
- Only has left or right child

##### Full binary tree
- no node in binary tree has a single child

##### complete binary tree
- All leaves of a binary tree are at same depth

##### Code implementation of binary tree
```C++
struct tree_node { 
	element ele; 
	tree_node *left; 
	tree_node *right;
}
```

