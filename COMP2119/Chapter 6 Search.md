- hash table are random and expected O(1) per operation
- In searching, considering worst case running time


## Problem
- a set of n elements, search for one with a specific key
Previously have 2 ways: [[Chapter 4 Hashing#Hashing|Hashing]] and [[Chapter 4 Hashing]] linear search

### Linear search
- Average worst case complexity of O(n)
### Hashing
- Averafe case of O(1+a) for chaining
- Average case of O(1/(1-a)) for open addressing
- Worst case of O(n)


- Consider several searching strategy have a vetter worst case complexity

- If the search is done to a no structure data type, the time complexity of search must be at least O(n)
- For ordering structure(e.g. sorted list), there is possibility to beat O(n)



## Jump search
Given a sorted L
- in linear search, we examine elements in order
- In jump search, we give a random index, e.g. L[5] 
	- If L[5] smaller than x, x is in l[1:4]
	- if L[5] = x, done
	- if l larger than 5, x is in L[5:]

### Strategy
- choose any k < n
- search for L[k], L[2k] until X is smaller or equal to L[ik] for some i
	- if X=L[ik], done
	- if X  smaller than L[ik], perform linear search on L[(i-1)k+1:ik]
-  $f(n,k) = \lfloor n/k \rfloor +k - 1$
- best k would be $k = \sqrt n$

## Square root search
- Jump search with $k = \sqrt n$
- Worst case = $O(\sqrt n)$


## Binary Search
- take $k = \lfloor n/2 \rfloor$
- Code implementation:
```C++
Binary Search (L, low, high, X) {
/* the segment to consider is L[low,high] */
while (high >= low) {
	mid = floor ((low+high)/2) 
	case L[mid] {
		< X: low = mid + 1;
		= X: return(mid);
		> X:high=mid-1;
	}
	return (“not found!”);
}
```





### Complexity of binary search
- Worst case: $O(log(n))$ for unsuccessful search
- Successful search: $O(log(n))$


## Interpolation search
- If L is an array and it uniformly partitions the set of numbers
- X should be near $L[\lfloor pn \rfloor]$ where  $p = \frac{X - L[Low]}{L[High]-L[Low]}$


### Complexity of Interpolation search
- $O(log(log(n)))$


## Practical problem: Critical height
### Scenario
- find the minimum floor of a building where an egg breaks if tossed out
- 500 floor and 10 egg




## Hashing
### Advantage
- gives best average search time
### Disadvantage
- Use more memory
- Does not support range search