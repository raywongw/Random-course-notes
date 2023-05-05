
[[COMP3278 Chapter 1 - Intro|Last Chapter]] [[COMP3278 Chapter 3- SQL|Next Chapter]]
### Entity and entity set
##### Entity
- Object that is distinguishable with other entity
- e.g. Accounts, Customers
	- They have attributes of names and address, ID

##### Entity set
- Set of entities of same type that shares same properties

##### ER diagram
- Rectangle: entity sets
- Ellipses: attributes
- Line between rectangle and ellipse: link between attribute and entity set


### Relationship and relationship set

##### Relationship
- association among entities

##### Relationship set
- set of relationships of same type
- represented as diamonds in [[#ER diagram]]


### Constraints
##### Mapping cardinalities
- No. of entities which another entity can be associated via relationship set
- e.g. how many account can a customer have
- Directed line (->) if there is one relationship
- Undirected line (--) if there is many between relationship set and entity set

##### Participation constraints
- whether all entities in the entity set have to participate in relationship set
- e.g. can there be a customer that have account with no record

**Total participation**
- every entity in entity set participates in at least one relationship in relationship set
- represented by double line

**Partial participation**
- some entity may not participate in any relationship in relationship set
- represented by single line


##### DB designer task
- Understand and model the data of application using ER diagram
- Interact with the client to get clear problem definition
- Find missing info and ask the client for it
- Give suggestion to optimize the DB for specific application

##### Pratical issue
- Are there enough information to build data model


### Keys of an entity set
**Super key**
- Its value uniquely determines each entity
- No other entity has same val in super key

**Candidate Key**
- Minimal type of [[#Super key]]
- no subset of candidate key is still a super key
- can have more than 1

**Primary Key**
- one of the selected [[#Candidate Key]]
- underlined in an ER diagram


### Different attributes type
**Single-valued attribute**
- Represented with a single ellipse

**Multi-valued attribute**
- Represented with double ellipse

**Derived attribute**
- Represented as dashed ellipse


### Weak Entity Set
- an entity set that has no primary key
- that other entity set associated with it
- the relationship set has double line with it
- double rectangle to denote it
##### Discriminator
- aka partial key
- set of attributes that distinguish among the weak entities that depend on the same identifying entity.


### Role
- specify how a subset of entities interact with another subset of entities
	- may not be distinct
- Useful in labelling hierachial structure ([[COMP2119 Chapter 5 - Tree#Tree|Tree]] like) and graph-like structure


### Specialization and Generalization
**Specialization**
-   designate sub-groupings within an entity set that are distinctive from other entities in the set
-   A lower-level entity set inherits all attributes and relationship set participation of the higher-level entity set to which it is linked
-   Lower-level entity set can have its own attributes

**Total or Partial**
-   Specifies whether an entity in the higher level-entity set must belong to at least one of the lower-level entity sets within a specialization.

**Disjoint or overlapping**
-   Constraints on whether entities may belong to more than one lower-level entity set within a single specialization.
    -   Disjoint: must be either A or B
    -   Overlapping: Can be both
-   _E-R Diagram_
    -   A disjoint specialization: "Disjoint" beside the "IS A"
    -   An overlapping specialization: Null, default








### Foreign Key
- a reference between two tables
- used to cross-reference different tables
	- link information together
	- essential in database normalization


