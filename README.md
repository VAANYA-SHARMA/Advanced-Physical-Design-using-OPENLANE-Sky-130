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
<br> SoC design and OpenLANE
<br> Starting RISC-V SoC Reference design
<br> Get familiar to open-source EDA tools

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
<br> #### Before starting with the concepts, here are some basic termonologies that will help you understand the after written things the better way:-
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
For designing such a circuit, we would first need to represnt it using a block diagram.
<br> Like this :-
<br> ![WhatsApp Image 2024-03-22 at 20 42 53_c0279c2d](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/e4aa7533-886a-483b-b1ec-ad111819a3db)
source of the image- VSD-IAT PLATFORM 
<br> So, now in the same manner of block diagram based representation; let us go inside the package.......................
<br> ![WhatsApp Image 2024-03-22 at 20 43 09_46be60ff](https://github.com/VAANYA-SHARMA/Advanced-Physical-Design-using-OPENLANE-Sky-130/assets/163661889/cae4a683-eabd-421e-a0bd-f1d08eecb9fe)
<br> So as you saw that inside the package(the white outline) is kept the chip. And what are those white thread like structures ?? You must be wondering. These are the WIRE BONDS. You can know what is there function at [termonologies]()


































































