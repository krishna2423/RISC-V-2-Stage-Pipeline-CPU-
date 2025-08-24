RISC-V CPU in Logisim

I built a RISC-V CPU from scratch using Logisim Evolution. The project started with designing the individual components of the processor, then wiring them together into a working datapath, and finally extending it to handle more complex instructions and pipelining.

What I Built

Arithmetic Logic Unit (ALU):
I designed an ALU that supports addition, subtraction, logical operations, comparisons, and shifts. It’s controlled by a multiplexer that selects the right operation based on instruction inputs.

Register File:
I implemented a 32-register file with two read ports and one write port. I made sure x0 always outputs zero, and I exposed useful registers like ra, sp, t0–t2, s0–s1, and a0 so I could see what was going on while debugging.

Immediate Generator:
I created a circuit that extracts immediates from different instruction types and sign-extends them properly. This was crucial for instructions like addi, loads, and branches.

Control Logic:
I wired up a control unit that decodes instructions and drives signals like ASel, BSel, ALUSel, MemRW, WBSel, and others. This allowed the CPU to switch between register, immediate, and memory operations correctly.

Memory Handling:
I added support for word, halfword, and byte loads/stores, along with proper sign and zero extension for partial loads.

Pipelining:
I split the CPU into classic pipeline stages (IF, ID, EX, MEM, WB) and added forwarding and stalling logic to deal with hazards. This let my CPU run faster programs without miscomputing results.

How I Tested

Component Tests:
I used the provided test scripts to check each component individually. For example:

bash test.sh alu
bash test.sh regfile
bash test.sh immediate


This helped me catch small mistakes early before wiring everything together.

Integration Tests:
Once the datapath was working, I ran full program tests with:

bash test.sh cpu
bash test.sh all


These compared my CPU’s outputs to a reference simulator to make sure everything matched.

Custom Programs:
I wrote small RISC-V assembly programs to test tricky cases like branching, hazards, and partial loads. Running them with:

bash test.sh custom myprog.s


helped me confirm the behavior of specific instructions.

Logisim Debugging:
I spent a lot of time stepping through cycles in Logisim, watching pipeline registers and control signals, and probing wires to see exactly where things were going wrong.

What I Learned

This project taught me how the pieces of a CPU actually fit together: how immediates are extracted, how registers and memory interact, how control signals are generated, and how pipelining speeds things up while introducing hazards. Building and debugging the datapath forced me to think about timing, dependencies, and low-level design in a way I hadn’t before.
