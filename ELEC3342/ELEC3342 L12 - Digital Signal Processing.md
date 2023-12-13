
[[ELEC3342 L11 - Digital System Timing|Previous Chapter]] [[ELEC3342 L13 - Advanced Arithmetic Circuits|Next Chapter]]
### Digital Signal Processing
- Sample sound waves with ADC
- Input: Time series of sampled input -> Signal


## Pipeline



## Binary Point Shifting
- Represent a decimal number with fixed point representation
- numbers before dot is above 1, after is below 1
- e.g. 100110.110
	- 100110 represents 38
	- .110 represents 0.75


## Fixed Point Operation
- Treat them same as normal integer addition
- Multiplication: a <8,3> and <8,3> multiplication results in <16,6> floating point number
- + and x are associative


### IEEE Floating Point Number
1 bit sing
8 bit exponent (2^0 to 128)
23 bit significand (mantissa)
	- Maybe in 1.xxx form or 0.xxx for 00 exponent


## Precision of FLP vs FXP
- Depends
- Need to know exact application for the number


### Absolute and Relative Error
- True value as x, represented value as x'
- 