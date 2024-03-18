
[[COMP3297 Lecture 2 - Software Process Models|Previous Slide]] [[COMP3297 Lecture 4 - Prototyping|Next Slide]]
# Requirement Engineering
- Most of projects go wrong due to problems in requirements
- 

##### Core issues in Requirements Engineering
- Understand the problem that your system has to solve
	- By understanding the customer and end-user needs
- Common for software developers to misunderstand business problem or users needs
- Customers/Users cannot describe their true needs
- Developers must understand work practices of end users
	- software system solves their problem in useful way

## Product-based vs. Project-based Development

- Reality
	- Software Product Development
	- Shifting to product-based approach


## Custom software
- Unique solutions for specific client
	- Government/Large Company
- Owns code after purchase
- Developed by in-house teams/custom-software development companies
- e.g. 
	- ATC
	- Online Banking
	- Field Service Management
	- Utility Billing


## Software Products
- Generic software products for most customers
- May have minor customization
- No specific client paying to develop this product
- e.g.
	- Games
	- Mass-market apps
	- Productivity tools and suites
	- core asset on software product lines


### Requirements
- Defined by the developers company than some client/users
- Developer's company decides
	- What poduct does
	- What features it provides
		- No contract with client to deliver functionality/insist on delivering feature
	- Priority of features and non functional constraints
		- Consult with potential customers
	- When features will be changed in production
	- When new features will be deployed
	- When features/product will be depreciated


- Drivers of requirements
	- Pure inspiration: rarely
	- Current product does not meet business/consumers need
	- Users dissatisfied as requirements are poorly met
	- New technologies created new needs and opportunities



### Process
- Racing against competitors/a release date
- Initial development can take many years
- Speed is key
- Agile is good match for this


### Management
- No Project Manager in agile development
- Agile teams are self managed
- Product backlog maintained by a member of team
	- Product Owner/Product Manager
	- In scrum case, Product Manager is Product Owner


### Software Requirement
- Functional
	- Behaviour of software
- Non functional
	- How and wellness of the software completing required function

### Types of requirements Information

- **Business Requirement**: High-level business objective of an organization.
- **Business Rule**: Policy, guideline, standard, or regulation that defines or constrains some aspect of the business.
	- Non functional + Quality Requirement
- **User Requirement**: Goal or task that specific classes of user must be able to perform with the system.
- **Functional Requirement**: Description of a behavior that a system must provide under specific conditions.
- **Feature**: One or more logically-related system capabilities that provide value to a user.
- **System Requirement**: Top-level requirement for a product that contains multiple subsystems.
- **Non-functional Requirement**: Description of a property or characteristic that a system must exhibit or a constraint it must respect.
- **Quality Attribute**: Kind of non-functional requirement describing a service characteristic or performance characteristic of a product.
- **External Interface Requirement**: Description of a connection between system and a user, another system, or a hardware device.
- **Constraint**: Kind of non-functional requirement restricting the choices available to the developer




Exercise: What are the types of the following? (so you will know where to record them)
- Under normal operating conditions, authorization of an ATM withdrawal request shall take no more than 2 seconds.
	- Quality
- Passengers want to check in for their flights online.
	- User requirement
- Passenger shall be able to print boarding passes for all flight segments following successful check in.
	- Functional Requirement - System must provide under specific conditions
- We wish to achieve a 95% positive customer satisfaction rating for our company's services.
	- Business Requirement - Business Objective
- Non-academic staff can borrow no more than 24 books from the library at any time.
	- Business Rule - Rule of library
- JSON shall be used as the format for all data-interchange.
	- Constraint - Restriction of choices
- Spell-checking on all input data.
	- Feature - Logically related system



### Software Requirements Specifications
- not common in agile project
- Documents both functional and non-functional requirement
- Basis for planning + design + sat+uat
	- No details
- Focus on **What must the system provide**

- Level of formality vary greatly depending on system specified
- Details of documentation will different from projects
	- How closely the developers can work with customers


### Traditional Requirements
- Little interactions with customers + stakeholders after actual product dev begin
- [[#Software Requirements Specifications|SRS]] as official record of what dev must implement, defines requirements in details
	- Mandatory requirements: "The system **shall**..."
	- Non-mandatory requirements: "The system **should**..."

### SRS in Agile Development
- [[#Vision and Scope Document]]
	- aka Design Doc
- dynamic Product Backlog
	- User Requirements
		- User Stories/Cases
		- UI outlines
		- Acceptance Criteria
	- Items of work needed to satisfy non-functional requirements
- Not analysed until iteration


### Recommendation for non-agile
- with PM, 23% success rate ad 19% failure rate
- without PM, 50% success rate and 9% failure rate
- dont be bureaucratic PM
- dont afraid to take risk
- make quick decisions



## Inception: Setting the Vision

### Establish the Product Vision and Scope
- First step in product developement
- Can be informal statement/document
	- Needed before more detailed descriptions/features and characteristics can be specified
- As minimum
	- Simple statements describing product
	- How the product differs from existing product (Vision Statement)


### Vision and Scope Document

#### Vision
- Answer big questions
- Captures thing need to know about product

	- Vision Outlines: What Who Why
	- Rough Planning: When What

##### Who
- **Stakeholders**: Person/Group/Organization
	- **Customer**: Individual/Organization that benefits from product
	- **Users**: People who uses product
		- Source of User requirements

#### Scope
- Defines what the product is+is not
- Identifies part of overall product vision each releases deliver (large project)
- May change over time under influence of factors
	- Budget constraint
	- Schedule
	- Quality
- Can be expected to change faster if current release is included

#### Usual Document Format
1. Business Requirements (Value)
- value
	1.1. Background
	1.2. Business Opportunity
	1.3. Business Objectives
	1.4. Success Metrics
	- Used as evaluation
	1.5. Vision Statement
	1.6. Business Risks
	1.7. Business Assumptions and Dependencies
	- May affect outcomes
1. Scope and Limitations
	2.1. Major Features
	2.2. Limitations and Exclusions
3. Stakeholders
	3.1 Stakeholder Profiles
4. Delivery and Deployment
	4.1. Product Roadmap
	- Long Term
	4.2. Release Plan
	- Short-term
	4.3. Deployment Considerations


#### Use and Practice
- Can be informal for small products
	- Goal still same
- Something that would be given to a new member of team to let them catch on the project
- In short
- Keep feature list short
	- Can be understand quickly
	- Making abstract features

#### Vision Statement
- For (some target customer)
- Who (statement of need or opportunity>
- the (product name)
- is (a product category)
- that (key benefit, main reason to use)
- Unlike (primary competitive alternative, current system, current business process)
- Our product (statement of main differentiation and advantages)



## Feature List
- Describe functional requirements
	- by user stories and use cases
- Major features are clear from user story and use cses
	- It's format may be difficult to see
- Coarse Planning: a rough roadmap for delivery, release of features by each release
-> a rough plan for developing next release in sprints



## Inception
- Start on planning what to do in this release
- See if the project is feasible
- Proceed with the project or not
- Elliciting needs

### Works in Inception
- 
Establish the Vision
- understand the problem, identify stakeholders and their interests; 
- make sure everyone agrees on vision and scope. All views must align; 
- identify, in broad terms, the required features of the product;
- Identify any major quality requirements (performance, security, ...); 
- make a rough plan for when features will be released and deployed; 
- build your own domain knowledge while building the Vision;
- iterate and update as necessary.
Go/NoGo
candidate architecture? 
should development proceed?
Prepare for Sprint 1
set up infrastructure, automation, and the development environment; create a Product Backlog, sufficiently refined for Sprint 1 planning.



### Requirement Cycle
Traditional
- Elicit needs
- Vision
- Each iteration
	- Elicit needs
	- Analyze Prioritize functions
	- Specify
	- Validata
- Build once in one of the specify stage

Agile
- Build in every iteration



## Tradition elicitation techniques

Several approaches
- Reading/Research 
	- Study existing documents for background knowledge
- Interviews 
- Observation 
	- Learn how users perform tasks
- Document Sampling 
	- Get clear picture of problem
- Questionnaires
- Focus Groups

### Interview
- Flexible
- Give valued information to build product if done well

#### Things should do
- Understanding on problem domain
	- gain confidence about knowing the client
- Clear set of objective
	- Plan with key interview questions as logical flow
	- Got a logical structure and overall flow
- Include open-ended questions
	- Focus on users roles, needs follow up on workflow
- Introduce teams and reason for there
- Thank client at start and end
- Start on time even someone havent get in
- Decide who take notes
- Use time to understand objectives, needs, constraints
- Use some time to recap and clear concepts
- Summarize some of the answers to make sure fully understanded
- Focus onquestions on problem
- Schedule a follow-up meeting/Send follow up emails of notes

#### Things should not do
- Read questions and ask one by one
	- Not building relationship with client
- One by one asking questions
- Argue with client
- Speak more than the client
- 

### Things to be notice
- Conflicting requirement
- put critical requirement
- Let client know tradeoffs in requirement


## Software Requirement: Analysis


### Procedures
- Convert stakeholders' needs to prioritized requirement that define what to build and satisfy them
- Create, refine statements of requirements
	- In the form that stakeholders understands
	- Changing high level requirements to lower level requirements
	- Sufficiently detailed for design, estimation, product testing
- Find requirements that are not explicitly stated
- Check for things not in requirements
- make prototypes if necessary
- make priority list of requirements


### Product Environment
- entities that system interfaces with
	- users/hardware/other system
	- data/control flow between external entities
	- no internal details

### Prioritizing Requirements
- Simplest: Things to be included/removed in next release

- Three level scheme
	- High: done before next release
	- Medium:  done in later release
	- Low: extra stuff

- Four level scheme - MoSCoW
	- Must have
	- Should Have
	- Could have
	- Wont have

- Consider only uses highest level of requirement (high in high) for high priority


## Software Requirement: Prototyping
- Limited version of system
- Supplement of the vision

Help lower risk of building wrong product
- Helps clear misunderstanding
	- Use prototype to confirm and clarify
- Try to get what user want from vague ideas
	- I know it when i see it

Help developers
- Reduce risk of making wrong technical decision
	- Choose one tech stack to be most effective
- Check and demonstrate feasibility/market potential of product
	- Reduce risk of failure
	- Attract funds
- Part of increment


#### Type of prototypes
**Wierframes**: UI with only main features of layout and content
- with wireflows to tell what button goes to what UI page
**Mockup**: Used in later stage of UI design



## User Requirement Analysis
- document user requirement with use case and user stories
- transform them to functional requirements




### Use Cases



#### UML
- includes Use Case Diagram
- Focus on what crosses boundary in system


#### Writing Use Cases
- keep flow simple
- from entry point to exit point
- One main success scenario
- Several branched scenario
	- Will rejoin main flow or get to exceptions

#### Levels of Formality
- **Brief**: Main success scenario
	- Few languages
- **Casual**: Alternate flow that go to success
	- Some paragraph
- **Fully detailed**: All possible flows
	- In details




### Product Backlog
- List of Product Backlog Items by priority
- To be (splitted and) put in sprints
- PBIs have to be specified in order to be splitted
- 


## Requirements Validation
- Check if requirements are realistic
- 

### Behaviour-driven development
Use Cucumber
- Match code with specs in doc

4 basic block
- Given: Condition
- When: Action to be executed
- Then: Output to be assured
- And

### Quality User Story
6 important factor
- Independent
	- Self contained, not overlapping
- Negotiable
	- Avoid waterfall approach
	- Avoid too many constraint
- Valuable
	- End-to-end stories
	- To end-users
- Estimatable
	- Need details
- Small
	- in hours of work
	- minimum useful features
	- must be sprintable
- Testable
	- objective and specific terms only
		Metrics for non-functional requirement:
		- **Fast**: Throughput, response time, Screen refresh time
		- **Easy to use**: Training time
		- **Robust**: Time to restart, Probability of data corruption
		- **Reliable**: MTTF, Probability of failure
	- Defined in exactly one place

### Reality of specifying metrics
- Sometimes there aren't suitable metrics at all
- Sometimes customers can't relate the metrics to their needs and experience
- Sometimes you find the cost of verification is too high


- Try to live with the value goals
	- Gives some idea how customer want a thing
	- 



[[COMP3297 Lecture 2 - Software Process Models|Previous Slide]] [[COMP3297 Lecture 4 - Prototyping|Next Slide]]
