
[[ELEC3441 Lecture 4 - Single Cycle Processor|Last Lecture]] [[ELEC3441 Lecture 6 - Branch Prediction|Next Lecture]]

## RISC vs CISC
- CISC can have CPI greater than 1
- RISC pipelined can have 1 CPI and short cycle time


## Pipelining
- Separating steps into different pipeline
	- Faster execution
- Complete n instructions in n+(d-1) time
	- d as number of steps in processing 1 instruction

E.g. Buy food from canteen
1. Order
2. Get Food
3. Get Drink


### Pipelined Control
- some instruction require previous data from register
	- use more register to delay it


#### Structural Hazard
- Limitation in Hardware
- More than 1 pipeline stage requests for same physical hardware

Solution:
- Add extra resources
- Change the resource to handle more than 1 instruction
- Change the instruction to let them access hardware at different time
	- Stage stall is needed

Example: Memory
- IF and MEM get memory at same time, mem cannot do concurrent read/write
- Solution: Replicate memory to instruction and data cache

Example: Regfile

##### Pipeline Bubble
- Causes pipeline stall
- e.g. NOP instruction (No operation), Special control decoding, 


#### Data Hazard
- Arises when pipeline stage access data location that is incompatible with ISA contract with programmer
- Happens on Memory location

- **Read After Write**: Later read happen before an earlier write
	- Only case for 5 stage pipeline
- **Write After Read**: Later write happens before an earlier read
- **Write After Write**: Later write happens before an earlier write
- 

**Solution 1 - Stalling**: Wait for result to be available by freezing earlier stage pipeline
**Solution 2 - Data Forwarding**: Route data as soon as after it is calculated to earlier pipeline stage



#### Control Hazard
- Result of branches and jumps

**Unconditional jumps**: Next instruction is determined by the jump instruction
**Conditional branches**: Next instruction depends on result of branch comparison

**Solution 1 - Change ISA**: 2 instruction following the branch operation will always execute
- Branch Delay slot created (2 consecutive instruction executed after possible branch)
- Compiler may insert instructions in branch delay or NOP
	- More efficient (instruction that is executed regardless of branch target)

[[ELEC3441 Lecture 4 - Single Cycle Processor|Last Lecture]] [[ELEC3441 Lecture 6 - Branch Prediction|Next Lecture]]