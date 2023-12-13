
[[ELEC3342 L8 - Sequential Building Blocks|Previous Chapter]] [[ELEC3342 L10 - Introduction to FPGA|Next Chapter]]

# Memory


## Memory Array
- Store **large amount of** data in a efficient way
- Storing Logic, storage, reorganizing data
- 2D Array of bit cells
- Layout of $N:2^N$ , Data bit to address bit
- Larger memory array of more bits are not scalable
	- Solution: Multiple Banks

### Read operation
- Activate the corresponding wordline(address)
- Use bitline as data bit output
- Other wordline as 'Z' state (high impedance)


### Write operation
- Activate  the bitline by the bits to be written
- Activate the wordline to be written with the bits


### Naive Memory Implementation
- Input: wordline, read, write, bitline
- Output: bitline

- DFF with enable and tristate buffer


## Three State Logic
- '1', '0', 'Z' as output
- 'Z' as floating value between 0 and 1
- Value of node depends on drivers and previous values(more dangerous)

## Semiconductor Memory
- Early semiconductor memory are SRAM
- Later to DRAM

### Static Random Access Memory
- aka SRAM
- Data stored and persisted as long as power is supplied
- Designed mostly on standard digital circuit
	- No capacitors
- Simple R/W

Problem
- Small capacity

#### SRAM Cell Design
- Cross-coupled inverter
- Read from either Q or Q'
- Additional logic needed to write to cross-coupled inverter

#### SRAM Write
- Write data by forcing values through 2 access transistors
- B and B' as desired value
- turn on WE for a moment
- Disable WE and keeps new value to Q and Q'

#### Typical 6T SRAM Cell
- Inverter by 2 tranistors
- 6 Transistor SRAM cell
- SRAM cell is 6-10x larger than 1 DRAM cell




### Dynamic Random Access Memory
- aka DRAM
- Data stored in a single capacitor
- R/W access through a transistor

###### Destructive Read
- Data stored in capacitor is lost after read
	- write back to data after read
###### Data lost over time due to charge leakage
- Refresh needed
	- Modern DRAM implemented auto refresh

#### Read Operation
1. Pre charge to Vdd/2
2. Enable target word line
3. Sense amps sense changes in bit line voltage
4. Select desired column from output latch

#### DRAM Operations

##### Row Access
- Select rows depending on address (row have up to 10s of KB)
- Sense amp senses very small change in bitline level
- Voltage change is small as charge is shared with long bitline
- Sens eamps restore full swing level and restore data in cell (refresh)

##### Column Access
- Select desired bits out of entire row
- Select just small portion ($2^n$ bits)
- On Read: Send data out of package
- On Write:
	- Write design data in sense amp latch
	- Let sense amp refresh array with new data and original data from unchanged bits

##### Precharge
- Precharge bitline for next operation

#### Read Timing
- Issue READ command


#### DRAM Performance
- Latency vs Bandwidth
- Each step takes 15-20ns
- First bit takes very long time
	- Leads to latency

## Memory in Digital System
### Read Only Memory
- aka ROM
- Pass a address and receive data
- Similar to Constant Array
	- Content is determined during manufacturing
- Combination all Read
- Usage:
	- $2^n \cdot M$ Lookup Table
	- N input, M output truth table
	- N input, M output combinational logic block

ROM in VHDL
```VHDL
use ieee.numeric_std.all;
architecture rtl of myrom is
  type romtype is array (0 to 15) of std_logic_vector(7 downto 0);
  constant romdata : romtype := ("11001010", "11011111", others=>"00000");
begin
  process (addr)
  begin
    dout <= romdata (to_integer(unsigned(addr)));
  end process;
end rtl;
```


### FIFO
- Buffer between 2 parts of circuit
- Form of data storage

#### Operations
- Push data from head
- Pop data from tail

#### Reading from FIFO
- Read from head
- Sequence of events
	1. Check if empty asserted
	2. Assert pop from reader
	3. Data received from dout
- Variations
	- Give count signal
	- Almost empty signal
- FIFO from DFF

## Using Memory as Logic

### ROM Logic
- implement n input logic by $2^n \cdot M$ bit ROM
- a 2:4 decoder with output bits linked(physically connect wires) to each output

### RAM Logic
- Similar as ROM Logic
	- Each wordline to bitline cell can be changed accordingly
	- Configurable

### Configurable Look Up Table
- Lookup each output by address
- 