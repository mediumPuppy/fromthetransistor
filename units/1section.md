# Section 1: Introduction to Hardware Fundamentals

## Overview
In this first section, you will gain a high-level understanding of how transistors underlie all modern computing hardware. You'll also see why we use emulation (Verilator or similar) rather than building physical circuits for this course. By the end of Section 1, you should be comfortable with the big-picture concepts of digital logic design and why emulation is a practical gateway to hardware exploration.

> **Resource**: [Introduction to Digital Logic Design](https://ocw.mit.edu/courses/6-004-computation-structures-spring-2017/pages/c1/c1s1/) by MIT OpenCourseWare

## Prerequisites
- Familiarity with basic binary concepts (bits, bytes)
- General understanding of how a computer functions at a conceptual level (CPU, memory, peripherals)

> **Resource**: [Bits, Bytes, and Binary](https://www.khanacademy.org/computing/computers-and-internet/xcae6f4a7ff015e7d:digital-information/xcae6f4a7ff015e7d:bits-and-bytes/a/bits-and-bytes) by Khan Academy

## Module Breakdown

### Module 1.1: So About Those Transistors

#### Learning Objectives
- [ ] Understand the fundamental role of transistors in integrated circuits
- [ ] Recognize how FPGAs simplify digital design without requiring deep transistor-level knowledge
- [ ] Outline the relationship between LUTs (Look-Up Tables) in FPGAs and simpler building blocks

#### Estimated Time Investment
- 1–2 hours of reading and conceptual study

#### Key Concepts
- Transistor as a switch
- FPGA as a reconfigurable collection of LUTs
- Practical reasons to abstract away transistor-level design

#### Practical Exercises
- [ ] Visual Exploration: Watch or read a short tutorial/demonstration for how LUTs are configured in an FPGA
- [ ] Diagram Sketch: Draw a minimal functional block diagram showing how transistors connect into logic gates and then become aggregated in an FPGA

#### Success Criteria
- You can explain, in your own words, how an LUT approximates different logic gates via transistor sets
- You can compare and contrast working at the transistor level vs. working at the FPGA level

#### Common Pitfalls
- Focusing too heavily on transistor physics rather than digital logic design
- Not appreciating how FPGAs let us skip many low-level practicalities

#### Self-Assessment
- "Could I give a layperson a convincing explanation of how a transistor enables digital logic?"
- "Do I grasp how an FPGA uses LUTs to emulate various logical circuits?"

#### Recommended Resources
- Short online lectures about transistor basics
- FPGA vendor documentation (Xilinx, Intel) for high-level FPGA architecture overviews

> **Resources**:
> - [Transistors - Electronics Basics](https://predictabledesigns.com/transistors-introduction/)
> - [FPGA Architecture Overview](https://www.xilinx.com/products/silicon-devices/fpga/what-is-an-fpga.html)

### Module 1.2: Emulation

#### Learning Objectives
- [ ] Appreciate how Verilator or similar tools emulate hardware logic on a standard PC
- [ ] Understand the trade-offs between real hardware deployment and emulation
- [ ] Set up a basic environment or conceptual plan for using a hardware simulator

#### Estimated Time Investment
- 1 hour setup or overview

#### Key Concepts
- Emulation vs. simulation vs. real hardware
- Verilator basics: translating Verilog to a C++/SystemC model for simulation
- Limitations of purely software-based hardware simulation

#### Practical Exercises
- [ ] (Optional/Conceptual) Set up a sample Verilator project and run a trivial test
- [ ] Explore sample outputs (waveforms, logs) to see how logic signals can be observed

#### Success Criteria
- You can explain how Verilator approximates actual hardware behavior
- You can weigh benefits (convenience, lower cost) and drawbacks (performance constraints) of emulation

#### Common Pitfalls
- Confusing emulation with virtualization
- Overlooking timing differences between a software model and real hardware signals

#### Self-Assessment
- "Can I articulate why large-scale hardware courses often rely on emulation to reach more learners?"
- "Am I comfortable with the idea of verifying logic designs via software-based waveforms?"

#### Recommended Resources
- Verilator official documentation and quickstart guides
- Community forums or GitHub examples for simple Verilator projects

> **Resources**:
> - [Verilator User's Guide](https://verilator.org/guide/latest/)
> - [Getting Started with Verilator](https://zipcpu.com/blog/2017/06/21/looking-at-verilator.html)

## Knowledge Validation Checkpoint
By the end of Section 1, you should feel comfortable discussing:
- [ ] The broad role of transistors in computing hardware
- [ ] How FPGA-based design (via LUTs) provides an abstraction away from transistor-level detail
- [ ] Why we use emulation for practical purposes in this course and how Verilator fits into that

> **Resource**: [Digital Design and Computer Architecture](https://safari.ethz.ch/digitaltechnik/spring2020/doku.php?id=schedule) by ETH Zurich

## Review and Reinforcement
- [ ] Revisit your notes on transistors, FPGAs, and emulation
- [ ] If possible, discuss with a peer or study group
- [ ] Optional group activity: present a short explanation about how an FPGA logically stands in for discrete collections of transistors

> **Resource**: [FPGA Design Flow Overview](https://www.intel.com/content/www/us/en/docs/programmable/683684/current/design-flow.html)

---

**You have completed Section 1!** Next, we'll move into writing and running actual hardware-coded programs in Verilog, starting with simple "hello world" style blinking LED scenarios—only we'll do them in simulation first.

## Citations
[1-63] *Citations preserved but formatted as footnotes or endnotes if needed*
