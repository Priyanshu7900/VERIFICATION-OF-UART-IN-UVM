# Verification of the UART in UVM

## Project Overview

This project implements the **Universal Asynchronous Receiver/Transmitter (UART) Verification Environment** using **SystemVerilog and UVM (Universal Verification Methodology)**.  
The design under test (DUT) is a **UART module**, and the verification is carried out using a reusable, layered UVM testbench that follows industry-standard practices.

The testbench supports **transmit** and **receive** verification, protocol compliance checks, and functional coverage collection.

---

## Features

- **UVM-based layered testbench** for modularity and reuse  
- Supports both **TX (transmit)** and **RX (receive)** paths  
- Constrained-random and directed testing support  
- **Scoreboard** for automatic result checking  
- **Coverage-driven verification** for completeness  
- Protocol compliance verification (start bit, data bits, parity, stop bit)  
- Simulation results and waveforms demonstrating correct operation  

---

## Architecture

The project consists of the following files and components:

- **clk_gen.sv** – Generates the clock signal for the UART system and testbench.  
- **uart_tx.sv** – Implements the UART transmitter logic for serial data transmission.  
- **uart_rx.sv** – Implements the UART receiver logic for serial data reception.  
- **uart_top.sv** – Top-level DUT integrating transmitter, receiver, and clock generator.  
- **uart_if.sv** – Interface connecting the DUT to the UVM environment.  
- **UVM Environment** – Includes driver, monitor, sequencer, scoreboard, agents, environment, and test files for complete verification.  
- **verification_results/** – Directory containing simulation logs, waveforms, and coverage reports showing verification outcomes.

---

## Run Locally

### Clone the project
```bash
git clone https://github.com/Priyanshu7900/VERIFICATION-OF-UART-IN-UVM.git
cd VERIFICATION-OF-UART-IN-UVM
```

### Install a SystemVerilog/UVM simulator
Example (free with Intel FPGA tools):  
[ModelSim Intel Edition](https://www.intel.com/content/www/us/en/software-kit/705184/modelsim-intel-fpgas.html)  

---

### Run in ModelSim / Questa
```bash
# Create working library
vlib work
vmap work work

# Compile DUT and Testbench
vlog +incdir+./tb +incdir+./src ./src/*.sv ./tb/*.sv

# Run simulation
vsim -c top -do "run -all; quit"
```

---

## Run on EDA Playground

1. **Open** [EDA Playground](https://www.edaplayground.com/)  
2. **Set Language**: *SystemVerilog*  
3. **Add Files**:  
   - `clk_gen.sv`  
   - `uart_tx.sv`  
   - `uart_rx.sv`  
   - `uart_top.sv`  
   - `uart_if.sv`  
   - All UVM TB files (`*.sv`)  
4. In the **Testbench pane**, include:
```verilog
`include "uvm_macros.svh"
`include "uart_if.sv"
`include "uart_tx.sv"
`include "uart_rx.sv"
`include "clk_gen.sv"
`include "uart_top.sv"
... (all TB files)
```
5. **Select Simulator**:  
   - Siemens Questa / Aldec Riviera (for full UVM support)  
6. **Enable** "Open EPWave" for waveforms  
7. **Click Run**  

---

## Verification Methodology

- **Testbench is UVM-based** (modular, reusable, scalable)  
- Supports **directed** and **constrained-random** stimulus  
- **Functional coverage** ensures all scenarios are tested  
- **Scoreboard** provides pass/fail results automatically  
- **Waveform and logs** provide detailed debug information  

---

## Repository Structure

```
VERIFICATION-OF-UART-IN-UVM/
│
├── src/                     # DUT source files
│   ├── clk_gen.sv           # Clock generator
│   ├── uart_tx.sv           # UART transmitter
│   ├── uart_rx.sv           # UART receiver
│   ├── uart_top.sv          # Top-level DUT
│   ├── uart_if.sv           # Interface
│
├── tb/                      # UVM testbench files
├── verification_results/    # Logs, waveforms, coverage reports
└── README.md
```
