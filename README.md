# NASSCOM_SoC_Design
>***2 Week digital VLSI SoC design and planning workshop with complete RTL2GDSII flow organised by VSD in collaboration with NASSCOM***

## Lab Session 1 : 'picorv32a' design synthesis using OpenLANE flow and calculate flop ratio.

OpenLANE is a completely automated RTL to GDSII flow that embeds open-source tools, namely, OpenROAD, Yosys, ABC, Magic, etc., apart from many custom methodology scripts for design exploration and optimization. Openlane is built around Skywater 130nm process node and can perform complete ASIC implementation steps from RTL down to GDSII.

### 'picorv32a' design synthesis using OpenLANE

![Screenshot (766)](https://github.com/user-attachments/assets/1256d4a0-2e27-455d-bad4-1a5bd55ba5b5)
![Screenshot (767)](https://github.com/user-attachments/assets/47845d3b-aa36-4a18-8d42-6685cf648d7b)
![Screenshot (768)](https://github.com/user-attachments/assets/f230417b-c1e1-42b3-8dee-237c9f005927)

### Calculate the flop ratio

Calculation of Flop Ratio and DFF % from synthesis statistics report file

The flop ratio is given as,

$$Flop\ Ratio = {\frac{Number\ of\ D\ Flip\ Flops}{Total\ Number\ of\ Cells}}$$

>Number of D Flip Flops
>![Screenshot (769)](https://github.com/user-attachments/assets/e71f3bd8-0c43-4a47-bb8f-523c6c55a60d)

>Total Number of Cells
>![Screenshot (770)](https://github.com/user-attachments/assets/cb184049-7e4c-40e8-a401-c960b8e1eb49)

>Calculation
>![Screenshot (771)](https://github.com/user-attachments/assets/8a000b00-f7df-4572-bb17-99e68e1e24ac)

$$Flop\ Ratio = \frac{1613}{14876} =0.1084 $$

$$Percentage\ of \ DFFs = 0.1084 \times 100 = 10.84%$$

## Lab Session 2: Good floorplan vs bad floorplan and introduction to library cells 

### objective
- Run 'picorv32a' design floorplan using OpenLANE flow and generate design output file.
- Calculate the die area in microns from the values in floorplan.def.
- Load generated floorplan.def in magic tool and explore the floorplan.
- Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
- Load generated placement def in magic tool and explore the placement.

  The die area is a quantity property representing the total area of an integrated circuit die. This value is given by

  $$Die\ Area\ (in\ micron)=Die\ Width\ (in\ micron)\ *\ Die\ Height\ (in\ micron)$$
1. Run 'picorv32a' design floorplan using OpenLANE flow and generate design output file.

Commands to invoke the OpenLANE flow and perform floorplan

```
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
  ```
```
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Now we can run floorplan
run_floorplan
```

Screenshot of floorplan run

![Screenshot (776)](https://github.com/user-attachments/assets/2148af66-0088-4cd8-a15c-8e0d0722dcce)

2. Calculate the die area in microns from the values in floorplan def.
   
Screenshot of contents of floorplan.def

![Screenshot (777)](https://github.com/user-attachments/assets/e1551b5a-5cd6-47ab-bfd0-727c6e505ba6)

According to floorplan def

$$ 1000\ unit\ distance=1 \mu m $$

$$ Die\ width\ in\ unit\ distance\ =\ 600685-0=660685 $$

$$ Die\ height\ in\ unit\ distance=671405-0=671405 $$

$$ Distance\ (in\ microns\) =\ \frac{value\ in\ unit\ distance}{1000} $$

```
# Change directory to path containing generated floorplan def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/31-08_20-57/results/floorplan/

# Command to load the floorplan def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &

```
Screenshots of floorplan.def in magic:

![Screenshot (780)](https://github.com/user-attachments/assets/ae5070a0-a28c-4f8f-9912-f19e6bc52986)

![Screenshot (826)](https://github.com/user-attachments/assets/ffd74d51-29a1-41cf-b55c-8ac380141160)

4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
   Command to run placement
   ```
    # Congestion aware placement by default
    run_placement
    ```
Screenshots of placement run

![Screenshot (832)](https://github.com/user-attachments/assets/f9d5ef5e-df72-4271-9f3b-ce8724036b91)
![Screenshot (833)](https://github.com/user-attachments/assets/a5ded406-f949-4064-9027-6bf40ee82283)

5. Load generated placement def in magic tool and explore the placement.
   
   Commands to load placement def in magic in another terminal

   ```
   # Change directory to path containing generated placement def
   cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/31-08_20-57/results/placement/

   # Command to load the placement def in magic tool
   magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &

   ```
![Screenshot (836)](https://github.com/user-attachments/assets/22c2406d-0998-49e5-bdb5-9406901214a3)
![Screenshot (837)](https://github.com/user-attachments/assets/f850b7ed-2032-41dd-b55a-041233240235)
![Screenshot (838)](https://github.com/user-attachments/assets/31090970-d5df-45f4-b246-f82d5d7d56df)

   
```
# Exit from OpenLANE flow
exit

# Exit from OpenLANE flow docker sub-system
exit
```
## Lab Session 3 : Design library cell using Magic Layout and Ngspice characterization

### Objectives
Clone custom inverter standard cell design from github repository: Standard cell design and characterization using OpenLANE flow.
Load the custom inverter layout in magic and explore.
Spice extraction of inverter in magic.
Editing the spice model file for analysis through simulation.
Post-layout ngspice simulations.
Find problem in the DRC section of the old magic tech file for the skywater process and fix them.

1. Clone custom inverter standard cell design from github repository
```
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Clone the repository with custom inverter design
git clone https://github.com/nickson-jose/vsdstdcelldesign

# Change into the repository directory
cd vsdstdcelldesign

# Copy magic tech file to the repo directory for easy access
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech 

# Check contents to see whether everything is present
ls

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &

```
Screenshot of commands run

![Screenshot (839)](https://github.com/user-attachments/assets/d02dce99-f4fd-4294-b6eb-a28baa10eda1)

2. Load the custom inverter layout in magic and explore

Screenshot of custom inverter layout in magic

![Screenshot (880)](https://github.com/user-attachments/assets/abf5cf6c-52f7-4369-9e8d-a155fc6e57b2)

NMOS and PMOS identified

![Screenshot (843)](https://github.com/user-attachments/assets/74b561cd-a615-4420-9daa-c6cf1737519d)
![Screenshot (844)](https://github.com/user-attachments/assets/7115db06-185e-4442-8bfb-bf021a3710a2)

Output Y connectivity to PMOS and NMOS drain verified

![Screenshot (841)](https://github.com/user-attachments/assets/e5b14f85-8399-46a8-816b-4cb3845a7596)

PMOS source connectivity to VDD (here VPWR) verified

![Screenshot (845)](https://github.com/user-attachments/assets/cc71ba80-e9b1-48a4-b407-7924e94e6490)

NMOS source connectivity to VSS (here VGND) verified

![Screenshot (847)](https://github.com/user-attachments/assets/b47b2ec8-c08c-4978-bb05-2c8b29acbf8d)

3. Spice extraction of inverter in magic.

Commands for spice extraction of the custom inverter layout to be used in tkcon window of magic

```
# Check the current directory
pwd

# Extraction command to extract to .ext format
extract all

# Before converting ext to spice, this command also enables the parasitic extraction
ext2spice cthresh 0 rthresh 0

# Converting to ext to spice
ext2spice
```
Screenshot of tkcon window after running above commands

![Screenshot (849)](https://github.com/user-attachments/assets/a5827d26-7060-4085-9bce-c9fa9960a9aa)

Final edited spice file ready for ngspice simulation

![Screenshot (861)](https://github.com/user-attachments/assets/b63374a7-2322-47a2-bf89-93c621a2ec6b)

5. Post-layout ngspice simulations. 
Commands for Ngspice simulation

```
# Command to directly load spice file for simulation to ngspice
ngspice sky130_inv.spice

# Now that we have entered ngspice with the simulation spice file loaded we just have to load the plot
plot y vs time a
```

Screenshots of Ngspice run

![Screenshot (860)](https://github.com/user-attachments/assets/e7cc4a50-1422-4c06-8760-e645ecfdde04)

Screenshot of generated plot

![Screenshot (862)](https://github.com/user-attachments/assets/ca4645e2-2714-4f01-ab93-fc35f1998c06)

**A.** Rise transition time calculation.

$` Rise\ time\ transition\ = Time\ taken\ for\ output\ to\ rise\ 80 \%-Time\ taken\ for\ output\ to\ rise\ 20 \% `$

$` 80 \%\ of\ 3.3\ V = 2.64 V `$

$` 20 \%\ of\ 3.3\ V = 660 mV `$

80% Screenshots
![Screenshot (865)](https://github.com/user-attachments/assets/e5c68bca-fc4a-4345-9bf6-8b4f8332f9c1)

20% Screenshot
![Screenshot (864)](https://github.com/user-attachments/assets/3e569367-645b-4ca8-911e-05142d85ce72)

Fall transition time calculation
![Screenshot (866)](https://github.com/user-attachments/assets/5b609eee-6aee-4204-b389-1d811947a473)
**Rise transition time is 63.75ps.**

**B.** Fall transition time calculation.

$` Fall\ time\ transition\ = Time\ taken\ for\ output\ to\ fall\ 20 \%-Time\ taken\ for\ output\ to\ fall\ 80 \% `$

$` 80 \%\ of\ 3.3\ V = 2.64 V `$

$` 20 \%\ of\ 3.3\ V = 660 mV `$


20% Screenshot
![Screenshot (872)](https://github.com/user-attachments/assets/ba71359e-cab3-4feb-8178-d94987af0c37)

Fall transition time calculation
![Screenshot (873)](https://github.com/user-attachments/assets/13bad28f-c386-4495-883b-2707ed59ad9a)
**Fall transition time is 42.47ps.**

**C.** Rise Cell Delay Calculation.

$` Rise\ cell \ Delay\ = Time\ taken\ for\ output\ to\ reach\ 50 \%-Time\ taken\ for\ input\ to\ fall\ 50 \% `$

$` 50 \%\ of\ 3.3\ V = 1.65 V `$


50% Screenshot
![Screenshot (874)](https://github.com/user-attachments/assets/c184fcf6-81f3-482e-80e8-be46678187d9)

Rise Cell Delay calculation
![Screenshot (875)](https://github.com/user-attachments/assets/8b60e90b-e555-4843-8249-9fa42f1a7bed)
**Rise Cell Delay is 27.48ps.**

## LAB SESSION 4 : Pre-layout timing analysis and importance of good clock tree
### Objectives

1. Fix up minor DRC errors and verify the design is ready to be inserted into our flow.
2. Save the finalized layout with a custom name and open it.
3. Generate lef from the layout.
4. Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.
5. Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.
6. Run openlane flow synthesis with newly inserted custom inverter cell.
7. Remove/reduce the newly introduced violations by introducing custom inverter cell by modifying design parameters.
8. Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.
9. Do Post-Synthesis timing analysis with OpenSTA tool.
10. Make timing ECO fixes to remove all violations.
11. Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.
12. Post-CTS OpenROAD timing analysis.
13. Explore post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'.
    
1. **Fix up a minor DRC error and verify the design is ready to be inserted into our flow.**
Conditions to be verified before moving forward with custom-designed cell layout:

- Condition 1: The input and output ports of the standard cell should lie on the intersection of the vertical and horizontal tracks.
- Condition 2: Width of the standard cell should be odd multiples of the horizontal track pitch.
- Condition 3: Height of the standard cell should be even multiples of the vertical track pitch.


Commands to open the custom inverter layout

```
# Change directory to vsdstdcelldesign
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &
```
Screenshot of tracks.info of sky130_fd_sc_hd
![Screenshot (876)](https://github.com/user-attachments/assets/db5caba2-a240-49ae-bed1-6f1fe14ad865)

Commands for tkcon window to set grid as tracks of locali layer

```
# Get syntax for grid command
help grid

# Set grid values accordingly
grid 0.46um 0.34um 0.23um 0.17um
```
Screenshot of commands run
![Screenshot (881)](https://github.com/user-attachments/assets/e3f74ab6-54fb-41a7-b827-fb8bcf8243e2)
Condition 1 verified
![Screenshot (879)](https://github.com/user-attachments/assets/fa306d91-edbe-48d7-8cb5-4fcb45c3bc26)
Condition 2 verified

$$ Horizontal\ Track\ Pitch = 0.46 \mu m $$

$$ Width\ of\ the\ Standard\ Cell = 1.38 \mu m = 0.46*3 $$

Condition 3 verified

$$ Vertical\ Track\ Pitch = 0.34 \mu m $$
$$ Heigth\ of\ the\ Standard\ Cell = 2.72 \mu m = 0.34*8 $$

2. **Save the finalized layout with custom name and open it.**

Command for tkcon window to save the layout with custom name
```
# Command to save as
save sky130_vsdinv.mag
```
Command to open the newly saved layout
```
# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_vsdinv.mag &
```
Screenshot of newly saved layout
![Screenshot (880)](https://github.com/user-attachments/assets/605a14ad-bdcb-4a77-972a-28328c931b65)

3. Generate lef from the layout.

Command for tkcon window to write lef
```
# lef command
lef write
```
Screenshot of command run
![Screenshot (882)](https://github.com/user-attachments/assets/4ae36a90-54c6-4fab-bbad-b08a4bcca624)

Screenshot of newly created lef file
![Screenshot (883)](https://github.com/user-attachments/assets/406472f5-ff2d-47ae-83c5-aaec511f7f59)

4. Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.
Commands to copy necessary files to 'picorv32a' design 'src' directory
```
# Copy lef file
cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# Copy lib files
cp libs/sky130_fd_sc_hd__* ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```
Screenshot of checking of commands run

![Screenshot (884)](https://github.com/user-attachments/assets/a581b2be-4dff-43f3-afa1-748b4d39c1b3)

5. Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.
Commands to be added to config.tcl to include our custom cell in the openlane flow
```
set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]
```
Edited config.tcl to include the added lef and change library to ones we added in src directory
![Screenshot (885)](https://github.com/user-attachments/assets/1ad0b1fd-c19c-4ac0-b748-e926bce35ce2)

6. Run openlane flow synthesis with newly inserted custom inverter cell.
Commands to invoke the OpenLANE flow include new lef and perform synthesis
```
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```
```
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```
Screenshots of commands run
![Screenshot (886)](https://github.com/user-attachments/assets/2a0f0ef7-1a9e-45c3-9d37-922741aaabd5)
![Screenshot (887)](https://github.com/user-attachments/assets/38018901-0bc7-4cef-9b3d-e64d56519095)
![Screenshot (889)](https://github.com/user-attachments/assets/64446e62-28a8-4508-81ed-67ac8e26e768)

7. Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.
Noting down current design values generated before modifying parameters to improve timing

![Screenshot (888)](https://github.com/user-attachments/assets/44ac9c8b-910e-460a-884e-596d78124a56)
![Screenshot (889)](https://github.com/user-attachments/assets/64446e62-28a8-4508-81ed-67ac8e26e768)

Commands to view and change parameters to improve timing and run synthesis

```
# Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 31-08_20-57 -overwrite

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to display current value of variable SYNTH_STRATEGY
echo $::env(SYNTH_STRATEGY)

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to display current value of variable SYNTH_BUFFERING to check whether it's enabled
echo $::env(SYNTH_BUFFERING)

# Command to display current value of variable SYNTH_SIZING
echo $::env(SYNTH_SIZING)

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```
Screenshot of command run and merged.lef in tmp directory with our custom inverter as macro

![Screenshot (890)](https://github.com/user-attachments/assets/0a74494d-681d-4058-9314-b25675b77666)
![Screenshot (892)](https://github.com/user-attachments/assets/a95cd642-5c08-487e-a7b1-334bf33c360b)
![Screenshot (893)](https://github.com/user-attachments/assets/e5c80a90-1ad2-454a-9e14-d7bdb1f12d74)
![Screenshot (901)](https://github.com/user-attachments/assets/6bd4e8d1-891f-4104-9653-fdc8978cc1f8)

Comparing to previously noted run values area has increased and worst negative slack has become 0

8. Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.
Now that our custom inverter is properly accepted in synthesis we can now run floorplan using following command
```
# Now we can run floorplan
run_floorplan
```
Since we are facing unexpected un-explainable error while using run_floorplan command, we can instead use the following set of commands available based on information from ```Desktop/work/tools/openlane_working_dir/openlane/scripts/tcl_commands/floorplan.tcl``` and also based on Floorplan Commands section in ```Desktop/work/tools/openlane_working_dir/openlane/docs/source/OpenLANE_commands.md```

```
# Follwing commands are alltogather sourced in "run_floorplan" command
init_floorplan
place_io
tap_decap_or
```
Screenshots of commands run ```run_floorplan```
![Screenshot (894)](https://github.com/user-attachments/assets/2edb872f-abb8-468d-b49b-5f5093c35891)
```error in run_floorplan and modified run ```starting from ```int_floorplan```
![Screenshot (895)](https://github.com/user-attachments/assets/0ea6281b-5137-4e52-ab6d-7fd4f2b2a6cb)
![Screenshot (896)](https://github.com/user-attachments/assets/6bda57b8-d03b-49eb-9010-ca4d91644059)

Now that floorplan is done we can do placement using following command
```
# Now we are ready to run placement
run_placement
```

Screenshots of command run
![Screenshot (904)](https://github.com/user-attachments/assets/75803462-2a44-4040-9a1c-a9f2a54447b9)
![Screenshot (905)](https://github.com/user-attachments/assets/e2a2dcc5-80a4-407f-a661-5f645fcb1e88)

Commands to load placement def in magic in another terminal
```
# Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/31-08_20-57/results/placement/

# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
Screenshot of placement def in magic
![Screenshot (907)](https://github.com/user-attachments/assets/6690d83b-bc6d-4076-9cf7-2b8cb4f75433)

Screenshot of custom inverter inserted in placement def with proper abutment
![Screenshot (908)](https://github.com/user-attachments/assets/4bebb66d-fdba-4c06-a7e0-1ef8e50c9587)

Command for tkcon window to view internal layers of cells
```
# Command to view internal connectivity layers
expand
```
Abutment of power pins with other cell from library clearly visible
![Screenshot (911)](https://github.com/user-attachments/assets/f8674295-2128-4fc3-984e-3ba5a65c0d67)

9. Do Post-Synthesis timing analysis with OpenSTA tool.
Since we are having 0 wns after improved timing run we are going to do timing analysis on initial run of synthesis which has lots of violations and no parameters were added to improve timing

Commands to invoke the OpenLANE flow include new lef and perform synthesis
```
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```
```
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```
Commands run final screenshot
![Screenshot (917)](https://github.com/user-attachments/assets/15ba48d9-7d16-46a4-98d3-953d555f4812)

Newly created ```pre_sta.conf``` for STA analysis in ```openlane``` directory
![Screenshot (923)](https://github.com/user-attachments/assets/539fbe60-c6f6-4000-b22a-ddad8c766e41)

Newly created ```my_base.sdc``` for STA analysis in ```openlane/designs/picorv32a/src``` directory based on the file ```openlane/scripts/base.sdc```
![Screenshot (924)](https://github.com/user-attachments/assets/1f091975-d4be-482c-bcc4-52661f255940)

Commands to run STA in another terminal
```
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Command to invoke OpenSTA tool with script
sta pre_sta.conf
```
Screenshots of commands 



