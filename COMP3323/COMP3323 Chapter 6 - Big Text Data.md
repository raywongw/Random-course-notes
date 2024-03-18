
[[COMP3323 Chapter 5 - Ranking and Top-k Queries|Last Chapter]] [[COMP3323 Chapter 7 - Relational Algebra|Next Chapter]]
## Text Database
- A Document Database
- Indexes for containment and similarity
- Collection of Documents
- Document as List of words


## Searching in Text Database
- Search with Keyword
	- if "car" in text document


## Containment Queries
- Searching is done with a formula of AND, OR, NOT predicates



#### Naive Approach
- Linear scan

#### Better approach
- Preprocess document and extract words
- Index the documents based on words


### Set comparison
- Containment queries with only AND predicates
- Each query is a set of keywords `s`
- Each document is a set of words `t`
- Check if s $\subseteq$ t
	- Sort s and t
	- nested for loop

## Signature
- Way to compress information to a vector
	- Lossy approximation
- Use as few bytes possible to express a item
- fast filter for set operation


## Signature-based Index
- Indexed in order
- a matrix like

### Signature Tree
- SImilar to R-Tree
- Leaf node is document signature
- directory node is entrues

## Inverted File
- inverted file for set of elements
- word as directory, document as id
	- see which document has such word

Easy for finding documents contains a set of word
- cost of joining is cheap, can use merge join


Comparison with signature-based technique
- 


## Term Frequency Vector
- a vector that store the frequency of terms
	- e.g. `{'test': 3, 'help': 1}`
- Adding the term frequency to the inverted file
	- {'word': ('doc id', term frequency)}
	- 



## [[COMP3278 Chapter 9 - Processing big data with MapReduce#Term Frequency - Inverse Document Frequency|tf.idf]]
- Improvement to Term relavance vector
- Filter out not-relavant word through idf(n)
$tf.idf(t, d) = tf(t, d) \cdot idf(t)$


- df:
	- percent of document with t/ no of document
- idf:
	- log(No. of documents/ df(term) + 1) + 1

## String Matching
- Stricter matching
	- e.g. "Advanced Database Systems" string in document


### Applications

#### Information Retrieval 
- Text searching
- Allow some error for the result
	- Approximate search

#### Computational Biology
- Searching over long sequence of ATCG
- Cannot be 100% correct in detecting correct sequence

#### Signal Processing
- Error correction


### Approximate String Search
- Edit distance
	- Number of operations to trnasform one to other


#### String Alignment
- Align the string to make them mostly similar
- 


[[COMP3323 Chapter 5 - Ranking and Top-k Queries|Last Chapter]] [[COMP3323 Chapter 7 - Relational Algebra|Next Chapter]]