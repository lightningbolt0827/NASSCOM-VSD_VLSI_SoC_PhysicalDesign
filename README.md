# DAY 1 Introduction to SoC Design Flow and Running Synthesis
## INTRO to SOC


## OPENLANE

**DESIGN PREPARATION**

- Open the OPENLANE Docker by using the command ``` docker ``` from the directory of 'openlane' inside 'openlane_working_dir' directory.

- Then run the opelane in interactive mode using ```./flow.tcl -interactive``` and  run the command ```prep -design picorv32a```  to merge the lef file.

![Screenshot from 2024-05-20 18-48-50](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/a95cee91-20e8-4517-9a05-2639797894b7)

- After Design Preparation run the Synthesis command ```run_synthesis```

![Screenshot from 2024-05-20 19-38-27](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/4e8dd6ee-62b7-4fec-8a5a-0dd9ceafcfe1)
Synthesis is Successful

![1](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/67c5e191-8f42-49e4-8944-5d67baf04089)

Chip area after running the Synthesis

![2](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/4d1e407a-0c87-46c6-b717-983eef61e287)

Finding the flop ratio

Flop Ratio = Number of flops / Number of cells = 1613/14876 = 0.108 = 10.8%

![Screenshot (584)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/67619e6a-7aa5-4a6d-87b4-70fa9a2a6f4b)

# DAY 2 Floorplan and Placement
## Floorplan
There are various floorplan configurations that can be modified based on the requirement
![Screenshot from 2024-05-20 20-25-00](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/c6455acc-9baa-4ffb-b0db-ab3a1768478e)


Run the floorplan using ```run_floorplan```
![Screenshot (585)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/5dccfb9b-8ada-4e4f-a249-f656939122c8)

The output logs files which are generated after floorplan:-
![Screenshot (586)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/0150027e-06f7-4c50-a480-341ed9e30350)

The Configurations of floorplan:-

![Screenshot (588)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/7d1d78d2-d05f-42a7-ba58-b74b8f898197)

### MAGIC Tool

The Magic tool is an open-source layout editor used for VLSI design. It provides a graphical interface for viewing and editing IC layouts, allowing designers to inspect and modify the floorplan, placement, and routing of their designs. Magic is widely used for its ease of use and integration with other tools in the ASIC design flow.

To open the magic window use the command

```magic -T home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def & ```

- To select entire layout click on ```s``` and then click on ``` v ``` to make it centre.

![Screenshot (589)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/aead14f9-489a-4e8e-926f-371cc215dd2c)

The cells in the layout can be identified by selecting the cell and typing the command ```what``` in the console

![Screenshot (591)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/ddb71550-40af-477a-8aaf-7ccac8ce8ac9)

As shown in the floorplan, all the macros, IPs, and ports are placed in their designated locations. However, the standard cells have not been placed yet and are currently located at the origin.

![Screenshot (594)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/0da32900-3613-4ced-aef1-39386229ccf7)


## Placement
To run the placement type the command ```run_placement```

We perform the global placement first which is used to achieve less wire length.

To Open the layout after placement type the command ```magic -T home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def & ```

Below is the image of the **layout after runnig placement**

![Screenshot (592)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/406273b4-ff32-43f4-a83f-b03319ec9212)


# Day 3 Design of Inverter cell using and transient chara of the designed cell using spice
We can see that the IO is placed diagonally equividistant in the floorplan.

![Screenshot (596)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/632084de-8f9d-4985-8499-60310e0031a2)

 This is can be changed in the command present in config.tcl
 
![Screenshot (595)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/f6314307-9a2e-4ff1-aac8-18e837204948)

In the next step we clone the inverter cell from the Github repository. 

To Clone, run the following command in working directory: ```git clone https://github.com/nickson-jose/vsdstdcelldesign.git```

![Screenshot (597)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/4300d960-4494-4e29-be27-83fa4981b9a8)

To open the layout in Magic tool, Use the command ```magic -T {absolute_path_of_the_tech_file_of_the_cell} {absolute_path_of_the_mag_file_of_the_cell}```

The inverter std_cell which was cloned is opened as shown in the figure

![Screenshot (599)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/ec624432-c5cd-460b-a8bb-aa915f0b64bd)

Characteristics of PMOS and NMOS of the inverter

![Screenshot (600)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/d930aa2a-52ba-4ebf-be91-0a9f0b4ddeb8)

- Next, create the extraction of inverter by executing the following command in console: ```extract all```
 
- To Create the spice file run the command ```ext2spice cthresh 0 rthresh 0``` follwed by ```ext2spice``` in console

The files are generated as shown in the figure

![Screenshot (601)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/056f69d3-9dcb-4463-bc9f-f45987fa4ca0)

The following modifications are made in the spice file

![Screenshot (602)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/b692b295-9fee-44e9-bb6a-d2849afe50de)

To run the spice simulation, execute the command ```ngspice sky130_inv.spice```

![Screenshot (603)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/142fc573-2258-4211-87ae-39b07c07ab14)

Next run the command ```plot y vs time a```

![Screenshot (604)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/0acb24cd-5702-4be1-89b2-e48ed83d3a9e)

**Calculation of Rise time and Fall time Delay**

Rise time is defined as the duration it takes for a signal to transition from 20% to 80% of its final value. The rise time can be calculated as [2.19 - 2.13[ x 10^-9 = 62.7 ps.

Zoom in to get the value of signal at 20% and 80% of VDD.

![Screenshot (605)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/cb62a7b5-6c9c-4fb1-844e-382a79772ecb)

The following values can also be obtained by the below method

![Screenshot (606)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/b81ade40-7cbd-40c1-a260-d0118f3efafe)

Fall time is the duration it takes for a signal to transition from 80% to 20% of its final value. The fall time is calculated as [4.09 - 4.053] x 10^-9 = 41.97 ps.

The Values can be calculated as:
![Screenshot (607)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/fec8a6ac-f382-4099-88ed-5f628d80fdae)

**Calculation of Propagation Delay**

Propagation delay is the time it takes for a signal to travel from the input to the output of a circuit. For instance, the propagation delay can be calculated as  [2.15 - 2.10] x10^-9 = 48.9ps

The Screen shot of Propagation Delay

![Screenshot (608)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/d043d674-a230-4875-89f3-760763b5441c)

## DRC correction and rules

To perform DRC correction, we have to execute the command ```wget http://opencircuitdesign.comopen_pdks/archive/drc_tests.tgz```

![Screenshot (609)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/f9a41636-d13e-4f74-a709-3765c5659109)

By Using command ```magic -d XR open the magic tool``` Open the met3.mag file

![Screenshot (610)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/77e4693f-fb3c-4ecf-bd60-30c9ff8d9f2c)

To find the DRC Error, select the part containing the error and type the command ```why``` in the console

![Screenshot (612)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/2fff6b4d-6ed2-4b7c-af31-b0b188dbeacc)

To see contact cuts execute the command ```cif see VIA2``` in the console 

![Screenshot (613)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/748496c9-2dc1-4ae0-9fae-2a879e38e67d)

There are many DRC errors found, to fix one of the error i.e, error poly.9 follow the follwing steps

- ```nwell.mag``` is loaded

- Find out why is the error occuring

![Screenshot (614)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/7f4e7d46-300b-4d76-afd0-4b5ad27068a2)

![Screenshot (615)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/c44a84fc-d1f8-48c0-8aaf-f3393fb5b7e7)

![Screenshot (618)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/43d46368-2c33-4353-95ea-77d7a765d2f3)

- As we can see, the spacing is 220µm, which does not meet the minimum size requirements.

- Fixing the Error

To fix this DRC error we make some changes in the sky130A.tech file

![Screenshot (616)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/225f73df-997f-4f3f-bf84-a543d01e5aae)

- After the changes, load the sky130A.tech file perform the DRC to check the poly.9 error

![Screenshot (621)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/bd5f6b54-6208-408b-9dcf-97d42d6b14c2)

### Now we perforam an activity to show a DRC error as a geometric construct:

Open ```nwell.mag``` and execute the following commands in the console

![Screenshot (619)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/26dafecb-9a7f-4313-972e-189f4b7d58cc)

To remove the error, open the tech file and make thefollwing changes:

![Screenshot (620)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/e57d8fe9-319b-4ed8-a6da-d487a85229e7)

After removing the error

![Screenshot (623)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/68772f26-fe72-443b-b204-ad36f2702388)


# Refrences
GitHub repo for vsd standard cell design : https://github.com/nickson-jose/vsdstdcelldesign

Github repo for google skywater-pdk : https://github.com/google/skywater-pdk

Link for the skywater-pdk docs : https://skywater-pdk--136.org.readthedocs.build/en/136/

# Acknowledgements
Kunal Ghosh, Co-founder (VSD Corp. Pvt. Ltd)

Nickson P Jose, Teaching Assistant (VSD Corp. Pvt. Ltd)
