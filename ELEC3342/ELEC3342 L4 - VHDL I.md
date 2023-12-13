
[[ELEC3342 L3 - Arithmetic Blocks|Previous Chapter]] [[ELEC3342 L5 - Sequential Logic|Next Chapter]]
### Hardware Description Language

- Describes connectivity and function of digital hardware
- Components
    - Combinational Logic
        - Building blocks
        - Registers
        - Finite State Machines
        
    

#### Leading HDLs 
##### SystemVerilog
- 60%

##### VHDL 2008
- 40%

#### VHDL
- make comment by --

##### Library packages `STD_LOGIC_1164`
- standard library for data types
    - Single bit: std_logic
        - Multi bit: std_logic_vector

##### Architecture
`architecture rtl of FA is  begin     s <= a xor b xor cin;     cout <= ( cin and (a xor b) ) or ( a and b);  end rtl;`
- Defines function of entity


### Instantiation
```VHDL
architecture rtl of foo is
	component AOI is
		port ( r : in STD_LOGIC;
			   s : in STD_LOGIC;
			   t : out STD_LOGIC);
	end AOI;
	signal tmp: STD_LOGIC;
begin
	G1: AOI port map (a, b, tmp);
	x <= tmp and c;
	y <= tmp and not c;
end rtl;
```

- G1 as instance name
- AOI as name of component for the instance name
- Port