
[[COMP3278 Chapter 8 - Collaboration Filtering|Last Chapter]]
### MapReduce
- programming model and software framework for process and generate large dataset


##### Design Goals
- Scalable
	- Run on applications in parallel over 1000 machnes and 10000 disks
	- Elastic
		- Add/remove compute nodes easily



##### Hadoop
- HDFS
	- Storing data
	- Data is stored in datanodes
		- One datanode for managing datanodes
		- File into blocks and replicate to a number of datanodes
- Hadoop MR
	- Executing applications
	- Data type: {key, value} pairs
	- Map Function: ${K_{in}, V_{in}} \rightarrow \text{list}(K_{\text{intermediate}}, V_{\text{intermediate}})$


##### Example: WordCount


1. Map phase
	- Master node controls job execution on multiple slave nodes
	- 
1. Shuffle and sort phase
2. Reduce phase



### Term Frequency - Inverse Document Frequency
- aka **tf.idf**
- function $tf.idf(t,d)$
- reflect on how important a term $t$ is to a document $d$

##### Preprocessing
1. **Tokenization**
	- Separate text to token(words)
	- Compound words
	- Some languages may not separate words by whitespace
2. **Stemming**
	- Merge closely related words
	- Remove useless suffix
	- Lexical stemming
		- Merge lexically related term
	- Phonetic stemming
3. **Stop word removal**
	- Remove useless word
		- 'be', 'is', etc

##### Processing
$tf.idf(t,d) = tf(t,d)\cdot idf(t)$

- $tf(t,d)$
	- frequency of term $t$ occurs in a document $d$



### OLAP on Search Logs
- Online Analytical Process

##### Query suggestion
- Forward Search
	- What most people search for after typing a key word
	- top k frequently searched sequence
- Backward Search
	- What the keyword is 
  