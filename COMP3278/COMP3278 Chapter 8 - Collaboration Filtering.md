
[[COMP3278 Chapter 7 - Indexing|Last Chapter]] [[COMP3278 Chapter 9 - Processing big data with MapReduce|Next Chapter]]

##### real life example
- Recommendation system
	- select things similar to user choice



- prediction on how a user rate on item



### Collaborative Filtering



#### Memory-Based Approach
- Main steps
	- Finding users who are similar to a user
	- Produce a prediction for active users based on ratings of similar item

##### How to measure similarity
- Vector Cosine-based similarity
	- n dimensional vector of different product
	- if the angle between 2 vector is small, they are more similar
	- cosine: if 2 vector are close, theta is small -> cos(theta) = similarity

- Correlation-based similarity
	- shifting effect
	- variation of ratings w.r.t. average rating of user
	- if Bob has 2,3 and Alice have 4,5, they are considered similar
		- Bob's deviation from average is (-0.5, 0.5), which is same as Alice

###### Pearson Coefficient$$P_{a,i} = \bar{r}_a + \frac{\Sigma_{u\in U}(r_{u,i} - \bar{r}_u)\cdot w_{a,u}}{\Sigma_{u\in U} |w_{a,u}|}$$




### Model-based Approach
－ 