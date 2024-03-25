# Advanced-Physical-Design-using-OPENLANE-Sky-130
This is a workshop which is about ASIC design using OPEN source tools.
<br>
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
<br> Chip Floor planning considerations
<br> Library Binding and Placement
<br> Cell design and characterization flows
<br> General timing characterization parameters

<br> Day 3 - Design and characterize one library cell using Magic Layout tool and ngspice
<br> Labs for CMOS inverter ngspice simulations
<br> Inception of Layout – CMOS fabrication process
<br> Sky130 Tech File Labs

Day 4 - Pre-layout timing analysis and importance of good clock tree
<br> Timing modelling using delay tables
<br> Timing analysis with ideal clocks using openSTA
<br> Clock tree synthesis TritonCTS and signal integrity
<br> Timing analysis with real clocks using openSTA

<br> Day 5 - Final steps for RTL2GDS
<br> Routing and design rule check (DRC)
<br> PNR interactive flow tutorial

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
<br> So as you saw that inside the package(the white outline) is kept the chip. And what are those white thread like structures ?? You must be wondering. These are the WIRE BONDS. You can know what is there function at [termonologies](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/blob/main/README.md#-before-starting-with-the-concepts-here-are-some-basic-termonologies-that-will-help-you-understand-the-after-written-things-the-better-way-)
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


