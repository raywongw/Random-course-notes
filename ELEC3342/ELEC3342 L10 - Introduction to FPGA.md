
[[ELEC3342 L9 - Memory|Previous Chapter]] [[ELEC3342 L11 - Digital System Timing|Next Chapter]]

## Field Programmable Gate Array
- ASIC alternatives
	- ASIC configured "in the field"
		- 
	- Configuration load into chip when power up
- Usage
	- Glue Logic
	- Prototype for ASIC
	- Replacement of ASIC for small vol and fast time-to-market


### Simplified View
- Logic block as combinational logic to register
- Connect logic block through switch and connection boxes
![[Pasted image 20231102130144.png]]


### Modern FPGA





#### Layout of Modern FPGA
![[Pasted image 20231102130239.png]]

### Logic Block
- N input LUT 
	- N input combinational logic
	- Result registered by FF
- Function controlled by configuration bits
	- Stores in config memory



### LUT in real life
- 3-LUT and 4 LUT most common
- Modern FPGA uses 6-LUT and 7-LUT
- SRAM Based


### Xilinx CLB
- 1 CLB to 2 slices
- 6-LUT with additional mux between as slice


### On-Chip Memory
- 2 Types of memory
	- Dedicated on-chip memory
	- LUT-based memory
- Implemented with SRAM
- Dedicated Block RAM have higher capacity


## Hard Memory Block
- Dual-port Memory
- Configurable
	- have FIFO logic
	- 32k x 1 to 512 x 72 in 1 36k block


## FPGA Routing
- Switch Block and Connection Block
- Programmable switches used


### Route setup
- Connect logic block through various switches in switch block and connection block


### Switch Block
- Problem: Too many possible connection in switch block
	- Too many switch
	- Hard to maintain
	- Too large
	- Use too much power
- Solution: Use simpler topology for block
	- **Disjoint**:
		- Used in Xilinx XC4000.
		- Changes the track number assigned to a net as it turns.
		 - Forms two disjoint paths, a feature called the diversity of a network

	- **Universal**:
	    - Designed to be fully routable when considered in isolation and only for two-point nets
	    - Said to be locally optimal
	    - Its local optimality does not extend to the entire routing fabric
	
	- **Wilton**:
	    - example of ad hoc design with experimental validation
	    - Considers its role as part of a larger switching fabric, including the effects of long wire segments
	    - In the context of tileable FPGA, a mix of Universal and Wilton switch block patterns lead to the best tradeoff in area, delay, and routability
- 

## FPGA vs ASIC
- ASIC has high initial NRE and lower per unit cost
	- Generation i+1 ASIC has double NRE but half unit cost (compared to gen i ASIC)
- FPGA has low initial NRE and high per unit cost
	- Generation i+1 FPGA has same NRE and half per unit cost (compared to gen i FPGA)

## FPGA Design Flow
- Functional simulation 
	- Logical operation of circuit
	- No info about timing
	- No info about target HW platform (FPGA or ASIC)
- Timing Simulation
	- Timing of result HW (speed)
	- Check if produced HW performs the function as expected with timing info

### Hardware Design Best Practice
- Design for Implementation
	- Design as if the VHDL will be implemented 
- 



### Elaborate Design
- Assemble netlists from various sources
- Syntax check
- Inference
	- First step of real synthesis

### Synthesis

- Behavioural HDL
	- Extract HW structure from code (e.g. MUX, ROM, Adders, FFs)
	- Careful writing styles needed to extract correct structure
	- Strange errors can be reasoned by incorrect synthesis result
	- Synthesis tools may optimize code for target device
- Structual HDL
	- HW structure presented in code
	- Synthesis tools only translate and assemble structures to correct netlist
	- Low level blocks will be instantiated directly
		- Code will no longer be portable

### Map
- Convert netlist to LUT, FFs, on-chip RAM, Multipliers, DSP blocks, etc
- Generate LUT equations
- Reorganize logics combine signals from different part of design to 1 large LUT

### Place and Route
- 
