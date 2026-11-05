# Microprocessor (VHDL)

A compact VHDL microprocessor with a 14-bit ISA. Top entity: processor (ports: rst, clk). The self-checking testbench is at test/processor_tb.vhd.

## Quick Start
- Install GHDL. Install GTKWave if you want to view waveforms.
- From the repo root, run:

      ./compile.sh

This analyzes the design, runs the testbench, produces compiled/processor_tb.ghw, and (on desktops) opens it in GTKWave.

Tip: on headless runners without GTKWave, run ./compile.sh to build and simulate; ignore the final GTKWave step if it cannot launch.

## ISA & Examples
- See instructions.txt for the instruction encodings and a short ISA overview.
- Example assembly programs: program.asm, program-branches.asm, program-primes.asm, program-test-ram.asm.
