
[[ELEC3342 L6 - Finite State Machine|Previous Chapter]] [[ELEC3342 L8 - Sequential Building Blocks|Next Chapter]]
## Implementing FSM in VHDL
- State register -> DFF
```VHDL
architecture Behavioral of fsmdesign is
	type state_type is (s_waitcard, s_waitpass);
	signal state, next_state : state_type;
begin

SYNC_PROC: process (clk)
begin
	if (clk'event and clk = '1') then
		if (r = '1') then
			state <= s_waitcard;
		else
			state <= next_state;
		end if;
	end if;
end process;
```
-Define a enumerated type to label states