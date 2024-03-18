
[[ELEC3441 Lecture 2 - Computer Performance|Last Lecture]] [[ELEC3441 Lecture 4 - Single Cycle Processor|Next Lecture]]

# Instruction Set Architecture
## RISC-V ISA
- RISC-V is a new RISC design from UC Berkeley.
- It’s a realistic and complete Instruction Set Architecture (ISA), but it’s open and small.
- It’s not over-architected for a certain implementation style.
- It has 16, 32, 64, 128-bit address space variants.
- This course focuses on RV32.

## Design and Features
- RISC-V is designed to be extensible.
- It supports high-performance multiprocessing.
- It has efficient instruction encoding for embedded systems.
- It’s easy to subset/extend for education/research.
- It comes with a complete compilation toolchain.
- It supports FPGA and ASIC designs.

## RISC-V ISA Overview
- The RISC-V processor has a load-store architecture.
- Most instructions operate on values directly to and from the register file.
- It has dedicated load/store instructions to transfer data between the register file and main memory.
- RV32 has a 32-bit word length.
- It has a fixed instruction length of 32 bits.
- A data word is 32 bits wide.
- RISC-V ISA is designed to allow variable-length instruction code and instruction extension.
- The course does not cover variable-length instruction code and instruction extension.


## RV32 Processor State - Base Integer Design
- Register file with 32 32-bit general purpuose registers
	- x0 - x31, x0 always be 0




## RISC-V Instruction Encoding
- each supported instruction in ISA must be uniquely encoded
- Good encoding optimize
	- Regularity
	- Simple hardware decode
	- Instruction Length
	- Entensibility
- Example: RV32
	- 32-bit wide instruction
	- Favors HW regularity than Human Readability
	- 6 general type of instruction
		- R-type, I-type, S-type, SB-type, U-type, UJ-type

### Integer Register-Register Operation
- Take 2 source register input(rs1, rs2) to produce 1 destination register (rd)

### R-type instruction Encoding
| 31 25  | 24 20 | 19 15 | 14 12  | 11 7 | 6 0    |
| ------ | ----- | ----- | ------ | ---- | ------ |
| funct7 | rs2   | rs1   | funct3 | rd   | opcode |

- Rightmost 7 bit as opcode
- rs2, rs1, rd always at exact bit position
- fucnt3 contains basic operation
- funct7 modifys nature of funct3
#### ADD/SUB
```RISCV
ADD t0, a0, a1
ADD t1, a2, a3
SUB a4, t0, t1
```
C equivalent:
```C
y = (e + f) Ð (g + h);
```
- 3 operands
	- 2 source and 1 destination
	- dest at first, then 2 source
- Discard overflow, only lower 32bit is written
#### Bit Operations
```riscv
AND rd, rs1, rs2 
OR rd, rs1, rs2
XOR rd, rs1, rs2
```
- Similar semantics with ADD/SUB

### Immediate Operations
- Register-Immediate Operations
	- Add a register variable with a numerical constant


### I-type Instruction Encoding
| 31 20     | 19 15 | 14 12  | 11 7 | 6 0    |
| --------- | ----- | ------ | ---- | ------ |
| imm[11:0] | rs1   | funct3 | rd   | opcode | 

- U-type needed to continue execution
- rs1 still at same pos
	- regularity proven

#### ADDI
C code:
```C
a1 = a1 + a0 + 1;
```

RISC-V Code
```RISCV
ADD t0, a1, a0
ADDI a1, t0, 1
```

- Subtract by using negative immediate

### Sign Extension
- Casting integer to more bits representation
- Fill additional bit with 1 for negative number
- Fill additional bit with 0 for non-negative number



### U-Type Instruction Encoding
| 31 12      | 11 7 | 6 0    |
| ---------- | ---- | ------ |
| imm[31:12] | rd   | opcode |

- Load upper bit of immediate constant
- Paired with any Register-Immediate constant
- Opcode and rd at same place



### Memory Operations
- All program data and instruction are stored in main memory
	- Array, structure, user data, string
- Need dedicated instruction to load/store data between register file and main memory

### RV32 Memory model
- Memory is byte-addressable
- Native data type
	- Word: 32bit (int length)
	- Half-word: 16-bit (short length)
	- Byte: 8 bit (char length)
- Little Endian
	- Least Significant byte in lowest address
| 0x000A0007 0x000A0006 0x000A0005 0x000A0004 0x000A0003 0x000A0002 0x000A0001 0x000A0000 |
| --------------------------------------------------------------------------------------- |
| 

### Word alignment
- Naturally aligned at 4-byte boundary
- Half words aligned at 2-byte boundary
- RV32I allows non-aligned access

### Bytes and Words
- Bits Left of least significant $k$ bits: Word address
- Bits right of least significant $k$ bits: Byte Offset

### Memory Operations


#### Load
- dest <- M[base + offset]
```C
int y = e + f[3];
```
Let e = a0, f = a1, y = a2, we have
```RISCV
lw t0, 12(a1) # 12 = 3(word position) x 4(word length)
ADD a2, a0, t0
```
LW: Load word
LH: Load Half-word
LB: Load byte

- as [[#I-type Instruction Encoding|I-Type]] instructions
- funct3 encodes length of value to be loaded
- 12-bit offset is sign extended


#### Store
```C
int f[7] = f[6] + f[5]
```
Let f be in a0, we have
```RISCV
lw t0, 20(a0)
lw t1, 24(a0)
ADD t0, t0, t1
SW t0, 28(a0)
```
SW: Save word
SH: Save Half
SB: Save Byte

- as [[#S]]


### Branch Operation
- Normally [[ELEC2441-LT3#Program Counter|Program Counter]] is incremented by 4 to get next instruction
- Fetching and changing the PC is needed during Decision-making constructs
	- if then else
- Two types of control transfer

#### Jump
- Unconditional
- Similar to `GOTO`
```riscv
		0xA000 addi a0, zero, 9
		0xA004 JUMP aLabel
		0xA008 ori a0, a0, 27
		.
		.
aLabel: 0xBC08 subi a0, a0, 18
		0xBC0C and a1, a1, a0
		0xBC10 <. . .>
```



#### Branch 
- Conditional

| 31      | 30     25 | 24 20 | 19 15 | 14 12  | 11     8 | 7       | 6    0 | 
| ------- | --------- | ----- | ----- | ------ | -------- | ------- | ------ |
| imm[12] | imm[10:5] | rs2   | rs1   | funct3 | imm[4:1] | imm[11] | opcode |


