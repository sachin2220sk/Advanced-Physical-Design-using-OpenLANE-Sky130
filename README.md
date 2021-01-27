<h3 align="center"> Advanced Physical Design using OpenLANE Sky130</h3>

![](Images_Day_1/Advanced-Physical-Design-using-OpenLANE_Sky130_1.png)

This GitHub repository will demonstrate the work done in Advanced-Physical-Design-using-OpenLANE-Sky130 workshop which is organized by VLSI System Design also called VSD. The main aim of this workshop is to give hands-on experiences on SoC design planning in OpenLANE flow using Google-SkyWater 130nm process design kit (pdk).


<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="##Day 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK">Day 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK</a>
      <ul>
        <li><a href="#ASIC Design Flow">ASIC Design Flow</a></li>
        <li><a href="#OpenLANE Based on Serval Open Source Project for ASIC Design Flow">OpenLANE Based on Serval Open Source Project for ASIC Design Flow</a></li>
        <li><a href="#Google-SkyWater 130nm pdk">Google-SkyWater 130nm pdk</a></li>
        <li><a href="#OpenLANE">OpenLANE Introduction</a></li>
      </ul>
      </li>
    <li>
      <a href="#Day 2 - Good floorplan vs bad floorplan and introduction to library cells">Day 2 - Good floorplan vs bad floorplan and introduction to library cells</a>
      <ul>
        <li><a href="#Floorplan">Floorplan</a></li>
        <li><a href="#View-Placement-in-Magic">View Placement in Magic</a></li>
      </ul>
    </li>
    <li>
      <a href="#Day 3 - Design library cell using Magic Layout and ngspice characterization">Day 3 - Design library cell using Magic Layout and ngspice characterization</a>
      <ul>
        <li><a href="#Extraction to Spice using Magic">Extraction to Spice using Magic</a></li>
        <li><a href="#Spice Simulation">Spice Simulation</a></li>
      </ul>
    </li>
    <li>
      <a href="#Day 4 - Pre-layout timing analysis and importance of good clock tree">Day 4 - Pre-layout timing analysis and importance of good clock tree</a>
      <ul>
        <li><a href="#LEF File">LEF File</a></li>    
      </ul>
    </li>
    <li>
      <a href="#Day 5 - Final steps for RTL2GDS using tritonRoute and openSTA">Day 5 - Final steps for RTL2GDS using tritonRoute and openSTA</a>
      <ul>
        <li><a href="#Generating Power Distribution Network">Generating Power Distribution Network</a></li>
        <li><a href="#SPEF Extraction">SPEF Extraction</a></li>
      </ul>
      </li>
    
  </ol>
  </details>

## Day 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK
### ASIC Design Flow

![](Images_Day_1/RTL_GDSII.JPG)

### OpenLANE Based on Serval Open Source Project for ASIC Design Flow

#### Synthesis
- yosys :- Generates gate-level netlist.
- abc :- Performs cell mapping.
- OpenSTA :- Performs pre-layout STA.

#### Floorplanning
- init_fg :- Define the core area for macro as well the cell sites and tracks.
- ioplacer :- Place macro input/output ports.
- pdn :- Generates the prower distrubution network.

#### Placement
- RePLace :- Performs global placement.
- OpenDP :- Performs details placement.

#### Clock Tree Synthesis.
- TritonCTS :- Performes clock tree synthesis.

#### Routing
- FastRoute :- Performs global routing.
- TritonRoute :- Performs detailed routing.

#### Sign Off
- Magic :- Generates GDSII layout file from routed def.

### Google-SkyWater 130nm pdk

We used Google-SkyWater 130nm pdk. The pdks folder contains all the information related to process design kit (pdk). There are 3 sub-directories that can be accessed as follows:- 

![](Images_Day_1/Capture1.JPG)

1.	open_pdks :- Contains scripts that are used to bridge the gap between closed-source and open-source pdk to EDA tool compatibility.
2.	sky130A :- Contain open-source compatibility pdk files.
3.	skywater-pdk :- Contain foundry provide pdk related files.

sky130A contain two sub-directories:-

1.	libs.ref :- Contains process specific files. 


![](Images_Day_1/Capture2.JPG)

File nomenclature is as follows:
sky130_fd_sc_hd
sky130 stands for process name
fd stands for foundry name
sc stands for standard cell
hd stands for high density (variant of the pdk) 

2.	libs.ref :- Contain files specific to tools that we will  be using for end to end VLSI design.


![](Images_Day_1/Capture3.JPG)



Designs Directory  
The design that runs within OpenLANE are extracted from openLANE_flow/designs directory 


![](Images_Day_1/Capture5.JPG)

Designs Directory  Hierarchy
For this  workshop, we will we using “picorv32a” design. The design hierarchy for picorv32a comes with follows components:-


![](Images_Day_6/Capture1.JPG)

1.	src directory  :- Contains Verilog files and sdc constaint files.
2.	config.tcl files :- Responsible for various design specific configuration switches and parameters which are used by OpenLANE flow tools. For example configuration file looks like this:-


![](Images_Day_1/Capture8.JPG)

### OpenLANE

Go to openLANE_flow directory and and type ./flow.tcl which run in docker that should be installed with OpenLANE tools.
To run OpenLANE interactively, type ./flow.tcl -interactive
To run OpenLANE in autonomous, type ./flow.tcl -design

![](Images_Day_1/Capture4.JPG)

OpenLANE requires different software to run it. So, run following command :-
package require openlane 0.9  


![](Images_Day_1/Capture7.JPG)

The keyword “prep” is used to preparing the design which effectively used by OpenLANE tools. Run command :- prep -design <design_name> 
design_name = picorv32a
During the preparation stage of OpenLANE, the cell LEF and technology LEF information are combined and are collectively termed as merge.LEF

After Preparation complete look in openlane_flow/designs/picrov32a directory whare, we see runs directory is created.


![](Images_Day_1/Capture9.JPG)

Inside the runs directory we have directory with present date and time and inside this directory we have these directories:

![](Images_Day_1/Capture10.JPG)

The config.tcl file contains all the parameters used by OpenLANE for this specific run.

To do synthesis run command run_synthesis

![](Images_Day_1/Capture11.JPG)

![](Images_Day_1/Capture12.JPG)

After Synthesis complete look in openlane_flow/designs/picrov32a/runs//reports/synthesis directory where we see yosys_2.stat.rpt which we used for calculates flop ratio, buffer ratio etc.


![](Images_Day_1/Capture13.JPG)


PDK fo

## Day 2 - Good floorplan vs bad floorplan and introduction to library cells

## Day 3 - Design library cell using Magic Layout and ngspice characterization

## Day 4 - Pre-layout timing analysis and importance of good clock tree

## Day 5 - Final steps for RTL2GDS using tritonRoute and openSTA

