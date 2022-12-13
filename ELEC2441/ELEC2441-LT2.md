# LT2 Basic Organization, Operations and I/O Mechanisms of Modern Computers

## 2.1 Logic Gates for Modern Computers
AND, OR, NEG, NAND, NOR


## 2.2 RS flip-flops (FFs), clocked RS-FFs and D-type FFs

### 1. RS Flip-flop (Latch)
Structure:
![[RSFF.png]]

Truth Table:
|`R`    `S`|`Qn+1` `Q'n+1`|
|----|-------------|
|0   0|`Qn` `Q'n`|
|0 1|1 0|
|1 0|0 1|
|1 1|0 0|


Avoid R = 1 and S = 1, since it makes Q and Q' 0 and 0, which is not complement to each other

- JK dlip flop uses NAND gate instead of NOR gate in RS flop flop


### 2. Clocked RS flip flop
Structure:
![[Clk_RSFF.png]]

Truth Table:
|`R`    `S`|`Qn+1` `Q'n+1`|
|----|-------------|
|0   0|`Qn` `Q'n`|
|0 1|1 0|
|1 0|0 1|
|1 1|0 0(avoid)|
- Avoid R = 1 and S = 1
- clock signal is synchronized with CPU clock(e.g. 4 GHz)

#### Level triggered flip-flop
- hold for long duration
- Multiple transitions may occur when R/S change and clock is on/off

#### Edge triggered flip-flop
- triggered at clock rise or clock fall
- More complex circuit to detect rising edge/falling edge
- 

### 3. D Flip flop
D: Data Transfer

- [[#RS Flip-flop]] with a inverter, such that it input `D` and `D'`
Structure:
![[CLK_DFF.png]]
- Truth Table: 
|`D`|`Q`|
|-|-|
|0|0|
|1|1|


##### Q: why not use a line instead
- To stabilize the signal since `D` can be fluctuating 
- Can be able to transfer data to other registers 


- input `D` is copied to `Q` and locked up until next clock pulse arrives
- Data (a bit) is locked in the DFF until next clock cycle
- Useful as a latch (temporary storage) and store data

#### Pratical waveforms:
Real signal is not as square as ideal form
- signal takes a finite amount to rise and fall



## 2.3 FFs As Registers to Transfer Data
### Registers
- transfer data to different component of computer
- Input -> databus -> register in CPU -> databus -> Output
- An n-bit register with `n` D flip-flops, which can store `n` bit of data
- To store input data, set LOAD to 1, then load x1, xn with data, then clock it from 0 to 1

##### Diagram of Register
![[Register.png]]
- Input: `x1`, `x2`, ... ,`xn` 
- Load: Control command to instruct flip flops to load in data from input and store
- Output: `y1`, `y2`, ... , `yn`


#### Parallel transfer from a register to another
Above: Register 0
Below: Register 1

![[Parallel Transfer.png]]
- Output of Register 0 is transferred to Register 1 when CLOCK changes from 0 to 1

To transfer, 2n DFF is needed to transfer n bit of data

#### Shift Register
- used in ARM processor
- Data are shifted bit by bit
- `Q1` shifted to `Q2`, `Q2` shifted to `Q3`, and etc... 
![[Serial transfer.png]]
- each bit may have specific format and have encrypted value
- when extracting 8 bit, 
	e.g. 8 bit info 1001 1101
	each bit can do some operation to other (e.g. arithmetic operations)
	- ARM processors have much usage on this


## 2.4 Basic Operations of Data Buses
- Registers can combine with other transportation medium
- Data bus, Control Bus, Address Bus
- Specific on data bus to show relationship on data bus to transfer data with register

#### Bus
- a set of parallel conductors carries signal
- a `n` bit bus has `n` parallel wires

Tri-state buffer (tri-state logic gate)
- Controlling the type of information to flow to buses
- Having state of High, Low and High Z (high impedance)
- control transfer of data
- an Active on High
	When enable input=1:
	- Logic operates with wither High and Low state
	When enable input=0:
	- output is disconnected, forming an open circuit

Simplified 1-bit data bus:
![[data bus.png|500]]
- controlled with 2 tri-state buffer (control writing the devices or reading from devices)
- Only one device can send data to multiple other devices during any clock cycle
- More than one device sending info is called bus contention
	- causing hardware damage
- A device has control of bus during the clock cycle is called bus master
	- others are called bus slaves
	- Bus arbitration is done from time to decide which device is bus master





## 2.5 Encoders, decoders, MUX and uses in Modern Computer

### Decoders 
^60040f
- decode n bit of binary number to $2^n$ outputs
e.g. 3-bit to 8-line decoder
![[3 bit decoder.png]]

### Encoders
- Inverse of [[#^60040f|decoder]], converting $2^n$ inputs to n bit output
e.g. 8-line to 3 bit encoder
![[3 bit encoder.png|400]]

### Multiplexer
- Select inputs from SELECT input, and outputs from the input ports ![[2-bit multiplexer.png|500]]
- Useful in ARM Processors
- Can be implemented using a decoder with logic gates



## 2.6 Basic Computer Organization (CPU, Memory & I/O Units)
### Input unit
- Get info from outside e.g. keyboard, mouse, storage device

### Output unit
- return processed data to outside e.g. Monitor, printer, storage device

### Memory unit
- Stores instructions and data
- Made up of large amount of memory unit
- Has a unique address for each unit hich contains collection of bits e.g. 0x100C
Memory table to its content e.g.
Address |Content 
--------|-------
0x1000  | 0110 1100 -> 6C (Hex value)
0x1004  | 


### CPU
- Consists of Control Unit and Datapaths

#### Control Unit
- One of the highest manager in the compute system
- Send control signal into other units
- Contains Timing and Control Logic (TCL), Instruction decoder

#### Datapath
- Consists of ALU and Registers

##### ALU 
- Performs arithmetic and logic operations

##### Registers
- aka Accumulators
- As storage (flip-flops) for storing temporary daya and intermediate results during calculations in CPU
- More general-purpuose registers influences performance of CPU
- e.g. R0-31 for general use / F0-63 for floating point operations


### Buses
##### Data Bus
- Transfer data from units to other units

##### Address Bus
- Carrying address information from [[#Memory unit|memory unit]] 
- 

##### Control Bus
- Carries control information



## 2.7 Basic Operations of an Arithmetic Logic Unit ([[#ALU|ALU]])

### Arithmetic Circuit
- Responsible for performing operations (+ - x /) and [[#2 1 Logic Gates for Modern Computers|logical operations]]



Simplified Example of Assembly Program



|Address|Content|
|-|-|
|$E0|$10|
|$E1 | $A1|
|$E2|$2B
|$E3| |


#### Basic step to execute any instruction
##### 1. Instruction Fetch (IF)
- CPU fetches first byte from $A0, which obtains $96


##### 2. Instruction Decode (ID)
- Control unit decodes this op-code
- Found out it is LDAA -> it knos the operand address is stored at next memory address.
- Control Unit goto address $A1 and fetch byte $80 and treat $80 as operand address

##### 3. Operand Fetch (OF)
- Control unit fetches byte at address `$80` into a data buffer/register of CPU
- Obtained $20 from the address

##### 4. Execution (EX)
- Loading value $20 from data buffer/register into accumulator A (ACC-A) of CPU.
- End of executing instruction


- CPU fetches next instruction until all instructions in program is ended


## 2.9  Three Basic I/O Mechanisms for Modern Computers

- (I) Programmed (or Memory-Mapped) I/O
- (II) Interrupt I/O
- (III) Direct Memory Access (DMA)

### 2.9.1 Programmed I/O
![[IO operation.png]]

3 buses:
|Bus Type|Usage|
|-|-|
|Control bus|control signals|
|Address bus|location being addressed|
|Data bus|data to be transferred|

- To programmer:
	- I/O board is a set of register ith specified address

- I/O can be achieved by sending command info to device's CSR -> read/rite the DBR
- on board hardare performs all operations according to control info
- 



### 2.9.2 Interrupt I/O
- CPU will consume time to check device status
- A device will sent an 'interrrupt request' to CPU
- CPU suspend its job to perform data transfer for that device

##### Procedures:
- CPU instructs I/O device to operate by riting a bit pattern to [[#csr|CSR]]
- CPU runs other job without waiting for the I/O device to finish
- When device finished reading a byte/word of data into the DBR (or in the case of writing operation, when the device is ready to write), it notifies the CPU by activating the "interrupt request (IRQ)" signal on the control bus (mark #1 in diagram).
- Some systems have multiple IRQ lines, with each line assigned a priority. A device with priority p is connected to the IRQ line of the same priority. Hence the CPU knows the priority of the device. In case there is only one IRQ line for all devices, the device activating the interrupt has to send its priority to the CPU by some means, e.g. thru’ additional signals.
- 

### 2.9.3 Direct Memory Access (DMA)
- During [[#2 9 2 Interrupt I O|Interrupt I/O]] , CPU is responsible to transfer each datum 
- (if 256 data items are to be read from input device)
	- CPU is interrupted 256 times and interrupt service routine is executed 256 times

- If a larger buffer is used, CPU is still responsible in an input operation for reading each datum from I/O biffer and rite it to memory (e.g. 'LDAA io_address' and 'STAA mem_address' instructions are executed for each datum)
- Double the instructions is used just to transfer 256 items
- Less efficient
- Most cases, only transfer data beteen memory and I/O device
	- Intervention of CPU is aste of time
- DMA controller gold buses and generate Read/rite and address signals to transfer data directly beteen I/O and memory
- CPU only needs to initialize operation at beginning and check result of operation
- CPU is disconnected from buses during transfer and reconnected after





Reminder
Assignment: 1