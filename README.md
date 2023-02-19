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
Difrence between required time and arrival time
![image](https://user-images.githubusercontent.com/120499567/219931897-f7600a11-2660-4ab3-a350-2250adfe5271.png)

![image](https://user-images.githubusercontent.com/120499567/219931957-1cf7e06d-9695-4759-a847-3eeb924f4765.png)
that is if slack is negative that means you dont get meet time then what we will do so you need to modify and fix the circuit
![image](https://user-images.githubusercontent.com/120499567/219932200-efd73709-febe-4a22-8359-d22c2438cecb.png)
![image](https://user-images.githubusercontent.com/120499567/219932498-c16b3fbf-e593-4974-b349-319e3e35a9cf.png)

## [SDC](https://teamvlsi.com/2020/05/sdc-synopsys-design-constraint-file-in.html#:~:text=SDC%20is%20a%20short%20form,and%20this%20file%20has%20extension%20.) comand(synopsis desine constraints formate which is defind in this library whole timing constraints so that verify STA ).

so the first command is `constraints for timing`


















