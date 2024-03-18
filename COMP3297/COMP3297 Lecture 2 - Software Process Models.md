
[[COMP3297 Lecture 1 - Introduction to Software Engineering|Previous Slide]] [[COMP3297 Lecture 3 -  Requirement Engineering|Next Slide]]


# Software Process Models
- Used to develop product
- How we should break development to steps and answering questions
	- What do we do next?
	- For how long do we do that?
	- What do we produce as a result?
	- Intermediate/Final product -> artefacts


## Waterfall Model
- Basis for traditional approaches to development
- Each stage start after previous stage is complete
- Cannot go back to previous stage once declared complete
- Each phase terminates a major milestone with a review following

1. Plan
2. Specification
	- Requirements Specification
3. Construction (Design and Implementation)
	- Design Specification
	- Code
4. Testing (Deployment)
	- Test Reports
	- Installed Systems
5. Evolution

- Predictive Model
	- Predict what is going to happen
	- Requirement can be known at start of project
		- Takes large amount of effort
	- Solution is clear


#### Advantages
- Easy to understand
- High Level of control
- Easy to verify at each stage
- Very clear on when different activities take place and when it will complete
	- Easy to use specialized teams for different phases
- Customer know what will be delivered exactly
	- Good for mission-critical and safety-critical software
- No need to waste time on prototyping and experiments
- No need to prevent design degrade during development
	- Design is never modified, defined at start

### Disadvantages
- Do not work for innovative/complex software development
	- Cannot handle change, have to loop back to redo whole project
- Cannot work if customer and developer have different vision in project or have incomplete requirement
- Lack flexibility in process
	- Difficult to accommodate requirements changes
- No working product until the end of project
	- Assumes all things will integrate successfully at the end that satisfies users
- Badly structured systems
	- Large amount of workarounds needed in code



### Improvement: Waterfall Model with Feedback
- Improved waterfall with feedback to previous phases
	- Allow refinement in early phases
- Expensive cost of rework
	- Mistakes in early phases takes much effort to be fix in later stage of development


#### When to choose waterfall model
- Requirements really are known in advance
	- Mission-critical systems
- no significant risks in the project
- Team has development experience of this kind of project
	- Has good understanding of problem domain
	- e.g. repeated development of product with simple customization for customers
- The schedule is known to be long enough to complete all work



## Predictive models use Defined Process Control
- Manufacturing model
- Treat Software development like manufacturing
	- All knowledge are available
	- Steps can be fixed and are repeatable with small variation

## Defined Process Control
- Open Loop


## What do we really need
- Self-organized developers to motivated, cooperative teans
- Collaborate closely than working in isolation/specialized group
- Produce work increments frequently than integrate large increment in longer timescale
- Revise understanding of requirements
- Respond to change quickly if necessary



## Adaptive Models
- Accept requirement cannot be known
- Change is most likely


## Empirical Process Control
Input -> Process -> Output -> Input | Loop
- New knowledge derived from output

### Three principles of Empirical Control
- Transparency
	- All information is important to develop product
	- Nothing is hidden, common understanding must be done
	- Enables inspection, adaptation
- Inspection
	- Frequently review the current state of work, progress and use of framework
- Adaptation
	- Make changes when necessary to adapt the product
	- Bring aspects that deviated back under control
	- Frequency of inspection and Adaptation depends on amount of risk we want to take

## How to organize technical activities
- Develop in a sequence of very small, self contained mini projects


### Generic iterative cycle
- Product vision
- Sprint in Scrum
- Last 1-2 weeks

1. Product vision, Rough initial planning
2. Choose features to be developed in this increment
3. Refine feature descriptions
4. Design Feature, implement and test
5. Integrate to system
6. System Testing
7. Review/Deploy

![[Pasted image 20240123175833.png]]






### Features of Iterative and Incremental Process
- Each iteration has well-defined goals. But these are not set until planning at the start of the iteration. Helps us handle change.
	- No massive, heavyweight up-front planning and commitment.
- Every iteration delivers a working release – a stable, integrated, tested, partially complete but releasable system
	- our proof that goals of the iteration are achieved and is a basis for involving the customer
- As the system grows, increment by increment, it is a working product at every stage. Potentially, we can release at any time, with the current subset of highest-value features.
BUT: 
- Adaptive Process Models handle change and complexity better than Predictive Models. However, these models tend to be more complex and may not be worth the effort for simple, low risk development.
- Adds overhead
- 


[[COMP3297 Lecture 1 - Introduction to Software Engineering|Previous Slide]] [[COMP3297 Lecture 3 -  Requirement Engineering|Next Slide]]

