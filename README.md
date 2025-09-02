RISC-V CPU in Logisim
Overview:

- This project involved building a RISC-V CPU from scratch using Logisim Evolution. It began with the design of individual processor components, followed by integration into a complete datapath, and was later extended with a two-stage pipeline for improved performance.

What Was Built:

Arithmetic Logic Unit (ALU):
- Designed an ALU supporting addition, subtraction, logical operations, comparisons, and shifts. Controlled by a multiplexer that selects the correct operation based on instruction inputs.

Register File:
- Implemented a 32-register file with two read ports and one write port. Ensured that x0 always outputs zero and exposed key registers such as ra, sp, t0–t2, s0–s1, and a0 for debugging.

Immediate Generator:
- Built a circuit that extracts immediates from different instruction types and sign-extends them properly. Supported instructions such as addi, loads, and branches.

Control Logic:
- Designed a control unit to decode instructions and drive signals like ASel, BSel, ALUSel, MemRW, and WBSel. Enabled the CPU to switch correctly between register, immediate, and memory operations.

Memory Handling:
- Added support for word, halfword, and byte loads/stores with proper sign and zero extension for partial loads.

Two-Stage Pipelining:
- Divided the CPU into two stages: Instruction Fetch/Decode (IF/ID) and Execute/Memory/Writeback (EX/MEM/WB). Added forwarding and basic stalling logic to handle hazards, allowing faster program execution without compromising correctness.

How It Was Tested:

Component Tests:
- Verified each component individually with provided scripts, e.g.:

  bash test.sh alu
  bash test.sh regfile
  bash test.sh immediate


Integration Tests:
- Validated the complete datapath by running program-level tests, e.g.:

  bash test.sh cpu
  bash test.sh all


Outputs were compared to a reference simulator to ensure correctness.

Custom Programs:
- Wrote RISC-V assembly programs to test edge cases like branching, hazards, and partial loads. For example:

  bash test.sh custom myprog.s


Logisim Debugging:
- Stepped through cycles in Logisim, monitored pipeline registers and control signals, and probed wires to trace and fix errors.
