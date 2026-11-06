# arq-comp-microprocessor

A simple microprocessor implemented in VHDL with simulation using GHDL and waveform inspection in GTKWave. This page orients newcomers and points to the key files and scripts in the repo.

## Quick start

Prerequisites:
- GHDL (analyzer/simulator)
- GTKWave (waveform viewer)

Build and run the top-level testbench:
```sh
# from the repository root
chmod +x ./compile.sh
./compile.sh
```
The script analyzes the design, compiles `test/processor_tb.vhd`, runs the simulation, and opens `compiled/processor_tb.ghw` in GTKWave.

## Testing

Testbenches live under `test/`.
- The default run uses `test/processor_tb.vhd`.
- Additional unit-level benches are available (for example: `control_unit_tb.vhd`, `reg_bank_tb.vhd`, `ram_tb.vhd`).

To run an individual testbench manually:
```sh
# Example for the processor testbench
# Analyze design files
# (see compile.sh for the authoritative list and order)
ghdl -a *.vhd
# Analyze the chosen testbench
ghdl -a test/processor_tb.vhd
# Run it and emit a waveform
ghdl -r processor_tb --wave=compiled/processor_tb.ghw
# Inspect the waveform
gtkwave compiled/processor_tb.ghw
```

## Project layout

- `compile.sh` — canonical build/run script using GHDL and GTKWave.
- `test/` — VHDL testbenches (e.g., `processor_tb.vhd`, `control_unit_tb.vhd`).
- `compiled/` — generated artifacts such as `.ghw` waveforms.
- `processor.vhd` — top-level processor entity.
- `control_unit.vhd`, `state_machine.vhd` — control path.
- `reg.vhd`, `reg_14.vhd`, `reg_bank.vhd`, `pc.vhd` — registers and program counter.
- `ula.vhd` — ALU (unidade lógica e aritmética).
- `rom.vhd`, `ram.vhd` — instruction and data memories.
- `mux2x1.vhd`, `mux4x1.vhd` — multiplexers.
- `program*.asm` — example programs/fixtures; `instructions.txt` documents the ISA.

## License & contributing

If this repository later adds `LICENSE` or contributing guidelines, consult those files for terms and contribution process.
