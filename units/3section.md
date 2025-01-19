# Section 3: Processor – What Is a Processor Anyway?

## 1. Overview
Section 3 delves into processor design and the low-level mechanics of executing code. You will build an assembler in Python, design and simulate an ARM7-like CPU core in Verilog, and write a minimal boot ROM in assembly. By the end of this section, you’ll have a functional simulated environment capable of running simple bootstrapped programs.

---

## 2. Prerequisites
- Completion of Section 2 (ability to write and simulate Verilog).
- Basic competence in Python scripting.
- Familiarity with ARM assembly syntax (will be further developed in this section).

---

## 3. Module Breakdown

### Module 3.1: Coding an Assembler (Python)
#### Learning Objectives
1. Understand the essentials of assembly language parsing.  
2. Gain exposure to how machine instructions are encoded into binary.  
3. Develop a basic assembler pipeline (read → parse → encode → write output).

#### Estimated Time Investment
- 3–5 hours for design and implementation, plus testing.

#### Key Concepts
- Lexical analysis: splitting input assembly into tokens.  
- Instruction set encoding for ARM7.  
- Translating labels and directives into addresses and data.

#### Practical Exercises
- [ ] Create a Python script that reads simple ARM assembly instructions and outputs a binary file.  
- [ ] Implement basic error handling (e.g., unknown instructions, malformed lines).  
- [ ] Test with a simple “hello world” type of assembly routine (even if just a few instructions).

#### Success Criteria
- You can assemble a sequence of ARM instructions into a correctly formatted binary file.  
- You can confirm the assembled output matches expected machine codes via a reference or documentation.

#### Common Pitfalls
- Mishandling labels and branch offsets.  
- Overlooking endianness issues.

#### Self-Assessment
- “Do I fully understand the instruction fields for ARM7?”  
- “Can I easily modify my assembler to support additional instructions if needed?”

#### Recommended Resources
- ARM Architecture Reference Manual (ARMv4T/ARMv5).  
- Basic Python references for text parsing and file I/O.

---

### Module 3.2: Building an ARM7 CPU (Verilog)
#### Learning Objectives
1. Understand pipeline stages (fetch, decode, execute, etc.).  
2. Implement a simplified ARM7-like CPU in Verilog.  
3. Address memory organization (instruction memory, data memory, registers).

#### Estimated Time Investment
- 1–2 weeks, depending on your familiarity with CPU design and debugging.

#### Key Concepts
- Pipelining basics (hazards, forwarding).  
- Register file mapping and memory interfaces.  
- Handling pipeline stages in Verilog (stall, flush logic).

#### Practical Exercises
- [ ] Outline an ARM7 pipeline architecture (simplified).  
- [ ] Implement the register file, ALU, and basic control logic in Verilog.  
- [ ] Build a testbench that loads a small, pre-assembled program into memory.  
- [ ] Simulate CPU fetch/execute cycles and verify correct instruction execution.

#### Success Criteria
- The CPU executes a test program (assembled with your Python tool) and produces the expected results (e.g., specific register values).  
- Pipeline hazards are handled (or simplified) correctly so that instructions execute in the right order.

#### Common Pitfalls
- Underestimating the complexity of pipelined CPU logic.  
- Not thoroughly testing branching, load/store instructions, or pipeline hazards.

#### Self-Assessment
- “Am I confident that each pipeline stage is synchronized correctly?”  
- “Can I trace signals in the pipeline to diagnose any mis-executed instruction?”

#### Recommended Resources
- Verilog coding examples of simple pipelined microprocessors.  
- ARM architecture references (especially pipeline operation topics).

---

### Module 3.3: Coding a Boot ROM (Assembler)
#### Learning Objectives
1. Write a minimal assembly routine for initializing hardware on reset.  
2. Implement a small bootloader-like sequence to load code into RAM.  
3. Integrate the boot ROM into your Verilog CPU design.

#### Estimated Time Investment
- 1–2 hours of assembly coding and debug.

#### Key Concepts
- Reset vectors and CPU startup sequence.  
- Simple load mechanism (serial or memory map).  
- Ensuring the boot ROM is recognized by your CPU design at startup.

#### Practical Exercises
- [ ] Write a short assembly program that initializes registers and memory, then jumps to a known location in RAM.  
- [ ] Integrate the boot ROM image into your CPU’s memory map within the Verilog simulation.  
- [ ] Verify that after reset, the CPU fetches and runs the boot ROM instructions without error.

#### Success Criteria
- The CPU successfully reads and executes the boot ROM code at reset.  
- Basic system initialization (e.g., zeroing out data sections, setting stack pointer) is evident in simulation logs.

#### Common Pitfalls
- Incorrect ROM placement in memory mapping.  
- Failing to handle CPU reset signals, causing undefined instruction fetch at startup.

#### Self-Assessment
- “Do I see the CPU’s PC (program counter) fetching instructions from the boot ROM as expected?”  
- “Does the program jump to the correct address for user code?”

#### Recommended Resources
- Example minimal boot code for ARM-based microcontrollers.  
- Discussion threads on embedded forums showing typical startup sequences.

---

## 4. Knowledge Validation Checkpoint
By the end of Section 3, you should be able to:
1. Write a basic Python assembler that outputs valid ARM7 machine code.  
2. Describe and implement the key parts of a pipelined CPU in Verilog.  
3. Integrate a boot ROM to initialize your custom CPU design at reset.

---

## 5. Review and Reinforcement
- Revisit and refine your assembler: add or fix instructions as needed.  
- Step through your CPU in simulation, verifying every pipeline stage for a sample program.  
- Confirm that your boot code runs correctly from reset, setting the stage for real or simulated memory loads.

---

**You have completed Section 3!** In the next section, you will explore compilers and take another step up the abstraction ladder by creating a simple C compiler in Haskell, linking your code, and expanding your system’s functionality.
