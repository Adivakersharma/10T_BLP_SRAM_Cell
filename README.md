# 10T_BLP_SRAM_Cell

### This Repositery shows Data Dependent Power Supply 10T SRAM cell
1. [Abstract](#Abstract)

2. [Synopsys Custom Compiler Tool Details](#Synopsys-Custom-Compiler-Tool-Details)

3. [Circuit Details](#Circuit-Details)

4. [Circuit Design](#Circuit-Design)

5. [Waveforms](#Waveforms)

6. [Spice Netlist](#Spice-Netlist)

7. [Acknowledgement](#Acknowledgement) 

8. [References](#References)

## Abstract
Low-power design has been a priority in recent years due to the increasing proliferation of battery-operated products. Furthermore, integrated SRAM units have become a critical component of current SoCs. From both a dynamic and static standpoint, the SRAM unit has become a power hungry block due to the increasing amount of transistors in the units
and the rising leakage current of the MOS transistors in scaled technologies. This paper proposes a new single-ended, bit-line powered 10T static random-access memory cell that increases access speed, dissipates minimal power, and allows bit-interleaving.


## Synopsys Custom Compiler Tool Details
The [Synopsys Custom Compiler™](https://www.synopsys.com/implementation-and-signoff/custom-design-platform/custom-compiler.html) design environment is a modern solution for full-custom analog, custom digital, and mixed-signal IC design. As the heart of the Synopsys Custom Design Platform, Custom Compiler provides design entry, simulation management and analysis, and custom layout editing features. It delivers industry-leading productivity, performance, and ease-of-use while remaining easy to adopt for users of legacy tools.

![custom_compiler](https://github.com/Adivakersharma/10T_BLP_SRAM_Cell/blob/ab1d11a800237febc7183dd733c51b50e67fdfb9/Schematics%20and%20Waveforms/custom_compiler.png)


## Circuit Details
  The need to reduce the power consumption of SRAM units has pushed numerous academics to develop new low-power circuits. Six transistors have long been seen to be a good choice for low-power applications. As access transistors, the CMOS standard 6T SRAM[1] cell has two PMOSs, two NMOSs, and two NMOSs. Two data-storage inverters are produced, and they are cross-coupled in a way that creates positive feedback. P1, N1, and P2, N2 are the names of the two inverters. It also has a Word Line (WL) and Bit Lines (BL and BLB) that are aligned horizontally and vertically, respectively. SRAM has three different modes of operation: standby, read, and write. Vdd is applied to BL during standby mode, and WL is turned off, causing the transistors connected to it to switch off as well. Because BL=VDD, the two cross-coupled inverters provide positive feedback, allowing data to be stored while power is delivered. Only during read and write operations will the WL line, which controls the state of the access transistors, be enabled.
  
The 6T SRAM cell basic Schematic.

![image](https://github.com/Adivakersharma/10T_BLP_SRAM_Cell/blob/ab1d11a800237febc7183dd733c51b50e67fdfb9/Schematics%20and%20Waveforms/6T_SRAM_Cell.png)  
  
  ### Read and write operation 
   For read and write operations, this circuit operates in single-end mode. The proposed architecture has 10 transistors[2], with transistors N1-N2 and P1-P2 forming the core latch structure. WL and WLB signals control the gate nodes of transistors N4 and N3,respectively. Because individual access transistors are employed for read and write operations, the aspect ratio of these devices may be maintained while simultaneously improving read stability and write ability. This also fixes the ATS problem. During the write process, transistor N3 is switched off. This breaks the left inverter&#39;s ground (GND) connection, making it weaker than the right side inverter in the core latch. In this configuration, a read decoupled structure is used to enhance read static noise margin. The read ground (RGND) signal is used to reduce bitline current leakage.The D2P signal is used to enable bit-line dependent power supply (BPS) for the planned 10T memory bit-cell. To turn on the PMOS transistors P3
and P4, the D2P signal is set to logic &#39;0&#39;. As a result, the core latch is activated by a pair of bit-lines (BLB, BL). As a result, instead of using a separate voltage source, the pre-charge on the bit-line pair is used as the source of supply voltage for the core latch in this configuration. In comparison to a standard 6T SRAM
cell, this configuration creates a bit-line dependent power supply (BPS) topology, which reduces total power dissipation.

The 10T BLP SRAM cell.

![image](https://github.com/Adivakersharma/10T_BLP_SRAM_Cell/blob/ab1d11a800237febc7183dd733c51b50e67fdfb9/Schematics%20and%20Waveforms/10T_BLP_SRAM_Cell.png)
  
  These operations can be observed in the below [waveforms](#waveforms)

## Circuit Design

The 10TBLP SRAM cell basic design.

![image](https://github.com/Adivakersharma/10T_BLP_SRAM_Cell/blob/ab1d11a800237febc7183dd733c51b50e67fdfb9/Schematics%20and%20Waveforms/Schematic_10T_BLP.png)

The symbol of 10T BLP SRAM cell in schematic for transient analysis.

![image](https://github.com/Adivakersharma/10T_BLP_SRAM_Cell/blob/ab1d11a800237febc7183dd733c51b50e67fdfb9/Schematics%20and%20Waveforms/Transient_Response_10T_BLP.png)


## Waveforms
 
 ### transient analysis of the SRAM cell.

![image](https://github.com/Adivakersharma/10T_BLP_SRAM_Cell/blob/ab1d11a800237febc7183dd733c51b50e67fdfb9/Schematics%20and%20Waveforms/10T_BLP_SRAM_Cell_Transient_Response.png)

### Total Power Dissipation of the 10T BLP SRAM cell.
![image](https://github.com/Adivakersharma/10T_BLP_SRAM_Cell/blob/ab1d11a800237febc7183dd733c51b50e67fdfb9/Schematics%20and%20Waveforms/Total_Power_Dissipation.png)

## Spice Netlist

```

*  Generated for: PrimeSim
*  Design library name: SRAM_Cell_Design
*  Design cell name: 10T_SRAM_Cell_transient_tb
*  Design view name: schematic
.lib 'saed32nm.lib' TT

*Custom Compiler Version S-2021.09
*Tue Mar  1 10:03:27 2022

.global gnd!
********************************************************************************
* Library          : SRAM_Cell_Design
* Cell             : 10T_SRAM_Cell
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
.subckt _10t_sram_cell bl blb d2p qb qr rbl rd rgnd wl wlb
xm20 blb d2p net10 net10 p105 w=0.1u l=0.03u nf=1 m=1
xm21 net9 d2p bl net9 p105 w=0.1u l=0.03u nf=1 m=1
xm19 net10 qr qb net10 p105 w=0.1u l=0.03u nf=1 m=1
xm18 qr qb net9 net9 p105 w=0.1u l=0.03u nf=1 m=1
xm25 net25 qr qb gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm22 qr qb gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm24 net25 wlb gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm23 net32 qb rgnd gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm26 qb wl blb gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm27 rbl rd net32 gnd! n105 w=0.1u l=0.03u nf=1 m=1
.ends _10t_sram_cell

********************************************************************************
* Library          : SRAM_Cell_Design
* Cell             : 10T_SRAM_Cell_transient_tb
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
xi0 bl_node blb_node gnd! qb_ q_ rbl rd_node rgnd_node wl_node wlb_node
+ _10t_sram_cell
v1 bl_node gnd! dc=1
v7 pc_node gnd! dc=0 pulse ( 0 1 0 1p 1p 4n 12n )
vbit_line_bar blb_node gnd! dc=0 pulse ( 0 1 0 1p 1p 12n 16n )
v4 wlb_node gnd! dc=0 pulse ( 1 0 0 1p 1p 4n 12n )
vword_line wl_node gnd! dc=0 pulse ( 0 1 0 1p 1p 4n 12n )
v3 rgnd_node gnd! dc=0 pulse ( 0 1 0 1p 1p 8n 12n )
v2 rd_node gnd! dc=0 pulse ( 1 0 0 1p 1p 8n 12n )
xm6 rbl pc_node bl_node bl_node p18 w=0.16u l=0.15u nf=1 m=1








.tran '0.01n' '24n' name=tran

.option primesim_remove_probe_prefix = 0
.probe v(*) i(*) level=1
.probe tran v(blb_node) v(pc_node) v(q_) v(qb_) v(rbl) v(rd_node) v(wl_node)
+ i(v1)

.temp 25



.option primesim_output=wdf


.option parhier = LOCAL






.end



```

## Acknowledgement

1. Kunal Ghosh, Co-founder, VSD Corp. Pvt. Ltd. - kunalpghosh@gmail.com
2. Cloud Based Analog IC Design Hackathon Team, IIT Hyderabad
3. [Synopsys Team/Company](https://www.synopsys.com/)


## References

[1] Govind Prasad, Dulari Tandon, Bipin Chandra Mandi, Member, IEEE, and Maifuz Ali, Member, IEEE, “A Low Power 1-Kb SRAM Memory Design using 10T SRAM Cell in 45nm CMOS Technology”, IEEE

[2] Sachdeva, A., Tomar, V.K. “A soft-error resilient low power static random access memory cell.” Analog Integr Circ Sig Process (2021). https://doi.org/10.1007/s10470-021-01898-9


[3] D. Anitha, K. M. Chari and P. S. Kumar, &quot;N-Curve Analysis of Low power SRAM Cell,&quot; 2018 Second International Conference on Inventive Communication and Computational Technologies (ICICCT), 2018, pp. 1645-1650, doi:10.1109/ICICCT.2018.8473215.
