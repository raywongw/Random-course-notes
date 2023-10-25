[[ELEC3342 L4 - VHDL I|Next Chapter]]
### Two's Complement
- TLDR: flip all bit and add 1

### Encoder
- One-hot to binary
- e.g. 4:2 encoder
	- 4 inputs, only 1 activates at a time
	- 2 output representing binary value of the corresponding wire


### Decoder
-  Binary to one-hot
- e.g. 3:8 decoder
	- 3 inputs representing a bit
	- 8 outputs represents the corresponding wire

### Circuit with sub-blocks
- A large circuit can be implemented with smaller building blocks
- e.g. 8:3 encoder
- MSB is activated when [4:7] is activated
- other bits are same as 4:2 encoder
- 


## Arithmetic Circuits


### Addition
- Add integers bit by bit


#### Half adder
- Basic addition of 2 1-bit value
- 2 input(bits to be added), 2 output(result bit, carry out)
- Result Bit = a XOR b
- Carry out = a AND b

#### Full adder
- Half adder but with a carry input
- 3 input (2 bit to be added, 1 carry in), 2 output (result bit. carry out)
- Result Bit = a XOR b XOR carry in
- Carry Out = (a and b) or (cin and (a or b))


#### Multi-bit adder
- Connect multiple one-bit adder , carry out to another's carry in
- From LSB to MSB
- Mimics long addition in digits

### Subtraction
- Implemented by using an adder and a 2's complement
- A negate circuit before B and a new input stating if it is adder



### Comparator
- XNOR bit by bit
- compare result by a and gate
- 


### Shifter
- Shift left/right by number of bits with MSB
	- Multiplication / division by powers of 2
- Use a number of mux to create a shifter
- Input: array of bits input, number of bits to be shifted
- 


### Rotator
- Rotating buts as if they sre in circle
- 01001 ROL 2 = 00101