# simSIMD
Development and Simulation Framework for Application Specific Vector Processor.
***

Abstract: ???

Keywords:
Vector Processor Architecture, SIMD, Single Instruction Multiple Data, ASIP, Application Specific Instruction Processor, NoC, Network on Chip, Data Driven Design, Cycle Accurate Simulation, System Simulation, Model Based Development and Optimization, SystemC 

## Overview
* A framework for application specific vector processor with exemplar building blocks 

* Simulation software with exemplar building blocks and application examples
  * This simplifies the architecture development of the hardware which performs operations on the data structures of finite length (vectors)
  
* Typical applications and their data vectors
  * Signal processing: _OFDM symbols and/or code blocks_
  * Cryptography: _cipher blocks_
  * Networking: _data packets_
  
* Framework also provides unified approach for the development of the functional components: Execution Units (EU) and Data Memories (DM) as well as for their interconnect and interoperation
  * **Specific set and configuration of the functional units are identified by the target application**

* Development and simulation methodology of the hardware architecture from system specifications (algorithms) and throughput requirements
* Follow top-down development and optimization strategy
  * Area: improvement of the utilization rate of the processing blocks and storage elements (RAMs)
  * Throughput: datapath is elaborated at the architecture development stage 
  * Dynamic Power
  * Minimization non-recurring engineering (NRE) resources and risks

* Benefits of using SystemC
  * Short update-simulation-analysis cycle which allows for simulation driven development and optimization of the architecture
  * Cycle accurate simulation for the vector core to obtain realistic timing and throughput estimates at the earlier stages
  * High level of abstraction for Vector Core preferences, runtime configuration and status to stay focused on the architectural tasks
  * Large ecosystem of C/C++ libraries for data manipulation and processing allows for top-down development approach: from high level processing functions down to elementary arithmetic operations
  * Integration into the existing simulation workflows
  * Open source
  
### Block Diagram of the Simulation Platform
![alt text](https://github.com/timurkelin/simsimd/blob/master/doc/block_diagram.PNG)  

### Components in Brief

### Outline of the development strategy

For more details please refer to [doc/simsimd.pptx](https://github.com/timurkelin/simsimd/tree/master/doc)

Directories:
```
doc          	- documentation
examples     	- application examples
	+- basic		- basic operation
		+- dm2dm	- data memory to data memory transaction (DM test)
		+- dm_init	- dm block initialization from file 
				  (DM initialization test. matio integration and basic operation)
		+- vri_test	- test for the valid-ready interface (integrity and connectivity test)
		+- transp       - transparent EU test. Examines different approaches to the EU implementation
		+- adder  	- chain of 2 vector adders A+B=C C+D=E (EU with multiple inputs, EU chaining)
		+- adder_stream	- vector adder with stream I/O (test for the streaming interface)
		+- adder_cache  - vector adder with cache-like operation (example of the basic system design)
	+- comp			- computational examples
		+- fft-r4	- R4/2R2 fft
		+- sort		- Bitonic sorter
	+- system		- system design examples		
simd_sys_bmux   - System component: control and event bus muxes (obsolete)
simd_sys_crm    - System component: clock and reset source for the execution core
simd_sys_core	- System component: simd execution core (interconnect and signals)
simd_sys_dm     - System component: data memory units  
simd_sys_eu     - System component: execution units  
simd_sys_pool   - System component: segmented memory pool  
simd_sys_scalar - System component: control unit (FSM or scalar processor)  
simd_sys_stream - System component: Streaming interfaces (timed or on-demand)   
simd_sys_xbar   - System component: cross-bar switch / NoC

simd_common  	- top-level functions  
simd_pref    	- simulation and system preferences  
simd_dump    	- data dump   
simd_report  	- logging and reporting functions  
simd_systemc 	- Files taken from SystemC sources  
simd_trace   	- waveform trace  
simd_time    	- simulation time and resolution  
tools        	- supporting scripts  
makefile     	- top-level makefile 
```
Prerequisites:   
   GCC      (4.8.5)  
   make     (3.82)  
   [SystemC  (2.3.3)](https://www.accellera.org/downloads/standards/systemc)  
   [Boost    (1.68.0)](https://www.boost.org/)  
   [matIO    (1.5.16)](https://sourceforge.net/projects/matio/)   
   [gtkwave  (3.3.95)](http://gtkwave.sourceforge.net/) or other VCD viewer 

Environment:
```
export  CC=$(command -v gcc)
export GCC=$(command -v gcc)
export CXX=$(command -v g++)
$BOOST_HOME 	contains Boost   installation path
$MATIO_HOME 	contains matIO   installation path
$SYSTEMC_HOME	contains SystemC installation path
```
Quick start:
```
Skim through the slides:
doc/simsimd.pptx

Clean:
make EXAMPLE=basic/vri_test clean

Build:
make EXAMPLE=basic/vri_test all

Run:
./build/Release/out/simsimd

Inspect the result:
In gtkwave File->Open New Window->trace.vcd 
```