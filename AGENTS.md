**Purpose**
- Give an AI coding agent clear, minimal rules for working in this VHDL microprocessor project.
- Keep guidance consistent across repos while noting project‑specific run and test commands.

**Scope**
- Applies to all files in the repository root and test/.
- The agent may create or edit source, tests, and scripts that improve build/test reliability.
- Do not change licensing, authorship, or introduce external services without maintainers’ approval.

**Repository Layout Highlights**
- VHDL sources live in the repository root (*.vhd).
- Testbenches live under test/ (e.g., test/processor_tb.vhd).
- Waveforms are written to compiled/*.ghw by the provided script.
- Assembly examples live in *.asm and are used by the ROM.

**Run**
- Prerequisites: bash, ghdl (VHDL simulator), and optionally gtkwave for viewing waveforms.
- Fast path (simulates the top‑level testbench and opens the waveform):
  - chmod +x ./compile.sh
  - ./compile.sh
- Headless run (no GUI):
  - ghdl -a mux4x1.vhd mux2x1.vhd ula.vhd reg.vhd reg_14.vhd reg_bank.vhd pc.vhd rom.vhd state_machine.vhd control_unit.vhd processor.vhd ram.vhd
  - ghdl -a test/processor_tb.vhd
  - ghdl -r processor_tb --wave=compiled/processor_tb.ghw

**Test**
- Static checks: ghdl -s *.vhd test/*.vhd
- Example targeted testbench run (produces a waveform file):
  - ghdl -a *.vhd && ghdl -a test/control_unit_tb.vhd
  - ghdl -r control_unit_tb --wave=compiled/control_unit_tb.ghw
- CI note: GUI tools aren’t required; validate by ensuring GHDL runs succeed and .ghw files are produced.

**Lint/Format**
- No dedicated formatter is configured. Keep lines readable and wrap long expressions.
- Use ghdl -s to catch syntax issues early.

**Build/CI**
- No CI is defined in this repo. If you add CI, prefer non‑GUI runs using ghdl only.

**Coding Conventions and Naming**
- Filenames and identifiers use lower_snake_case (e.g., reg_bank.vhd).
- Prefer explicit std_logic/std_logic_vector widths and numeric_std conversions.
- Keep testbench clocks, resets, and stop‑time logic simple and self‑contained.
- One entity per file; architecture immediately follows the entity.

**Decision Records (optional)**
- If a non‑obvious architecture or interface choice is made, add a short note at docs/decisions/YYYY-MM-DD-slug.md.

**Secrets Policy**
- Do not commit secrets, credentials, or machine‑specific paths. Scripts must not hard‑code usernames or tokens.

**PR Checklist**
- Run: ./compile.sh completes without errors (or the headless sequence above).
- Tests: representative testbenches execute; generated .ghw is valid.
- No unneeded files in compiled/ besides wave outputs needed for review.
- No secrets or tokens added; no license or authorship changes.
- Documentation updated if commands or structure changed.

**How to Update This File**
- Keep sections concise. Update Run/Test commands if scripts change.
- Stay under 200 lines and avoid placeholders. Reflect actual project behavior.
