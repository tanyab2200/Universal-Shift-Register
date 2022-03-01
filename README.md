# Implementation of a 4-bit Universal Shift  Register

A 4-bit Universal Shift Register is capable of 
storing and shifting data either left or right, along with 
the capability to load data serially or parallelly. In this 
paper, we aim to design an energy-efficient 4-bit 
Universal Shift Register using 28nm technology, which 
performs 3 major operations namely, Parallel Load, 
Shift Left and Shift Right. To keep power dissipation as 
a factor, the design includes usage of multiplexers and 
flip flops. Moreover, a universal shift register, if 
designed efficiently, can be of major use in data transfer, 
counters, memory elements and so much more


REQUIREMENTS
Synopsys Custom Compiler

REFERENCE CIRCUIT DIAGRAM
![WhatsApp Image 2022-02-19 at 1 14 32 PM](https://user-images.githubusercontent.com/44083640/156220260-7e8d8ba2-6252-4efe-941e-e958fe6b21f6.jpeg)

OPERATION TABLE
![image](https://user-images.githubusercontent.com/44083640/156220585-520d6320-e712-40ba-a6dc-afcdf8530e94.png)


SIMULATED CIRCUIT DIAGRAM
![image](https://user-images.githubusercontent.com/44083640/156220496-eb5222be-5564-4d8f-ab5e-270853cbbde4.png)

WORKING
The working of the design is simply operated by two inputs, S0 and S1, called as select lines for multiplexers. As shown in the operation table, depending on what inputs are provided to the select lines. For example, if inputs are low for both the pins, the circuit remains in locked state acting as a storage element. Now, if the inputs provided are 0 and 1 for S0 and S1 respectively, a left shift operation is done. For loading data parallelly, the inputs required would be 1 and 1. Now, depending on the inputs, each multiplexer produces an output which is fed to the input of the D flip flop. These flip flops are sequential circuits and hence are controlled by the clock, and so controls the outputs.


NAND Gate Schematic 

<img width="296" alt="nand_schematic" src="https://user-images.githubusercontent.com/44083640/156218293-f4e869c9-2a83-4aaf-8bca-76389af76eac.PNG">

NAND GATE TESTBENCH



<img width="416" alt="nand_tb" src="https://user-images.githubusercontent.com/44083640/156218454-605d40a4-f453-4849-a8a9-709264e5524b.PNG">

OUTPUT WAVEFORM

<img width="848" alt="nand_gate_outputwave" src="https://user-images.githubusercontent.com/44083640/156218786-39d8e6ba-5013-40d2-9730-bfb6413e7bfd.PNG">

Netlist 

*  Generated for: PrimeSim
*  Design library name: USR
*  Design cell name: nand_gate_tb
*  Design view name: schematic
.lib 'saed32nm.lib' TT

*Custom Compiler Version S-2021.09
*Mon Feb 28 11:44:25 2022

.global gnd! vdd!
********************************************************************************
* Library          : USR
* Cell             : nand_gate
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
.subckt nand_gate va vb vout vdd vt_bulk_n_gnd! vt_bulk_p_vdd!
xm1 vout vb vdd vt_bulk_p_vdd! p105 w=0.1u l=0.03u nf=1 m=1
xm0 vout va vdd vt_bulk_p_vdd! p105 w=0.1u l=0.03u nf=1 m=1
xm3 net10 vb gnd! vt_bulk_n_gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm2 vout va net10 vt_bulk_n_gnd! n105 w=0.1u l=0.03u nf=1 m=1
.ends nand_gate

********************************************************************************
* Library          : USR
* Cell             : nand_gate_tb
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
xi0 va vb vout net11 gnd! vdd! nand_gate
c1 vout gnd! c=1p
v9 net11 gnd! dc=1.8
v11 vb gnd! dc=0 pulse ( 0 0.05 0 0.1u 0.1u 5u 10u )
v10 va gnd! dc=0 pulse ( 0 1.05 0 0.1u 0.1u 5u 10u )








.tran '1u' '20u' name=tran

.option primesim_remove_probe_prefix = 0
.probe v(*) i(*) level=1
.probe tran v(va) v(vb) v(vout)

.temp 25



.option primesim_output=wdf


.option parhier = LOCAL






.end


D Flip Flop

DFF Schematic
<img width="439" alt="DFF_schematic" src="https://user-images.githubusercontent.com/44083640/156218638-3d76d1b2-5b2d-4488-803b-19053dd98237.PNG">

DFF TESTBENCH
<img width="435" alt="DFF_tb" src="https://user-images.githubusercontent.com/44083640/156218687-05da91c6-3b55-4958-b50a-1a6c2e9b518d.PNG">

OUTPUT WAVEFORM
<img width="942" alt="DFF_waveform" src="https://user-images.githubusercontent.com/44083640/156218722-4b99752e-47fb-4eac-a035-218dc8398a99.PNG">

NETLIST
*  Generated for: PrimeSim
*  Design library name: USR
*  Design cell name: DFF_tb
*  Design view name: schematic
.lib 'saed32nm.lib' TT

*Custom Compiler Version S-2021.09
*Mon Feb 28 12:36:53 2022

.global gnd! vdd!
********************************************************************************
* Library          : USR
* Cell             : nand_gate
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
.subckt nand_gate va vb vout vdd vt_bulk_n_gnd! vt_bulk_p_vdd!
xm1 vout vb vdd vt_bulk_p_vdd! p105 w=0.1u l=0.03u nf=1 m=1
xm0 vout va vdd vt_bulk_p_vdd! p105 w=0.1u l=0.03u nf=1 m=1
xm3 net10 vb gnd! vt_bulk_n_gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm2 vout va net10 vt_bulk_n_gnd! n105 w=0.1u l=0.03u nf=1 m=1
.ends nand_gate

********************************************************************************
* Library          : USR
* Cell             : DFF
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
.subckt dff d q qbar vdd clock vt_bulk_n_gnd! vt_bulk_p_vdd!
xi4 net19 qbar q vdd vt_bulk_n_gnd! vt_bulk_p_vdd! nand_gate
xi3 q net16 qbar vdd vt_bulk_n_gnd! vt_bulk_p_vdd! nand_gate
xi2 clock net12 net16 vdd vt_bulk_n_gnd! vt_bulk_p_vdd! nand_gate
xi1 d clock net19 vdd vt_bulk_n_gnd! vt_bulk_p_vdd! nand_gate
xi0 d d net12 vdd vt_bulk_n_gnd! vt_bulk_p_vdd! nand_gate
.ends dff

********************************************************************************
* Library          : USR
* Cell             : DFF_tb
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
xi0 d q qbar net23 clock gnd! vdd! dff
c1 qbar gnd! c=1p
c2 q gnd! c=1p
v17 clock gnd! dc=0 pulse ( 0 1.05 5u 0.1u 0.1u 5u 10u )
v16 d gnd! dc=0 pulse ( 0 1.05 0 0.1u 0.1u 5u 10u )
v15 net23 gnd! dc=1.8








.tran '1u' '20u' name=tran

.option primesim_remove_probe_prefix = 0
.probe v(*) i(*) level=1
.probe tran v(d) v(q) v(qbar) v(clock)

.temp 25



.option primesim_output=wdf


.option parhier = LOCAL






.end


4x1 MULTIPLEXER (MUX)


4x1 MUX SCHEMATIC

<img width="307" alt="mux_design" src="https://user-images.githubusercontent.com/44083640/156218961-153a9ce4-0d3c-4b56-af1f-aab02fd71ae4.PNG">

4x1 MUX TESTBENCH

<img width="368" alt="mux_tb" src="https://user-images.githubusercontent.com/44083640/156219027-fbb42090-542a-421d-9c84-c3f445831f2a.PNG">

4x1 MUX WAVEFORM
<img width="951" alt="mux4by1_wave" src="https://user-images.githubusercontent.com/44083640/156219084-2d46968d-d85f-48fb-ac06-2129f54e7598.PNG">

NETLIST

*  Generated for: PrimeSim
*  Design library name: USR
*  Design cell name: mux4by1_tb
*  Design view name: schematic
.lib 'saed32nm.lib' TT

*Custom Compiler Version S-2021.09
*Tue Mar  1 16:52:49 2022

.global gnd! vdd!
********************************************************************************
* Library          : USR
* Cell             : nand_gate
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
.subckt nand_gate va vb vout vdd vt_bulk_n_gnd! vt_bulk_p_vdd!
xm1 vout vb vdd vt_bulk_p_vdd! p105 w=0.1u l=0.03u nf=1 m=1
xm0 vout va vdd vt_bulk_p_vdd! p105 w=0.1u l=0.03u nf=1 m=1
xm3 net10 vb gnd! vt_bulk_n_gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm2 vout va net10 vt_bulk_n_gnd! n105 w=0.1u l=0.03u nf=1 m=1
.ends nand_gate

********************************************************************************
* Library          : USR
* Cell             : mux4by1
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
.subckt mux4by1 d0 d1 d2 d3 sel0 sel1 sel1bar vdd out sel0bar vt_bulk_n_gnd!
+ vt_bulk_p_vdd!
xi8 net35 net36 out vdd vt_bulk_n_gnd! vt_bulk_p_vdd! nand_gate
xi7 net31 sel1 net35 vdd vt_bulk_n_gnd! vt_bulk_p_vdd! nand_gate
xi6 sel1bar net28 net36 vdd vt_bulk_n_gnd! vt_bulk_p_vdd! nand_gate
xi5 net23 net24 net28 vdd vt_bulk_n_gnd! vt_bulk_p_vdd! nand_gate
xi4 net19 net20 net31 vdd vt_bulk_n_gnd! vt_bulk_p_vdd! nand_gate
xi3 sel0 d3 net19 vdd vt_bulk_n_gnd! vt_bulk_p_vdd! nand_gate
xi2 sel0bar d2 net20 vdd vt_bulk_n_gnd! vt_bulk_p_vdd! nand_gate
xi1 sel0 d1 net23 vdd vt_bulk_n_gnd! vt_bulk_p_vdd! nand_gate
xi0 sel0bar d0 net24 vdd vt_bulk_n_gnd! vt_bulk_p_vdd! nand_gate
.ends mux4by1

********************************************************************************
* Library          : USR
* Cell             : mux4by1_tb
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
xi0 d0 d1 d2 d3 sel0 sel1 sel1bar net12 out sel0bar gnd! vdd! mux4by1
v1 net12 gnd! dc=1.8
c2 out gnd! c=1p
v22 d0 gnd! dc=0 pulse ( 0 0.2 0 0.1u 0.1u 5u 20u )
v21 d1 gnd! dc=0 pulse ( 0 0.15 0 0.1u 0.1u 5u 20u )
v20 d2 gnd! dc=0 pulse ( 0 0.1 0 0.1u 0.1u 5u 20u )
v19 d3 gnd! dc=0 pulse ( 0 0.05 0 0.1u 0.1u 5u 20u )
v18 sel0 gnd! dc=0 pulse ( 0 0.05 0 0.1u 0.1u 5u 10u )
v17 sel0bar gnd! dc=0 pulse ( 0 0.05 5u 0.1u 0.1u 5u 10u )
v14 sel1bar gnd! dc=0 pulse ( 0 0.05 5u 0.1u 0.1u 5u 10u )
v13 sel1 gnd! dc=0 pulse ( 0 0.05 0 0.1u 0.1u 5u 10u )








.tran '1u' '20u' name=tran

.option primesim_remove_probe_prefix = 0
.probe v(*) i(*) level=1
.probe tran v(d0) v(d1) v(d2) v(d3) v(sel0) v(sel0bar) v(sel1) v(sel1bar) v(out)

.temp 25



.option primesim_output=wdf


.option parhier = LOCAL






.end



FINAL CIRCUIT
4-bit UNIVERSAL SHIFT REGISTER (USR)

4-bit USR SCHEMATIC

4-bit USR TESTBENCH

4-bit USR WAVEFORM



REFERENCES

[1] S. Pervez, M. Sahoo and A. Noor, "Implementation of 4-BIT 
universal shift register using diode free adiabatic logic," 2017 8th 
International Conference on Computing, Communication and 
Networking Technologies (ICCCNT), 2017, pp. 1-6, doi: 
10.1109/ICCCNT.2017.8204026.

[2] IOSR Journal of VLSI and Signal Processing (IOSR-JVSP) Volume 
9, Issue 1, Ser. I (Jan. - Feb. 2019), PP 28-33 e-ISSN: 2319 – 4200, pISSN No. : 2319 – 4197

[3] 8-Bit Universal Shifter using Verilog (IJSRD/Vol. 6/Issue 
12/2019/167)

[4] IOSR Journal of VLSI and Signal Processing (IOSR-JVSP) Volume 
7, Issue 3, Ver. I (May. - Jun. 2017), PP 08-13 e-ISSN: 2319 – 4200, 
p-ISSN No. : 2319 – 4197


ACKNOWLEDGEMENT

Kunal Ghosh, Co-founder of VLSI System Design (VSD) Corp. Pvt. Ltd.
