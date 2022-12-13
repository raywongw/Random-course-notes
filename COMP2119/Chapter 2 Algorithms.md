## Chapter 2 Algorithms
Index:

### Programs
- Data structure with algorithm
- finite sequence of instructions

### Algorithms
- Computational procedures transforming input -> desired output
- Specifying the step for computer to take
- written in a specific langiage
- language independent, machine independent
	- Same strategy is used across python, java, c++
- well-defined operations -> stops after a finite amount of time
- use time and space complexity to find a best algorithm for use

### Data Structure
- Representation, organization and storage of information


### Problem Size
- reflecting the complexity of the problem


### Measuring time resource
Method 1: write 2 programs usign different algorithms and time their speeds
- Advantage: straightforard
- Disadvantage: 
	- Too much noise: Programmer, language, compiler, OS, machine, input
	- Hard to get a predictor function


Method 2: Counting the set of operations that an algorothm performs -> derive a estimation on number of operations required


### Plan to solve a computational algorithm
- recognizing problem
	- solvable by computer
- Abstract model ith alloed set of operations
- Design algorithm to solve problem ithin the model
- Analyze the algorithm to get an upper bound on ork needed
- Analyze algorithm to get an lower bound on work needed (show that its not possible to improve further by any other algorithm)
- Try to get a better alternative if not satisfied
- Build data structures to efficiently implement the algorithm


#### Upper bound
- How bad a particular algorithm can be

#### Lower bound
- how hard a problem is


#### Operations
- Compare their orders of growth/complexity


#### Complexity
- compare their orders of growth
- describe their growth rate relative to the other algorithm's growth rate


#### Asymptotic notations
- Big O Notation: Ο(n)
- Big Theta Notation: Θ(n)
- Big Omega Notation: Ω(n)
- Little o notation: ο(n)
- Little Omega Notation: ω(n)

##### Big O: identifies an algorithm with growing complexity

###### Rules for Big O:
- $f(n) = O(f(n)'') e.g. n^2 = O(n^3)$
- $O(f(n)) + O(g(n)) = O(f(n) + g(n))$
- $c . O(f(n)) = O(f(n))$ where c is a constant
- $O(f(n)) . O(g(n)) = O(f(n) . g(n))$
- $O(f(n).g(n)) = f(n) . O(g(n))$
- $O(f(n)) + O(f(n)) = O(2(f(n))) = O(f(n))$
	- cannot be used repeatedly

##### Big Θ: identifies a most significant term(largest power(?))
- $f(n) = \Theta(g(n))$ : a collection of function that f(n) satisfies
- Θ(g(n)): a set of functions that has a common thing
- $\lim_{n\to\infty} \frac{f(n)}{g(n)}$ = constant


##### Big Ω: identifies a lower bound

##### Little o 
- to denote an upper bound that is not asymptotically tight
$f(n) = o(g(n))$
where f(n) is far smaller than g(n), that $\lim_{n -> \infty}, \frac{f(n)}{g(n)} = 0$


##### Little ω


### Calculating running time
There are things to consider when calculating running time
- Loops
- If then else


If then else
- if c then s1; else s2: max(s1+s2)





### Compute Exponentation
x ^ n = x times x for n times
#### Naive method
- takes n - 1 multiplications  -> Θ(n)

##### Recursion: Compute $f(n) = x^n, f(n) = x^n = x . f(n-1)$
If n is even = 2r, $f(2r) = x^{2r} = x^r . x^r$
If n is odd = 2r +1, $f(2r +1) = x^r . x^r . x$

Q： 



V n+1 = A . Vn = A^2 Vn-1 = A^n V1


Each matrix multiplication takes O(1) time because dimension is either 3 x 3 matrix or 3 for col vector


Compute matrix of A^n

g(n) = A^n = A.A.A. ... .A.A
 
if n = even, g(n) = g(n/2) x g(n/2)
if n is odd, g(n) = g(n-1/2) x g(n-1/2) x A


