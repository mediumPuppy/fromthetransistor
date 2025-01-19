# Section 4: Compiler – A “High” Level Language

## 1. Overview
Section 4 scales the abstraction ladder by introducing you to writing a C compiler from scratch in Haskell. You’ll also create a simple linker in Python, implement core parts of the standard C library (libc), and develop an Ethernet controller and bootloader. By the end of this section, you’ll have a working compilation toolchain, a network-capable hardware design, and a rudimentary environment for loading and running C programs on your custom CPU.

---

## 2. Prerequisites
- Completion of Section 3 (functioning CPU core and assembler).  
- Basic familiarity with Haskell syntax and functional programming concepts.  
- Intermediate Python skills for creating the linker.  
- Some C programming knowledge.

---

## 3. Module Breakdown

### Module 4.1: Building a C Compiler (Haskell)
#### Learning Objectives
1. Understand compiler design fundamentals (lexing, parsing, semantic analysis, code generation).  
2. Write a small, self-contained C compiler that outputs ARM assembly.  
3. Learn how to manage compiler phases in a functional programming paradigm.

#### Estimated Time Investment
- About 2–3 weeks (this is a more complex project).

#### Key Concepts
- Lexing and parsing C syntax in Haskell.  
- Generating ARM assembly code for your CPU design.  
- Managing symbol tables, scopes, and basic optimizations (if time permits).

#### Practical Exercises
- [ ] Implement a lexer/parser that can handle a subset of C (e.g., basic expressions, functions, control flow).  
- [ ] Generate ARM assembly for simple examples (factorial, fibonacci).  
- [ ] Produce object code that matches your custom assembler/linker flow.

#### Success Criteria
- Your compiler can compile small C programs into ARM assembly correctly.  
- You can integrate the output with your Python assembler (from Section 3) or a pipeline where the compiler outputs assembly, which is then assembled and tested on your CPU.

#### Common Pitfalls
- Underestimating how much of the C grammar you need to support.  
- Handling corner cases (pointer arithmetic, tricky control flow constructs).

#### Self-Assessment
- “Can I compile a basic C function (like a loop) and see the correct instructions in my CPU simulation?”  
- “Do I feel comfortable refining or extending the compiler if a new feature is needed?”

#### Recommended Resources
- Compiler textbooks (“Compilers: Principles, Techniques, and Tools” or similar).  
- Haskell parsing libraries (e.g., Parsec or Megaparsec) and tutorials.

---

### Module 4.2: Building a Linker (Python)
#### Learning Objectives
1. Understand how object files are merged into a single executable.  
2. Manipulate symbol tables, relocations, and address space management.  
3. Output an ELF file or a suitable format for your CPU environment.

#### Estimated Time Investment
- 1–2 days to design and implement.  
- Additional time for integration testing.

#### Key Concepts
- Linking object files with their symbols and sections.  
- Handling relocations for external references.  
- Executable file format basics (e.g., ELF header structure).

#### Practical Exercises
- [ ] Write a Python script to merge multiple object files (assembled by your tools).  
- [ ] Handle symbol resolution, relocations, and finalize addresses.  
- [ ] Output an ELF (or a minimal custom) format for use with QEMU or your simulator.

#### Success Criteria
- Your linker produces valid, loadable executables recognized by your bootloader or CPU environment.  
- Symbol references across multiple modules (e.g., function calls) are properly resolved.

#### Common Pitfalls
- Mixing up different sections (e.g., .text, .data, .bss).  
- Not handling relocations for instructions that reference external symbols.

#### Self-Assessment
- “Can I take two or more separately assembled modules and produce a single binary that runs on my CPU?”  
- “Do I understand how addresses get fixed up at link time?”

#### Recommended Resources
- ELF file specifications or simpler custom loader documentation.  
- Python tutorials on binary file handling.

---

### Module 4.3: libc + malloc (C)
#### Learning Objectives
1. Implement minimal C library functions (e.g., memcpy, memset, printf).  
2. Write a simple heap allocator (malloc/free).  
3. Increase the complexity of programs you can run.

#### Estimated Time Investment
- 1–2 weeks, depending on how many libc functions you plan to support.

#### Key Concepts
- Basic I/O stubs or “semihosting” to bridge with your environment.  
- Internal memory management for dynamic allocations.  
- Understanding of how higher-level library calls relate to system calls (which your OS will eventually handle).

#### Practical Exercises
- [ ] Implement string and memory functions (memcpy, strcpy, memset, etc.).  
- [ ] Implement a simple malloc/free mechanics with a contiguous heap region.  
- [ ] Write test programs (e.g., dynamic data structures) to verify correct library behavior.

#### Success Criteria
- You can compile a C program that uses standard functions like printf and dynamic allocations, and run it on your CPU.  
- Memory operations work as expected without corruption or crashes in your simulation.

#### Common Pitfalls
- Failing to initialize or track free vs. allocated memory properly.  
- Assuming advanced OS-level features that aren’t yet implemented.

#### Self-Assessment
- “Am I testing enough real use-cases (like strings, arrays, etc.) with my library?”  
- “Do my memory usage patterns stay coherent under repeated allocations and frees?”

#### Recommended Resources
- Any open-source minimal libc implementations (for reference).  
- Basic memory allocation algorithms (e.g., a simple bump allocator or a free-list allocator).

---

### Module 4.4: Building an Ethernet Controller (Verilog)
#### Learning Objectives
1. Learn to design a network interface hardware module.  
2. Extend and refine your system bus/MMIO interface to accommodate network traffic.  
3. Handle PHY-level considerations (if simulating or interfacing with a model).

#### Estimated Time Investment
- 2–3 days of Verilog design and integration, plus debugging.

#### Key Concepts
- Ethernet fundamentals (frames, MAC addresses, Rx/Tx buffers).  
- MMIO registers for configuration and status.  
- Simple state machines to handle DMA or direct memory buffering.

#### Practical Exercises
- [ ] Implement transmit/receive logic in Verilog with a minimal buffer.  
- [ ] Write a testbench that simulates network traffic input and checks your module’s output frames.  
- [ ] Plan how software (running in your CPU) will access the Ethernet controller (read/write register interface).

#### Success Criteria
- You can send a simulated Ethernet frame and confirm it is received or echoed back properly.  
- The MMIO interface integrates smoothly with your CPU design (no address conflicts or bus timing issues).

#### Common Pitfalls
- Managing buffer pointers and data alignment.  
- Handling asynchronous Ethernet clock domains, if your simulation tries to replicate real-world timing.

#### Self-Assessment
- “Do I see frames correctly formed, and do they conform to Ethernet size and format rules?”  
- “Have I tested edge cases like undersized or oversized frames?”

#### Recommended Resources
- Standard documentation on Ethernet framing and MAC layer specifics.  
- Examples of simple Ethernet MAC designs for FPGAs.

---

### Module 4.5: Writing a Bootloader (C)
#### Learning Objectives
1. Create a small piece of software that can initialize the network and load a kernel or user program from Ethernet.  
2. Understand how to incorporate your new Ethernet module into a real boot flow.  
3. Build a flexible process to switch between serial or network booting.

#### Estimated Time Investment
- Approximately 2–3 days of implementation and testing.

#### Key Concepts
- Network boot protocol fundamentals (e.g., UDP-based downloading).  
- Setting up hardware (Ethernet controller, CPU state, memory) before loading user code.  
- Handling error conditions (timeouts, invalid packets).

#### Practical Exercises
- [ ] Write a simple bootloader in C that configures the Ethernet controller and listens for a kernel image via UDP.  
- [ ] Integrate bootloader into your existing boot process (the assembly boot ROM jumps here, then the bootloader takes over).  
- [ ] Validate that the downloaded code is placed in RAM at the correct address and then jumped to.

#### Success Criteria
- You can reliably boot from Ethernet in your simulation environment.  
- The bootloader transitions control to a newly loaded program without crashing.

#### Common Pitfalls
- Incorrect initialization of Ethernet controller delays or register settings.  
- Packet parsing logic mishandling corner cases (e.g., partial or fragmented packets).

#### Self-Assessment
- “Can I reliably load a small program via network and see it run?”  
- “Do I feel comfortable modifying the bootloader to add new features or boot sources?”

#### Recommended Resources
- UDP reference for minimal packet-based data transfer.  
- Bootloader examples from embedded systems or open-source projects.

---

## 4. Knowledge Validation Checkpoint
By the end of Section 4, you should be able to:
1. Write and maintain a functional C compiler in Haskell.  
2. Generate and link object files into executable images for your custom ARM environment.  
3. Integrate networking capability into a bootloader, culminating in an Ethernet-based program load.

---

## 5. Review and Reinforcement
- Compile multiple test programs with your new C toolchain, ensuring correct linking and execution.  
- Run performance or stress tests on the Ethernet module (within the limitations of simulation).  
- Discuss your experiences in a study group or online forum; share tips and troubleshoot tricky compiler or linker bugs.

---

**You have completed Section 4!** Next, we’ll move on to Section 5, where you will venture deeper into operating system design and implement essential system calls, user space threading, and more.
