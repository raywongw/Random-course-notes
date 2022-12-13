
### Balancing a search tree
-

### AVL Tree
- binary tree with a balance condition
	- for every single node, difference of depth of left subtree and right subtree is at most 1
- value of nodes in left subtree must be smaller than root node
- value of nodes in right subtree must be greater than root node

#### Prove AVL tree with n nodes has height O(log n)


### Tree rotation

#### Right rotation
- pair of child oarent node k1, k2 (set k2.left= k1)
- after rotation, k1.right = k2


#### Left rotation
- pair of child oarent node k1, k2 (set k2.right= k1)
- after rotation, k1.left = k2



#### Violation of AVL Tree property
- attempt to perform rotation to restore its property
- Some rotation operation may still violate the property


### Double rotation


### Deletion




