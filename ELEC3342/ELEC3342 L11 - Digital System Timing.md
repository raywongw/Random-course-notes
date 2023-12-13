
[[ELEC3342 L10 - Introduction to FPGA|Previous Chapter]] [[ELEC3342 L12 - Digital Signal Processing|Next Chapter]]

## Timing Introduction
- Why the result will be changed with a delay

- How to quantify delay
	- Random time


Propagation Delay $t_{pd}$ = Max delay from input to output
Contamination Delay $t_{cd}$ = Min delay from input to output

Delay Caused by
- Physical phoenomenon
	- Capacitance and resistance
	- Speed of light limitation




### Long and Short Paths
- Critical Path (Longest Path): $t_{pd}$ = 2$t_{pd \text{AND}}$ + $t_{pd \text{OR}}$
- Short Path$t_{cd}$ = $t_{cd \text{AND}}$


## Delays from Different Path
- Circuit modules require specifications about delay due to different internal delay path
- Unbalanced path cause glitches


### Glitch
- Single input change causes output change multiple time
- Anytime that the output change for no reason
- Happens due to simulation glitch and real world situation
	- e.g. capacitive coupling between wire

#### Way to fix glitch
- introduce additional condition in 



## Hold Time Constraint




## Clock Skew
- Difference in clock signal arriving time



## Metastability
- Bistable devices: 2 stable states and a metastable state
- e.g. Flip-flop: 2 stable states (1 and 0), with one metastable state
- Can stay in metastable state for inf time

### Probability that  output Q is in metastable circuit
$$P(t_{\text{res}} > t) = \frac{T_0}{T_C}\cdot e^{\frac{-t}{\tau}}$$
$T_0$ is constant
$\tau$ is time constant that determines how fast a FF resolve metastability
$T_C$: Probability that input changes at a bad time


- Probability of failure -> t becomes $-(T_C - t_{\text{setup}})$


## Mean Time Before Failure
- P(failure)/second = $\frac{N\cdot T_0}{T_C}\cdot e^{\frac{-(T_c - t_{\text{setup}})}{\tau}}$
MTBF will be 1/P(failure/second)