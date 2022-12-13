##### Index
- Compression (CMP) and branches
- Loops
- Shortcut for bound checks
- Procedures


## 4.1 ARM Instructions/Programs for Decision Making
- ARM assembly includes a lot of decision making instructions
 - similar to if else statements
```armasm
CMP r3, r4; Compare r3 and r4
BEQ L1; Branch to L1 if r3 has same value as r4
BNE L2; Branch to L2 if r3 has different value as r4
```
### Conditional branches
- BEQ, BNE, etc are conditional branches
- B and BAL are unconditional branches


##### Example: finding the maximum value of 2 element
C/Java code: 
```Java
if (a > b) {
 max = a; 
} else {
 max = b; 
}
```


ARM assembly equivalent:
```armasm
 CMP r3,r4; Compare a&b 
 BLE b_max; b is the max
 MOV r5, r3; a is the max goto Exit
 B Exit; 
b_max MOV r5, r4; r5 (max) = r4 (b)
Exit
```




##### Example: bad employer
C/Java code:
```Java
if (year == next_leap) {
 pay = earn + bonus; 
} else {
 pay = earn - bonus; 
}
```



ARM assembly equivalent:
```armasm
 CMP r0, r1 ; Compare year & next_leap 
 BNE Else ; goto Else if year != next_leap
 ADD r2, r3, r4; pay = earn + bonus
 B Exit ; goto Exit
Else SUB r2, r3, r4; pay = earn - bonus
Exit
```


### Iteration in ARM assembly
```armasm
Loop ...; 
 CMP....;
 BNE ...;
 B Loop; Recursive
Exit
```



##### Example: Array searching
- C:
```C
while (a[i] == k)
 i++;
```


ARM assembly equivalent:
```armasm
/*  r6 = base address of a[i]
    r5 = vakue of k
    */

Loop ADD r12, r6, r3, LSL #2; r12 = address of a[i] with index i (r3) x 4 thru’ (r3 << 2)
 LDR r0, [r12, #0]; Temp reg r0 = a[i] 
 CMP r0, r5; Compare a[i] & k
 BNE Exit; goto Exit if a[i] != k 
 ADD r3, r3, #1; increment i if a[i] ==k 
 B Loop; goto Loop
Exit
```


### Shortcut for boubd checks
- Assume x is the [[ELEC2441-LT3#Signed integer|Signed integer]] of index of array
- when performing bound checking, x is treated as [[ELEC2441-LT3#unsigned integer|unsigned integer]] to perform

##### Example: check for IndexOutOfBounds error
- r1 holds x = -1, $x = 1111 1111 1111 1111 1111 1111 1111 1111_2$
- r2 holds another 32-bit of y = 12(upper bound)
`
```armasm
CMP r1, r2; Compare x & y
BHS IndexOutOfBounds; if x < 0 or x >= y goto IndexOutOfBounds (error)
```

##### Instruction format:
|Cond|$C|Address|
|-|-|-|
|4 bits|4 bits|24 bits|

- Table for condition field
|Hex Value|Meaning|Hex Value|Meaning|
|-|-|-|-|
|$0|EQ (Equal)| $8|HI (unsigned Higher)|
|$1|NE (Not equal)| $9|LS (unsigned Lower or Same)|
|$2|HS (unsigned Higher or Same)| $A|GE (signed Greater than or Equal)
|$3|LO (unsigned LOwer)| $B|LT (signed Less Than)|
|$4|MI (Minus, <0)| $C|GT (signed Greater Than)|
|$5|PL (Plus, >=0)| $D|LE (signed Less than or Equal)|
|$6|VS (oVerflow Set, overflow occurs)| $E|AL (Always)|
|$7|VC (oVerflow Clear, no overflow)| $F|NV (reserved)|

### Conditional Execution
- ARM instruction allows [[ELEC2441-LT3#Cond|cond]] field to be added to other instruction formats
 - e.g. ADDEQ
- More efficient for the ARM processor and coding

##### Example: [[#Example: bad employer|bad employer]]
Original assembly code:
```armasm
 CMP r0, r1 ; Compare year & next_leap 
 BNE Else ; goto Else if year != next_leap
 ADD r2, r3, r4;pay = earn + bonus if year = next_leap
 B Exit ; goto Exit
 
Else SUB r2, r3, r4; pay = earn - bonus if year != next_leap
Exit
```


New implementation with the new Cond:

```armasm
CMP r0, r1 ; Compare year (r0) & next_leap (r1) 
ADDEQ r2, r3, r4; pay (r2) = earn (r3) + bonus (r4) if year==next_leap 
SUBNE r2, r3, r4; pay (r2) = earn (r3)- bonus (r4) if year!=next_leap
```


## 4.2 ARM Instructions for Calling Procedures
##### Procedure
- a module/subroutine that a programmer use to structure programs
- The module can be reused multiple times
- Easier to understand

##### Steps to Implement a procedure
1) Put parameters in a place where the procedure can access;
2) Transfer control from the main or calling program (caller) to the procedure (callee);
3) Acquire the storage resources needed for the procedure;
4) Perform the desired task of the procedure;
5) Put the result in a place where the caller can access;
6) Return control to the point of origin – i.e. the caller.

Example: 
1) Put parameters in `r0 – r3`;
2) BL X; where X is the procedure to call
3) Acquire the storage resources needed for the procedure;
4) Perform the desired task of the procedure;
5) Place the results (if any) back to `r0` & `r1` as the return value registers;
	- `r0` and `r1` are reserved output
6) MOV pc, lr; return control back to caller

##### Link Register
- Contains a return address to return to the caller
	- [[ELEC2441-LT3#PC|PC]]+4 instead of [[ELEC2441-LT3#PC|PC]] as it will call itself indefinitely


Example of the function(procedure call) in C:
```C
int simp_F(int g, int h, int i, int j){ 
	int k;
	k = (g + h) – (i + j);
	return k;
}
```

ARM Assembly equivalent:
```arm-asm
simp_F:
	SUB sp,sp,#12 ; adjust sp for 3 registers
	STR r6, [sp,#8] ; push r6 onto stack
	STR r5, [sp,#4] ; push r5 onto stack
	STR r4, [sp,#0] ; push r4 onto stack
	ADD r5, r0, r1; perform calc : r5 = g+h
	ADD r6, r2, r3; perform calc : r6 = i+j
	SUB r4, r5, r6; r4 = (g+h) – (i+j)
	MOV r0, r4; copy r4 to the return value register r0
	LDR r4, [sp,#0] ; pop r4 from stack
	LDR r5, [sp,#4] ; pop r5 from stack
	LDR r6, [sp,#8] ; pop r6 from stack
	ADD sp, sp, #12 ; adjust sp to delete items
	MOV pc, lr; jump back to the caller
```


Simple Recursive program:
```armasm
Main MOV r0, #10 ; assign r0 (n) = 10
	BL Accum ; call the recurive procedure Accum
	END
	
Accum SUB sp,sp,#8 ; adjust sp for lr & r0
	STR lr, [sp,#4] ; push lr onto stack
	STR r0, [sp,#0] ; push r0 onto stack
	CMP r0, #1 ; Compare r0 (= n) to 1
	BGT L1 ; if n > 1 goto L1
	MOV r0,#1 ; if n <= 1, r0 = 1 (base case)
	ADD sp, sp, #8 ; pop lr & r0 off stack
	MOV pc,lr ; return to the caller
	
L1 SUB r0,r0,#1 ; if (n >=1) n = n-1
	BL Accum ; call Accum with (n-1)
	MOV r12,r0; save the return result from BL to r12
	LDR r0, [sp,#0] ; restore argument n from stack
	LDR lr, [sp,#4] ; restore return address from stack
	ADD sp,sp,#8 ; update sp pointer to pop 2 registers
	ADD r0,r12,r0 ; compute n + Accum(n-1)
	MOV pc,lr ; return to the caller
```



## 4.3 A Diversity of ARM Addressing Modes
### Addressing modes
- Total of 12 addressing modes
- Ways to specifies the address
- To make the addressing mode more precise/compact
	- shifting or arithmetic operands are alowed
	
##### Immediate addressing mode
- The operand is a constant
- e.g. `ADD r2, r0, #32`

##### Register addressing mode
- aka simple register addressing mode
- The operand is a register
- `ADD r2, r0, r1`

##### Scaled Register addressing mode
- second operand is shifted before taking the value to perform instruction
- `ADD r2,r0,r1,LSL #2; r2 = r0 + (r1 << 2)`

##### PC-Relative addressing mode
- the addressing mode which involves sum of [[ELEC2441-LT3#PC|PC]] and a constant
- `BEQ 1000; Branch to 1000`

##### Immediate offset addressing mode
- Constant is added to a register
- `LDR r5, [r3, #32]; address in r3 + 32 = address of load`

##### Register offset addressing mode

- `LDR r5, [r3, r1]; load value in [address in r3 + address in r1] to r5`

##### Scaled Register Offset
- Perform shift on register before it is added to base register
- `LDR r5, [r3, r1, LSL#2] ;` addr. in r3 + (r1<< 2) to get the mem. location for loading into r5




## 4.4 Translating & Starting a Program
- Compiler translate C program to assembly program (.c -> .s)
	- something machine understands
- Assembly program is assembled/compiled to object module (.s -> .o)
- 