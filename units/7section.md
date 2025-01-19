# Section 7: Physical – Running on Real Hardware

## 1. Overview
Section 7 is the culmination of everything learned, as you bring your simulated system onto an actual FPGA board. You’ll design and assemble the necessary hardware, connect all relevant peripherals, and verify everything from your Verilog CPU to your operating system is running as intended in the physical world. By the end of this section, you should have a working FPGA-based computer system, capable of blinking LEDs, loading an OS, handling network traffic, and displaying a simple interactive environment.

---

## 2. Prerequisites
- Completion of Section 6 (fully functional OS with networking, PC-based simulation tested).  
- Familiarity with or willingness to learn FPGA board design and basic electronics assembly.  
- Access to an appropriate FPGA development setup (or custom board you design/assemble).

---

## 3. Module Breakdown

### Module 7.1: Talking to an FPGA (C) – USB MCU & JTAG
#### Learning Objectives
1. Understand how programming an FPGA works through JTAG or other relevant protocols.  
2. Implement or customize a small USB microcontroller (MCU) program that drives JTAG signals.  
3. Integrate your existing workflow so the compiled bitstream can be flashed onto the FPGA.

#### Estimated Time Investment
- 2–4 days for software and hardware integration.

#### Key Concepts
- JTAG protocol basics (TCK, TMS, TDI, TDO).  
- USB-to-JTAG bridging via MCUs (e.g., Cypress, STM32, or similar).  
- Generating FPGA configuration files from your Verilog code.

#### Practical Exercises
- [ ] Write or adapt a C program on your chosen USB MCU that toggles JTAG lines based on incoming USB commands.  
- [ ] Verify you can upload a bitstream to the FPGA reliably.  
- [ ] Confirm basic communication between the MCU, FPGA, and your PC host software.

#### Success Criteria
- You can successfully write your hardware design bitstream to the FPGA and have it power up and run your CPU logic.  
- The FPGA enumerates or signals “done” when the bitstream is loaded, and it responds to real hardware signals (e.g., LED toggles).

#### Common Pitfalls
- Incorrect pin assignments or timings for JTAG signals.  
- Overcomplicating the USB bridging code when a simpler approach might suffice.

#### Self-Assessment
- “Do I see the correct handshake and state transitions in the JTAG TAP (Test Access Port)?”  
- “Can I reflash the FPGA multiple times without error?”

#### Recommended Resources
- FPGA vendor documents (Altera/Intel, Xilinx) on bitstream formats and JTAG protocols.  
- Community examples of USB-JTAG bridges.

---

### Module 7.2: Building an FPGA Board (Hardware Design)
#### Learning Objectives
1. Design or assemble a custom FPGA board that includes essential components: flash memory, clock, power regulation, and peripherals (Ethernet, SD card, serial console).  
2. Understand PCB layout basics for high-speed signals and BGA packages.  
3. Gain experience in reflow soldering or alternative assembly methods.

#### Estimated Time Investment
- Several weeks (design, ordering parts, assembly, testing) if done from scratch.

#### Key Concepts
- FPGA packaging (BGA, pin assignments, configuration modes).  
- Required power rails and voltage regulation for the FPGA core, I/O, and other peripherals.  
- Handling signals for Ethernet PHY, SD card lines, and other connectors.

#### Practical Exercises
- [ ] Create a schematic that includes an FPGA, its configuration flash, a 50 MHz clock source, power circuits, USB JTAG interface, SD card slot, and Ethernet port.  
- [ ] Prepare a PCB layout ensuring correct trace lengths, routing, and signal integrity.  
- [ ] Reflow solder or otherwise assemble the board and test for basic power-up functionality (LED indicators, stable voltages, etc.).

#### Success Criteria
- Your new FPGA board successfully powers on with stable supply rails, and the FPGA configures from flash or external JTAG.  
- The board exposes the necessary I/O for your CPU design, providing a working physical environment.

#### Common Pitfalls
- Shorts or opens under BGA packages make debugging extremely difficult.  
- Inadequate decoupling for FPGA power lines leading to unstable operation.

#### Self-Assessment
- “Am I certain each voltage rail is within spec, and the FPGA properly receives a clean clock signal?”  
- “Have I tested basic communications (e.g., serial or debug LEDs) before attempting the full system?”

#### Recommended Resources
- Manufacturer-specific hardware design guides for chosen FPGA family.  
- PCB layout tutorials focused on high-speed digital design.

---

### Module 7.3: Bringup – Compiling and Downloading the Verilog for the Board
#### Learning Objectives
1. Synthesize your Verilog CPU and peripheral modules for the target FPGA.  
2. Replace the simulation environment with actual hardware signals (clocks, resets, I/O).  
3. Validate functionality step by step—blinking an LED, serial console, Ethernet, OS boot, etc.

#### Estimated Time Investment
- 1–2 weeks of iterative debugging and testing.

#### Key Concepts
- FPGA synthesis flow vs. simulation flow.  
- Constraints files for pin assignments and timing specifications.  
- Incremental hardware debugging (test simplest functionality first).

#### Practical Exercises
- [ ] Generate an FPGA synthesis project with pin constraints matching your board design.  
- [ ] Load the bitstream onto the FPGA and confirm a basic LED blink or UART echo.  
- [ ] Integrate each subsystem (SD card, Ethernet, etc.) step by step, verifying correct operation before adding more complexity.

#### Success Criteria
- Your entire system—from the CPU to the OS—runs on the physical board, demonstrating the same functionality you had in simulation.  
- You can connect via serial or Ethernet, load programs, and interact with the OS in a real environment.

#### Common Pitfalls
- Timing constraints that pass in simulation but fail in physical hardware (e.g., setup/hold violations).  
- Overlooking board-level quirks (like different oscillator frequencies or out-of-spec signals).

#### Self-Assessment
- “Can I do a partial bringup approach, verifying each peripheral individually before integrating the OS?”  
- “Does my system remain stable for extended runtime, or do I see sporadic hardware issues?”

#### Recommended Resources
- FPGA vendor’s synthesis and place-and-route tools (e.g., Quartus, Vivado).  
- Online communities offering bringup checklists and troubleshooting tips.

---

## 4. Knowledge Validation Checkpoint
By the end of Section 7, you should:
1. Have a custom FPGA board or a configured development kit running your CPU architecture.  
2. Achieve verified hardware-level functionality for CPU, memory, networking, and SD storage.  
3. Boot and interact with your custom OS on real hardware, not just in simulation.

---

## 5. Review and Reinforcement
- Document your board design process thoroughly for future revisions.  
- Confirm all major functionalities (Ethernet, SD, serial) are operational on hardware.  
- Reflect on the journey from transistor concepts through to a physical, running system—an impressive achievement!

---

**You have completed Section 7!** At this point, you have a full-stack computer system that you designed, implemented, and deployed—ranging from the transistor abstraction in FPGAs up to a functioning web browser on your custom OS!  
