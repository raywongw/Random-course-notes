## 5.1 Addition and Subtraction in ARM Processors
- Integers exists in signed and unsigned
- Unsinged integer:
	- Bit pattern are interpreted as positive integer
	- $0100_2 = 4_{10} , 1101_2 = 13_{10}$
- Singed integer: 
	- Bit pattern can be positive or negative
	- 2's complement is adopted
	- $0100_2 = 4_{10} , 1101_2 = -3_{10}$

### Addition and subtraction
- Up to user to interpret whether the bits are singed or unsigned
|Binary pattern|Unsigned integer|Signed integer|
|-|-|-|
|$1101_2 - 0100_2 = 1001_2$|$13_{10} - 4_{10} = 9_{10}$|$-3_{10} - 4_{10} = -7_{10}$|

- ARM processor does not need to know if the bit pattern is signed or not



## 5.2 Multiplications in ARM Processors