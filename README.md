# Advanced-Physical-Design-using-OPENLANE-Sky-130
Author : Vaanya Sharma 

<br>This is a workshop which is about ASIC design using OPEN source tools.

## Advanced Physical Design- OpenLANE\Sky130
![Screenshot 2024-03-19 195759](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/9e3eb63d-d8ec-4051-96e3-3a3a06a7a540)
<br>
# ABOUT THE PROJECT...............
## Workshop Day wise Content 

Day1 – Inception of open-source EDA, OpenLANE and Sky130 PDK
<br> [How to talk to computers](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/blob/main/README.md#-how-to-talk-to-computers)
<br> [SoC design and OpenLANE](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/blob/main/README.md#-soc-design-and-openlane)
<br> [Get familiar to open-source EDA tools](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/blob/main/README.md#get-familiar-to-open-source-eda-tools)

Day 2 - Understand importance of good floorplan vs bad floorplan and introduction to library cells
<br> [Chip Floor planning considerations](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/blob/main/README.md#-chip-floor-planning-considerations)
<br> [Library Binding and Placement](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/blob/main/README.md#-library-binding-and-placement)
<br> [Cell design and characterization flows](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/tree/main#-cell-design-and-characterization-flows)

<br> Day 3 - Design and characterize one library cell using Magic Layout tool and ngspice
<br> [Labs for CMOS inverter ngspice simulations](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/tree/main#--labs-for-cmos-inverter-ngspice-simulations)
<br> [Inception of Layout – CMOS fabrication process](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/blob/main/README.md#-inception-of-layout--cmos-fabrication-process)

Day 4 - Pre-layout timing analysis and importance of good clock tree
<br> Timing modelling using delay tables
<br> Timing analysis with ideal clocks using openSTA
<br> Clock tree synthesis TritonCTS and signal integrity
<br> Timing analysis with real clocks using openSTA

<br> Day 5 - Final steps for RTL2GDS
<br> Routing and design rule check (DRC)
<br> PNR interactive flow tutorial

Acknowledgements

## Day1 – Inception of open-source EDA, OpenLANE and Sky130 PDK
### <br> How to talk to computers
#### <br> Before starting with the concepts, here are some basic termonologies that will help you understand the after written things the better way:-
<br> 1.**PACKAGE:-** ***The case which has the chip and is connected to the circuit board. It is kind of a housing in which the chip is placed.***
<br> 2.**WIRE BONDS:-** ***Through which the chip is connected to the package and the outside signals are received by the chip.***
<br> 3.**Pads:-** ***Through which we can send in the signals to the chip or recive the signals from the chip.***
<br> 4.**CORE:-** ***Where all the logic sits. All the AND, NOT gates and the MUXES are placed here.***
<br> 5.**DIE:-** ***It is basically, the size of the entire chip.***
<br> 6.**FOUNDRY:-** ***It is a very critical term for chip design. It is a like a big factory with many large machines. It is where the chip gets manufactured.***
<br> 7.**IPs:-** ***Intellectual Property. It requires some _intelligence_ to be built.***
<br> 1.**MACROs:-** ***They are pure logic based.***

<br> You must have seen a circuit board like an arduino. 
<br> ![WhatsApp Image 2024-03-22 at 20 42 40_546c53fa](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/77287e70-be46-4858-9855-655b4036fe4d)
source of the image- VSD-IAT PLATORM
<br> The _highlighted_ part of the circuit board is the chip or preferably the **_package_**.
For designing such a circuit, we would first need to represent it using a block diagram.
<br> Like this :-
<br> ![WhatsApp Image 2024-03-22 at 20 42 53_c0279c2d](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/e4aa7533-886a-483b-b1ec-ad111819a3db)
source of the image- VSD-IAT PLATFORM 
<br> So, now in the same manner of block diagram based representation; let us go inside the package.......................
<br> ![WhatsApp Image 2024-03-22 at 20 43 09_46be60ff](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/cae4a683-eabd-421e-a0bd-f1d08eecb9fe) 
<br> SOURCE OF THE IMAGE - VSDIAT PLATFORM
<br> So as you saw that inside the package (the white outline) is kept the chip. And what are those white thread like structures ?? You must be wondering. These are the WIRE BONDS. You can know what is there function at [termonologies](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/blob/main/README.md#-before-starting-with-the-concepts-here-are-some-basic-termonologies-that-will-help-you-understand-the-after-written-things-the-better-way-)
<br> The package shown above is a QFN-48 whose size is 7mm by 7mm, and these obviously vary in size and model.
<br> So what if we try to know this package in a more detailed manner. Let us see the insides of a package :-
<br> ![WhatsApp Image 2024-03-22 at 20 43 20_67d9d238](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/4aafde57-5a33-4864-a7fb-0f7b566c83fa)
<br> SOURCE OF THE IMAGE - VSDIAT PLATFORM
<br> As you can see that there are many parts of a package namely _PADS, CORE AND DIE_.You can know about these terms by looking at the [termonologies](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/blob/main/README.md#-before-starting-with-the-concepts-here-are-some-basic-termonologies-that-will-help-you-understand-the-after-written-things-the-better-way-)
<br> Now you know what is a core, lets get deep into it and know what kind of logic sits in the core. So if we take an example of a RISC V processor, let us know what sits in its core.
<br> ![WhatsApp Image 2024-03-22 at 20 43 26_d5f743fc](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/74dc13bc-7109-43fe-b9c3-f6d461e96ca9)\
<br> SOURCE OF THE IMAGE -VSDIAT PLATFORM
<br> It consists of many components such as SoC, SRAM and other couple of components. Other typical packages usually have the same kind of components. Out of these components, some are defined as FOUNDRY IPs and MACROs.
<br> ![WhatsApp Image 2024-03-22 at 20 43 28_33aa067e](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/066722b0-f1ff-40d9-975d-ad5f57ff85e1)
<br> SOURCE OF THE IMAGE -VSDIAT PLATFORM
<br> You can know about these terms by going to [termonologies](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/blob/main/README.md#-before-starting-with-the-concepts-here-are-some-basic-termonologies-that-will-help-you-understand-the-after-written-things-the-better-way-).
To build a chip like this,we need to constantly keep in contact with the foundry using some interface. This interface might be a file that the foundry provides us with

So let us arrive at a very important question. **_HOW DO APPLICATION SOFTWARES WORK ?_**
![WhatsApp Image 2024-03-22 at 20 43 29_a2b39049](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/904cb523-c789-4cfd-9794-a938a5a01cbe)
<BR> SOURCE OF IMAGE ~ VSD-IAT PLATFORM
<br> As you can see in the image that there is a c type program and a layout. For apps to work,  we in the same way need to convert the c-type program to the kind of layout shown. Let us see how........
<br> ![WhatsApp Image 2024-03-22 at 20 43 45_12738892](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/fa35563f-f055-45cc-a674-84bde10faed2)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM
<br> These application softwares enter into a box called the _SYSTEM SOFTWARE_, which converts these applications to _BINARY FORMAT_. This system software has many components namely 
<br> OPERATING SYSTEM
<br> COMPILER
<br> ASSEMBLER
<br> First is the job of the OS, whose regular jobs are to handle:-
<br> IO OPERATIONS
<br> ALLOCATION OF MEMORY
<br> LOW LEVEL SYSTEM FUNCTION
<br> The main job apart from the regular jobs of the *OS* is to convert the app to its respective assembly language program and finally to binary language program, so it can be understood by the hardware. The output of the OS are nothing but small instructions in c, c++ or java format.
<br> These are then taken by the *compiler* and converted to respective instructions. The syntax of these instructions depend upon the type of hardware.
<br> Example- If, the type of hardware is RISC V, then the instructions will also be RISC V instruction set architecture.
<br> Now next is the job of the *assembler*.It takes in the output of the compiler that is instructions and converts them to their respective *binary format*. This *binary language* is also known as the *MACHINE LANGUAGE*. 
<br>  *MACHINE LANGUAGE*- Its name is very much self-explanatory. It is a language that is understood by machines.
<br> Then the output of this assembler is fed to the hardware, and the required function is performed.

LET US NOW SEE AN EXAMPLE OF AN APPLICATION TO UNDERSTAND THIS BETTER. 
> STOPWATCH
![WhatsApp Image 2024-03-22 at 20 43 46_b79e1e07](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/d9d792fa-28df-45fa-825f-20d03f022821)
<br> SOURCE OF THE IMAGE-VSDIAT PLATFORM.


<br> NOW IS THERE SOMETHING THAT WE CAN KNOW UPON EXPANDING THE PROCESS ??
<br> Yes!!
<br> The instructions that we got as an output of the compiler act as an ABSTRACT interface between C- program and the hardware. This interface is known as the *Instruction set Architecture* or *The architecture of the computer*. It basically represents your hardware.
![WhatsApp Image 2024-03-22 at 20 43 49_9417651e](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/fdfe44b5-ea5c-445a-b6e7-6b502be8cd5d)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now there is another interface known as the *Hardware Description Language*.  
![WhatsApp Image 2024-03-22 at 20 44 06_6de4e362](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/c14df629-2b9e-4d78-8f23-6654e137a910)
<br> SOURCE OF THE IMAGE-VSDIAT PLATFORM 
<br> As you can see in the image that there are some instructions and the output of the assembler. The instruction is to add x6, x10, x6 and the output of the asssembler has to be in binary so that the hardware or we can say the machine can actually understand what is to be done. So its output will be somewhat like 000000000110010110000001100110011.
<br> NOW! You would require a *RTL Description Language* that would understand and perform the given specifications. It is known as the implementation of specifications.
<br> After this, it is getting synthesized into netlist. This basically is in form of ANDs, NOTs, FLIP FLOPS and so on.....
<br> Then the physical design implementation of the netlist is done. 
(image below as a representation of the above written process)
![WhatsApp Image 2024-03-23 at 07 45 11_57b9fe52](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/9db018ff-2777-4777-84d4-284a3f3f9bcd)
<br> SOURCE OF THE IMAGE-VSDIAT PLATFORM

### <br> SOC DESIGN AND OPENLANE
<br> SOC DESIGN USING OPENLANE
<br> DIGITAL APPLICATION-SPECIFIC INTEGRATED CIRCUIT (ASIC) DESIGN.
<br> For designing an ASIC design, there are many componenets tht must be presesnt:-
<br>~ RTL IPs
<br>~ EDA TOOLS
<br>~ PDK DATA

<br>"For designing 100% open source digital ASIC Design ......" by this statement it is meant that the  RTL, EDA, PDK, all must be opensource. 

<br>On the internet, there are many open source RTL Designs like:-
                                                 <br>  librecores.org
                                               <br>    github.com
                                                                


<br>On the internet, there are many open source EDA Tools like:-
                                                 <br>  QFlow
                                                 <br>   OpenLANE
                                                         



WHAT IS A PDK ??
<br> ~ PDK is the short form for Process design Kit.
<br> ~ It is the interface between the FAB (Semiconductor Fabrication Plant) and the designers 
<br> ~ It is a collection of files used to model a fabrication process for the EDA Tools used to design an IC (Integrated Circuit or we can call it a Chip). 
<br> ~ It contains alot of important information like :- 
<br> } Process Design Rules
<br> } Device Models
<br> } Digigtal Standard Cell Libraries
<br> } I/O Libraries

<br> For open source PDK, there is collabration between Google and SkyWater Technology Foundry to provide a 100% open source PDK. the pdk is named as 130 nm Production PDK.
<br> Now that we have all the essential components for ASIC Design.

<br> ASIC DESIGN FLOW
<br> It is a piece of software.
<br> Its main objective is to take ASIC design from Resistor-Transistor Level to GDS-II
format, which is used for final layout. 



![WhatsApp Image 2024-03-23 at 21 40 52_6f37343a](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/43d0e814-1b69-4a6b-bd37-493cc6b5973b)
<br> SOURCE OF IMAGE- VSDDIAT PLATFORM.
<br> The above is the image of the simplified ASIC Design flow. 
<br> First major step of ASIC Design Flow is **_SYNTHESIS_**. In this RTL is converted to a circuit out of components from the Standard Cell Library (SCL). The Circuit is described in HDL and usually reffered as Gate Level Netlist. 

The next step is **_Floor and Power Planning_**. Floor Planning has different meaning depending whether we want to implement the whole chip or just the small elements known as **MACROS** about which you can know in the [termonologies](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/blob/main/README.md#-before-starting-with-the-concepts-here-are-some-basic-termonologies-that-will-help-you-understand-the-after-written-things-the-better-way-).

If we try to know the difference , it would be like:-
 <br> CHIP FLOOR PLANNING
 <br> Partition the chip **die** [termonologies](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/blob/main/README.md#-before-starting-with-the-concepts-here-are-some-basic-termonologies-that-will-help-you-understand-the-after-written-things-the-better-way-) between different system building blocks and place the I/O pads.
 <br> MACRO FLOOR PLANNING
 <br> In this Dimensions, Pin Locations and Rows are defined.

POWER PLANNING- To provide power to the every macros and standard cells present in the design.

The next step is **_PLACEMENT_**.
<br> For MACROs, we'll place gate level netlist cells on the floor plan rows. Obviously these cells must be placed very close to each other to reduce interconnect delay. 
<br> It is done in 2 steps:- 
<br> GLOBAL:- Tries to find optimal position for more cells, Such positions are not necessarily leagal. So cells might overlap.
<br> DETAILED:- In this the positions recieved from the global step are minimally altered to be legal.

 <br> The next step is **_CLOCK TREE SYNTHESIS_**. The CTS is used to create network namely the **CLOCK DISTRIBUTION NETWORK** WHICH GIVES THE CLOCK TO ALL SEQUENTIAL ELEMENTS.
 <br> The next step is **_ROUTING_**. SIGNAL ROUTING. Given the placement and fixed metal layers, is required to know the pattern of horizontal and vertical wires to implement the nets. It is done on routing grids for least DRC erreors.

 <br> The last step is **_SIGN-OFF_**. Basically, it is the step in which verification are done.
 <br> Like:- _PHYSICAL VERIFICATION_ -DESIGN CHECKING AND LAYOUT VERSUS SCHEMATIC.
 _TIMING VERIFICATION_- STATIC TIMING ANALYSIS.

##### INTRODUCTION TO OPENLANE striVe

OPENLANE
<br> It started as an opensource flow for a true open source tape out experiments.

<br> STRIVE SOC FAMILY 
<br> It has many open source SoCs with different features, the list is as follows:-
<br> striVe- SKY130 SCL+ SYNTHESIZED 1KB SRAM.
<br> striVe 2- SKY130 SCL + 1KB OPENRAM BLOCK
<br> striVe 2a- striVe 2 WITH A SINGLE CHIP CORE MODULE
<br> striVe 3- OSUSCL + SYNTHESIZED 1KB SRAM
<br> striVe 5- SKY130 SCL +  SYNTHESIZED 1KB SRAM.
 <br> striVe 6- striVe 2 WITH DFT.

 MAIN GOAL OF OPEN LANE ASIC FLOW- to produce a ***clean*** GDS II with no human in the loop or human intervention.
 <br> Here the word CLEAN means :-
<br> No LVS violations 
<br> No DRC violations 
<br> Timing violations (work in progress)


It can be used to harden(to generate GDS II orthe final layout) 
<br> It has two modes of operation :-
<br> Autonomous- We configure the flow, push the button. Wait for some time as per the design size. And the GDS II layout is generated.
<br> Interactive- As per the interactive we can run commands and steps one by one. So that we can look at the intermediate result while completing the process. This can be helpful for experimentation.


### Get familiar to open-source EDA tools

OpenLANE has the following main folders and their divisions.
![Screenshot 2024-03-24 210436](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/f2818996-f7cc-47ae-bf7b-8303b9a0cf3e)

![Screenshot 2024-03-24 210524](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/d91ae271-d273-4232-b03d-6509423eb21a)

![Screenshot 2024-03-24 211520](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/df29ddcb-6d13-47ea-8ff3-87cb3c05e8cb)

DESIGN PREPARATION
<br>To invoke openLANE, use the *docker* command.Then put the interactive command (./flow.tcl-interactive). % package require openlane 0.9 runs version 0.9 of OpenLANE.
<br>![Screenshot 2024-03-24 211753](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/84e3bcd1-c593-409e-9840-dd93528898eb)

OpenLANE has many design types and the one we'll be using is picorv32a. the command is ***prep -design picorv32a***.  
![Screenshot 2024-03-24 213929](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/025ed681-841d-4586-9a52-16112d526cdc)

![Screenshot 2024-03-24 225926](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/d3c61443-4759-4e93-b1b2-362e8686415c)
![Screenshot 2024-03-24 215416](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/84d00283-6c4f-46b5-887f-88a2be35b561)

![Screenshot 2024-03-24 222542](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/f30b796b-288f-435d-9f74-e5569d9ccde2)

THE NEXT STEP IS TO SYNTHESIZE. YOU CAN DO THIS THROUGH THE COMMAND run_synthesis. It might take a couple of minutes for it to complethe process.
![Screenshot 2024-03-24 224834](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/7252045a-20bd-4e70-9a33-291a9a9e37ad)

The result after synthesisis:-
![Screenshot 2024-03-24 225040](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/5485b5fd-c1d3-4b0f-a356-c0417ca8009a)
![Screenshot 2024-03-24 224956](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/5c76c724-9481-4043-bdbf-1af01619aaba)


THE DFF COUNT IS 1613 AND TOTAL NO. OF CELLS IS 14876.
THE D FLIP-FLOP RATIO = 1613/14876= 0.108429685
<BR>![Screenshot 2024-03-24 232503](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/3c32008d-462d-4986-b5a0-d6b7e52e6404)

After synthesis you can check the reports by going to the shown location below....
<br> ![Screenshot 2024-03-24 233958](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/76a008bd-ab07-47e3-abd6-5d11024f8344)


## Day2 – Good floorplan vs bad floorplan and introduction to library cells
### <br> Chip Floor planning considerations
##### DEFINING WIDTH AND HEIGHT OF CORE AND DIE
First we will be knowing how to know the length and width of the chip die and core.
<br> ![Screenshot 2024-03-25 160420](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/224639e6-26a2-47be-8e1d-aab18f3f4c5b)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM
<BR> This, in the physical design overview flow was first step. So let us look how to get the values oh W and H.
<br> So let us begin with a basic netlist. With two filpflops (lounge and capture) and a basic 
combinational logic between them. So it is like two flops and and two gates with connection as shown.
<br> ![Screenshot 2024-03-25 163817](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/0734e670-bf64-4370-b59f-9b975c9162df)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

So for the netlist let us have proper dimensions. The would look something like below......
<br> 
![Screenshot 2024-03-25 170426](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/439cb666-c8f5-4ed4-8216-4796cbdd617f)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM
<br> basically we depend on the dimensions of the gates and the flops. So in this we donot care about the dimensions of wires but the gates and flops. Obviously wires will be in use in later operations but not when we want to know the dimensions of the chip's die and core.

So let us try giving these standard cells rough dimensions. If we consider their to be length and width to be 1 unit by 1 unit. Area is 1 sq. unit. And let us consider the same dimensions for the flipflops as well. So now let us join four of the components in single plate without the wires. now if we try to calculate the area, it would by 2 by 2 unit and the area will be 4 sq. unit.
<br> ![Screenshot 2024-03-26 184740](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/ade1e8bd-55f0-46c7-8784-9ae4d5b0d4db)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

So now we know the rough dimensions of the netlist or we can say that we have found the minimum area that will be covered by the netlist when placed anywhere.
<br> So now let us know the core and the die section of the chip. Here is the image of a silicon wafer and the location of the chip's die and core.
<br> ![Screenshot 2024-03-26 185838](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/8623a25e-5c6d-4556-95f6-d0c7f9a94742)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now what if we place our logic inside the chip. We have to place it in the core of our chip. 
<br ![Screenshot 2024-03-26 190349](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/869e3935-3d30-400f-9cc8-ea4efad8500d)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM
<br> As your cells cover all the area of the chip, it is known as 100 % utilization. Here comes a term from 100 % utilization that is utilization factor. It is the factor that is equal to the AREA OCCUPIED BY THE NETLIST/TOTAL AREA OF CORE. So if we put in the dimensions here it would be = 4x1 sq. unit/2 unit x 2 unit= 4 sq. unit/ 4 sq. unit. So the utilization factor will 1. The utilization factor being 1 means that the core of the chip is fully occupied and if in any cas we have to add any more cells, it is not possible. If we look at it as a practical scenario, we donot opt for 100% utilization rather we opt for 50-60 % utilization. So the utilization factor should 0.5 or 0.6. 
<br> Now there comes another term related to these dimensions which is aspect ratio. If we look at its definition it would be HEIGHT/WIDTH. 2 unit/2 unit = 1. If the aspect ratio is 1, it signifies that the chip is square in shape. If the aspect ratio is some other no. rather than 1, it signifies that it is rectangle in shape.


##### DEFINE THE LOCATION OF PREPLACED CELLS.
<br> So the next step is to define the location of preplaced cells. So what exactly are preplaced cells ?? To understand, let us take an example of a combinational logic. The assumption about this logic is that it does some amount of function. It does such a big task that its output is a huge circuit. The output circuit is so huge that it almost consists of 50k-100k gates. The circuit is :-
<br> ![Screenshot 2024-03-26 221026](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/0d0ee0be-7b07-4cef-ba7c-4c4da109da90)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM
<br> There is another way in which we could implement this circuit. That is by dividing it into two parts. If the circuit is of 100k gates, we could divide it into 50k and 50k gate blocks. Its division could be something like this.
<br> ![Screenshot 2024-03-26 221752](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/37a502e6-e99a-44f0-ae41-4c0d5af4a3bc)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM
<br> The block 1 and 2 will be implemented separately. After making two blocks (or parts) we need to extend the IO pins. 
<br> ![Screenshot 2024-03-26 222652](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/f3c98b5a-05c7-45de-a7fa-890d0e8bb88e)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM
<br> Next step, would be black boxing the blocks. Which would be like this :-
<br> ![Screenshot 2024-03-26 222850](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/c77f60b8-1b2a-49b5-aa3b-9291b7a90617)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

To implement these two separately, we need separate them like below.
<br>![Screenshot 2024-03-26 223330](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/9f68e3ed-41ee-456a-ad65-133868b313c8)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM
<br> These type of blocks can be given separately to different users and implemented separately but only once. They are being placed only once in a chip. That is why they are known as preplaced cells as they must be placed before routing. So these basically are macros or IPs which are implemented once but used several times.
<br> We need to place them in such a manner that their output pins are on one side and input pins on the other side.  And once they are placed their location cannot be moved and they are not touched again.
<br> ![Screenshot 2024-03-26 225552](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/206d06a9-2376-4cf0-9284-2905f8106c02)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM
<br> And this was how we define the location of preplaced cells. So now next step is to surround them using decoupling capacitors.


##### SURROUND PREPLACED CELLS WITH DECOUPLING CAPACITORS.
<br> Consider the following image.
<br> ![Screenshot 2024-03-27 120246](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/78e7ae8d-0b0f-4689-ad0d-aef636e9d275)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM
<br> Let us consider the piece of circuit to be a part of block A, B or C. Whenever the logic switches, like from 0 to 1; it demands for switching current that is peak current. What actually happens is that there is some capacitance sitting near the gates and the transition of logic from 0 to 1 will make the capacitor require some current so that the capacitor can represent the logic 1. This current will be provided to the circuit by supply voltage. But if the logic is changing from 1 to 0, it is the responsibility of the vss to take that amount of charge from the circuit. This will make all the capacitances to get discharged and these discharged current should be handled very well by the ground line of the power supply.    
<br> But in a practical scenario, when the voltage is supplied to the circuit there is a voltage drop. This because of inductance, resistance and capacitance peresent in the wire. The wires have physical dimensions and anything that has a physical dimension will surely have some inductance, resistance and capacitance.  This drop is reffered as VDD'. Also there is a issue in this. This is that we  need to make sure that this vdd falls in the noise margin region. If it is somewhere in the undefined region, it will be dangerous. That is the problem of having a large physical distance from the power supply and the main circuit.
<br> So if there is a problem, there must be a solution. And the solution to this problem is the use of DECOUPLING CAPACITORS. You can consider them as large capacitors completely filled with charge, the equivalent voltage across the capacitor is same as seen in the voltage supply.
<br> And if we try to understand its exact meaning, it can be understood by its name. That is, it decouples the main circuit and provides the circuit with voltage supply. But how would it solve the problem ?? So if we see our main problem was the voltage drop. It mainly happened because of large physical gap between the supply and the main circuit. Placing our capacitor would reduce that gap.
<br>![WhatsApp Image 2024-03-27 at 17 04 14_9c686eba](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/7a2105a9-7fc5-4806-af42-c76d96e3d13c)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM
![Screenshot 2024-03-27 171055](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/1a117df8-dc45-4679-939d-c539c78534c6)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM



##### POWER PLANNING
<BR> Let us consider a problem. Refer to problem image of the previous step. In that we provided it with current using a capacitor. Now let us imagine that circuit as a black box which repeated on a chip multiple times.   

![Screenshot 2024-03-27 172254](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/f6b5c959-3356-4e7f-be62-20eccc7d31a6)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

![Screenshot 2024-03-27 172313](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/940aef2d-6846-4ae3-ad1c-d1e22732d400)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

So consider the above image. You can see that the particular macro is being repeated 4 times on the chip. Now if you see, there is a line drawn from the driver to the load. It is specifying that there is a signal being sent from the driver to the load. And our problem question is, we have to make sure that the line maintains the signal so that the load recieves the same shape of the signals.  
<br> So first we will provide them all with power supply, something like below......
<br> ![Screenshot 2024-03-27 173841](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/96bb022a-eeb5-45b3-aefd-51829f49c053)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now for the line to retain the same signal i.e 0 to 1 it has to get necessary supply from the power as there is no decoupling capacitor over here to take care of the signal. It is the power supply which has to supply power to this line. Also it is not so feasible to put capacitors all over the circuit. Now if you notice, the power supply is far from the line, so there is always a chance of voltage drop. and vdd at the point near Rdd might be something different from the vdd on the line. Let us see what could be the vdd and the gnd on the line. 
<br> We could assume that this is a 16 bit bus. Whenever there is a 1 that means that the capacitor is charged to vdd. If there is 0 it means that the capacitors is getting discharged to gnd. 
<br> ![Screenshot 2024-03-27 204336](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/eda20f44-1531-438a-bc41-d28c0aa6e9e0)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

<br> As you could see in the image before this one that there was a inverter in the load that was connected to the line. So you can see in the image that the input value is 1110010111000110. So when it would be put by the inverter the output will be fully opposite of the input. It means that the capacitors that were charged to vdd will be discharged to ground and the ones that were discharged wil be charged.  
<br> Now since all the discharging will happen at  the same time and we have a single ground line for all, there will be several taps at the ground line and this would create a bounce. Due to this bounce the things might get unpredictable and they might get into the undefined region about which we read earlier. 
<br> About the charging if we say, that all the charging capacitors will ask for supply at the same time. Due to this there wil be a voltage droop. This is like one tap multiple buckets requiring water at the same time. And the voltage droop will be like shortage of water. 
<br> Exactly what is the reason of this problem ?? 
<br> The main reason is that there is only one power supply. If there would have been multiple sources, this problem wouldn't have occured.  
<br> So let me show you how it should have been.      
<br> ![Screenshot 2024-03-27 215637](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/960ae535-b195-4b33-898c-4fa412b0e077)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

![Screenshot 2024-03-27 222759](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/1e1309f1-cc4a-4a12-8415-10edabdc7cff)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM



##### PIN PLACEMENT

Before directly moving on to pin placement, let us before take an example.

There are two sections of a circuitry. And also some preplaced cells are their in these two parts of the circuits. It has 4 input pins and 3 output pins till now. And the connections are as follows.

![Screenshot 2024-03-27 225351](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/32694277-b215-45ab-aff0-919cac2f3e37)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now there are more 2 sections of a circuit, almost same to the ones seen earlier. Now we know 2 new input and 2 new output pins. And another preplaced cell, block c.

![Screenshot 2024-03-27 231013](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/11b8fecc-2f1b-45ab-9d88-29c799c2c2b3)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

So let us now see the whole complete design.

![Screenshot 2024-03-27 231154](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/ea0e7253-603b-47f2-9e3c-e7a6ed273c98)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now let's try to modify this circuit a bit. Starting with the repitition of Clk1 and Clk2 input pins twice and we could form just 1 pin and join to both the points. And this connectivity information is defined using a language known as VHDL or Verilog language and is called as the netlist. 

![Screenshot 2024-03-27 231748](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/d5d1bc00-ab22-438d-a97a-d6557e8bd30f)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

So let us put this design in the chip we are trying to design. It would look something like this.
<br>![Screenshot 2024-03-28 093522](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/8f437ecb-bd8f-4bff-b3bd-829455a6e253)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now we will do some thing known as Logical Cell Placement Blockage. This would not allow any cell to be placed in the area where the pins have been placed.

<br>![Screenshot 2024-03-28 093522](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/327a7cca-aea9-4d35-a5fb-7856cf7fdb3a)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now let us look at the labs. 
Till now we have done the labs till the command run_synthesis. So in our design flow the next step is run_floorplan. So we will be in the OpenLANE % prompt.

![Screenshot 2024-03-29 220201](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/3cf21dfe-d4f7-4093-9746-643415942dab)

![Screenshot 2024-03-29 220245](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/3b59c2d3-f008-45bb-9852-5dabd7e8fb17)

Now there is another file that contains the dimensions of core and die. 
![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/30652ae8-10d8-476a-b1d1-4e7e76c0415d)

And now if you wish to the see the layout after program, you can visit magic. 
<br>![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/e2882e4d-12f8-4ce1-8717-4bb885cf982d)

Through this we can review the layout of our design. So there are some features that we would need to know for using magic, as below:-

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/5193281b-2c4a-49ce-9aec-f04cee4b6df7)

1st - If you want the the layout to fit to your screen, select the layout and click on V.
<br> 2nd - If you want to zoom in, left click on mouse then right click and then Z on the keyboard. 
<br> Now if youn want to know about any component in the layout window, hover your pointer over it. Press S on your keyboard. And go the tkcon window opened. An while the component is selected type what in the tckon window. 

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/8aa3928c-0bc2-471f-bfbb-461ddd321a4b)

You can also zoom in and look at the details of many components. Also to tell this layout that we call is the floorplan, So it doesnot care about the placement of standard cells.

### <br> Library Binding and Placement 
#### Placement And Routing 
##### Bind the Netlist with Physical Cells

To know what this step means let us have a look at the netlist we took earlier. 
<br> ![Screenshot 2024-03-27 231154](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/dd0b0bde-ffce-44d8-8571-bb08b4beaa9f)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now you must have seen the specific shapes of the gates. Like the NOT gate has a triangle which as a bubble at the tip. So basically these shapes represent the functionality of the gate. But in our physical world these gates are in shape of a box either square or rectangle. And perform the function the gate they are supposed to perform. Now you can consider these cells as some books on a shelf. this shelf has many kind of these books and is known as a library. This library along with the cells has many kinds of information about them like - timing info, dimensions and the conditions for them to omit an output. It also has the same cell in various sizes. The bigger the size, the less the resistance, the faster the cell.

So what are the components that we have all ready. A well defined flooor plan, A netlist and a physical view of logic gates.
![Screenshot 2024-03-28 120616](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/8e138385-f863-487b-bb8e-67d6ce1b41e5)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

##### Placement

Now. We won't be using the shapes of the gates from the netlist but the connections. And the shapes we will be taking from the physical view of logic gates. Now on our floor plan there are some preplaced cells, that were placed during the floor planning step. In this step we need to make sure that automated router does not effect or move these cells and no components are placed on the area where these cells are placed. 
<br> How do we place these cells?? We have to place in such a manner that they are almost as in the circuit. Like in the circuit the FF 1 in the 1st section is near the Din 1, in the floor plan it should be in the same way. This would reduce the large physical gap, which can lead to delay. 

![Screenshot 2024-03-28 142730](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/06763ca9-c136-457c-8341-464f89e1f188)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

So now there is a thing that is to be noticed:-
<br> As the blue section input pin is Din3 and output pin is Dout3, then how will we place it as both pins are way far from each other...? And same is the problem for the green section....

So let us first see how will be the blue section placed. 

![Screenshot 2024-03-28 143549](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/dbd842ef-e4a1-44ce-9bee-05705d59c06c)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM
<br> Now still we can see that there is a large gap between the input pin and the output pin. We will look at that problem after placing the green section. If you would have noticed that even the distance from the Din 4 to Dout 4 is still large, these two are the pins of section 4 green.So its placement would look something like below.  

![Screenshot 2024-03-28 144104](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/66f7851b-b3f6-45fb-a282-c2bae34f4f80)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM


Let us now arrive at our problems. The only answer to our problem is optimize placement.

##### Optimize Placement

So first we will make some estimations. The estimations we are going to make will be about the capacitances even before the wiring or we can say routing. But how would it make a difference ??   
<br> So in actual there is a wire from one point to another. Like from Din2 to yellow FF1.  So if we look at the area of the wire from the Din2 and FF1(yellow) it is pretty large. So the capacitance and resistance will also be more. 
<br> If we see it would be like two people, one standing at the point Din 2 and one at the flipflop. So if the person at Din2 shouts it would be very much difficult for the person to hear as the distance is huge. So this problem can be solved by placing two people in between so that they hear the other person clearly and pass on the message. This is known as signal integrity. Here comes the task of repeaters. These repeaters are basically buffers, they will recondition your signal make a new signal that replicates your signal and send it again. 
<br> But again there comes a problem, which is that these repeaters will occupy more n more space on the floorplan. 

Now turn by turn we will seeing where there is a need of a repeater.
<br> First let us look at the orange section. Here if we see, all the components have decent distance in between. So hee the signal integrity can be maintained without any use of repeaters.
<br> Now let us move onto the yellow section. In this case the distance between FF1 and Din2 is pretty large, so here some repeaters should be placed to maintain the integrity. 

![Screenshot 2024-03-28 170814](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/1e0b1c7c-65b5-41d3-abe2-27c0d5981142)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

<br> Here comes the turn of blue section of circuit. First if we see the distance between Din3 and FF1, it is feasible here for the signals to pass without any repeaters. The same is the case, with the distances between FF1 and gate 1, and gate 1 and gate 2.But the distance between gate 2 and FF2 is bit longer. So we need to place a buffer in this area. Next is the distance between FF2 and Dout3, which can let signals pass without repeaters.

![Screenshot 2024-03-28 175602](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/89e6b309-48c6-4573-9e29-46dcd4a1e0ee)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Green section now.  First if we see the distance between Din4 and FF1, it is not feasible here for the signals to pass without any repeaters, so we will place a repeater here. 
![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/5ab2ecac-cd6f-492a-8188-656158d7ea00)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now as you can see, the line we have drawn for the placement of the repeater passes through the preplaced cells. It is (as we discussed earlier) a area where we are not supposed to put any component. So we will place a buffer above the area already occupied. Now if we look at the distance betwen FF1 and gate 1, the distance is decent but there is a kind of  criss cross as the wire of the connection blue Buff and Blue FF2 are also going the same way. And this is completely okay and how to fix this, we will be seeing ahead. If I tryna explain it simply,it is like that there are different layers. And if there are some overlapping wires, we can print them in different layer. So now the gate 1 and gate 2. The distance between them is pretty large and there is a cell in between and as I told earlier it was completely normal. So yeah we would place a buffer in between. And the distances between gate 2 to FF2 and FF2 to Dout4 is pretty feasible to cover without repeaters.                                                                                   

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/74474a5a-5055-4cf5-aef2-3e36a7be7f68)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Lab lesson 5-

So till now we have done till the process of floorplanning. Now our next step is placement. For the command will run_placement. 
![Screenshot 2024-03-29 232628](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/eecaf5de-bdfd-4f8e-a332-e84e83a93c05)

![Screenshot 2024-03-29 232644](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/56f08b3e-5de3-47bc-853e-f0b430c6e312)

For checking onto your placement, go to maic with the following directory.

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/fef3f1da-6531-4818-84cc-dfafd6ff6c3f)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

### <br> Cell Design and characterization Flows
#### Cell Design FLow

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/343dd35e-8bb0-4eef-8ce2-df7121e22499)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

The above chip is placed and routed. If you take up any cell like a buffer, gate or a flipflop it would be known as STANDARD CELL. This term is an essential one.

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/3eb1d20c-ec42-43dd-89cd-7733a3e3d4eb)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

These all standard cells are placed into a section known as _Library_. Also here the macros, The IPs and the DECAPs are kept in this library. This library is also discussed earlier.

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/2b803fa0-94d1-4fc3-a47e-05d99b764330)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/18751edb-8c2e-4689-95e6-224b2fbe59a3)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now, if you take any gate, like inverter only. We might consider it as a only a single input gate. But for a IC design, it has got something else to do with it. This simple cell has to go through a great design flow. 

 This process has got 3 major steps :- Inputs, Design steps and Outputs.

<br>Inputs- These are the inputs that we need to create this cell.
<br> PDKs consisting of DRC & LVS rules, SPICE models, library and user-defined specs. 

<br>Design Steps- designing stage.
<br>  Circuit design, layout design, characterization.

<br>Outputs- The outputs actually used by the EDA tools.
<br>CDL (circuit description language), GDSII, LEF, extracted spice netlist (.cir), timing, noise, power .libs, function.

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/42edb348-ed04-4b45-b2b3-b1a9b8904cbc)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

We have the following things from the 3 steps we about which read you earlier :-

Layout, description, spice extracted netlist, inverter sub circuit. 
<br> Let us now using these things follow the characterization flow. 

1st step - Read the model file.
2nd step - Read the extracted spice netlist file.
3rd step - Define or recognise the behaviour of the buffer.
4th step - Read the sub circuit file.
5th step - Attach the necessary power supplies.
6th step - Apply the stimulus.
7th step - Provide the necessary output capacitances.
8th step - Provide the necessary simulation command

The last step is to provide all this data to a software namely GUNA in form of a configuration.
<br> Using guna, we can classify characterization into mainly 3 types:-
<br>>Timing
<br>>Power
<br>>Noise

## Day 3 - Design and characterize one library cell using Magic Layout tool and ngspice
### <br>  Labs for CMOS inverter ngspice simulations
 
Now we will doing some spice simulations on some MOSFETS. But first we need to create a spice deck. A spice deck is a connectivity information of a netlist. So we need to create for PMOS And NMOS as well. We need to define the following things for creating this spice deck.....

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/6722add4-f2e0-4c68-88c6-526f670b1f0c)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

The connectivity information of PMOS.

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/75e9eac4-0354-419f-8509-3a27294d9833)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

The connectivity information of NMOS.

![Screenshot 2024-03-30 002823](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/4f142434-8d47-44af-a6ed-927d88ce5c38)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

The connectivity information of CLOAD(capacitor load).

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/79060827-7836-4c3f-938f-b980ff80c5bd)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM


The connectivity information of VDD.

![Screenshot 2024-03-30 003047](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/0f5d5ee5-e00e-4e2b-8458-55365507b29f)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now we will git clone a repository which has the .magic file. The github repository [github repository](https://github.com/nickson-jose/vsdstdcelldesign#standard-cell-design-and-characterization-using-openlane-flow)

Then gitclone the repository link through:-

![Screenshot 2024-03-30 131247](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/c5ec9e1b-0612-429d-b1f7-3312df5c71e2)

Now after copying go to openlane directory in terminal........
<br>Put git clone command and then paste the URL.

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/50c1aa1e-2ace-489b-97d8-b26ab34938d0)

This will create a folder of the same name as the repository. 
![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/9b5f0854-2ec4-44dd-9960-1ffaa385ad2d)

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/c91a7451-2ad2-439e-a78a-cb41d1b12718)

Now lets look at what is there inside this..

![Screenshot 2024-03-30 135241](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/90f7486d-56ab-4418-bd61-7a16dffd25c1)

Now if you look at the repository and the terminal, they have the same files.

Now we will go to magic with our cloned file. 

![Screenshot 2024-03-30 152739](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/2710d3b9-24bd-4d66-a1cc-aeaa38207f4b)

![Screenshot 2024-03-30 152759](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/dad500ad-72b3-49e5-95c3-f9ac597289a2)



### <br> Inception of Layout – CMOS fabrication process

16 MASK CMOS PROCESS

1. Selecting a Substrate
<br>  A substrate is something onto which you fabricate your design. The one we will be choosing will be a p-type. Out of all the qualities of the substrate, we will be mainly focusing on resistivity and doping level. The main focus for our doping level will be that the Substrate doping should be less than well doping.

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/4e054482-3f94-49b9-9314-f045aa33065d)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

2. Creating active region for transistors.
<br>  These are the regions where actually you see the pmos and nmos transistors. So basically we will be creating some bucket kind of in the substrate, where we will create pmos and nmos. First we will create some isolation between the pockets so they don't interfere in eachother's working. So for this you can deposit layers. First, a 40 nm SiO <sub>2</sub>. Then, 80 nm Si<sub>3</sub>N<sub>4</sub> and a 1um photoresist.  
There is a term Mask. The layout particularly in the fabrication term is known as mask. The layouts that we see in custom design are converted to these masks. 
<br> Now the areas where we donot want any chemical reactions to happen, we will place the masks over there. Then we will the expose the areas not covered to UV light. Then we will wash or remove the area which was not covered.

![Screenshot 2024-03-28 230516](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/eaf51411-8cf1-425c-9319-e6e174ad5e4b)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

![Screenshot 2024-03-28 230525](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/70deb806-dd10-42b6-adab-c3ff55025342)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Then you remove this mask layer. Now if you do any reactions or depositions, the area under the photoresist won't be effected. 

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/9b437569-8972-4852-b62f-e064674226d6)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now we will also remove the layer of 80 nm Si<sub>3</sub>N<sub>4</sub> that was exposed to UV light and the photoresist as well. The remaining layer of Si<sub>3</sub>N<sub>4</sub> will also act as a good layer of protection as well. 

![Screenshot 2024-03-29 091448](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/ffdedb54-c277-4b16-977e-12124c980023)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

When we will put this substrate in a very hi temperature furnace, the area of SiO <sub>2</sub> that is not covered by Si<sub>3</sub>N<sub>4</sub> will grow and the area that was covered won't grow. Let us see how. So first we need to place this in an oxidation furnace. It looks something like this.....

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/86106984-fcce-447d-991f-6db2b3777fbc)
<br> SOURCE OF THE IMAGE- THE WEB PAGE OF IIT KANPUR. 
<BR> THE LINK- (https://www.iitk.ac.in/dordold/index.php?option=com_content&view=category&layout=blog&id=186&Itemid=205#:~:text=Oxidation%20Furnace&text=Thermal%20oxidation%20is%20a%20simple,filler%20material%20in%20gaps%20etc).


THIS WOULD NOW LOOK SOMETHING LIKE BELOW.........

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/352132d4-2f1f-4e4e-9ff4-f10c3687b267)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

The grown part is referred to field oxide or the bird's beak. And the process is known as "LOCOS"(Local Oxidation of Silicon.). 


![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/9b2bb907-4f36-4eab-9fcb-df72e2e3e120)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Si<sub>3</sub>N<sub>4</sub> will be stripped using hot phosphoric acid. 

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/27250d7e-7b42-4b6c-b7b8-48c177530030)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now, let me define the regions. The well kind of regions that were protected regions are the active regions. And the grown part is the isolated region, which won't allow one transistor to interfere in other transistor's working. 

3. Creating N-well and P-well. 
<br> Now the N-well will be used for the fabrication of PMOS transistors and the P-well will be used for NMOS transistors. In this also, one area needs to be protected as both the wells cannot be formed at the same time. The process to be followed now is pretty similar to the one followed earlier. First put a layer of photoresist, and then the mask upon the area you want to protect. Expose to UV light. Wash off the exposed area. Remove the mask. And now for making a P-well in the exposed area, we will use Boron. Boron is a P-type substance. To diffuse Boron into the well, we would use the process namely Ion implant.

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/ee97d44b-1083-4bcb-9450-677afb126e43)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

<br> You follow the same steps for N-well as well. But in place of Boron you use Phosphurous as it is an N-type substance. 

![Screenshot 2024-03-29 095933](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/b3fba42f-d639-476a-8668-8844de6c164e)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

![Screenshot 2024-03-29 100125](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/ed522c49-f405-4aa6-b027-eeac85f7a847)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

![Screenshot 2024-03-29 100145](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/ef433249-5875-4781-9c44-be7788037501)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

These wells are also known as the twin tubs. Now we need to diffuse the well, so that it covers almost half of the substrate. This will decide the depth of the wells. So for this we will be putting this into a high temperature furnace.  

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/40937700-52fa-4c2b-a397-da16f605463a)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM


4. Formation of Gate

Gate as we see now, is the most important termianl of the transistors beacause you control the threshold voltage(turning on voltage of the transistor) from here. So the fabrication of gate terminal becomes really important. 

![Screenshot 2024-03-29 110459](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/f2c6eb80-51fa-422a-b6b3-b45961398e2b)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/e1857037-d872-4624-927f-f87cd33e506c)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM


So, we need to control the oxide capacitance and doping concentration.
<br> First let us control doping capacitance. Now, we will follow the same steps as before. Now we will be using the mask4, and as the name suggests for this CMOS process we will be using total of 16 masks. And for this we will be using boron but with lesser force. We will maintain the dose of boron in such a manner, so that we have the required doping concentration. And this doping concentration depends upon the threshold voltage seen in the above images. 

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/a06c31c2-ed88-482a-8f71-a165f6ede0f8)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now using mask 5 we will be following same process for NMOS but again using phosphorous or we can also use arsenic.  

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/9fc26e48-d3a2-42c4-bbd0-96610c630481)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

As we have been implementing many layers an P & N type substances, So our oxide is being damaged multiple times. So we will repair this layer.

First we etch the original damaged oxide layer using dilute hydrofluoric solution. Then we regrow this layer to give high quality oxide.  
<br> ![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/730dccb6-a8d9-4e6d-bbf8-251a99118eea)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now we will deposit a layer of 0.4 um polysilicon layer. 
![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/fb12fc0f-9531-46ab-93b8-57777177978d)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Then we ion implant any N-type substance either phosphurous or arsenic for low gate resistence.

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/716ca0e7-879e-4a48-bc48-c36354ab867e)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now using photoresist and mask 6, we will make something like below. 

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/26dd0251-2c9c-4366-91d1-000d46a36636)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now we can remove the mask and etch away the polysilicon layer that was not covered by photoresist. And then remove the photoresist layer.

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/0ea48563-dcb0-42b3-8ae0-e51c66a9336d)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

5. Lightly Doped Drain formation

We need to create LDD of two types, P- and N-. First we will put a layer of photoresist then mask7 and expose the other side to UV light. Then remove the mask. And as firstly we have exposed the P well to UV light. So we tend to make a NMOS there. So we would use phosphorous for ion implant. So for this we will be choosing the force and the dosage very carefully, so the n- implant does not penetrate fully into the well and hovers at the top. 

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/53e09902-8d39-4c4f-abb3-6d54f3aa387d)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

But why is it n- and not n+ ?? It is so, because if p or n type has "-" as after them, it means it is lightly doped.


Same process for PMOS. But with Boron. 

![Screenshot 2024-03-29 130424](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/09a8fe90-641f-491e-94ab-74c3e7f5836f)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now somehow we have to protect the implants so in the further processes nothing gets into them. So we will put some spacers over there. So first deposit a thick layer of either SiO <sub>2</sub> or Si<sub>3</sub>N<sub>4</sub>. So we will do Plasma anisotropic etching. In this all of the layer is etched but the substance near the side walls remains.  

![Screenshot 2024-03-29 132323](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/5443e6cb-7545-4645-b07d-8ae29389c08c)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

6. Source and Drain formation.

Now add a thin layer of screen oxide. The purpose of adding it is to avoid the effect of channeling. The effect of channeling is when we do alot of ion implant and when the vector velocity of the crystaline structure of our P substrate matches with the velocity of the ions. When this happens, the ions might go deep into the substrate without even hitting any of the silicon atoms. 

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/d5f9729d-2f8a-453b-a0cd-269afc1469fd)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now again thesame process. Photoresistor, Mask 9, other side's exposure to UV light, Ion implant of arsenic.

![Screenshot 2024-03-29 134206](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/1fc364ef-f0eb-485d-a657-782a11efc25c)

Same for the otherside. Ion implant with Boron. 

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/a680b85d-500c-4723-ad76-0d86f23a1196)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now we will do High Temperature Annealinng.
![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/eb7571dc-4472-4f08-a03c-7c3474cb1ffb)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

7. Steps to form contacts and interconnects(local) 

So contacts are really important because, that is the only thing that is accessible to an user. It is a medium through which you can control the electrical characteristics of your transistors.   

So to start with, we will first etch the thin oxide layer that we had put in the earlier steps. Then, deposit titanium on wafer surface, using sputtering. But what is sputtering?? It is a process in which we take the metal, which in this example is titanium and hit argon gas at it. And this will make the atoms of the titanium sputter and enter into the substrate.    

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/f8930305-c0ae-425c-8442-d52e6c5d1c39)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM


![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/4e2ef4a8-3eca-444c-b2a6-944161b4f6a7)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/775101e8-9a99-4fd5-a863-b56bc645f4b5)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Apart from the above result for the N<sub>2</sub> being an ambient there is another result. That is TiN that is used only for local comunication.  

So now, If you look at the previous image you will able to see a dark blue layer which is in the area where there are no thick layers. That layer is TiSi<sub>2</sub>. And the light blue layer above every structure is TiN.


Now we need to decide which contacts to bring to the next level. As some connections can be made internally and there is no need of taking them above. 

Now we will put the layers of photoresist and mask 11 on the areas which we want to reach above. 

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/436b90f8-e747-480b-893f-d1d412f7b405)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Then remove the mask and etch off the extra TiN using RCA cleaning. RCA cleaning is done a solution known as RCA only. Its solutes vary from use to use. In this it would consist of:- 
<br> 1. De-ionized water (H<sub>2</sub>O), 5 parts
<br> 2. Ammonium hydroxide (NH<sub>4</sub>OH), 1 part
<br> 3. Hydrogen peroxide (H<sub>2</sub>O<sub>2</sub>O), 1 part

It would look ssomething like below- 
<br>![Screenshot 2024-03-29 173223](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/ac10b124-11bb-4ee9-ae70-a18310fdf3c9)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now we remove the photoresist layer. 

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/00101cc3-cf73-4591-a111-2bee45ef3553)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM


8. Higher level metal formation.

Now if we see surface topogaraphy of this state of the substrate is not suitable for further ados. 

So for this we will deposit a thick layer of SiO <sub>2</sub>. And this is a specific  SiO <sub>2</sub> doped with phosphorous or boron (known as phosphosiicate glass or borophosphosilicate glass) depsited on wafer surface.

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/c441258f-c33d-447a-8406-87a3c1d96236)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now, we will use the Chemical Mechanical Polishing technique for planarizing wafer surface. 

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/46b26ebe-736a-40a3-80aa-2de1822cd001)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Now we will follow some more processes and form the below kind of substrate.

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/2a3f77a1-8b7b-48f1-808b-e97053e13807)
<br> SOURCE OF THE IMAGE- VSDIAT PLATFORM

Labs -

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/738658ea-111f-42b7-82e2-26f06f00c364)

So this is the layout for our inverter that we got in the previous labs. In this are two transistors PMOS and NMOS. 

![image](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/2cdd3ecc-4fc9-4666-bae5-5ece858a7a26)

And the red line is polysilicon. In the repository mentioned, the steps of making an inverter from scratch are also given.


## Day 4 -  Pre-layout timing analysis and importance of good clock tree

### <br> Timing modelling using delay tables
 
As of now, we have done till placement in the flow and extracted a spice file given a .magic file. Now if we see into the amgic layout, it has many kinds of information, but we donot need that file for routing purpose. We need the info inside that layout. And this is where the .lef file comes in picture. This lef file contains all the info. So our first task will be the extraction of lef file. But beforehand we should know some guidelines---

1st- Always put input and output ports on the intersection of the vertical and the horrizontal tracks. 

2nd - The width of the standard cell must be in the odd multiples of the track pitch and the height in the odd multiples of the vertical track pitch. 


































































 
