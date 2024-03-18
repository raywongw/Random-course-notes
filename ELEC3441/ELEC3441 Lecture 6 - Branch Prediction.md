
[[ELEC3441 Lecture 5 - Pipelining|Last Lecture]] [[ELEC3441 Lecture 7 - Memory and Cache I|Next Lecture]]


## Branch Prediction
- ~95% accuracy for modern branch prediction


## Static Branch Prediction
- Determine by whether it jump to previous code or next code

### Dynamic Branch Prediction
- Temporal correlation: Learn how a branch is resolved to predict
- Spatial correlation


### 2-Bit Branch Prediction
- a FSM based on branch history
- a Branch History Table of lower k bit of address
	- made up of flip flops
	- a mistake -> lower accuracy
	- still same 

## Two-Level Branch Predictor
- much better result

## Branch Target Buffer
- a data structure with predicted target address and branch target buffer
- if bp = taken then nPC = target address else nPC = PC+4
- help jump to other address faster
- 


## Combining BTB and BHT
- BTB more expensive than BHT
- BTB can redirect fetch at early stages in pipeline and accelerate indirect branch
- BHT can hold more entries
- Use BTB at early stage(Instruction Fetch), BHT at later stage(Branch Address Calculation)


## Uses of Jump Register


## Exceptions and Interrupts
### Interrupt
- Event requests attention of processor
- asynchronous
- External event

- more easier to handle
	- wait several clock cycle to handle it

### Exception
- Internal event
- Synchronous
- can happen in all stages
	- PC address exception, illegal opcode, overflow, data address exception
### Handling Exception
Make pipeline with exception
- TO make the exception happened one by one



[[ELEC3441 Lecture 5 - Pipelining|Last Lecture]] [[ELEC3441 Lecture 7 - Memory and Cache I|Next Lecture]]