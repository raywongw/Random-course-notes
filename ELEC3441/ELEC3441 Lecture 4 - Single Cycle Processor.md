
[[ELEC3441 Lecture 3 - Instruction Set Architecture|Last Lecture]] [[ELEC3441 Lecture 5 - Pipelining|Next Lecture]]


### Register
n-bit register -> n DFFs
only focus on thig in 1 clock cycle


### Register File
- Reading is combinational
- Writing is sequential
	- Only happen at rising clock edge
	-


## Datapath: Reg-Reg ALU instructions
![[Pasted image 20240208105956.png]]PC sent to memory to fetch instruction and increment by 4 at same time
- move to next 

ra1 -> rd1 (address to data)
ra2 -> rd2 (address to data)

see [[ELEC3441 Lecture 3 - Instruction Set Architecture#R-type instruction Encoding|R-type instructions]] for details

## Datapath: Reg-Imm ALu Instructions
![[Pasted image 20240208113955.png]]
see [[ELEC3441 Lecture 3 - Instruction Set Architecture#I-type Instruction Encoding|I-type instructions]] for details


Problem: To merge 2 instructions
- have to identify if it contains R-type instruction/I type instruction
Solution: use mux to select from opcode
- OP vs OP-Imm
![[Pasted image 20240208114829.png]]

## Load Instructions
- use ALU calculate address
- use mux to select data for regfile
	- mem/ALU


## Store Instructions
- also use ALU to calculate address


### Conditional Branches
- logic to compare rs1 and rs2
	- equal / not equal / less than / greater than



![[Pasted image 20240219114327.png]]
- Add a mux to select either PC+4 or the address to be jumped to
- Add branch logic for comparing them
	- Use result for selecting where to jump
- red arrow: hardware signal


## Unconditional Jump
![[Pasted image 20240219121535.png]]

## Hardwired Control Table
| Instruction | Op2Sel | AluFunc | WBSel | RegWriteEn | MemWrite | PCSel   |
| ----------- | ------ | ------- | ----- | ---------- | -------- | ------- |
| **ADD**     | RS2    | ADD     | ALU   | T          | F        | PC+4    |
| **SUB**     | RS2    | SUB     | ALU   | T          | F        | PC+4    |
| **ADDI**    | IMI    | ADD     | ALU   | T          | F        | PC+4    |
| **SLL**     | RS2    | SLL     | ALU   | T          | F        | PC+4    |
| **LW**      | IMI    | ADD     | MEM   | T          | F        | PC+4    |
| **SW**      | IMS    | ADD     | X     | F          | T        | PC+4    |
| **BEQ**     | IMB    | X       | X     | F          | F        | PC+4/BA |
| **JAL**     | IMJ    | X       | PC+4  | T          | F        | JA      |
| **JALR**    | IMI    | X       | PC+4  | T          | F        | JRA     |
|             |        |         |       |            |          |         |



## Single-Cycle Hardwired Control
- Assume clock period is sufficiently long for all instruction to be completed
	1. Instruction Fetch
	2. Decode and register fetch
	3. ALU operation
	4. Data fetch
	5. Register write-back
- Too slow for actual use
	- Pipelined design




[[ELEC3441 Lecture 3 - Instruction Set Architecture|Last Lecture]] [[ELEC3441 Lecture 5 - Pipelining|Next Lecture]]