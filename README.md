# ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library

## Table of Contents
1. [Problem Analysis](#problem-analysis)
2. [Hardware Design](#hardware-design)
3. [Verification](#verification)
4. [Logic Synthesis](#synthesis)
5. [Physical Design](#physical-design)
6. [Sign-Off](#sign-off)
7. [Discussion](#discussion)
8. [Conclusion](#conclusion)

## Problem Analysis

Today’s world heavily depends on video files, especially as virtual communication rises. Videos are widely used, from movies to education. With 4K (and soon 8K), video sizes grow, making storage and sharing challenging. Motion Estimation is crucial; it calculates and stores motion vectors, drastically reducing file size.

Motion estimation compresses video data while maintaining quality. This project aims to develop a Motion Estimator from HDL to GDS for cutting-edge 14nm CMOS technology. The design reads a 16x16 Reference Frame and a 31x31 Search Frame, both in Grayscale. Clock speeds are 130MHz and 260MHz, aiming for a minimum search speed of 15 Frames/Second.

The objective of this project is the RTL2GDSII implementation of Motion Estimator design used for lowering data size while retaining video quality in video compression in cutting-edge 14nm Finfet technology. 

In the realms of computer vision and image processing, motion estimation is the intricate task of deducing motion vectors. These vectors encapsulate the transformation from one 2D image to another, commonly between successive frames in a video sequence. This undertaking is considered 'ill-posed' due to the complexity of motion occurring in three dimensions (3D), while the captured images only reflect a projection of this 3D motion onto a 2D plane. These motion vectors can pertain to the entirety of the image (known as global motion estimation), or to specific components like rectangular blocks, arbitrarily shaped patches, or even on a per-pixel basis. The representation of these motion vectors can be achieved through various models, ranging from translational to more intricate ones mimicking the motion of an actual video camera, encompassing rotations, translations in all three dimensions, and zooming effects.

Motion Estimator

• Task: Detect blocks of video data in successive frames that are related only via a translation.

• Digital Video is captured as blocks of 16x16 pixels

• Want to determine if block has moved largely unchanged

• If true can transmit motion vector rather than block

• Permits high level of compression

Example (4x4 block)

![blocks](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/882a490a-35b6-40e7-82d9-f516b09f6c4c)

Search Algorithm
Describe for 16x16 reference block:
1. Move a window the size of the reference block over the search space in the second frame.
2. For each window location (i,j) determine the distortion vector.
3. Maintain the best distortion and appropriate motion vector produced so far.

   ![block2](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/66091c22-07ed-4a60-9129-5223a4edb931)

### Hardware Design

A behavioral structure is planned before writing Verilog code. Operations occur on the rising clock edge. The design utilizes external memories for R, S1, and S2 (Reference Frame and Search Frames). The motion vectors for X and Y axes range from -8 to 7 pixels in Two’s Complement form.

![hardware](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/2728fa54-d33f-4f0a-8efb-e1be5d2e53c9)


### Verification

Several testbenches verify the Motion Estimator modules in a waveform simulator. Submodules are simulated individually, aiming for bug detection. Figures display Memory Elements, Processing Element (PE) Waveforms, PETotal (16 Processing Elements) Waveform, Comparator Module Waveform, and various test cases for the Top Module.

![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/623bbedf-4489-4d13-9fa5-c5aaf9f21d1a)
**Figure 2 - Memory Element Display**  

![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/0e119b5b-ad7e-417b-878e-d2ba077f7dfb)
**Figure 3 - PE Waveform**  

![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/35a88562-5381-4763-923d-83920b1df520)
**Figure 5 - PETotal Waveform**  

![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/db853fff-9048-440f-8224-b86cc289169b)
**Figure 6 - Comparator Waveform**  

![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/c9d3e94a-b3b7-41fe-83f0-f48f076b4cbe)
**Figure 7 - Comparator Stimulus** 


# Logic Synthesis

Logic synthesis is the process of converting a high-level design description into an optimized gate-level representation. It uses a standard cell library containing basic logic gates (AND, OR, NOR) and macro cells (adders, muxes, memory, flip-flops). 

## Design Compiler and Synthesis Process

Design Compiler (DC) from Synopsys Inc. is a synthesis tool that translates a Register Transfer Logic (RTL) hardware description (Verilog/VHDL) into a technology-dependent gate-level-netlist. The synthesis process involves several steps:

- High-level RTL optimization
- RTL to optimized Boolean logic conversion
- Technology-independent optimizations
- Technology mapping to available standard cells in the technology library (target library)

### Flowchart of Synthesis Process
![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/8abf775c-809c-493d-9f9c-5fd793c603db)


### Inputs and Outputs of Logic Synthesis
Design Compiler reads technology libraries and DesignWare libraries to implement synthesis. It translates RTL descriptions to components extracted from these libraries. 
![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/aa47de16-9e59-4d2f-8eba-3a758daaab8f)


## Synthesis Constraints and Schematic

### Synthesis Constraints
![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/1d472e26-84b2-4ce9-a057-b72a315fbfd5)

### Synthesis Schematic
![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/b9a96eae-5765-4dd2-9083-e647df2d20d4)

After synthesis, the tool generates key files:

- Gate-level netlist (`*.v`, `*.vhd`)
- .sdc timing constraints file

### Post Synthesis Gate Level Netlist
![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/ec6a4a42-d0fa-4bac-8c5b-bae12eb1f8b4)


### Post Synthesis SDC Constraints
![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/c110b31b-fb7c-4f84-a1eb-daaabdaa018a)


## Synthesis Reports

The synthesis tool generates text reports (`.rpt` files) providing crucial design insights:

### Post Synthesis Area Report
![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/8b674580-8f4c-4311-8910-669aeacab3bf)


### Post Synthesis Power Report
![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/df48cbc2-729c-41bb-ad02-66dc9ad3735b)


### Post Synthesis QOR (Quality of Results) Report
![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/a05ba82f-0ebe-4a97-930c-32b2d9fd4cee)


### Timing Reports
- Post Synthesis Primetime Setup Report  
  ![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/98d2f833-865b-4d02-803a-baade1218599)


- Post Synthesis Primetime Hold Report  
  ![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/54c8ee5a-5fe1-457f-a6ab-86ae7b2fbbb9)

# Physical Design

The physical design involves transforming a circuit description into the physical layout, focusing on minimal area and wire length.

## Steps in Physical Design

![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/70957790-d851-478b-b221-bceed9edc1d8)
**Figure 24 – Physical Design Flow**

1. **Partitioning:** Breaks a circuit into smaller sub-circuits or modules for individual analysis.
2. **Floorplanning:** Determines the arrangement of modules, external ports, IP, or macro-blocks.
3. **Power and Ground Routing:** Distributes power and ground nets throughout the chip.
4. **Placement:** Determines spatial locations of cells within each block.
5. **Clock Network Synthesis:** Handles clock signal buffering, gating, and routing.
6. **Global Routing:** Allocates routing resources for connections.
7. **Detailed Routing:** Assigns routes to specific metal layers within global routing resources.
8. **Timing Closure:** Optimizes circuit performance through specialized placement or routing techniques.

### Inputs Required for Physical Design

![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/a1bcfb90-02c4-4b95-acee-e7a167ced4c5)
**Figure 25 – Physical Design Inputs**

1. **Gate-Level Netlist:** Result of synthesizing RTL code with standard cell libraries.
2. **Constraint File (SDC):** Includes system interface, design rule constraints, timing specifics, and exceptions.
3. **Standard Cell Libraries:** Logical and Physical libraries providing cell timing, area, pin information, and power characteristics.
4. **Technology File:** Contains metal layer information, vias, design rules, and resistance data.
5. **RC Coefficient File:** Used for RC estimation and extraction.
6. **MMMC View File:** Generates different analysis views based on delay corners and constraint modes.
7. **Block-Level PnR Implementation:** Specifies block size, pin definition, power distribution, and intent.
8. **Switching Activity Files:** Used for dynamic IR analysis based on chip-level switching activities.

### Constraints for Physical Design
- Chip aspect ratio: square-shaped (aspect ratio 1)
- Utilization: 70%

![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/0ef5b358-7d44-4ab8-a539-1d32ea328447)
**Figure 25 – Physical Design Constraints**




## Post-Physical Design Outputs

### Layout Views
- Post Routing Layout View  
  ![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/3f4d30b9-46af-47a5-8f92-2877e1ac805f)

  
- Layout View with Routes Turned Off  
  ![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/7b0047f8-e106-4338-8e90-1a9c7f6d3759)

  
- Layout View of Signal Interconnections  
  ![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/a6d3d72e-82a6-4d4b-9eac-d2a55e52a77b)

### Post-Layout Reports
- Post Layout Area Report  
 ![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/68137b54-69ff-4939-b822-cb036b240a34)

- Post Layout Power Report  
  ![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/cedb11f4-ea98-4cd1-96b5-ee19ae98c93d)

### Post Layout SPEF File
![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/af1f5b2e-c1a7-4035-bc6c-58a62e3b24ab)

## Sign-Off and Verification

### Timing Analysis
- Post Layout Primetime Setup Report  
 ![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/cef2aed8-77c9-45a2-8a9e-f47e388cc4fc)

- Post Layout Primetime Hold Report  
  ![image](https://github.com/saifullaj97/ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library/assets/61980110/1236550b-516c-43a5-88d4-bf5c82996013)

### Design Rule Check (DRC)
- DRC Check  
  ![Uploading image.png…]()

## Discussion and Conclusion



