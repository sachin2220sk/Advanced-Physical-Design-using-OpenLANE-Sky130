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
        <li><a href="#Important Parameter related to floorplans ">Important Parameter related to floorplans </a></li>
        <li><a href="#Floorplan using OpenLANE">Floorplan using OpenLANE</a></li>
        <li><a href="#View Floorplan using Magic tool">View Floorplan using Magic tool</a></li>
        <li><a href="#Placement using OpenLANE">Placement using OpenLANE</a></li>
        <li><a href="#View Placement using Magic tool">View Placement using Magic tool</a></li>
      </ul>
    </li>
    <li>
      <a href="#Day 3 - Design library cell using Magic Layout and ngspice characterization">Day 3 - Design library cell using Magic Layout and ngspice characterization</a>
      <ul>
        <li><a href="#Cloning Design File from GitHUB Repository and Copy Tech File">Cloning Design File from GitHUB Repository and Copy Tech File</a></li>
        <li><a href="#Inverter Layout using Magic tool">Inverter Layout using Magic tool</a></li>
        <li><a href="#Extract Spice file using Magic tool">Extract Spice file using Magic tool</a></li>
        <li><a href="#Understanding of spice file using ngspice">Understanding of spice file using ngspice</a></li>
        <li><a href="#Characteristics of Inverter">Characteristics of Inverter</a></li>
      </ul>
    </li>
    <li>
      <a href="#Day 4 - Pre-layout timing analysis and importance of good clock tree">Day 4 - Pre-layout timing analysis and importance of good clock tree</a>
      <ul>  
        <li><a href="#PnR Guideline for Standard Cell Ports">PnR Guideline for Standard Cell Ports</a></li>   
        <li><a href="#Analysis of Inverter Layout using Magic tool">Analysis of Inverter Layout using Magic tool</a></li>   
        <li><a href="#Include Standard Cell into OpenLANE">Include Standard Cell into OpenLANE</a></li>
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
`sky130_fd_sc_hd`
- sky130 stands for process name
- fd stands for foundry name
- sc stands for standard cell
- hd stands for high density (variant of the pdk) 

2.	libs.tech :- Contain files specific to tools that we will  be using for end to end VLSI design.


![](Images_Day_1/Capture3.JPG)


The design that runs within OpenLANE are extracted from openLANE_flow/designs directory 

![](Images_Day_1/Capture5.JPG)

For this workshop, we will we using “picorv32a” design. The design hierarchy for picorv32a comes with follows components:-

![](Images_Day_1/Capture6.JPG)

- src directory  :- Contains Verilog files and sdc constaint files.
- config.tcl files :- Responsible for various design specific configuration switches and parameters which are used by OpenLANE flow tools. For example configuration file looks like this:-


![](Images_Day_1/Capture8.JPG)

### OpenLANE

Go to openLANE_flow directory and and type > ./flow.tcl > which run in docker that should be installed with OpenLANE tools.
To run OpenLANE interactively, type ./flow.tcl -interactive
To run OpenLANE in autonomous, type ./flow.tcl -design

![](Images_Day_1/Capture4.JPG)

OpenLANE requires different software to run it. So, run following command :-

`package require openlane 0.9` 

The keyword “prep” is used to preparing the design which effectively used by OpenLANE tools. Run command :-

`prep -design <design_name>` 

design_name = picorv32a

During the preparation stage of OpenLANE, the cell LEF and technology LEF information are combined and are collectively termed as merge.LEF

![](Images_Day_1/Capture7.png)

After Preparation complete look in openlane_flow/designs/picrov32a directory whare, we see runs directory is created.


![](Images_Day_1/Capture9.JPG)

Inside the runs directory we have directory with present date and time and inside this directory we have these directories:

![](Images_Day_1/Capture10.JPG)

The config.tcl file contains all the parameters used by OpenLANE for this specific run.

To do synthesis run command 

`run_synthesis`

![](Images_Day_1/Capture11.JPG)

![](Images_Day_1/Capture12.JPG)

After Synthesis complete look in openlane_flow/designs/picrov32a/runs/23-01_16-45/reports/synthesis directory where we see yosys_2.stat.rpt which we used for calculates flop ratio, buffer ratio etc.

![](Images_Day_1/Capture13.png)



## Day 2 - Good floorplan vs bad floorplan and introduction to library cells

### Important Parameter related to floorplans 

- A "die " which consists of "core" is small semiconductor material specimen on which the fundamental circuit is fabrication. Placed all logical cell inside the “core”.
- Netlist :- The connectively information between the gates is coded using VHDL/Verilog language is called as “netlist”
- Utilization Factor :- It is ratio of area occupied by netlist to total area of the core. When utilization factor is 1 then it means “core” is completely occupied. Ideally we don’t go with 100% utilization. We go with 50-60% utilization i.e., 0.5 or 0.6.
- Aspect ratio :- It is ratio of height of core to width of core. When aspect ratio is 1 then chip is in square shape.

### Floorplan using OpenLANE

The season started with introduction to keyword “tag” which used to provide user defined name to run. This is implement while preparing the design by following command: -

`prep -design <design_name> -tag <tag_name>`

Design_name = picorv32a and tag_name = woekshop

![](Images_Day_2/Capture1.JPG)

![](Images_Day_2/Capture2.JPG)

This creates new directory within designs/picorv32a/runs directory as “woekshop”.

![](Images_Day_2/Capture3.JPG)

Here, we change CLOCK_PERIOD variable

![](Images_Day_2/Capture4.JPG)

Then run synthesis.

![](Images_Day_2/Capture5.JPG)

![](Images_Day_2/Capture6.JPG)

To run floorplan in openLANE run following command: -

`run_floorplan`

![](Images_Day_2/Capture7.JPG)

Floorplan also runs as per the configuration settings present in the designs config.tcl files. 

![](Images_Day_2/Capture8.JPG)

After floorplan complete look in openlane_flow/designs/picrov32a/runs/woekshop/results/floorplan directory where we see "picorv32a .floorplan.def" file which contain information about core area and placement of cell sites.

![](Images_Day_2/Capture9.JPG)

![](Images_Day_2/Capture10.JPG)

`UNIT DISTANCE MICRONS 1000` represents 1000 data base unit per 1 Micron.

`DIEAREA ( 0 0 ) ( 1004135 766580 )` represents the placement of die as follows ( Lower_right_x-value Lower_left_y-value ) ( Upper_right_x-value Upper_right_y-value )

### View Floorplan using Magic tool

We require three file: -
-	Magic Technology file 
-	Magic lef file from preparation  stages
-	Floorplan generated def file

Use following command for viewing floorplan using magic tool

`magic -T <magic tech file> lef read <lef file> def read <def file>`
  
Here, magic tech file = sky130A.tech

lef file = merged.lef

def file = picorv32a.floorplan.def

![](Images_Day_2/Capture11.JPG)

Press s followed by v to select and view floorplan of whole design: -

![](Images_Day_2/Capture12.png)
  
### Placement using OpenLANE

Usually happens in two stages: -
-	Global Placement: - Main aim is optimization. This is done by reducing wire length by Half Perimeter Wire Length (HPWL).
-	Detail Placement: - Main aim is legalization.

To run placement is use following command: -

`run_placement`

![](Images_Day_2/Capture13.JPG)

![](Images_Day_2/Capture14.JPG)

 After Placement complete look in openlane_flow/designs/picrov32a/runs/woekshop/results/placement directory where we see picorv32a .placement.def file
 
### View Placement using Magic tool

We require three file: -

-	Magic Technology file 
-	Magic lef file from preparation  stages
-	Placement generated def file

Use following command for viewing floorplan using magic tool

`magic -T <magic tech file> lef read <lef file> def read <def file>`

Here, magic tech file = sky130A.tech
lef file = merged.lef
def file = picorv32a.placement.def

![](Images_Day_2/Capture15.JPG)

Press s followed by v to select and view floorplan of whole design: -

![](Images_Day_2/Capture16.png)

## Day 3 - Design library cell using Magic Layout and ngspice characterization

### Cloning Design File from GitHUB Repository and Copy Tech File

Use following command for clone design file from GitHUB repository to `openlan_working_dir/openLANE_flow` directory

`git clone https://github.com/nickson-jose/vsdstdcelldesign`

![](Images_Day_3/Capture0.JPG)

After cloning complete look in Desktop/work/tools/ openlan_working_dir/openLANE_flow directory where we see `sky130A_inv.mag` file.

![](Images_Day_3/Capture1.JPG)

Now, use following command for copy tech (i.e, sky130A.tech) file which is present in the `openlane_working_dir/pdks/sky130A/libs.tech/magic` directory, to the `vsdstdcelldesign` directory in openLANE_flow.

` cp sky130A.tech /home/sachinkumar/Desktop/work/tool/openlan_working_dir/openLANE_flow/vsdstdcelldesign`


![](Images_Day_3/Capture2.JPG)

### Inverter Layout using Magic tool

Use following command for viewing inverter using magic tool

`magic -T sky130A.tech sky130_inv.mag &`

![](Images_Day_3/Capture4.JPG)


![](Images_Day_3/Capture5.png)

### Extract Spice file using Magic tool

88Use following command in sequence on magic terminal for extraction of spice file

`extract all`
`ext2spice cthresh 0 rthresh 0`
`ext2spice`
  
 
![](Images_Day_3/Capture8.JPG)

Now go to `/Desktop/work/tools/openlsne_working_dir/openLANE_flow/vsdstdcelldesign` directory where we see `sky130_inv.ext` and `sky130_inv.spice` file.

![](Images_Day_3/Capture9.JPG)

#### Understanding of spice file using ngspice

Do some modification in ` sky130_inv.spice` file


![](Images_Day_3/Capture10.JPG)

Now open the `sky130_inv.spice` file using ngspice using following command: -
`ngspice sky130_inv.spice`

![](Images_Day_3/Capture11.JPG)


![](Images_Day_3/Capture12.JPG)

Now we can view the plot using following command

`plot y vs time a`

![](Images_Day_3/Capture13.JPG)

![](Images_Day_3/Capture14.png)

### Characteristics of Inverter

Rise Time: - It is time during transition, when output value switches from 20% to 80% of maximum value.

Fall Time: - It is time during transition, when output value switches from 80% to 20% of maximum value.

Propagation Delay: - It measured between 50% transition point of input and output waveform.



## Day 4 - Pre-layout timing analysis and importance of good clock tree

### PnR Guideline for Standard Cell Ports

-	Input and output port must be placed on vertical and horizontal tracks.

-	Width of standard cell must be odd multiple of track horizonal pitch and likewise height should an odd multiple of track vertical pitch.

`tracks.info` file which is present in `/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/openlane/sky130_fd_sc_hd` directory contains the offset and pitch information of different layers.

To view `tracks.info` file run following command: -

`less tracks.info`


![](Images_Day_4/Capture2.JPG)

![](Images_Day_4/Capture3.JPG)

Here, we observe the metal1 layer or horizontal layer is at an offset of 0.17 and pitch of 0.34. The metal2 layer or horizontal layer is at offset of 0.23 and pitch of 0.46 and so on.

### Analysis of Inverter Layout using Magic tool

Run following command to open layout of inverter using magic tool

`magic -T sky130A.tech sky130_inv.mag &`


![](Images_Day_4/Capture1.JPG)

To show the grids in magic tool use `grid` command magic terminal as shown in below and for any kind of help run `grid help` command

`grid 0.46um 0.34um 0.23um 0.17um`

![](Images_Day_4/Capture4.JPG)


![](Images_Day_4/Capture5.png)

Now to save this run following command in magic terminal

`save <file_name>`

Here, file_name = sky130_vsdinv.mag


![](Images_Day_4/Capture7.JPG)

This creates new file (i.e., sky130_vsdinv.mag) in `/Desktop/work/tools/openlane_working_dir/openLANE_flow/vsdstdcelldesign` directory


![](Images_Day_4/Capture8.JPG)

Now, open this new created layout file (i.e., sky130_vsdinv.mag) using magic tool.


![](Images_Day_4/Capture9.JPG)

Magic tool allows for user to create their cell lef  file. For this run command `lef write` in magic terminal


![](Images_Day_4/Capture10.JPG)

Now go to `/Desktop/work/tools/openlane_working_dir/openLANE_flow/vsdstdcelldesign` directory where we see new lef file is created (i.e., sky130_vdsinv.lef).


![](Images_Day_4/Capture11.JPG)

### Include Standard Cell into OpenLANE

Use following command to copy `sky130_vsdinv.lef` file into `/home/sachinkumar/Desktop/work/tools/openlane_working_dir/openLANE_flow/designs/picorv32a/src` folder

`cp sky130_vsdinv.lef/home/sachinkumar/Desktop/work/tools/openlane_working_dir/openLANE_flow/designs/picorv32a/src `


![](Images_Day_4/Capture12.JPG)


![](Images_Day_4/Capture13.JPG)

Also, copy all .lib files to `/home/sachinkumar/Desktop/work/tools/openlane_working_dir/openLANE_flow/designs/picorv32a/src`


![](Images_Day_4/Capture14.JPG)


![](Images_Day_4/Capture15.JPG)

Now come to `/home/sachinkumar/Desktop/work/tools/openlane_working_dir/openLANE_flow/designs/picorv32a` directory and edit `config.tcl` file.

![](Images_Day_4/Capture16.JPG)

![](Images_Day_4/Capture17.JPG)

Next, we need to prepare the design again using openLANE. For this we use following command 

`prep -design <design_name> -tag <tag_name> -overwrite`

Here design name = picorv32a

Tag name = 25-01_12-58

And “-overwrite” is significant for overwrites the new changes made in `config.tcl` file

![](Images_Day_4/Capture18.png)

Once preparation is complete we run following commands to include the additional lef file in flow: -

`set lefs [glob $::env(DESIGN_DIR)/src/*.lef]`
  
`add_lefs -src $lefs`

Next, we need to run synthesis.


![](Images_Day_4/Capture19.JPG)


![](Images_Day_4/Capture20.JPG)

Here, we observed Hold time is positive that’s means there is no hold time violations. And setup slack time is negative. Hence, there is setup time violation.

And chip area is

![](Images_Day_4/Capture21.JPG)

So, to fix this we set SYNTH_STRATEGY variable to 1 which indicates that we want to prefer more faster response as compared to low area. And set SYNTH_SIZING to 1 that indicates OpenLANE to prefer sizing of cells as compared to including buffer.

Next, run synthesis and after synthesis we get reduced slack value as compared to previous one.

![](Images_Day_4/Capture22.JPG)

![](Images_Day_4/Capture23.JPG)

Also, chip area gets increased

![](Images_Day_4/Capture24.JPG)

Now, run floorplan and then run placement.

![](Images_Day_4/Capture25.JPG)

### Layout of Placed Standard Cell Using Magic Tool

To view the placement of standard cell run following command 

`magic -T /home/sachinkumar/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sly130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &`

![](Images_Day_4/Capture27.JPG)

Now, we open the design using magic tool 

On zoom in and run command `expand` in magic terminal to see layout of standard cell.

![](Images_Day_4/Capture28.png)

### Fixing slack violation

For this we need configuration file which state library location and some initial condition.

![](Images_Day_4/Capture29.JPG)

![](Images_Day_4/Capture30.JPG)

Also need constraints file (here, my_base.sdc) which is followed by whole VLSI industry . So, copy this file to `/home/sachinkumar/Desktop/work/tools/openlane_working_dir/openLANE_flow/designs/picorv32a/src`

![](Images_Day_4/Capture31.JPG)

![](Images_Day_4/Capture32.JPG)

Do some modification to my_base.sdc file

![](Images_Day_4/Capture33.png)

Now run command `sta pre_sta.conf`

![](Images_Day_4/Capture34.JPG)

Here we get reduced slack

![](Images_Day_4/Capture35.JPG)

For further reduction in slack value, we need to reduced fan out. To do this run following command

`set ::env(SYNTH_MAX_FANOUT) 4`

And run synthesis

![](Images_Day_4/Capture37.JPG)

### Upsizing the cell


For further improvement in the slack value, we need to upsize the cell. 

![](Images_Day_4/Capture38__.JPG)

To do this we replace the downsize cell with upsize cell. This is done using following command: -

` replace_cell _<net_number>_ <buffer_name>`

After this run following command to check the slack value

`report_checks -fields {net cap slew input_pins} -digits 4`

Now write this synthesis file after changes in buffer using following command.

`write_verilog /home/sachinkumar/designs/picorv32a/runs/ 25-01_12-58/results/synthesis/picorv32a.synthesis.v`

### Clock Tree Synthesis

Now, for clock tree synthesis run following command: - 

`run_cts`

![](Images_Day_4/Capture40.JPG)

![](Images_Day_4/Capture41.JPG)

After CTS complete look into `/Desktop/work/tools/openlane_working_dir/openLANE_flow/designs/picorv32a/runs/25-01_12-58/results/synthesis` directory where we see `picorv32a.synthesis.cts.v` is created 

![](Images_Day_4/Capture42.JPG)

### STA using OpenROAD

For timing analysis enter openROAD using command `openroad`

Here, we need to generate .db file which required lef and def files so run following command

For lef file use following command

`read_lef /openLANE_flow/designs/picorv32a/runs/25-01_12-58/tmp/merged.lef`

![](Images_Day_4/Capture47.JPG)

![](Images_Day_4/Capture48.JPG)

For def file use following command

`read_def /openLANE_flow/designs/picorv32a/runs/28-01_12-58/results/cts/picorv32a.cts.def`

![](Images_Day_4/Capture50.JPG)

![](Images_Day_4/Capture51_.JPG)

Now use following command for further timing analysis

`read_verilog /designs/picorv32a/runs/28-01_12-58/results/synthesis/picorv32a.synthesis_cts.v`

`read_liberty $::env(LIB_SYNTH_COMPLETE)`

`link_design picorv32a`

`read_sdc /designs/picorv32a/runs/28-01_12-58/src/my_base.sdc`

`set_propagated_clock [all_clocks]`

`report_checks -path_delay min_max -fields {slew trans net cap input_pin} -format full_clock_expanded -digits 4`


## Day 5 - Final steps for RTL2GDS using tritonRoute and openSTA

