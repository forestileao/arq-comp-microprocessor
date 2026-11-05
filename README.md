# Microprocessor (VHDL)

## Overview
A simple VHDL microprocessor with a 14-bit instruction format and a synchronous interface: rst (reset, active-high) and clk (clock). The top-level entity is processor, and the project includes a self-checking testbench named processor_tb under test/.

## ISA
See instructions.txt for the full instruction encodings and examples. At a high level, the core supports:
- Load-immediate to a register
- Register-to-register move
- Integer add and subtract
- Unconditional jump
- Compare plus conditional branches (e.g., not-equal, equal, greater-or-equal)
- RAM load and store via a register pointer

## Directory layout

    mux2x1.vhd        2:1 unsigned data selector
    mux4x1.vhd        4:1 unsigned data selector
    ula.vhd           arithmetic/logic unit
    reg.vhd           16-bit register
    reg_14.vhd        14-bit register
    reg_bank.vhd      8x16-bit register file
    pc.vhd            7-bit program counter with write-enable
    rom.vhd           instruction ROM (14-bit words)
    ram.vhd           data RAM (16-bit words)
    control_unit.vhd  decodes 14-bit instructions and issues control signals
    state_machine.vhd instruction/flag sequencing
    processor.vhd     top-level microprocessor (ports: rst, clk)

    compiled/         GHDL waveform output directory (created/used by flows)
    instructions.txt  ISA summary and encodings
    compile.sh        convenience script to analyze, run, and open GTKWave

    test/
      processor_tb.vhd  top-level testbench for processor

## Prerequisites
- GHDL for analysis/elaboration/simulation.
- GTKWave for viewing VCD/GHW waveforms (optional, GUI-only). In headless or CI environments, skip launching GTKWave.

## Quickstart
Analyze sources and run the top-level testbench with GHDL. All paths are relative to the repository root.

    # Create output directory for the waveform file if needed
    mkdir -p compiled

    # Analyze design units (same order as in compile.sh)
    ghdl -a mux4x1.vhd
    ghdl -a mux2x1.vhd
    ghdl -a ula.vhd
    ghdl -a reg.vhd
    ghdl -a reg_14.vhd
    ghdl -a reg_bank.vhd
    ghdl -a pc.vhd
    ghdl -a rom.vhd
    ghdl -a state_machine.vhd
    ghdl -a control_unit.vhd
    ghdl -a processor.vhd
    ghdl -a ram.vhd

    # Analyze the testbench
    ghdl -a test/processor_tb.vhd

    # Run the testbench and generate a waveform file
    ghdl -r processor_tb --wave=compiled/processor_tb.ghw

Tip: compile.sh provides an all-in-one local flow, ending with gtkwave compiled/processor_tb.ghw. In headless environments (CI/containers/SSH), skip the GTKWave step and use the GHDL commands above.

## Simulation
The GHDL run generates compiled/processor_tb.ghw. To inspect interactively on a desktop:

    gtkwave compiled/processor_tb.ghw

If GTKWave is unavailable or you are on a headless runner, keep to the non-GUI flow shown in Quickstart.

## Example programs
Assembly examples illustrating immediate loads, branching, arithmetic, and RAM access are provided:
- program.asm
- program-branches.asm
- program-primes.asm
- program-test-ram.asm

Refer to instructions.txt for the instruction encodings used by these examples.
