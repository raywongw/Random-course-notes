
[[COMP3278 Chapter 3- SQL|Last Chapter]] [[COMP3278 Chapter 5 - Relational Database Design|Next Chapter]]
Basic operators 
- Select (σ) 
- Project (π) 
- Union (U) 
- Set difference (-) 
- Cartesian product (×)
- Rename (⋃)

##### Selection
- commutative
- o_p(o_q(E)) = o_q(o_p(E))


##### Project




##### Union
- R U S
- Only union the items that share same name and same property
- 

##### Set Difference
Only find difference of items that share same name and property



##### Cartesian Product
$R\times S = \set{t\cdot q | t\in R \wedge q\in S}$


##### Rename
$p_x(E)$
- rename E to name x


##### Selection power
- how the intermediate relation can be reduced


##### Q1



##### Q2



##### Q3
- Find the dept.id where employees named Smith Work
- Consider selection power




##### Set Intersection
R⋂S = R - (R - S)

- R and S must have same number of atttributes and compatible attribute domain


##### Natural join
associative
(E_1 natural join E_2) natural join E_3 = E_1 natural join (E_2 natural join E_3)


##### Assignments
used to assigning temporary relation variables
←


##### Outer join

Left Outer Join
- First perform inner join
- 


##### Division


### NULL Value




## Views

##### CERATE VIEW
- Provide mechanism to hide certain data from certain users
- 