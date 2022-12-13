#### Master Theorem
T(n) = a.T(n/b) +n^c.    a,b,c are constant and b > 1
T(1) = theta(1)

T(n) >= a.T(n/b) -> a^2 .T(n/b^2) -> a^k.T(1) = a^log(b,n) = n^log(b,a) (repeat k = log(b,n))


compare n^c and n^log(b,a)
case 1: log(b,a) > c 



Akra-Bazzi(more advanced)

/28-10-2022
#### Building an egg problem

- n: number of floor
- k: no of egg

##### Objective:
1) Find critical height of egg
2) Use min number of probes

T(n,k) = min of probes to solve problem correctly

##### Case 1: k=1
- [[Chapter 6 Search#Linear search|Linear Search]] must be done
- Worst case: probing every floor, $O(n)$

##### Case 2: k > $log_2(n)$
- [[Chapter 6 Search#Binary Search|Binary search]] can be done
- Worst case: 

##### Case 3: k = 2
- Throw a egg at half n
	- Best case: $O(log(n))$
	- Worst case(egg broke): $O(n)$


- Another way: [[Chapter 6 Search#Jump search|Jump search]] can be done
	- use k as a step, iterate through k, 2k until an ik that egg broke
	- partition a range[(i-1)k:ik-1] and use another egg to try 1 by 1
	- $T(n,2)$ worst case: $\lfloor \frac{n}{k} \rfloor+k-1$
		- since we want k at a suitable place, take optimal $k = \lfloor\sqrt n\rfloor$
		- Complexity = $O(\sqrt n)$
	- $T(n,2)$ lower bound: 
		- any correct method will use a large no(omega(sqrt(n)) of probes on some instance
		1) what happen if egg does not break at any ik floor?
		dis use P probes
		case 1: $p\geq n$ concludes this method uses at least $\sqrt n$ probes
		case 2: $p < n$ 
		






/28-10-2022
## Binary Search Tree questions




/08-11-2022 BST questions Cont'd
## Given a binary tree, give an algo to check if it is binary tree

- check for max value in left subtree is smaller than root node 
-  check for min value in right subtree is smaller than root node 
- if max(left subtree) < x < min(right subtree) then true

```C++
struct node{
	int val;
	node *left;
	node *right;
}

bool isBST(node *root, int &min, int &max){
	/* only call if root != null*/
	min = root->value;
	max = root->value;

	//left part checking
	int minL, maxL; bool checkL;
	if (root->left){
		checkL = isBST(root->left, minL, maxL)
		min = minL;
		if (maxL > root->value || !checkL) check = false;
	}

	//right part checking
	int minR, maxR; bool checkR;
	if (root->right){
		checkR = isBST(root->right, minR, maxR)
		max = maxR;
		if (minR < root->value || !checkR) check = false;
	}

	return check;
}
```
### Running time of above algorithm
- Let time = O(n), n = no of node in a tree
- Structural induction

- Base case: n = 1, $T(1) = O(1) \leq C$
- nL = no of node in left subtree, nR = no of node in right subtree
- n = 1 + nL+nR
- In this case, $T(n) = O(1) + T(nL) + T(nR)$ where T(0) = 0
- $T(n) \leq C + C.nL + C.nR$
- $T(n) \leq C.(1 + nL + nR) = C.n$

#### its a fucking trap
- in C, there is recursion stack
- there is more memory when a recursion calls
- e.g. 9 variable in isBST() function,
- subinstances in left subtree $\propto$ height of left subtree (h)

Memory usage in this case:
- $M(h) = O(h) + M(h-1)$
- $M(h) = O(h)$



## Converting a sorted linked list to a balanced binary search tree
Todo: 
- get the no. of node in linked list
	- Linear scan to find size of linked list

pseudocode:
- take head of a list
- create BST from the first k node in the list
- update head to k+1th node or NULL if there are no more node in a list


take k = no of subnodes
- $k_L = \lceil \frac{k-1}{2} \rceil, k_R = \lfloor \frac{k-1}{2}\rfloor, k = k_L + k_R$

- k = 0: base case
- for $k \geq 1, k_L = \lceil \frac{k-1}{2} \rceil, k_R = \lfloor \frac{k-1}{2}\rfloor$
- 

```C++
Struct nodeL{
	int val;
	nodeL *next;
}

Struct nodeT{
	int val;
	nodeT *left;
	nodeT *right;
}

// take the head of  a list
nodeT convertBST(nodeL *head, int k){
	// check size
	int size;
	nodeL *curr;
	
}
```

- Time: $O(n)$
- Memory: O(depth of tree) = $O(log(n))$







//18/11/2022
##### Stable sorting
how to sort of 2 keys are same
- If extra information can be assingned to the data structure
	- assign a label to them, e.g. 1 for k_1 , 2 for k_2, ..., n for k_n
	- sort via the key first, then if the key is same, assign by label



## Analysis on randomized quicksort
$T(1) = O(1)$
$T(n) \leq  \frac{2}{n} \sum_{q=1}^{n-1} T(q) + cn$

- Attempt 1: $T(n) \leq  \frac{2}{2} T(1) + 2c$
- prove: $T(2) \leq A.n\log(n)$ for n $\geq$ 2
	- pick a large enough A

- ilog(i) <= i log(n)


