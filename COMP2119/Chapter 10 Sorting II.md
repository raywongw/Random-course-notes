
### Merge Sort
- possible input format: array, (singly/doubly) linked list
- divide list into 2 roughly equal part
- recursively divide
- merge the resulted 

##### Code implementation of Merge sort
```C++
MergeSort (A, low, high)
/* sort the subarray A[low..high] */
	if (high > low) {
		mid = floor ((low+high)/2);
		MergeSort(A,low,mid);
		MergeSort(A,mid+1,high);
		Merge(A, low, mid, high); // maintain stable property while merging
		/* merge the lists A[low..mid] and A[mid+1..high] */}}
```

#### Complexity of Merge Sort
- Worst case O(n log(n))

##### Array Merge Sort
- Merge() Time: $O(n)$, Extra mem: $O(n)$

##### Linked List Merge Sort
- Merge(): Time: $O(k)$, Extra mem: $O(1)$



### Quick Sort
- similar to merge sort
- 2 part are divided according to some value
- the value picked is a `pivot`
- partition: A[1 : q], A[q+1 : n]
- Code for partition in Quick Sort
```C++
PARTITION (A, p, r) {
/* partition the array segment A[p..r] */
	v = A[p]     /* 1st element as pivot */
	i=p-1; j=r+1 /* i and j scan the left and right part of A */
	while (TRUE) {/* extending the right sublist */
		do j--; while (A[j] > v)/* extending the left sublist */
		do i++; while (A[i] < v);
	if (i<j) /* not done yet */
		swap(A[i],A[j]);
	else return(j)/* A[p..j], A[j+1..r] are the 2 sublists */ }}

QuickSort (A,p,r) {
	if (p<r) {
		q = PARTITION(A,p,r);
		//(Can we guarantee q < r?)
		QuickSort(A,p,q);
		QuickSort(A,q+1,r);}}


```

#### Analysis on Quick Sort
- Worst case (array sorted): $\Theta (n^2)$
- Best case: $O(n\log(n))$

#### Ways to pick pivot
- The code above pick first as pivot
- Picking median wastes time
	- picking randomly costs less time
- Pick 3 element and find median is better



### Lower bound for sorting
- given n unsorted element, no. of possible orderings = $n!$




### Counting Sort
- if given singly linked list
	- the time is same
	- extra space needed: O(k)



### Radix Sort
- extension of [[#Counting Sort]]
- sort a list of num in a known range in linear time
- base k, d digits

- Methodology: sort least significant digit first -> most significant digit last 
	- in 21345, sort from 5 , then 4, then 3, then 1, then 2

- d iterations of counting sort
```C++
RadixSort(A,d) {
	for (i=1; i<=d; i++) {
		// singly linked list
		prepare k buckets: B[0..k-1];
		/* distribution */
		scan A from head to tail, 
		for each element x, let m = x’s i_th rightmost digit, append x to the end of bucket B[m];
		/* concatenation */
		concatenate the bucket lists.
		
		
		// list}}
```


##### Achieving stable sort


##### Complexity of radix sort
- Time complexity: $O((n+k)d)$
	- Assume k is constant(at most n): $O(nd)$
- Extra space:
	- Array: $O(k+n)$
	- Singly linked list: $O(n)$



## Conclusion
- Lower bound for comparison sorting
	- [[Chapter 9 Sorting I#heap sort|Heap sort]], [[#Merge Sort]] of worst case $O(n \log(n))$
	- [[#Quick Sort]] of average case $O(n\log(n))$
	- 