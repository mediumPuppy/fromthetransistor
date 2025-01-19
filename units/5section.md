# Section 5: Operating System – The Software We Take for Granted

## 1. Overview
Section 5 pulls together everything you've done so far to build a simple UNIX-like operating system for your custom hardware environment. You’ll implement an MMU for memory translation, create a kernel that manages processes and threads, and add basic filesystem support. By the end of this section, you’ll have a rudimentary but functional OS environment that can run multiple programs, handle I/O, and even interact with an SD card and a FAT filesystem.

---

## 2. Prerequisites
- Completion of Section 4 (functional C compiler, linker, bootloader, and Ethernet interface).  
- Intermediate C coding skills.  
- Familiarity with basic operating system concepts (processes, threads, file I/O).

---

## 3. Module Breakdown

### Module 5.1: Building an MMU (Verilog)
#### Learning Objectives
1. Implement memory management features (paging or segmentation) in hardware.  
2. Understand how ARM9-like TLBs (Translation Lookaside Buffers) handle virtual-to-physical address translation.  
3. Integrate MMU control registers and logic into your CPU pipeline.

#### Estimated Time Investment
- 1–2 weeks (hardware design + integration testing).

#### Key Concepts
- Virtual memory and page tables.  
- TLB entries and handling TLB misses.  
- New CPU signals or control logic to manage memory translation.

#### Practical Exercises
- [ ] Outline a simple page table structure (e.g., single-level or two-level).  
- [ ] Modify the Verilog CPU to include address translation before instruction fetch and data access.  
- [ ] Write test routines that switch from a flat memory model to paged memory, verifying correct address translation in simulation.

#### Success Criteria
- You can run a simple test program that uses virtual addresses, and the MMU correctly translates them to physical memory.  
- TLB faults or misses trigger the correct fallback logic (e.g., a kernel-mode exception).

#### Common Pitfalls
- Forgetting to invalidate or synchronize TLB entries when changes occur.  
- Improper handling of kernel-mode vs. user-mode permissions.

#### Self-Assessment
- “Can I follow the path of an address through the CPU pipeline as it’s translated?”  
- “Do I handle edge cases (e.g., addresses outside valid ranges) without crashing?”

#### Recommended Resources
- ARM9/ARMv5 Architecture Reference Manual (detailing TLB flow).  
- Other minimal OS or microkernel projects that show simple MMU setups.

---

### Module 5.2: Building an Operating System (C)
#### Learning Objectives
1. Design and implement a simple UNIX-like kernel that supports user space processes.  
2. Integrate system calls for file I/O and process management (fork, execve, wait, sleep, exit).  
3. Add minimal concurrency with user space threads (optional advanced exercise).

#### Estimated Time Investment
- 2–3 weeks for kernel design, coding, and debugging.

#### Key Concepts
- System call interface and kernel-user transitions.  
- Process creation, scheduling, context switching.  
- Basic concurrency mechanisms (mutexes, semaphores) if desired.

#### Practical Exercises
- [ ] Implement at least these system calls: open, read, write, close, fork, execve, wait, sleep, exit.  
- [ ] Create a simple scheduler that switches between processes in round-robin or priority-based fashion.  
- [ ] Write a user space test program that spawns child processes, reads/writes files, and prints results to the console.

#### Success Criteria
- Multiple processes can run concurrently and perform basic file I/O.  
- Scheduling, context switching, and system call entry/exit all work without corruption or crashes.

#### Common Pitfalls
- Incorrect saving/restoring of CPU registers and memory mappings during context switching.  
- Not properly synchronizing shared kernel data structures, leading to race conditions.

#### Self-Assessment
- “Can I spawn a second process that executes its own code and returns to the parent?”  
- “Do I handle edge cases like failed exec or missing files gracefully?”

#### Recommended Resources
- General OS textbooks (e.g., “Operating System Concepts”).  
- Tutorials or references on writing minimal UNIX-like kernels.

---

### Module 5.3: Talking to an SD Card (Verilog)
#### Learning Objectives
1. Implement and integrate an SD card interface in hardware.  
2. Understand SD card protocol basics (SPI mode vs. native SD mode).  
3. Use this interface as a secondary storage medium for your OS.

#### Estimated Time Investment
- 1 week (hardware + basic driver integration).

#### Key Concepts
- SD card initialization sequence.  
- Reading and writing blocks from/to the card.  
- Timing and signal considerations (SPI or SD bus signals).

#### Practical Exercises
- [ ] Implement a compact Verilog SD card controller (preferably SPI-based for simplicity).  
- [ ] Write a kernel driver for reading blocks from the SD card.  
- [ ] Test reading/writing raw blocks as a precursor to filesystem support.

#### Success Criteria
- Your OS can detect an SD card and read data from known locations.  
- Block-level I/O works consistently, with no data corruption in simulation or on real hardware (if available).

#### Common Pitfalls
- Failing to match the SD card’s expected clock speeds or command/response format.  
- Incorrectly handling responses for card initialization (timeouts, card busy states).

#### Self-Assessment
- “Can I initialize the card reliably each time the system boots?”  
- “Do I fully understand how to translate OS read/write requests into card transactions?”

#### Recommended Resources
- SD Association specifications (summary guide).  
- SPI-based SD interface examples.

---

### Module 5.4: FAT Filesystem (C)
#### Learning Objectives
1. Implement a basic FAT (File Allocation Table) driver in your kernel.  
2. Allow user space programs to create, read, list, and delete files in a FAT-formatted partition.  
3. Expand the kernel’s file system calls (open, read, write, close) to work with FAT data structures.

#### Estimated Time Investment
- 2–4 days of coding and testing.

#### Key Concepts
- FAT layout (boot sector, FAT table, clusters, root directory).  
- Directory parsing and file manipulation.  
- Mapping file descriptors to clusters/sectors on the card.

#### Practical Exercises
- [ ] Parse a FAT boot sector and validate the filesystem.  
- [ ] Implement cluster allocation and deallocation logic.  
- [ ] Write user space utilities (ls, cat, rm) to test file creation, listing, and deletion.

#### Success Criteria
- You can mount an SD card with a FAT partition, list files, read them, write new files, then verify data persists across reboots.  
- User space programs can seamlessly perform file I/O without specialized kernel knowledge of FAT internals.

#### Common Pitfalls
- Confusion around the different FAT variants (FAT12, FAT16, FAT32).  
- Mishandling cluster chaining, leading to fragmentations or data loss.

#### Self-Assessment
- “Do I correctly handle edge cases, such as out-of-space conditions or corrupted FAT entries?”  
- “Can I confirm file contents remain intact after multiple edits?”

#### Recommended Resources
- Official FAT file system specifications (though often partial or behind paywalls—community documentation can help).  
- Open-source references (simple FAT implementations in embedded systems).

---

### Module 5.5: init, shell, download, cat, ls, rm (C)
#### Learning Objectives
1. Develop simple user space programs that leverage your kernel’s system calls and FAT filesystem.  
2. Provide a minimal shell for interactive command execution.  
3. Demonstrate process creation, I/O, and data manipulation across multiple commands.

#### Estimated Time Investment
- 2–3 days to write user programs and integrate them into your OS image.

#### Key Concepts
- Basic command-line parsing in your shell.  
- Using open/read/write system calls to interact with files.  
- Spawning separate processes for commands like cat, ls, rm.

#### Practical Exercises
- [ ] Create an “init” process that runs at startup and spawns a shell.  
- [ ] Implement shell commands to list files (ls), remove files (rm), view file content (cat), and download files (download).  
- [ ] Experiment with concurrently running multiple shell sessions if your OS supports it.

#### Success Criteria
- The system boots, starts init, and transitions to a shell interface.  
- File-related commands work reliably, showing correct data or listing directory contents.

#### Common Pitfalls
- Handling user input parsing for commands incorrectly.  
- Not properly cleaning up child processes, leaving “zombie” processes in the system.

#### Self-Assessment
- “Can I navigate directories, create files via my shell, then store and retrieve files from my FAT partition?”  
- “Does my shell handle invalid commands or arguments gracefully?”

#### Recommended Resources
- Any minimal shell tutorials or examples (common in embedded Linux docs or hobby OS projects).  
- Documentation on how to structure a simple init process.

---

## 4. Knowledge Validation Checkpoint
By the end of Section 5, you should be able to:
1. Integrate an MMU into your CPU design and handle virtual address translation.  
2. Write a functional, minimal UNIX-ish kernel with multi-process support.  
3. Deploy basic file management and user space utilities using a FAT filesystem on an SD card interface.

---

## 5. Review and Reinforcement
- Test your OS with multiple processes and various input commands to ensure stability.  
- Validate filesystem reliability with repeated read/write cycles, including power-cycle or reset scenarios if using real hardware.  
- Share your progress with peers or online communities—compare approaches to memory management, scheduling, and filesystem handling.

---

**You have completed Section 5!** Next, we’ll bring everything online in Section 6 by building a TCP stack, implementing a basic telnetd, and even working towards a text-based web browser that runs on your custom OS. 
