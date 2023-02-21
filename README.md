# VSD-IAT-Sign-off-Timing-Analysis---Basics-to-Advanced

![Screenshot 2023-02-18 213203](https://user-images.githubusercontent.com/120499567/219875835-9e6ea51a-b66a-492e-8950-592d6f864d00.png)


[Static timing analysis (STA)](https://www.synopsys.com/glossary/what-is-static-timing-analysis.html) is a method of validating the timing performance of a design by checking all possible paths for timing violations. STA breaks a design down into timing paths, calculates the signal propagation delay along each path, and checks for violations of timing constraints inside the design and at the input/output interface. The workshop covers all the basic concepts in STA and Timing constraints.

## Table of Contents










# Day  - 1
## STA feature
- static
Fast and large capacity, does not using dynamic logic simulation
- Functionality
- Exhaustive
- Conservative
- STA is valid only for synchronus clock

## Inputs to STA
- Netlist
- SDC or constraints file
- Logic Libraries

## Timing paths
### STA Breaks the paths at
- port
- sequential element

![image](https://user-images.githubusercontent.com/120499567/219889519-9f403bf7-6c70-4d55-81ed-b36999eb5004.png)

## Timing path Elements
- Startpoint
Typically startpoint is data pin or input pin where data is available

- Endpoint
where data is captured by clock edge
or where the data must be avaiable at a specific time
generaly output pin or register data pin

- combinational logic
Element that have no memory or internal state
Difrent path can have diffrent dealy

### [Setup check](https://vlsiuniverse.blogspot.com/2013/07/setup-and-hold-checks-static-timing.html)
- Data should be avilable at the input of sequential device before clock edge that capture the data
- this inforce max dealy on the data path
- setup time of a flop
is indepent on the technology node 
valu is availbale in logic libraary
![image](https://user-images.githubusercontent.com/120499567/219908887-f133db57-7897-4ef3-b0de-950408b9804d.png)

### Hold check

![image](https://user-images.githubusercontent.com/120499567/219909011-5283c87a-0f9c-4aa5-ae64-aaba8eb36322.png)

![image](https://user-images.githubusercontent.com/120499567/219909140-bb78f564-7419-4e38-86b0-ca15ee6d96eb.png)

## Setup slack calulation

- Setup slack = Data required time - Data arrival time

Data arrival time

![image](https://user-images.githubusercontent.com/120499567/219931645-11d4bb2a-11f6-4185-90b7-b75faa005643.png)


Required Time 
The signal should arrive before required time

### Slack
Difrence between required time and arrival time.

![image](https://user-images.githubusercontent.com/120499567/219931897-f7600a11-2660-4ab3-a350-2250adfe5271.png)

![image](https://user-images.githubusercontent.com/120499567/219931957-1cf7e06d-9695-4759-a847-3eeb924f4765.png)

that is if slack is negative that means you dont get meet time then what we will do so you need to modify and fix the circuit

![image](https://user-images.githubusercontent.com/120499567/219932200-efd73709-febe-4a22-8359-d22c2438cecb.png)

![image](https://user-images.githubusercontent.com/120499567/219932498-c16b3fbf-e593-4974-b349-319e3e35a9cf.png)

## [SDC](https://teamvlsi.com/2020/05/sdc-synopsys-design-constraint-file-in.html#:~:text=SDC%20is%20a%20short%20form,and%20this%20file%20has%20extension%20.) comand(synopsis desine constraints formate which is defind in this library whole timing constraints so that verify STA ).

so the first command is `constraints for timing`

![image](https://user-images.githubusercontent.com/120499567/219933097-3555ed41-6a16-41b1-a447-e3b20ce1a57d.png)

`Area and power`

![image](https://user-images.githubusercontent.com/120499567/219933160-0c48c23e-e1cc-4943-8635-ffd3f2118e3c.png)

`constraint for desine rule`

![image](https://user-images.githubusercontent.com/120499567/219933214-c660dcaf-70ec-4943-b964-176ef651e8d6.png)

### create_clock 

![image](https://user-images.githubusercontent.com/120499567/219933641-63849b83-8b98-434c-92a8-810f9e70d5ec.png)

![image](https://user-images.githubusercontent.com/120499567/219933713-f0c88577-9dac-4b2e-8f03-81dc953765e8.png)

if waveform is not specified then by deault it will take 50 % duty cycle

#### create_clock - add switch
with this we can give the clock more than one clock 

![image](https://user-images.githubusercontent.com/120499567/219933866-5528bffe-5591-4e71-a2d0-7830a5aca158.png)

#### Create_generated_clock
we can generate the clock from the parent clock by dividing and multiplication

![image](https://user-images.githubusercontent.com/120499567/219934235-51795d89-02fb-4342-b6c9-d1e38164adfe.png)

![image](https://user-images.githubusercontent.com/120499567/219934476-9ea32270-ab80-49bd-9ef7-9056249e89bb.png)

![image](https://user-images.githubusercontent.com/120499567/219934648-855433aa-e672-4097-a1a7-fbb1e44d3dbb.png)

![image](https://user-images.githubusercontent.com/120499567/219934781-cf0686dd-1f9c-4dfc-a617-6eea6482ff60.png)

so the we generate difrent types of clock path and from this pick up the worst case for STA analysis
### Port Delays
`set_input_delay`
`set_output_delay`

![image](https://user-images.githubusercontent.com/120499567/219935379-c544394a-dc80-4a01-b7ee-8c2c5c85dc1e.png)

![image](https://user-images.githubusercontent.com/120499567/219935528-c93cf989-8184-4e18-81af-23bd6f996d1c.png)

here we defind how fast input side transiation 

![image](https://user-images.githubusercontent.com/120499567/219935642-fddf3d8e-cda0-4c59-9c23-4757eb49f291.png)

how fast output is transition 

## DAY 1 LAB
Inputs to OpenSTA
The inputs to the opentimer are design, standard cells associated with the netlist and the constraints.

Here verliog file

![Screenshot 2023-02-20 162639](https://user-images.githubusercontent.com/120499567/220127778-2bb0c353-8ceb-44d4-aec7-a0ec590a782c.png)

## Constraints creation - Defining clock
Clocks are defined using create_clock command
Lets define a clock with period 50 on port tau2015_clk
create_clock –period 50 –name tau2015_clk [get_ports tau2015_clk]
The SDC file provided for the lab. This consists of the clock period, IO delays, input transition and capacitance delays.
![2](https://user-images.githubusercontent.com/120499567/220128387-46eb6528-cb97-4cf4-a6cb-8a41cddae25e.png)

OpenTimer Run script

![3](https://user-images.githubusercontent.com/120499567/220128938-6d04b272-c922-4714-be06-626dcc9e34c0.png)

“run.tcl”

![runscript file4](https://user-images.githubusercontent.com/120499567/220129206-6173646f-8545-4d38-898c-1b1f78827eca.png)

Negative Slack violating

![5 neg slack](https://user-images.githubusercontent.com/120499567/220129567-10fc7ea2-36ca-47a7-bddc-f95c3b717849.png)

Here meet slack

![pos slack](https://user-images.githubusercontent.com/120499567/220132009-586e0774-78d9-444b-8fea-8e396b2045c5.png)


# DAY 2 Theory

[Clock geeting](https://anysilicon.com/the-ultimate-guide-to-clock-gating/)
STA also check Clock getting check and Asynchronus pin such as `clear preset set` and also check data to data pin which is skew ..
Clock geting check on clock enable pin with respect to the clock pin
and all of these are available in library and constraints file. 

![image](https://user-images.githubusercontent.com/120499567/220355090-4261b77a-df6a-41b3-9e9d-8c1fb3aa94df.png)

that is another set of check which are also done by STA which is desine by DRC

Slew/Transition Analysis
slew is nothing but time taken by a single which is rising by 30% of the Vdd to 70% of the Vdd that is known as rise slew 
and by fallwing 70% to 30% is called fall slew
and in the library their is max and min value and when STA run then check the meet condition and to verify work properly or not 

![image](https://user-images.githubusercontent.com/120499567/220357172-007bfa33-5a29-43ee-9cdb-a716392ba847.png)

Second category of check is Load Analysis
- min and max capitance on ports and nets
- Fanout load on ports and output pins

STA also ceck the Clock Skew Analysis
Slew and Skew both are diffrent thing 
Skew is the diffrance in dealy of the clock at diffrent point. Skew is positive means captured clock is more dealy

![image](https://user-images.githubusercontent.com/120499567/220360221-00c3a423-94ef-4f11-b008-7c5380dbf4b9.png)


SKEW can also be negative 
If lunch has more cealy then Captured 

![image](https://user-images.githubusercontent.com/120499567/220361356-76a2a555-e4fd-48ff-86f5-3da3ac7bb72f.png)

STA also check the Pulse width check
Shrining the pulse due to this if shrinking beyound the limit which is defined in library then hapened pulse width violation

![image](https://user-images.githubusercontent.com/120499567/220362408-cff4cee1-2e17-4765-82df-d8c5cdb6b570.png)

## [Flop Based designs](https://www.vlsi-expert.com/2019/12/latch-based-timing-analysis-part-1.html)

data is launched and captured on edges

![image](https://user-images.githubusercontent.com/120499567/220367984-25405a26-3b9c-4290-91d3-380d2b507b71.png)

![image](https://user-images.githubusercontent.com/120499567/220369064-1676a087-aa72-41fd-a3a3-4388b5c9cbc6.png)

Latch Based designe allow more flexibility in timing 
because latch is active for whole duration so that even data is come after the active of clock. it also captured the data
so latch give the facility even data arive later the clock edge

![image](https://user-images.githubusercontent.com/120499567/220372736-1c3c3f55-ea58-48a7-b5c3-cb99a3cf52cb.png)

![image](https://user-images.githubusercontent.com/120499567/220373045-857cb807-8dbf-4d96-ac64-b768b60df2ef.png)

### Time borrowing

Latch gives the facility to time borrow let asume first combinational ckt take more time even more than the one time period and other combination ckt takes less time even less than the one time period then second combinationl ckt gives the borrow to first combinational ckt

![image](https://user-images.githubusercontent.com/120499567/220412885-74a06b3e-005c-445b-a72c-b14c81030173.png)

STA Text Report

![image](https://user-images.githubusercontent.com/120499567/220414158-e8865b0f-6b09-48c9-89eb-5ef507f9bbab.png)

![image](https://user-images.githubusercontent.com/120499567/220415265-db34e3c5-3b9d-4e14-b058-414291608052.png)

## Dat 2 LAB









































