# Microprocessor (VHDL)

## Overview
A simple VHDL microprocessor with a 14-bit instruction format and a synchronous interface:  (reset, active-high) and  (clock). The top-level entity is , and the project includes a self-checking testbench  under .

## ISA
See  for the full instruction encodings and examples. At a high level, the core supports:
- Load-immediate to a register
- Register-to-register move
- Integer add and subtract
- Unconditional jump
- Compare plus conditional branches (e.g., not-equal, equal, greater-or-equal)
- RAM load and store via a register pointer

## Directory layout
processor

## Prerequisites
- GHDL for analysis/elaboration/simulation.
- GTKWave for viewing VCD/GHW waveforms (optional, GUI-only). In headless or CI environments, skip launching GTKWave.

## Quickstart
Analyze sources and run the top-level testbench with GHDL. All paths are relative to the repository root.



Tip:  provides an all-in-one local flow, ending with . In headless environments (CI/containers/SSH), skip the GTKWave step and use the GHDL commands above.

## Simulation
The GHDL run generates . To inspect interactively on a desktop:



If GTKWave is unavailable or you are on a headless runner, keep to the non-GUI flow shown in Quickstart.

## Example programs
Assembly examples illustrating immediate loads, branching, arithmetic, and RAM access are provided:
- 
- 
- 
- 

Refer to  for the instruction encodings used by these examples.
