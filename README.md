# NASSCOM_SoC_Design
>***2 Week digital VLSI SoC design and planning workshop with complete RTL2GDSII flow organised by VSD in collaboration with NASSCOM***

## Lab Session DAY 1 - 'picorv32a' design synthesis using OpenLANE flow and calculate flop ratio.

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

## Good floorplan vs bad floorplan and introduction to library cells 

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

   
