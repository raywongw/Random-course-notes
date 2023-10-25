[[ELEC3342 L4 - VHDL I|Previous Chapter]] [[ELEC3342 L6 - Finite State Machine|Next Chapter]]
## Combinational v.s. Sequential

**do not use latch in vivado**

## Sequential Logic

- Contains state elements
	- hold value over time
	- store states of circuit

### Bistable Circuit
- 2 outputs, Q and not Q
- No input

### Edge Triggered Flip Flops
- Changed output when input is different during
	- rising edge (0 -> 1)
	- falling edge (1 -> 0)


### D Flip-flop
- 1 data input, 1 clock input
	- Make sure D is only 1 or 0 at edge
- Optional: Reset, Enabler
- Capture value of input at rising edge
- Output the same value as captured after small delay

##### Example: Shift Register
- Connect DFFs at serial (DFF1 output to DFF2 input, DFF2 output to DFF3 input, ...)

### Enabled DFF
- DFF with a mux
- if enable is on, use D instead of DFF output


### Resettable DFF
- DFF with a reset
- input and not reset
- if reset is on, force reset DFF output to 0

#### Synchronous Reset
- Happen only at next clock edge

#### Asynchronous Reset
- Happen whenever reset is on
- More common in FPGA

### Toggle Flip-Flop
- Toggles output to opposite when toggle signal is high and at rising edge clock
- Logic: T xor Q -> nextQ


### SR Latch
- for storing data
- S = 0, R = 0, output previous state
- S = 0, R = 1, set output to 0
- S = 1, R = 0, set output to 1
- S = 1, R = 1, invalid input


### D Latch

- SR latch that prevented S, R = 1
- D input, Clock input
- Q output

- CLK = 1, D Latch opened, Q = D
- CLK = 0, D Latch closed, Q = Qprev


### D Flip-flop from D Latch
- First D latch with reversed clock signal
- Second d latch accept input from first d latch's output
- with normal clock signal
- 