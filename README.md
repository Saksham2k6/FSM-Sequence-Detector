# Sequence Detector FSM

A SystemVerilog-based implementation of a **1111 sequence detector** using finite state machines (FSMs).

This project implements the detector using both **Moore and Mealy FSM architectures**, with support for **overlapping and non-overlapping detection**. A Cocotb testbench is included to verify the RTL implementations through simulation.

## Overview

The detector monitors a serial binary input and asserts the output when the sequence **1111** is detected.

Four FSM variants are implemented:

* Moore FSM — Overlapping
* Moore FSM — Non-overlapping
* Mealy FSM — Overlapping
* Mealy FSM — Non-overlapping

The project was developed to compare the behavior of these FSM architectures and understand the practical differences between Moore and Mealy implementations, particularly in terms of state transitions and output generation.

## Features

* Detection of the `1111` bit sequence
* Moore and Mealy FSM architectures
* Overlapping sequence detection
* Non-overlapping sequence detection
* Synchronous state-machine operation
* Active-low asynchronous reset
* SystemVerilog RTL implementation
* Cocotb-based functional verification
* VCD waveform generation for simulation analysis

## RTL Implementations

| Module                | FSM Type | Detection       |
| --------------------- | -------- | --------------- |
| `moore_overlap.sv`    | Moore    | Overlapping     |
| `moore_nonoverlap.sv` | Moore    | Non-overlapping |
| `mealy_overlap.sv`    | Mealy    | Overlapping     |
| `mealy_nonoverlap.sv` | Mealy    | Non-overlapping |

### Moore FSM

In the Moore implementations, the detector output depends only on the **current FSM state**. A dedicated state represents successful detection of the `1111` sequence.

### Mealy FSM

In the Mealy implementations, the detector output depends on the **current state and input**. This allows the sequence detection to occur directly during a state transition.

### Overlapping vs Non-overlapping

The overlapping versions allow a newly detected sequence to share bits with the next sequence.

For example, an input stream containing:

`11111`

can contain two overlapping occurrences of `1111`.

The non-overlapping versions return to the appropriate initial state after detecting a sequence, preventing the detected bits from being reused for another detection.

## Verification

Functional verification is performed using **Cocotb**. The testbench applies input sequences to the different implementations and checks their output behavior.

The verification covers:

* Moore overlapping detector
* Moore non-overlapping detector
* Mealy overlapping detector
* Mealy non-overlapping detector

Simulation waveforms are generated in **VCD format**, allowing signal transitions and FSM behavior to be inspected using waveform viewers such as GTKWave.

## Tools and Technologies

* **SystemVerilog** — RTL design
* **Cocotb** — Functional verification
* **Icarus Verilog / ModelSim / Vivado Simulator** — Simulation
* **GTKWave** — Waveform analysis

## Learning Outcomes

This project provided practical experience with:

* Designing finite state machines from sequence-detection requirements
* Implementing Moore and Mealy FSMs
* Understanding overlapping and non-overlapping sequence detection
* Writing synthesizable SystemVerilog RTL
* Using `always_ff` and `always_comb`
* Developing a Cocotb-based verification environment
* Analyzing simulation waveforms and FSM state transitions
* Comparing different RTL implementations of the same digital function
