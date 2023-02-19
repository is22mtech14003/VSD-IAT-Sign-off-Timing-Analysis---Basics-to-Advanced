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

### Setup check
- Data should be avilable at the input of sequential device before clock edge that capture the data
- this inforce max dealy on the data path
- setup time of a flop
is indepent on the technology node 
valu is availbale in logic libraary
![image](https://user-images.githubusercontent.com/120499567/219908887-f133db57-7897-4ef3-b0de-950408b9804d.png)

### Hold check

![image](https://user-images.githubusercontent.com/120499567/219909011-5283c87a-0f9c-4aa5-ae64-aaba8eb36322.png)

![image](https://user-images.githubusercontent.com/120499567/219909140-bb78f564-7419-4e38-86b0-ca15ee6d96eb.png)












