## 7.1. Introduction to the Memory Hierarchy / Organization of Modern Computer Systems
- main memory is bottleneck in ARM/MIPS computer system
	- people want large amount of fast ram
- a faster memory(e.g. [[#Static Random Access Memory|SRAM]]) is more costly at large amount (MB-> TB)

### Memory Hierachy
- Use multiple levels of memory unit consists of [[#Static Random Access Memory|SRAM]], [[#Dynamic Random Access Memory|DRAM]], [[#Magnetic Disk|Disk]]
	- faster memory closest to CPU
	- slower memory farthest to CPU


#### Data transfer in Memory Hierachy
- Only happen at adjacent layer, e.g. level 1 -> level 2

##### Hit
- The data requested is in higher level
- Hit rate = $\frac{\text{No. of hit}}{\text{No. of memory request}}$

##### Miss
- The data requested is not in higher level
- A lower level of memory will be accessed (SRAM -> DRAM)


#### Static Random Access Memory
- Nearest to Processor in memory hierachy
- has fastest access time
- much more costly

#### Dynamic Random Access Memory
- Middle in memory hierachy
- slower access time than SRAM
- less costly than SRAM

#### Magnetic Disk
- Lowest in memory hierachy
- Slowest in memory hierachy
- cheapest in memory hierachy



## 7.2. Basics of Cache Memory
### Cache
- Level of memory hoerachy between processor and main memory

### Example of cache memory

| SRAM | Item |
| ---- | ---- |
| 0x0  |  A    |
| 0x1  |   B   |
| 0x2  |    D  |
| 0x3  |     E |

1. Search for C in SRAM
	- missed




## 7.3. Measuring the Cache Performance

- CPU time consists of 2 part
	- CPU execution clock cycles
	- Waiting time for memory operations
- CPU Time General formula: 
	- (CPU execution clock cycles + Memory-stall clock cycles) × Clock cycle time

where memory-stall clock cycles = Read-stall cycles + Write-stall cycles
- If assume write buffer stalls is negligible
	- Memory-stall clock cycles = Memory access/ Program ×Miss rate×Miss penalty
	- = Instructions/Program × Misses/Instructions ×Miss penalty


### Example
- Processor has 2 [[ELEC2441-LT6#Cycle per Instruction|CPI]] without memory stalls
- Miss rate of data cache = 4%
- 

















