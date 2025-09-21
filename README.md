# Lightweight AI Accelerator for Microwatt (Caravel Integration)

## Overview
This project extends the [Microwatt](https://github.com/antonblanchard/microwatt) open-source PowerPC core with a **custom AI accelerator**.  
The accelerator performs **matrix/vector operations** (dot-product, small matrix multiply, ReLU), which are key building blocks in neural networks.  

The design demonstrates **hardware/software co-design**:
- **Hardware (VLSI):** Accelerator in Verilog/VHDL integrated as a memory-mapped peripheral.
- **Software:** [MicroPython](https://micropython.org/) running on Microwatt controls the accelerator for AI workloads.

---

## Motivation
AI workloads rely heavily on **multiply-accumulate (MAC) operations**. CPUs alone are inefficient for these tasks.  
By creating a **lightweight AI accelerator** and attaching it to an open-source CPU, we show how domain-specific accelerators can deliver **higher performance per area** while staying within the open-source silicon ecosystem (Caravel + SKY130).

---

## Features
- **AI Accelerator**
  - Supports dot-product and 4×4 matrix multiplication
  - Fixed-point arithmetic (configurable bit-width)
  - ReLU activation
  - Memory-mapped registers for data/control
  - Handshaking interface (start/done)

- **Integration with Microwatt**
  - Connected via Wishbone bus
  - Accessible from MicroPython using `machine.mem32[...]`
  - Enables AI inference controlled from Python scripts

- **Demo Application**
  - Run a tiny neural network inference (e.g., XOR classification)
  - MicroPython code initializes accelerator, executes computation, and prints results

---

## Implementation Plan
### Primary Plan
- Integrate **Microwatt + Accelerator** into the Caravel user area
- Control accelerator directly from MicroPython running on Microwatt

### Fallback Plan (in case of area/I/O constraints)
- Implement **Accelerator Only** in the Caravel user area
- Use **Caravel’s built-in management RISC-V** core to control the accelerator
- Provide Microwatt + Accelerator integration in simulation for demonstration

---

## Project Timeline
- **Week 1**: Define accelerator spec, set up Microwatt + Caravel environment  
- **Week 2**: Implement accelerator datapath (MAC/Matrix unit) + testbench  
- **Week 3**: Integrate with Microwatt, verify memory-mapped I/O access  
- **Week 4**: Run MicroPython demo, finalize results and documentation  

---

## Deliverables
- RTL code (Verilog/VHDL) for accelerator  
- Testbenches with simulation waveforms  
- Integrated Microwatt system with accelerator (simulation)  
- MicroPython scripts demonstrating AI inference  
- Caravel integration files (wrapper, I/O mapping)  
- Final documentation (design + block diagrams)  

---

## Skills & Tools
- **Domain:** VLSI Design, Computer Architecture, Embedded Systems  
- **Skills:** Verilog, MicroPython, Digital Design, RTL Verification, OpenLane (SKY130)  
- **Tools:** ModelSim / GHDL / Vivado for sim, OpenLane for ASIC flow, Caravel platform  

---

## Future Work
- Expand accelerator with convolution/pooling units  
- Optimize for larger models and external memory  
- Prototype on FPGA for real-time testing  
- Benchmark vs. software-only execution  
