library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity TrafficLightController is
port (
  clock: in STD_LOGIC;
  reset: in STD_LOGIC;
  sensor: in STD_LOGIC;
  highway_light: out STD_LOGIC;
  farm_light: out STD_LOGIC
);
end TrafficLightController;

architecture Behavioral of TrafficLightController is

type Light_state is (Green, Yellow, Red);
signal current_state: Light_state := Green;
signal counter: integer := 0;
constant yellow_duration: integer := 3;  
constant red_duration: integer := 10;  

begin

process(clock, reset)
begin
  if (reset = '1') then
    current_state <= Green;
    counter <= 0;
  elsif rising_edge(clock) then
    case current_state is
      when Green =>
        highway_light <= '1';
        farm_light <= '0';
        if (sensor = '1') then
          current_state <= Yellow;
          counter <= 0;
        end if;
      when Yellow =>
        highway_light <= '1';
        farm_light <= '0';
        if (counter = yellow_duration ) then  -- 
          current_state <= Red;
          counter <= 0;
	  highway_light <= '0';
          farm_light <= '1';
        else
          counter <= counter + 1;
        end if;
      when Red =>
        highway_light <= '0';
        farm_light <= '1';
        if (counter = red_duration) then 
          current_state <= Green;
	  highway_light <= '1';
          farm_light <= '0';
          counter <= 0;
	  
        else
          counter <= counter + 1;
        end if;
    end case;
  end if;
end process;

end Behavioral;
