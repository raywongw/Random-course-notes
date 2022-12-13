# LT3 Instructions of the ARM Assembly


## 3.1 Introduction of An Instruction Set
von Neumann
- father of computer
- force us study this course ge cls ppl
- Instructions should be placed on same memory

### ARM 32-bit
- easier to write
- Compatible with ARM64


## 3.2 Basic Operations of the ARM Assembly Language
Most arithmetic and lofical operations reqire 1 or 2 operands.

- There are some unconditional branch and conditional branch instruction

###### 3 basic type of operand:
- Register operand
- Memory operand
- Constants


### ADD operation
 `ADD a(rd), b(src), c(src);`
- `a b c`: represents different registers with unsigner decimals
- `a`: destination register to place the sum of b and c
- `b c`: Source register to add
```
r8 -> [ALU] <- r9
        |
        v
	   r10
```
##### Example of ADD operation
- `a = b + c + d + e;` in C/Java operation
- Translation to ARM instruction:
``` armasm
ADD a, b, c; 
ADD a, a, d;
ADD a, a, e;
```

### SUB operation
`SUB a(rd), b(src), c(src);`
- `a b c`: Different registers
- `a`: destination register to place the difference of b and c
- `b c`: Source register to subtract from and to respectively


### MOV operation
`MOV r1, r2;`
- Copy value of r2 to r1 (r1 = r2)


### B operation 
- aka BAL operation (Branch as always)

`B 2500;`
- unconditional branch to [[#PC|Program Counter]] + 8 + (2500 words * (4 byte))
- integer behind B: no of word

##### PC 
- Current address in the ==program counter==

### LDR operation
- aka Load into Register
- load values/pointers to register
- 


### Demo program to compute sum and difference of 2 decimal
```arm-asm
Num1 DCD 100 ; assign
```
- Assign a variable `Num1` as a decimal number 100

```arm-asm
Num2 DCD 200
```
- Assign a variable `Num2` as a decimal number 200

```arm-asm
	 LDR r0,=Num1 ; 
```
- load address of `Num1` into register `r0`

```arm-asm
     LDR r1, [r0,#0] ; 
```
- load the value of `Num1` into `r1`
- `[*address of variable*, offset of integer]`first variable in [] means address of variable in the [[ELEC2441-LT2#Registers|register]]
- second variable in [] means the offset of bytes

```arm-asm
	 LDR r2, [r0,#4] ; 
```
- load the value of `Num2` into `r2`

```arm-asm
	 ADD r3, r1, r2 ; 
```
- r3 = r1 + r2, refer to [[#ADD operation|ADD]]

```arm-asm
     SUB r4, r3, r1 ; 
```
- r4 = r3 - r1, refer to [[#SUB operation|SUB]]


```arm-asm
     END
```
- End the program



## 3.3 Operands of the ARM Assembly Language

/### what is he talking

### Registers
- most primitive and frequently i
- used operands in any assembly program
- size of an register in ARM: 32 bit
- assuming only 16 registers is available (`r0`,`r1`,`r2`,...`r15`)


### Summary of ARM operands and instructions
|Name|Example|Usage|
|------|---------|-------|
|16 registers|r0, r1, r2,...,r11,r12,sp,lr,pc|Fast storage for data, where it is stored for performing arithmetic
|2^32 memory addresses| Memory[0], Memory[4],....,Memory[4294967292]|Accesssed only by data transfer 



## 3.4 Signed and Unsigned Numbers
- ARM uses 32 bit unsigned integer as a word

### Unsigned integer
- 32 bit integer 
- Range: 0 - $2^{32}-1$

### Signed integer
- aka signed 
- Uses the MSB to represent sign
	- 0 means positive
	- 1 means negative
- Range: -$2^{31}-1$to +$2^{31}-1$
- Repeated 100.....0000 (-0) and 000.....0000(+0)

### 2's complement
- Avoiding the +0 and -0 case in [[#Signed integer]]
- Most used in modern computer
- MSB still denote magnitude of number
	- When MSB is 0, other bitd represents magnitude （0 to $2^{31}-1$)
	- When MSB is 1, other bits have to flipped to represent magnitude ($-2^{31}$ to -1)
- Range: -$2^{31}$ to +$2^{31}-1$


### Sign extension
- Take the MSB and extend it until the new limit is reached
- e.g.16bit 1000...0011 extend to 32 bit
	- original: 0000 0000 0001 0000
	- new: 0000 0000 0000 0000 0000 0000 0001 0000
- Useful when transfering value in immediate field to ARM register


### Overflow
- the value in ALU cannot be represented by all bits in register
- handled by program or the OS
- e.g. The 2's complement MSB will be incorrect



## 3.5 Instruction Formats of the ARM Processors
- All ARM instruction are 32 bits

### Format of a ARM instruction
|[[#Cond]]|[[#F]]|[[#I]]|[[#Opcode]]|[[#S]]|[[#Rn]]|[[#Rd]]|[[#Operand2]]|
|-|-|-|-|-|-|-|-|
|4 bits|2 bits|1 bit|4 bits|1 bit|4 bits|4 bits|12 bits|
#### Cond
- For conditional branch instructions

#### F
- aka Format of instruction
- allows ARM to different instruction format when needed

#### I
- aka Immediate
- Two cases: 
	- I == 0: 2nd Source Operand will be a register
	- I == 1: 2nd Source Operand will be a 12-bit constant (immediate)

#### Opcode
- Operation code of the ARM instruction

#### S
- aka Set Condition Code
- Related to conditional branch instructions

#### Rn
- First source register

#### Rd
- Destination register for storing the result of operation

#### Operand2
- aka Second source operand
- A register or a immediate




### Format of a Data Transfer instruction
- Used for load and storing instructions
|Cond|F|Opcode|Rn|Rd|Offset12|
|-|-|-|-|-|-|
|4 bits|2 bits|6 bits|4 bits|4 bits|12 bits|



## 3.6 Logical Operations of the ARM Assembly

### Bit-by-bit AND (AND)
- similar to `&` in C/Java

### Bit-by-bit OR (ORR)
- similar to `|` in C/Java

### Bit-by-bit NOT (MVN)
- similar to `~` in C/Java


### Bit shifting
- usually bundled with other ARM instructions
- e.g. MOV r6, r5, LSR r3; (r6 = r5 >> r3)

#### Shift left (LSL)
- similar to `<<` in C/Java
- used to multiply a number by $2^n$, where n is the number of bit shifted


#### Shift right (LSR)
- similar to `>>` in C/Java
- used to divide a number by $2^n$, where n is the number of bit shifted


## Summary

 The ARM Assembly Language (or Instruction Set) is the most popular 32-bit instruction set with its simplicity & efficiency as based on the stored-program concept.
 ̈ Basic ARM instructions include the fundamental operations for arithmetic (ADD/SUB) and (binary) logical operations [AND/OR] typically requiring 3 operands. Besides, the ARM assembly language also has other instructions requiring 2 or 1 operand only. Examples include the MOV instruction for data transfer and the conditional / unconditional branch instructions to control the program flow.
 ̈ ARM allows 3 major operand types including: register operands, memory operands & constant operands to be used in various instructions.
o Registers (including 16 registers as r0....r12, sp, lr, pc) are the most common and frequently used operands in many ARM instructions;
o Memory operands can be used to hold simple variable values or data structures such as arrays (base address + offset) or linked lists. They are often used in many data transfer instructions (like LDR – load word into register or STR – store word from a register) to transfer data between the memory and registers. Each computer word (as integers, instructions or other data values) in ARM is 32 bits (i.e. 4 bytes) sequentially stored as 4 consecutive bytes in the main memory. Thus, it is important to notice that with the base address of an array as v, to access v[i] as the i-th integer/word, the address of v[i] = v + i * 4 (i.e. in multiples of 4 bytes);
o Constant operands: a constant (to be specified as #c) can be used in various ARM instructions. An example is to specify the “constant” offset as in “LDR r0, [r1, #8]” for a fixed offset of 8 bytes from the base address stored in r1.



When an ARM word (of 32 bits) is used to represent an unsigned integer, the range of values is from 0 to 232-1 (i.e. 0 ....4,294,967,295 ~ 4.3G). With the leading sign for sign and the remaining 31 bits for magnitude/value, the sign-and-magnitude has its range of -ve and +ve integers as : -(231- 1)....-0,+0,...., +(231- 1). To avoid the shortcoming of both -0 and +0 in sign-and-magnitude scheme, the ARM computers adopt the 2’s complement scheme with the range of:
-(231)....-1,0,...., +(231- 1) to denote any signed integer as
(b31 × -2 31) + (b30 × 2 30) +....+ (b1 × 2 1) + (b0 × 2 0).
Basically, for any signed integers,
o Sign extension concerns about extending a signed integer of n bits (under the 1’s or 2’s complement scheme) to a number with more than n bits – without changing its magnitude. The shortcut technique is to take the MSB (sign bit) from the smaller quantity and “extend” it to fill the new bits of the larger quantity, thus the name “sign extension”!
o When the result of such operation cannot be represented by all the H/W bits (say the 32 bits of an ARM register), overflow occurs.




All ARM instructions are exactly 32 bits – the same size as a computer word. This general design principle of “regularity” for instruction formats promote “simplicity” (and also efficiency) as in the RISC architectures. There are 3 common instruction formats for the data processing (DP), data transfer (DT) and conditional instructions. Each type of instruction format differs in the number of bits allocated to the op-code, constant/register operand(s) and/or conditional codes.


ARM instructions (like AND/ORR/MVN) operate on fields of bits within a word or even on individual bits are called logical operations. In ARM, shift operations are NOT separate instructions. Typically, they are bundled with other microprocessor instruction set. That is ARM offers the ability to shift the 2nd operand as part of any data processing (DP) instruction. For example, shifting the 2nd register operand r2 to left by 2 bits (i.e. = r2 × 4) before adding with r1 and storing the result to r5 as in the following ADD instruction:
ADD r5, r1, r2, LSL #2; r5 = r1 + (r2 << 2)


