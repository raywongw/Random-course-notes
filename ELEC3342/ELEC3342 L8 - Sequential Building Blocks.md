
[[ELEC3342 L7 - VHDL II|Previous Chapter]] [[ELEC3342 L9 - Memory|Next Chapter]]

## Counter
- Increments on clock edge
- cycle through binary numbers 


```VHDL
-- Binary Counter
library ieee;
use ieee.numeric_std.all;
architecture rtl of bcounter is
	signal cnt: unsigned(31 downto 0);
begin
	q <= std_logic_vector(cnt);
	proc_cnt: process(clk)
	begin
		if (clk'event and clk='1') then
			cnt <= cnt + 1;
		end if;
	end process;
end rtl;
```
- Use unsinged numbers for counter
- input clock cycle, output a bit vector


```VHDL
-- Binary Counter with Clear
architecture rtl of bcounter is
	signal cnt: unsigned(31 downto 0);
begin
	q <= std_logic_vector(cnt);
	proc_cnt: process(clk, clr)
	begin
		if (clr = '1') then
			cnt <= x"00000000";
		elsif (clk'event and clk='1') then
			cnt <= cnt + 1;
		end if;
	end process;
end rtl;
```

### Example: 1 PPS signal
- Circuit output 1 for a cycle every 1 second
- Clock at 1MHz
- Design
	- 1 MHz clock -> 1,000,000 count
	- Counter, Comparitor(with 1m)
```VHDL
architecture rtl of onepps is
	signal cnt: unsigned(31 downto 0);
	signal cntsup : std_logic;
	constant amillionm1: unsigned(31 downto 0) := x"000F423F";
begin
	pps <= cntsup;
	cntsup <= '1' when (cnt = amillionm1) else '0';
	proc_cnt: process(clk)
	begin
		if (clk'event and clk='1') then
			if cntsup = '1' then
				cnt <= (others => '0');
			else
				cnt <= cnt + 1;
			end if;
		end if;
	end process;
end rtl;
```


## Shift Register
- Shift a bit at clock edge


### Shift Register with Parallel Load
- Shift register with parallel load bit, serial in and clock
- Outputs wither serial out, parallel out