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
Understanding .lib file

The .lib file is an ASCII representation of the timing and power 
parameters associated with any cell in a particular semiconductor 
technology
The .lib file contains timing models and data to calcumax

I/O delay paths
Timing check values
Interconnect delays

![image](https://user-images.githubusercontent.com/120499567/220427255-5b13fa33-93d5-47f2-abc6-8b974b366c3e.png)

## Understanding SPEF file and SPEF parsing
SPEF can be generated by place-and-route tool or a parasitic extraction tool, and then this SPEF is used by timing analysis tool for checking the timing, in-circuit simulation or to perform crosstalk analysis.

Parasitics can be represented at many different levels. A Typical SPEF File has 4 main sections

- Header
- Name Map
- Top Level Ports
- Parasitic description

![image](https://user-images.githubusercontent.com/120499567/220429861-82b23c6b-2136-476a-a7e3-3811fd6e9c42.png)


Report Timing

![image](https://user-images.githubusercontent.com/120499567/220433115-c2976618-c15c-44b2-bb4e-c5828a7d195e.png)

Here slack is violated

![image](https://user-images.githubusercontent.com/120499567/220433872-4f4014e7-37a5-4a10-93d3-01f4c70e48f2.png)


# DAY 3 Theory

SETup Check

![image](https://user-images.githubusercontent.com/120499567/220438877-3421bc7d-6547-40bd-96ad-4a5c050a99a1.png)

Hold check
- Data launched by setup launch edge must not be captured by privious capture edge
- Data launched next launch edge must not be captured by curen capture edge

![image](https://user-images.githubusercontent.com/120499567/220440772-5f6ea110-eb71-461a-9cfc-8f3b40e15f62.png)

Timing Arcs
Two types of timing arcs
cell arcs, net arcs
cell arcs are input to output conection which is defined in logical  library what the dealy ..
Net arcs are the conection from one cell to another cell

![image](https://user-images.githubusercontent.com/120499567/220446328-f6ec1cfd-0371-479e-95a8-1e09d152d907.png)

Combinational arcs

Sequential arcs

![image](https://user-images.githubusercontent.com/120499567/220447830-5c8fba96-23de-4d9c-912e-1aba762b64df.png)

positive unit arc 
when input change and output follw the same direction
Negative unit arc
when input change output follow in the oposite direction

Non unate
when input change output may change in both dirction rise and fall


## Cell Delays

![image](https://user-images.githubusercontent.com/120499567/220450528-f818acbd-cf6a-42a6-a96c-ec48a2f7abea.png)

Positive clock skew

![image](https://user-images.githubusercontent.com/120499567/220451868-5200f7d7-783c-4cf5-a45e-4c80a374e92b.png)


Negative Clock skew

![image](https://user-images.githubusercontent.com/120499567/220452669-ca85ca06-5d1a-4b5f-8cd3-7fa4a053069d.png)


Clock Latency

![image](https://user-images.githubusercontent.com/120499567/220453315-26a0f44e-ca6e-45b7-974e-76e201007557.png)

[Clock Jitter](https://vlsi.pro/clock-jitter/)

thir is some uncertantinity came in ideal clock

![image](https://user-images.githubusercontent.com/120499567/220509940-eec78c13-52b3-4c07-b12d-166b3c357a25.png)

Setup check and clock check in details

![image](https://user-images.githubusercontent.com/120499567/220510855-44ef6e52-5abc-4c64-bffa-5064b02bf60e.png)

if skew is postive then we get more tmie to setup the signal and it is good but the skew is negative nd arive earlier than the clock period then it s very perimistic and it is not good

![image](https://user-images.githubusercontent.com/120499567/220511908-c1272ed1-b979-4cca-a0d6-ec8e7e6cef51.png)

if clock jitter is negative and skew is positive then both compensate

Hold time with clock skew

![image](https://user-images.githubusercontent.com/120499567/220513853-bb69c3ed-de0c-4f21-a961-88da7aad189c.png)

Hold time with skew and jitter

![image](https://user-images.githubusercontent.com/120499567/220514259-40a99cb5-0e91-446c-b218-7b87c16510b5.png)

Difrent Dealy value s on paths - Setup Check
Captured path dealy should be minimum and lunch path dealy should be maximum dealy

![image](https://user-images.githubusercontent.com/120499567/220515675-ba4964d4-5d54-42f0-b145-15273cac1287.png)

Difrent Delay values on path - Hold Check
Lunch path should be minimum and captured path should be maximum dealy

![image](https://user-images.githubusercontent.com/120499567/220517170-ac2fe162-0122-4f6c-a19a-10c9385cf1b3.png)

[Difrent delays causing pessimism](https://vlsi.pro/common-path-clock-reconvergence-pessimism-removal/) 

![image](https://user-images.githubusercontent.com/120499567/220517641-60ec3f82-6114-4771-8251-134dda5d925e.png)

[CRPR](https://chipedge.com/what-is-crpr-in-vlsi/#:~:text=What%20is%20CRPR%20in%20VLSI%20all%20about%3F,delays%20of%20clock%20network%20cells.)

## Understanding the SLACK computation
Run ‘sta run.tcl -noexit | tee out.txt'

![image](https://user-images.githubusercontent.com/120499567/220538551-8243d332-bd6f-4af0-817e-cabe31d75ac6.png)

![image](https://user-images.githubusercontent.com/120499567/220541664-7f633536-6413-451e-ba95-6d6745b85840.png)

![image](https://user-images.githubusercontent.com/120499567/220542727-94a312c2-7a50-4fc1-91ea-cd9b3e5bbc5a.png)

![image](https://user-images.githubusercontent.com/120499567/220545461-aed05da5-491b-4827-af66-ba9383c20886.png)

![image](https://user-images.githubusercontent.com/120499567/220545829-1a36d855-c8cd-4499-a346-438775b6578b.png)

# DAY4 THEORY

Crosstalk - impacting dealys

Crosstalk Glitches

if the signal change in the same direction then dealys in the ckt can become laser 

and the signal change in opposite direction then transtion can become slower and dealy is more

![image](https://user-images.githubusercontent.com/120499567/220549711-6cc14ba9-20ac-48e8-ba29-42b91ea21772.png)

![image](https://user-images.githubusercontent.com/120499567/220550363-604e7e9f-02e2-4665-9ee2-40bcbf686a6a.png)

### Global process variation
Can differ from one wafer to other wafer and within the wafer can be vary one die to other die so the dealy and transition time diffrent

![image](https://user-images.githubusercontent.com/120499567/220552823-cd9ec021-829d-4046-9a73-24e41d06bf34.png)

### Clock getting check

![image](https://user-images.githubusercontent.com/120499567/220556886-c1fa8c97-eb08-449d-8adc-a46029d346b4.png).

![image](https://user-images.githubusercontent.com/120499567/220562953-e4b491f4-8eae-4575-8d7f-72b8a8ccfe61.png)

![image](https://user-images.githubusercontent.com/120499567/220563320-2ac1b91b-8ce8-4119-9708-f90c9950d728.png)

Async Pin checks

Aseration is asynchronous event and no relation with clock 
so asyn pin like reset and clear its not depend on clock, let asume active low clear pin high that means output goes to zero or clear and when active low clear pin is low then flop depend on the clock and this transition specified in the STA timing constraints.

![image](https://user-images.githubusercontent.com/120499567/220567294-238e7f3f-355a-4e13-aec7-ff9bbf32086f.png)

![image](https://user-images.githubusercontent.com/120499567/220568327-53267849-8420-499b-b6c7-8345f927aa6f.png)

![image](https://user-images.githubusercontent.com/120499567/220568720-e2c1382b-b966-42ba-bce3-c75f939e0eb2.png)

# THEORY

### Clock Groups

![image](https://user-images.githubusercontent.com/120499567/220575687-1cbe9dda-a98f-4459-a619-4c4ace851f69.png)


![image](https://user-images.githubusercontent.com/120499567/220570297-01c00537-dfe3-4def-aa9c-3b99d39117ae.png)

But the STA run on synchronus clock

### Logicaly exclusive clocks 
STA tool select at a time one clock path

![image](https://user-images.githubusercontent.com/120499567/220577594-923e4f25-8b0e-4138-8cbb-ee31bb8e5e95.png)

### physically exlusive Clock
two clock will not hapen at a same time for same shematic only one clock will send , it will ot crosstalk
but in Logically exclusive it may be cross talk

![image](https://user-images.githubusercontent.com/120499567/220579247-976b7347-ae9a-4d7c-a294-96e23dc187ba.png)

By default STA take synchronus clock

SET_CLOCK_GROUPS

![image](https://user-images.githubusercontent.com/120499567/220581560-a591c529-a3c3-46c0-8fdd-906fea25a05d.png)

![image](https://user-images.githubusercontent.com/120499567/220582019-3c3f7a1e-71c2-41a1-b8fd-54234b310fac.png)

## Clock properties

![image](https://user-images.githubusercontent.com/120499567/220599502-b76dd4aa-ba7f-4cbc-89ff-12d59ebdd597.png)

## Path specification comand(SDC comand)

from the path specification we can modify the timing path from the ideal path which is set earlier

![image](https://user-images.githubusercontent.com/120499567/220601365-27950b28-d4c7-46c2-bcf1-0c34c4eab978.png)

we can modify from either 3 comand

- From   is used for start point
- To is used for end point
- Through is used beetween the path from start point to end point
from and to option can be used only one but through option can be used mpore than one because through give guide to many place

set_fale_path

The Set False Path ( set_false_path ) constraint allows you to exclude a path from timing analysis, such as test logic or any other path not relevant to the circuit's operatio

![image](https://user-images.githubusercontent.com/120499567/220605199-e7b92af9-d0fa-4d2e-b030-5c26aeee9f7a.png)

set_multicycle path

You access this dialog box by clicking Constraints > Set Multicycle Path in the TimeQuest Timing Analyzer, or with the set_multicycle_path Synopsys® Design Constraints (SDC) command. Allows you to define a path that requires more that one clock cycle to propagate data.

![image](https://user-images.githubusercontent.com/120499567/220606222-88fd7762-8dfa-4ae7-ade7-e592e797a8d3.png)


![image](https://user-images.githubusercontent.com/120499567/220607457-045857a9-44bf-42ca-958a-e6ae6a637ecf.png)

#### set_case_analysis
is used to specify certain portion of the designe or specify the constaint value

# DAY 5 LAB




























































































