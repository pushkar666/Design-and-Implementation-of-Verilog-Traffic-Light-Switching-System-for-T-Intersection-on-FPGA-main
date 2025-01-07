# TF Design and Testbench

This project implements a finite state machine (FSM) for a traffic flow design, where LEDs represent various states of different signals (M1, MT, M2, and S). The FSM transitions between six states based on time intervals controlled by a counter.

## Table of Contents
- [Overview](#overview)
- [Design Details](#design-details)
- [State Descriptions](#state-descriptions)
- [Inputs and Outputs](#inputs-and-outputs)
- [Testbench Details](#testbench-details)
- [How to Run](#how-to-run)
- [Files in Repository](#files-in-repository)
- [License](#license)

## Overview
The module `TF_design` models a traffic flow controller. It uses a clock (`clk`) and reset (`rst`) signal to transition between states and controls the LEDs (`led_M1`, `led_MT`, `led_M2`, and `led_S`) accordingly. A testbench (`TF_design_tb`) is provided to verify the functionality of the FSM.

## Design Details
- The FSM operates with six states: ST1 to ST6.
- Each state controls the LED signals for M1, M2, MT, and S.
- State transitions are based on predefined time intervals, achieved using a 40-bit counter.
- The design uses a synchronous reset to initialize the state and counter.

### Clock and Reset
- **Clock (`clk`)**: Drives the FSM transitions and counter.
- **Reset (`rst`)**: Resets the FSM to its initial state (ST1).

### Counter
The 40-bit counter increments with every clock cycle and determines the duration of each state based on thresholds specific to each state.

## State Descriptions
| State | LED Outputs                                     | Duration (Clock Cycles)  | Description                   |
|-------|-------------------------------------------------|--------------------------|-------------------------------|
| ST1   | `led_M1=001, led_M2=001, led_MT=100, led_S=100` | 3,000,000,000            | Initial state of traffic flow |
| ST2   | `led_M1=001, led_M2=010, led_MT=100, led_S=100` | 400,000,000              | Transition state for M2       |
| ST3   | `led_M1=001, led_M2=100, led_MT=001, led_S=100` | 3,000,000,000            | Traffic flows to MT           |
| ST4   | `led_M1=010, led_M2=100, led_MT=010, led_S=100` | 400,000,000              | Transition for M1 and MT      |
| ST5   | `led_M1=100, led_M2=100, led_MT=100, led_S=001` | 2,000,000,000            | Signal S active               |
| ST6   | `led_M1=100, led_M2=100, led_MT=100, led_S=010` | 400,000,000              | Transition for S              |

## Inputs and Outputs
### Inputs
- `clk`: Clock signal to synchronize the FSM.
- `rst`: Reset signal to initialize the FSM to its default state.

### Outputs
- `led_M1 [2:0]`: LED signal for M1.
- `led_MT [2:0]`: LED signal for MT.
- `led_M2 [2:0]`: LED signal for M2.
- `led_S [2:0]`: LED signal for S.

## Testbench Details
The testbench (`TF_design_tb`) verifies the design functionality by:
1. Generating a clock signal with a period of 10 time units.
2. Simulating the reset signal to initialize the FSM.
3. Simulating each state for its respective duration.
4. Observing the LED outputs and state transitions.

### Testbench Signals
- **Inputs**: `clk`, `rst`
- **Outputs**: `led_M1`, `led_MT`, `led_M2`, `led_S`

### Waveform Simulation
Run the testbench to observe the following:
- Correct initialization upon reset.
- Accurate state transitions based on time intervals.
- LED outputs matching the expected behavior for each state.

## How to Run
1. Open the design and testbench files in your Verilog simulator.
2. Compile the design (`TF_design`) and testbench (`TF_design_tb`).
3. Run the simulation.
4. Observe the waveforms or outputs for state transitions and LED signals.

### Example Tools
- **ModelSim**
- **Xilinx Vivado**
- **Cadence Xcelium**

## Files in Repository
- `TF_design.v`: Verilog code for the traffic flow FSM.
- `TF_design_tb.v`: Testbench for simulating the FSM.
- `README.md`: Documentation of the project.

## License
This project is licensed under the MIT License. Feel free to use and modify the code as per your needs.

---
Developed by: [Pushkar D](https://github.com/pushkar666)
