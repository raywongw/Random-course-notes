
[[ELEC3342 L5 - Sequential Logic|Previous Chapter]] [[ELEC3342 L7 - VHDL II|Next Chapter]]
## Example - Ticket Gate at MTR
- Gate open after valid Octopus Card is scanned
- Close gate after person pass through

2 states
- Wait for card
	- if valid then open gate and pass to wait for passenger apss
- Wait for Passenger pass
	- if passenger passed then close gate and pass to wait for ca


## Finite State Machine
- Abstraction of computation


Definition
- Finite number of states that machine is in
- Conditions for machine to transfer from a state to another
- Only be in one defined state at a given time



### State Transition Diagram
- Graphical tool represents the FSM Behaviour
- States as Blocks
- Transitions as directed edge
- Includes all possible states and transitions in a diagram


### FSM Output
- Dependent on current state of FSM

**Moore machine**
- Output depends only on current state

**Mealy State**
- Output depends on current state and input


### Complete FSM
- states all possible transitions in a diagram



### State Encoding
- Ways that the abstract FSM states are represented in hardware
	- usually in bit form (State 000, State 001) or one hot (0001, 0100, 1000)
	- for identification purpuose only
	- implement reset state with all 0 bits


#### Unused code
- Some code may not be used (5 states but 111 occur)

Ways to handle invalid state
- Ignore
- Raise exception
- Reset machine
- 