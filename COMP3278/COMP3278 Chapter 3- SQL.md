## Data definition
[[COMP3278 Chapter 2 - ER Model|Last Chapter]] [[COMP3278 Chapter 4 - Relational Algebra|Next Chapter]]
### Create table
- create a table with different types of column
```MySQL
CREATE TABLE BRANCH{
	branch_id VARCHAR(15)
	name VARCHAR(30) NOT NULL
	asset INT UNSIGNED NOT NULL
	PRIMARY KEY(branch_id)
}
```
##### NOT NULL
- each the value in the column must not 


### DROP Table
- drops the table when needed
- If the value in table is referenced by other table, it may reject the DROP command
- e.g. If the table `student` has its student ID referenced by another table, dropping the `student` table will result in error
- can be modified to drop the other referenced table first by iteration.


### ALTER Table
- Add columns
```MySQL
ALTER TABLE student ADD student_number INT(10);
```
- Remove columns
```MySQL
ALTER TABLE student DROP student_id;
```
- Add constraints like a primary key or foreign key(?)
```MySQL
ALTER TABLE student ADD PRIMARY KEY (student_id);
```


### Foreign Key Constraints
- Refering values btween 2 tables
- It should reference the columns of primary key OR super key in referenced table
  
```MySQL
  
CREATE TABLE Owner{
customer_id VARCHAR(20),
account_id VARCHAR(15),
PRIMARY KEY(customer_id, account_id),
FOREIGN KEY(customer_id) REFERENCES Customer(customer_id), 
FOREIGN KEY(account_id) REFERENCES Account(account_id)
}
```
- The foreign key can be defined by [[#ALTER Table]]  command

```MySQL
ALTER TABLE Owner 
ADD FOREIGN KEY (customer_id) REFERENCES Customer(customer_id);
```

##### Storage engine
- Tables using InnoDB support the foreign key constraints
- To specift which storage engine to use, add the `ENGINE = INNODB` after the create table line
- `ALTER TABLE name ENGINE = INNODB` also does the job



## Insert, Delete and Update
### INSERT
- insert records into table

##### Insertion of values through tuple
- primary wat to insert values to table
- useful if only few values needed to be inserted
```MySQL
INSERT INTO Branch VALUES 
( 'B1' , 'Central', 7100000),
( 'B3' , 'Kowloon Tong', 12465000);
```
- End the command with ;


##### Insertion of values through data file
- alternative wat to insert values to table
- useful if large amount of data have to be loaded
```MySQL
LOAD DATA LOCAL INFILE 'text.txt' INTO TABLE Branch
FIELDS TERMINATED BY ';'
LINES TERMINATED BY '\n';
```
- Specifies what symbol as separating field
- Specifies what symbol as separating lines

### DELETE



  

### Aggregate functions
- Takes values and return a single value
- e.g. Average balance of all accounts in a bank branch
```MySQL
SELECT AVG (balance) FROM Account
WHERE branch_id = 'B2'
```
- Functions: AVG, MIN, MAX, SUM, COUNT

### GROUP BY 
- group the rows in table by a parameter
```MySQL
SELECT branch_id , AVG(balance) FROM Account
GROUP BY branch_id;
```
- The query first perform the grouping, then perform the aggregation and 
- Note that the query cannot process a `WHERE` before `GROUP` since there is no data available to 


### HAVING
- Condition filtering for [[#GROUP BY]]


### JOIN
- aggregate 2 table together 
- different to directly select * from 2 tables, which returns a cartesian product of 2 table


##### OUTER JOIN
- join the table with missing data
- e.g. If the left table/right table has missing value,
```MySQL
SELECT * FROM Employee E LEFT OUTER JOIN Department D ON E.department_id = D.department_id;
SELECT * FROM Employee E RIGHT OUTER JOIN Department D ON E.department_id = D.department_id;
```
- The first query uses the all data in left table and joins 2 table even if there is value in left table that does not have data in right table (with NULL data)
- second query does the opposite




### SET Operations



##### UNION



##### INTERSECT



##### EXCEPT



### Nested Queries
- nested under [[#W1]]




