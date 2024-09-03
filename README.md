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

