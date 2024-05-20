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

Layout when Zoomed in

![Screenshot (593)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/2663731e-4580-4bf3-aba0-ec0c539fd826)

We can see that the IO is placed diagonally equividistant in the floorplan. This is can be changed in the command present in config.tcl

![Screenshot (595)](https://github.com/lightningbolt0827/NASSCOM-VSD_VLSI_SoC_PhysicalDesign/assets/109969895/f6314307-9a2e-4ff1-aac8-18e837204948)

# Day 3 Design of Inverter cell using and transient chara of the designed cell using spice

















# Refrences
GitHub repo for vsd standard cell design : https://github.com/nickson-jose/vsdstdcelldesign

Github repo for google skywater-pdk : https://github.com/google/skywater-pdk

Link for the skywater-pdk docs : https://skywater-pdk--136.org.readthedocs.build/en/136/

# Acknowledgements
Kunal Ghosh, Co-founder (VSD Corp. Pvt. Ltd)

Nickson P Jose, Teaching Assistant (VSD Corp. Pvt. Ltd)
