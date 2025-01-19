# Section 2: Bringup – What Language Is Hardware Coded In?

## 1. Overview
Section 2 introduces hardware description languages (HDLs)—specifically Verilog. This module builds the foundation for all subsequent hardware design. By the end of Section 2, you’ll have a working simulator setup, and you’ll have written simple Verilog projects that emulate classic “hello world” behavior on hardware.

---

## 2. Prerequisites
- Completion of Section 1 (knowledge of what FPGAs and transistors are, and how emulation works).  
- Basic command-line skills to run Verilator (or another simulator).  

---

## 3. Module Breakdown

### Module 2.1: Blinking an LED (Verilog)
#### Learning Objectives
1. Familiarize yourself with the Verilog syntax and file structure.  
2. Understand how to simulate hardware clock signals.  
3. Create a basic Verilog module that toggles an “LED” signal.

#### Estimated Time Investment
- 1–2 hours for initial exploration and setup.

#### Key Concepts
- Verilog module definition and instantiation.  
- The concept of simulation clocks and time steps.  
- Simple testbench creation.

#### Practical Exercises
- [ ] Write a Verilog module named “blink_led” that toggles a register on every clock cycle.  
- [ ] Create a testbench to verify the LED toggling over time in simulation (using waveforms/log output in Verilator).  
- [ ] Adjust the toggle speed to mimic a real LED blink, verifying timing in simulation.

#### Success Criteria
- You can define a basic Verilog module and write a minimal testbench.  
- You successfully observe a toggling LED waveform in Verilator simulation.

#### Common Pitfalls
- Missing clock or reset signals, leading to undefined simulation behavior.  
- Not properly assigning or driving signals in Verilog modules.

#### Self-Assessment
- “Can I trace the LED signal in a waveform viewer and see it flipping at the expected interval?”  
- “Do I understand how to scale timing to match real hardware cycles in simulation?”

#### Recommended Resources
- Basic Verilog tutorials (online articles, open-source HDL reference guides).  
- Verilator’s user manual sections on setting up waveforms.

---

### Module 2.2: Building a UART (Verilog)
#### Learning Objectives
1. Gain experience with more complex Verilog constructs (state machines, I/O).  
2. Understand the concept of memory-mapped I/O (MMIO).  
3. Implement a UART design that can echo characters and interface with external code or semihosting.

#### Estimated Time Investment
- 3–5 hours for design, coding, and testing.

#### Key Concepts
- UART fundamentals (baud rate, serial data format).  
- State machine design in Verilog.  
- MMIO addressing for data registers and control registers.

#### Practical Exercises
- [ ] Implement a simple UART transmitter and receiver in Verilog.  
- [ ] Write a testbench that simulates incoming data and checks for correct echo output.  
- [ ] Experiment with semihosting or a serial console for interactive testing (if your setup supports it).

#### Success Criteria
- You can demonstrate a UART module in simulation sending and receiving data correctly.  
- You can articulate how this module would map to a real serial port implementation.

#### Common Pitfalls
- Getting baud rate divisors wrong leading to framing errors.  
- Failing to handle buffer states correctly (overruns, underflows).

#### Self-Assessment
- “Can I send a character in the testbench and confirm the same character is returned?”  
- “Do I understand how the UART registers and signals would physically connect to external pins or a USB-serial converter?”

#### Recommended Resources
- Basic UART tutorials to understand framing (start bit, data bits, parity, stop bit).  
- Verilog simulation examples focusing on serial I/O.

---

## 4. Knowledge Validation Checkpoint
By the end of Section 2, you should be able to:
1. Write simple Verilog modules and testbenches.  
2. Simulate digital circuits using a clock signal.  
3. Implement a straightforward UART design and see it operating in a simulated environment.

---

## 5. Review and Reinforcement
- Double-check your blinking LED code and verify it runs smoothly in simulation.  
- Ensure your UART echo test works consistently over multiple inputs.  
- Discuss any challenges with a peer or online community.

---

**You have completed Section 2!** Next, we’ll dive deeper into processor design in Section 3, where you’ll build and simulate your very own ARM7 CPU in Verilog.
