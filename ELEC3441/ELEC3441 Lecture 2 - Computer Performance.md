
[[ELEC3441 Lecture 1 - Introduction|Last Lecture]] [[ELEC3441 Lecture 3 - Instruction Set Architecture|Next Lecture]]

### Ways to measure performance
- Execution time
	- Time required to finish a task
- Throughput
	- Number of tasks can be finished per unit time

### Relative Performance
- Define as 1/Execution Time

if computer A is n times faster than computer B by n times:
$$n = \frac{\text{Performance}_B}{\text{Performance}_A} = \frac{\text{Execution Time}_A}{\text{Execution Time}_B}$$
### Ways to measure execution time

##### Wall Clock Time
- Time elapsed from user perspective
- includes OS overhead, I/O, idle time, time shared with other users
##### CPU Time
- Time spent on user task on CPU
- User CPU + OS CPU
- focus of this course
- Calculated by $$\frac{\text{number of instruction}}{\text{program}} \cdot \frac{\text{number of cycle}}{\text{instruction}} \cdot \frac{\text{time}}{\text{cycle}}$$
- CPU Time = Cycle Count x Cycle time = Cycle Count / Clock Frequency

To improve performance
1. Increase clock frequency
2. Reduce Cycle Count


##### Cycles per Instruction
- Generally Average CPI
- For n class of instructions:
Average CPI would be $$\sum_{i = 1}^{n}\text{CPI}_i \cdot \frac{\text{InstructionCount}_i}{\text{InstructionCount}}$$

### Number of instructions

##### Example 1 : addition
Key takeaway: Actual instruction count can be different from normal lines count
```armasm
	i = 0
loop: a = a + 1
      i = i + 1
      if i < 10 goto loop
```
- Number of instructions: 4
- Number of dynamic instruction: 1 + 3 x 10 = 31
- Number of cycles: 31

##### Example 2: multiplication
Key takeaway: Number of instructions can be data dependent
```armasm
r = 0
for (i=b; i>0; i=i-1)
  r = r + a

r = a * b
```
- Naive way: add a for b times
	- Number of dynamic instructions: 3b
	- Number of cycles: 3b
- Smart way: a * b
	- Number of instructions: 1
	- Cycles: 1?



### Instruction Count and CPI
- The number of instructions in a program depends on
	- Nature of application
	- Compiler techniques
	- Type of available instruction of an ISA
- Average cycles per instruction depends on
	- CPU microarchitecture
	- ISA (CISC vs RISC)
	- The current running state of CPU
- Different instructions may have different CPI
	- Average CPI affected by instruction mix




### CISC vs RISC
- CISC: Complex Instruction Set Computer
- RISC: Reduced Instruction Set Computer

- 2 different strategies
- CISC: CPI > 1, short cycle time.
- RISC (unpipelined): CPI = 1, long cycle time.
- RISC (pipelined): CPI = 1, short cycle time.


### CISC
- Complex instructions and addressing modes.
- Implemented using multiple clock cycles (microcode).
- Allows shorter compiled code, easier for compiler.
- Relevant in embedded systems.
- Drawbacks: Less attractive as compiler techniques improve, complex hardware is slow.

### RISC
- Simple instructions and addressing modes.
- Simpler hardware design allows optimization and easy pipelining.
- Simple ISA allows compiler optimization.
- Generated code length is generally longer.
- Most ISAs after the 80s are RISC.

### Amdahl's Law
- Describes overall speedup due to speed improvement that applies to a portion of the system.
- Speedup = 1 / ((1-P) + P/S), where P is the portion of the system that can be sped up by a factor of S.
- In most applications, only a portion of the computation can be sped up.

### Benchmark Programs
- A set of programs used to compare processor performance.
- Need to be representative of typical workload.
- Avoid over-optimization for specific benchmark.
- Example: SPEC CPU2006.


[[ELEC3441 Lecture 1 - Introduction|Last Lecture]] [[ELEC3441 Lecture 3 - Instruction Set Architecture|Next Lecture]]


riscv32-unknown-elf-gcc -O0 -S branch1.c -o branch1_0.s 
riscv32-unknown-elf-gcc -O0 -S branch2.c -o branch2_0.s 
riscv32-unknown-elf-gcc -O1 -S branch1.c -o branch1_1.s 
riscv32-unknown-elf-gcc -O1 -S branch2.c -o branch2_1.s 
riscv32-unknown-elf-gcc -O2 -S branch1.c -o branch1_2.s 
riscv32-unknown-elf-gcc -O2 -S branch2.c -o branch2_2.s 
riscv32-unknown-elf-gcc -O0 -S loop1.c -o loop1_0.s 
riscv32-unknown-elf-gcc -O0 -S loop2.c -o loop2_0.s 
riscv32-unknown-elf-gcc -O1 -S loop1.c -o loop1_1.s 
riscv32-unknown-elf-gcc -O1 -S loop2.c -o loop2_1.s 
riscv32-unknown-elf-gcc -O2 -S loop1.c -o loop1_2.s 
riscv32-unknown-elf-gcc -O2 -S loop2.c -o loop2_2.s 
riscv32-unknown-elf-gcc -O0 -S branch.c -o branch_0.s 
riscv32-unknown-elf-gcc -O0 -S case.c -o case_0.s 
riscv32-unknown-elf-gcc -O1 -S branch.c -o branch_1.s 
riscv32-unknown-elf-gcc -O1 -S case.c -o case_1.s 
riscv32-unknown-elf-gcc -O2 -S branch.c -o branch_2.s 
riscv32-unknown-elf-gcc -O2 -S case.c -o case_2.s 
riscv32-unknown-elf-gcc -O0 -S funcall1.c -o funcall1_0.s 
riscv32-unknown-elf-gcc -O0 -S funcall2.c -o funcall2_0.s 
riscv32-unknown-elf-gcc -O1 -S funcall1.c -o funcall1_1.s 
riscv32-unknown-elf-gcc -O1 -S funcall2.c -o funcall2_1.s 
riscv32-unknown-elf-gcc -O2 -S funcall1.c -o funcall1_2.s 
riscv32-unknown-elf-gcc -O2 -S funcall2.c -o funcall2_2.s