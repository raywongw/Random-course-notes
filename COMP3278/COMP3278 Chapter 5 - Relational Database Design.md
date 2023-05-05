``
[[COMP3278 Chapter 4 - Relational Algebra|Last Chapter]] [[COMP3278 Chapter 6 - File & Storage |Next Chapter]]
### Functional dependency
- test if a database instance is legal

##### Armstrong's Axioms
###### Reflexivity
- $AB\rightarrow A$ is true, since $A \subseteq AB$
- If $B \subseteq A$, then $A \rightarrow B$


###### Transitivity
- If $B \rightarrow C, C\rightarrow D$, Then $B \rightarrow D$.

###### Augmentation
- If $B \rightarrow D$, then $AB \rightarrow AD$
- Notice The converse may not be true


###### Union
- If $A \rightarrow B \text{ AND } A \rightarrow Y\text{, then} A \rightarrow BY$


###### Decomposition
- Reverse of Union
- If $A \rightarrow BY\text{, then } A \rightarrow B \text{ AND } A \rightarrow Y$


###### Pseudo-transitivity
- If $A \rightarrow B \text{ AND } YB \rightarrow S \text{, then } AY \rightarrow S$




###### Example
Given a set of functional dependencies $F = \set{A \rightarrow B, B \rightarrow C, DE \rightarrow A}$
- Prove $A \rightarrow C$ is true
	- Since $A \rightarrow B, B \rightarrow C$, $A \rightarrow C$ by [[#Transitivity]]

- Prove $AD \rightarrow B$ is true
	- Since $A \rightarrow B$, $AD \rightarrow BD$ by Augmentation rule
	- Since  $BD \subseteq B$, $BD \rightarrow B$ by Reflexivity
	- Since $AD \rightarrow BD, BD \rightarrow B

##### Q2a) IF $A \rightarrow E, A \rightarrow D \text{ and } E \rightarrow B \text{, then }A \rightarrow BD$
- Since $A \rightarrow E \text{ and } E \rightarrow B \text{, then }A \rightarrow B$ by Transitivity rule
- Since $A \rightarrow B \text{ and } A \rightarrow D \text{, then } A \rightarrow BD$ by union



### Attribute Set Closure $\alpha ^+$
- closure of $\alpha$
	- set of attributes that can be functionally determined by $\alpha$

- e.g. $F = \set{A \rightarrow B, B \rightarrow C}$
- then $\set{A}^+ = \set{A, B, C}$,   $\set{B}^+ = \set{B, C}$ and  $\set{C}^+ = \set{C}$
-  $\set{A,B}^+ = \set{A, B, C}$

##### Prove candidate key
- For R(A, B, C, D), Proof if C is a candidate ley
	- Proof C can map to A, B, C, D



### Functional Dependency Closure $F^+$
- $F^+$ in relation R
	- TReat every subset of $R$ as $A$
	- For every $A$, compute $A^+$
	- Use $A$ as LHS, generate FD for every subset of $A^+$ on RHS


- update database design through functional dependency

### Normalization goal
decompose the schema to a set of functional dependencies to several relation

- Loseless join
- Reduce-redundancy
- Dependency-preserving


##### Loseless join
- consider a correct functional dependency
- prove that $R_1 \cap R_2 \rightarrow R_1 \text{ OR } R_1 \cap R_2 \rightarrow R_2$

##### Dependency preserving
- Let $R = (A, B, C, D) \text{ and }F = \set{A \rightarrow B, B \rightarrow CD, A \rightarrow CD}$
- Since $A \rightarrow CD$ is proved prev 2 functional dependency
	- $A \rightarrow CD$ is redundant

##### Boyce-Codd Normal Form
- decompose it to 
