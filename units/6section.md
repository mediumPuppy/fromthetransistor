# Section 6: Browser – Coming Online

## 1. Overview
Section 6 focuses on networking at a higher level, including implementing a TCP stack in your kernel, adding support for telnet-like remote connections, and culminating in the creation of a basic browser that can render text-based web pages in your custom OS environment. By the end of this section, you’ll have fundamental internet connectivity on your homemade platform and a working, if minimalist, web client.

---

## 2. Prerequisites
- Completion of Section 5 (functional OS with MMU, filesystem, user processes, and Ethernet interface).  
- Familiarity with socket-like concepts and TCP/IP networking basics.  
- Comfortable with C programming for systems-level network logic.

---

## 3. Module Breakdown

### Module 6.1: Building a TCP Stack (C)
#### Learning Objectives
1. Understand TCP/IP fundamentals (packets, three-way handshake, sequence and acknowledgment numbers).  
2. Implement a simplified TCP stack in the kernel, integrating your existing Ethernet driver and IP layer.  
3. Add socket-like system calls (send, recv, bind, connect) to manage connections from user space.

#### Estimated Time Investment
- 1–2 weeks (networking can be tricky to debug).

#### Key Concepts
- IP layer for basic packet routing and addressing (if not already done for bootloader).  
- TCP state machines (LISTEN, SYN-SENT, ESTABLISHED, FIN, etc.).  
- Handling retransmissions, timeouts, and packet segmentation.

#### Practical Exercises
- [ ] Implement the IP layer if needed (ARP, ICMP optional or partial).  
- [ ] Write TCP connection handling for both client and server roles.  
- [ ] Network testing with packet sniffers or loopback tests in your simulation environment.

#### Success Criteria
- You can open a TCP connection from your OS to a remote server (e.g., a local machine or second instance in simulation).  
- Basic data transfer (send/recv) works reliably without dropped or misordered packets (or if it happens, your stack recovers).

#### Common Pitfalls
- Mishandling corner cases in TCP state transitions.  
- Overlooking delayed or lost packets and failing to implement retransmission logic.

#### Self-Assessment
- “Does my TCP handshake consistently succeed and transition into ESTABLISHED state?”  
- “Am I seeing correct ACK and sequence numbers in a packet capture?”

#### Recommended Resources
- TCP/IP reference guides (Stevens’ “TCP/IP Illustrated” is classic).  
- Wireshark or tcpdump for debugging packet traces.

---

### Module 6.2: telnetd – The Power of Being Multiprocess
#### Learning Objectives
1. Create a simple telnet-like daemon that listens on a TCP port and spawns a command shell for each connection.  
2. Leverage kernel’s multi-process feature for handling simultaneous remote sessions.  
3. Gain deeper insights into how classic “remote shells” operate.

#### Estimated Time Investment
- 2–3 days of network service coding.

#### Key Concepts
- Server sockets (listen, accept) vs. client sockets (connect).  
- Forking or threading to handle multiple simultaneous connections.  
- Terminal I/O considerations in a remote context.

#### Practical Exercises
- [ ] Write a telnetd-like daemon that binds to a TCP port and awaits connections.  
- [ ] Once connected, spawn a shell process so the user can run commands remotely.  
- [ ] Handle basic telnet protocol negotiation or keep it raw TCP for simplicity.

#### Success Criteria
- Multiple users can connect (telnet or netcat) to your OS and see a shell prompt.  
- Each session runs in its own process, with independent commands and output.

#### Common Pitfalls
- Failing to properly close or cleanup processes when the remote client disconnects.  
- Handling special telnet control sequences if you choose to partially comply with the telnet protocol.

#### Self-Assessment
- “Can multiple connections be active without interfering with each other?”  
- “Am I properly echoing user keystrokes and capturing commands on each session?”

#### Recommended Resources
- Simple telnet protocol references (RFCs 854, 855) if you want some level of compliance.  
- Basic socket programming tutorials in C for server-client models.

---

### Module 6.3: Space-Saving Dynamic Linking (C)
#### Learning Objectives
1. Implement or refine a dynamic linker in user space.  
2. Reduce memory usage and storage footprint by sharing libraries across processes.  
3. Investigate the runtime linking process and how it affects application startup.

#### Estimated Time Investment
- 3–4 days for dynamic loader coding and testing.

#### Key Concepts
- Shared libraries vs. static linking.  
- Relocation, symbol resolution at runtime.  
- Potential performance trade-offs and memory benefits.

#### Practical Exercises
- [ ] Write a tiny dynamic loader that loads shared objects (.so or similar) on program startup.  
- [ ] Adapt your existing programs to dynamically link against libc or other libraries.  
- [ ] Monitor memory usage and verify that multiple processes share library code segments.

#### Success Criteria
- Applications run successfully with shared libraries, reducing the overall memory footprint.  
- The OS can handle library updates or replacements more easily (optional advanced feature).

#### Common Pitfalls
- Not setting up correct symbol resolution tables, leading to missing or incorrect function calls.  
- Failing to protect code sections, allowing unintentional overwrites.

#### Self-Assessment
- “Does every dynamically linked program find its library functions without symbol conflicts?”  
- “Have I tested scenario where multiple processes load the same library simultaneously?”

#### Recommended Resources
- ELF dynamic linking specifics.  
- Examples from Linux’s dynamic linker (ld-linux.so), though heavily more complex than your minimal approach.

---

### Module 6.4: So About That Web (C)
#### Learning Objectives
1. Develop a text-based web browser that fetches and renders simple HTML or text content.  
2. Integrate the TCP stack for HTTP client requests.  
3. Provide basic terminal-based UI (with ANSI escape codes or plain text).

#### Estimated Time Investment
- 1–2 weeks, depending on how sophisticated the browser becomes.

#### Key Concepts
- HTTP request/response structure.  
- Parsing and rendering simplistic HTML or raw text.  
- Handling multiple sessions or minimal concurrency in the user space.

#### Practical Exercises
- [ ] Implement an HTTP client function that sends GET requests and receives responses.  
- [ ] Write a simple parser for basic HTML, ignoring advanced elements.  
- [ ] Display content in a text-based format, potentially highlighting links or headings with ANSI colors.

#### Success Criteria
- You can connect to a known URL (local network or the internet, if accessible) and retrieve webpage content.  
- The browser displays text content in the terminal, with minimal markup interpretation.

#### Common Pitfalls
- Handling chunked or compressed response data incorrectly.  
- Overly complicated HTML parsing leading to bugs or partial displays.

#### Self-Assessment
- “Do I handle basic hyperlinks, text formatting, and line breaks gracefully?”  
- “Can I easily adapt my browser to handle more complex protocols or HTML features?”

#### Recommended Resources
- HTTP/1.1 RFC (2616) or simplified overviews.  
- Other minimal text-based browsers (like w3m, lynx) for concept inspiration.

---

## 4. Knowledge Validation Checkpoint
By the end of Section 6, you should be able to:
1. Implement a functioning TCP stack in your kernel with send, recv, bind, connect calls.  
2. Run a simple telnet-like daemon to allow remote shell access.  
3. Perform dynamic linking to reduce code redundancy.  
4. Browse basic text or HTML content with a minimal web browser on your custom OS.

---

## 5. Review and Reinforcement
- Test your TCP stack with various real-world servers or local network devices.  
- Confirm your telnetd handles multiple concurrent connections robustly.  
- Explore more advanced HTTP features or SSL if you want to push further.  
- Discuss with peers or online communities how you tackled TCP reliability, dynamic linking, and HTML parsing.

---

**You have completed Section 6!** Next, we move into Section 7, where you’ll take everything off the simulation stage and get it running on real FPGA hardware—going full circle from transistor concepts to a fully operational computer system.
