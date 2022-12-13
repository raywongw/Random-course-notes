## Introduction


### Induction
on one parameter (n >= 0)
base case n = 0, p(0) is true


###### induction hypothesis:
assume p(k) is true for some k >= 0

###### induction step:
- if p(k) is true, then p(k+1) is also true

eg sub k = 1 is true for p(1), then p(2) is also true



induction on to parameters $(n,m) >= 0$

e.g. Ackermann function
$A(0,n) = n+1$
$A(m,0) = A(m-1,A(m,n-1) \text{ where }(n = 0)$
$A(m,n) = A(m-1, A(m,n-1)) \text { where }(m > 0, n > 0)$

base case m = 0, 
$A(0,n) \text {     is true for all } n \geq  0$

Induction hypothesis:

the mth row is ell defined for some m >= 0
for some m >= 0, A(m,n) is true for all n >= 0

Induction step: goal: A(m+1, n) is true for all n >= 0

Apply induction on n,
base case (n = 0):
$A(m+1, 0) = A(m,1)$, hich is true

Induction hypothesis:
Assume $A(m+1, n)$ is true for some  n >= 0

Induction step:
Consider $A(m+1, n+1) = A(m,A(m+1,n))$
Evaluate $y = A(m+1, n) = A(m, y)$




