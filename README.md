# DAY 1 Introduction to SoC Design Flow and Running Synthesis

## OPENLANE Flow

OpenLane is an open-source digital ASIC (Application-Specific Integrated Circuit) design flow that integrates a comprehensive set of tools for designing and implementing digital circuits. It is part of the broader effort to make VLSI (Very-Large-Scale Integration) design accessible and affordable by leveraging open-source tools and methodologies.

![Screenshot (655)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/eabb22a1-52e8-4f2a-848d-f7ce64558cd8)


**DESIGN PREPARATION**

- Open the OPENLANE Docker by using the command ``` docker ``` from the directory of 'openlane' inside 'openlane_working_dir' directory.

- Then run the opelane in interactive mode using ```./flow.tcl -interactive``` and  run the command ```prep -design picorv32a```  to merge the lef file.

![Screenshot from 2024-05-20 18-48-50](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/a95cee91-20e8-4517-9a05-2639797894b7)

- After Design Preparation run the Synthesis command ```run_synthesis```

![Screenshot from 2024-05-27 22-51-13](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/e9882dc7-3f1f-495e-99da-8a454fb3fb10)

Synthesis is Successful

![Screenshot from 2024-05-27 22-56-26](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/dfd9939f-9dd1-463f-bc46-8732a208be3c)

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

![Screenshot from 2024-05-27 22-59-29](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/f159ac1a-dbae-4509-b9c6-ec7c0682dba0)



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

![Screenshot from 2024-05-27 12-45-29](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/56d89dac-3fee-4ab5-8aea-a9052706247a)


## Placement
To run the placement type the command ```run_placement```

![Screenshot from 2024-05-27 23-17-41](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/a754fa15-d746-49c4-b0ee-c43d95a17792)

We perform the global placement first which is used to achieve less wire length.

To Open the layout after placement type the command ```magic -T home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def & ```

Below is the image of the **layout after runnig placement**

![Screenshot from 2024-05-27 12-45-46](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/d8dba3c5-baf0-4828-92ff-b54fcff8e0f8)


# Day 3 Design of Inverter cell using and transient chara of the designed cell using spice
We can see that the IO is placed diagonally equividistant in the floorplan.

![Screenshot (596)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/632084de-8f9d-4985-8499-60310e0031a2)

 This is can be changed in the command present in config.tcl
 
![Screenshot (595)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/f6314307-9a2e-4ff1-aac8-18e837204948)

In the next step we clone the inverter cell from the Github repository. 

To Clone, run the following command in working directory: ```git clone https://github.com/nickson-jose/vsdstdcelldesign.git```

![Screenshot from 2024-05-27 23-17-57](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/0e7a0730-840e-4017-a43c-8f880a971132)


To open the layout in Magic tool, Use the command ```magic -T {absolute_path_of_the_tech_file_of_the_cell} {absolute_path_of_the_mag_file_of_the_cell}```

The inverter std_cell which was cloned is opened as shown in the figure

![Screenshot from 2024-05-27 13-32-25](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/dcc91f42-7a5a-4741-805d-9ecca51ffd0c)

Characteristics of PMOS and NMOS of the inverter

![Screenshot (600)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/d930aa2a-52ba-4ebf-be91-0a9f0b4ddeb8)

- Next, create the extraction of inverter by executing the following command in console: ```extract all```
 
- To Create the spice file run the command ```ext2spice cthresh 0 rthresh 0``` follwed by ```ext2spice``` in console

The files are generated as shown in the figure

![Screenshot from 2024-05-27 23-22-37](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/3843085b-19f1-4e59-b284-895d41c6122a)

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

![Screenshot from 2024-05-27 23-30-26](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/b7646031-3dc1-49ee-ba5a-6584f86625c3)

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




# Day 4 - Prelayout design and Clock Tree Synthesis


**Primary Requirement for P&R:**

The I/O ports must be positioned at the junctions where the vertical and horizontal tracks intersect. The standard cell's width should be an odd multiple of the track's horizontal pitch. Additionally, the standard cell's height must be an odd multiple of the track's vertical pitch.

Coverting to grid info by using command ```grid [xSpacing [ySpacing [xOrigin yOrigin]]]``` 
i.e, ```grid 0.46um 0.34um 0.23um 0.17um```

![Screenshot (635)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/f22e92f6-a189-41d3-ad7d-48b66a93d981)

![Screenshot (636)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/0999ef79-fe53-4b37-aeaa-ca69116fdc59)

The new file is generated to edit the changes, the contents of new file is as follows

![Screenshot (638)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/3a2cbe13-10d4-4528-b617-40829ecdc825)

Make the following changes to the ```config.tcl``` file after copying ```.lib``` and ```.lef``` files to ```src``` of the picorv32a

![Screenshot (639)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/78cdee82-80c9-4310-9f48-f75ed0b75562)

Run the flow from the beginning and then run the following command

```set lefs  $::env(DESIGN_DIR)/src/*.lef```
```add_lefs -src $lefs```

Then run the command ```run_synthesis``` to check the new inverter is added to the picorv32a

![Screenshot (640)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/162c2670-78c7-4c7e-845c-4e705b44b28f)

But the slack is not yet met. We can do the follwoing changes to remove the slack

![Screenshot (643)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/5355240b-1388-45ba-b897-b31ec588ee4b)

The slack is removed

![Screenshot (644)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/774113c7-e7f6-4cec-b67c-09d829370b2c)


Then run the following commands to run floorplan
- ```init_floorplan```
- ```place_io```
- ```tap_decap_or```

Run ```run_placement```

Using the magic layout, we can view the placement layout and our custom cells

![Screenshot (645)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/ff8f30ed-7672-448f-9d87-b90940c47c99)

![Screenshot (646)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/d36486d8-9239-4262-9a8c-185510f7da23)

## Post Timing Analysis using OpenSTA

Create ```pre_sta.conf``` file and ```my_base.sdc``` file using the following commands

![Screenshot (647)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/cca4b83d-9afb-419d-99c0-60c94cd2a713)

Make the following changes

![Screenshot (648)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/0c4c0b52-3c3a-4bb4-81fd-a41dc7fe7f79)

Now run STA ```sta pre_sta.con```

![Screenshot (649)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/bce36d3a-664d-4af4-9109-b712b99b6db5)

Then use the command ```write_verilog``` to save the design into a file, which overwrites the current synthesis file. Placement is then carried out using the generated netlist.

![Screenshot (650)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/c7994b61-5c19-4769-85ab-aa6a105343eb)

- Use the command ```run_cts``` to run clock tree synthesis

-  ```_cts.v``` file will be generated as the result of synthesis.

![Screenshot (651)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/92910214-3b38-4892-8458-a981400bc4ca)

Use the following commands to analyse timing using real clocks

```read_lef /openLANE_flow/designs/picorv32a/runs/27-05_14-16/tmp/merged.lef```

```read_def /openLANE_flow/designs/picorv32a/runs/27-05_14-16/results/cts/picorv32a.cts.def```

```write_db pico_cts.db```

```read_db pico_cts.db```

```read_verilog /openLANE_flow/designs/picorv32a/runs/27-05_14-16/results/synthesis/picorv32a.synthesis_cts.v```

```read_liberty $::env(LIB_SYNTH_COMPLETE)```

```read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc```

```set_propagated_clock [all_clocks]```

```report_checks -path_delay min_max -format full_clock_expanded -digits 4```

![Screenshot (652)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/fe4c0370-935f-46e5-8d40-3d94d6308ded)


# Day 5

**Building Power Distribution Network**

A Power Distribution Network (PDN) in a System on Chip (SoC) ensures efficient and reliable delivery of power across the chip. It includes components like power pads, bumps, power rings, and a mesh of horizontal and vertical metal lines, along with decoupling capacitors and voltage regulators. Key design considerations involve managing IR drop, electromigration, dynamic and static power consumption, and ground bounce. The PDN design process involves defining power requirements, performing simulations to analyze power integrity issues, optimizing the network for performance and reliability, and validating the final design through post-layout simulations and testing to ensure robust operation.

![Screenshot (654)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/6fddc8d8-04d1-43f3-9b3d-303b3db79ba4)

Using the command ```gen_pdn``` build power distribution network

![Screenshot (634)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/37f2472d-0593-48be-a7e9-da7e94e98e83)

## Routing
**Triton Routing**

![Screenshot (631)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/d1ddc942-4eb0-4e97-81bf-6faa799f01de)

![Screenshot (630)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/8ee6f231-dfa2-4c2c-8ffa-96a670e24f02)

![Screenshot (629)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/3c548b3c-f43d-4333-9acc-56f3197b92d8)

![Screenshot (628)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/3da808ff-8f36-4f6d-b863-a7dce9211c92)


TritonRouting algorithm is used for rounting.

To execute the automated rounting, we run the command ```run_routing```

![Screenshot (624)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/6f408b5b-5ed6-4b4e-8404-80caf2c28abb)

![Screenshot (633)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/a4bc924e-71c9-41af-a99f-27424d985d8b)

Routed Layout

![Screenshot (632)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/ab2672ed-d92a-4c35-96b0-472d40d2e36d)

After zooming in

![Screenshot (627)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/e57127a6-6273-4607-8b94-f6f5d16ca53e)

Final image of the layout

![Screenshot (626)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/6e20d4bc-27c9-456c-af41-89015928bcee)




# Refrences
GitHub repo for vsd standard cell design : https://github.com/nickson-jose/vsdstdcelldesign

Github repo for google skywater-pdk : https://github.com/google/skywater-pdk

Link for the skywater-pdk docs : https://skywater-pdk--136.org.readthedocs.build/en/136/

# Acknowledgements
Kunal Ghosh, Co-founder (VSD Corp. Pvt. Ltd)

Nickson P Jose, Teaching Assistant (VSD Corp. Pvt. Ltd)
