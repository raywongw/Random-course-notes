
### Problem Definition
- A list `A` of n numbers, arrange A in increasing value
- Sorting help make searching efficient



### Model
- derive order info by comparing eleents
- Special case: 
	- keys are integers
	- there is a small range of keys


### Bubble sort
- Compare first 2 element
	- if first element > second element, swap
- continue until nth element is touched
- Repeat for iterations and the list will be sorted
- No. of swaps done: $\frac{\binom{n}{2}}{2}$
- 

#### Code implementation of bubble sort
```C++
BubbleSort (A) {
/* elements in A[1..n] */
	for (i=n; i>=2; i--) {
		for (j=1;j<=i-1;j++) {
			if (A[j]>A[j+1])
				swap(A[j],A[j+1]);
		}}}
```

#### Complexity of bubble sort
- $\sum_{i=0}^{n-1} {i}$ = $\frac{n(n-1)}{2}$
- Time complexity = $\Theta (n^2)$
- Memory usage:
	- 2 variable
	- Constant space, O(1)




### Insertion Sort
- maintain a sorted list with a iteration
- only swapping adjacent element
- 

#### Code implementation of insertion sort
```C++
InsertionSort(A) {
	for (i=2; i<=n; i++) {
		j = i-1;
		while ((j>=1) && (A[j]>A[j+1])) {
			Swap(A[j], A[j+1]);
			j--;
}}}
```

#### Complexity
- Worst case: $\sum_{i=1}^{n-1}{i}$ = $\frac{n(n-1)}{2} = \Theta(n^2)$
- Average case: $\sum_{i=1}^{n-1}{\frac{i}{2}}$ = $\frac{n(n-1)}{4} = \Theta(n^2)$
- Best case: sorted, $\Theta(n)$


### Selection sort
- swapping elements far apart to beat $\Omega(n^2)$
- swap eleents at the end


#### Code implementation of Selection sort
```C++
SelectionSort(A) {
	for (i=n; i>=2; i--) {
	max = i;
		for (j=1; j<=i-1; j++) {
			if A[j] > A[max]
			max = j;
	}
	swap(A[i],A[max]);
}}
```

#### Complexity of selection sort
- No. of comparisons = $\sum_{i=1}^{n-1}{i}$ = $\frac{n(n-1)}{2} = \Theta(n^2)$
- Constant memory



### heap sort
- efficient variant of [[#Selection sort]]

- build a heap, pick maximum value in heap, then rebuild heap

#### Complexity of heap sort
- O(1) extra memory 
- $O(n \log(n))$ time for array
- 
- Complexity of building a heap:
	- O)(2^h) = O(n)
	-   

### Priority Queue
- implemented with Heap
- schedule jobs with priorities
- a set ADT supports 3 operations
	- INSERT(S, x), which insert x into the set S
	- MAXIMUM(S), which returns the largest element in S
	- DELETE_MAX(S), remove largest element in S
	
- When job J arrives
	- INSERT(S,J)
- When processor is ready to serve a job
	- MAXIMUM(S)
	- DELETE_MAX(S)

```C++

INSERT(S,x) {
	n++;A[n] = x;
	i=n;
	while ((i>1) && (A[floor(i/2)]<A[i])) {
		swap (A[i],A[floor(i/2)]);
		i = floor(i/2);
	} }


MAXIMUM(S) {
/* suppose the elements are stored in array A */
	return(A[1]);}
DELETE_MAX(S) {
/* let n = size of heap */
	if (n<1) return (“Heap underflow”);
	swap(A[1],A[n]);
	n--;
	Heapify(A,1,n);
}
```







##### Array implementation of Priority Queue
- init: pick some array size of $n_0 = 100$
- when it is about to full
	- create another array with size of 2n
	- copy the existing data of array to new array


##### C++ Vector implementation of Priority Queue
- no need to take care of size
- take care of the actual and exact time complexity/memory usage


##### Node + pointer implementation
- Tree/


##### Complexity of Priority Queue
- $O(\log n)$