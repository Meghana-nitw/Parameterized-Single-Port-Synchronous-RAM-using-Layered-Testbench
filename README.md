# Parameterized Single-Port Synchronous RAM using Layered Testbench

A SystemVerilog-based design and verification project implementing a parameterized single-port synchronous RAM. The project demonstrates a scalable RAM architecture and verifies its functionality using a layered testbench with object-oriented verification components such as generator, driver, monitor, scoreboard, and mailboxes.

---

## Project Overview

Memory blocks are fundamental components of digital systems and are widely used in processors, embedded systems, communication devices, and FPGA/ASIC designs. This project focuses on designing a configurable single-port synchronous RAM and validating its functionality through a reusable layered verification environment.

The RAM supports synchronous read and write operations through a single port and is parameterized to allow easy modification of memory size and data width without changing the core design.

---

## Features

- Parameterized RAM architecture
- Synchronous read operation
- Synchronous write operation
- WRITE_FIRST behavior
- Reset functionality
- Layered verification environment
- Randomized transaction generation
- Self-checking scoreboard
- Reference memory model
- Object-oriented verification using SystemVerilog classes
- Mailbox-based communication
- Scalable and reusable verification architecture

---

## Design Specifications

| Parameter | Value |
|-----------|-------|
| Data Width | 8 bits |
| Memory Depth | 16 locations |
| Address Width | 4 bits |
| Language | SystemVerilog |

---

## Functional Behavior

The RAM supports the following operations:

### Write Operation

When **Write Enable (we)** is asserted, the input data is written into the selected memory location on the rising edge of the clock.

### Read Operation

When **Write Enable (we)** is deasserted, the stored data is read synchronously from the selected address during the next clock cycle.

### WRITE_FIRST Behavior

If a read and write occur simultaneously for the same address, the newly written data is immediately available on the output.

### Reset Operation

Reset initializes the memory interface to a known state before normal operation begins.

---

# Verification Methodology

The verification environment follows a layered architecture to ensure modularity, scalability, and reusability.

The major verification components include:

- Transaction
- Generator
- Driver
- Interface
- Monitor
- Scoreboard
- Environment
- Top Testbench

---

## Verification Architecture

```
Generator
      │
      ▼
Mailbox
      │
      ▼
Driver
      │
      ▼
Interface
      │
      ▼
Single-Port RAM (DUT)
      │
      ▼
Monitor
      │
      ▼
Mailbox
      │
      ▼
Scoreboard
```

---

## Verification Components

### Transaction

The transaction class represents a single RAM operation.

It contains:

- Write Enable
- Address
- Write Data
- Read Data

Random constraints ensure generated addresses remain within the valid memory range.

---

### Generator

The generator creates randomized RAM transactions.

Responsibilities include:

- Random transaction generation
- Constraint checking
- Sending transactions to the driver through mailboxes

---

### Driver

The driver receives transactions from the generator and drives the DUT signals using the virtual interface.

Functions:

- Apply inputs on positive clock edge
- Generate write/read operations
- Synchronize DUT communication

---

### Interface

The interface groups all DUT signals into a single reusable communication block.

Signals include:

- clk
- rst
- we
- addr
- wdata
- rdata

---

### Monitor

The monitor observes DUT activity without driving any signals.

Responsibilities include:

- Capturing write operations
- Capturing read operations
- Handling synchronous timing
- Reconstructing transactions
- Sending data to scoreboard

---

### Scoreboard

The scoreboard acts as the reference model.

Functions:

- Maintains software memory model
- Compares expected output with DUT output
- Reports PASS/FAIL status
- Detects mismatches automatically

---

### Environment

The environment connects all verification components together.

It creates:

- Generator
- Driver
- Monitor
- Scoreboard

It also manages mailbox communication between components.

---

### Top Testbench

The top-level testbench performs:

- DUT instantiation
- Interface instantiation
- Clock generation
- Reset generation
- Environment creation
- Simulation control

---

# Simulation Flow

1. Reset the RAM.
2. Generate randomized transactions.
3. Send transactions to the driver.
4. Driver applies inputs to DUT.
5. Monitor captures DUT responses.
6. Scoreboard compares expected and actual outputs.
7. PASS or FAIL messages are displayed.
8. Simulation continues until all transactions are completed.

---

# Test Cases Verified

The verification environment validates:

- Write operation
- Read operation
- Read-after-write
- WRITE_FIRST behavior
- Reset functionality
- Back-to-back memory accesses
- Random address accesses
- Random data generation
- Timing correctness

---

# Sample Console Output

```
WRITE PASS addr = 7 data = 6C

READ PASS addr = 7 data = 6C
```

The scoreboard compares DUT outputs against the reference memory model and reports successful verification for every valid transaction.

---

# Technologies Used

- SystemVerilog
- Object-Oriented Programming (OOP)
- Layered Verification Methodology
- Mailboxes
- Virtual Interface
- Constraint Randomization
- Self-Checking Testbench

---

# Learning Outcomes

This project helped in understanding:

- SystemVerilog design
- Parameterized hardware modules
- Memory architecture
- Layered verification methodology
- Object-oriented verification
- Constraint randomization
- Mailbox communication
- Virtual interfaces
- Scoreboard-based verification
- Functional verification concepts

---

# Future Enhancements

Possible improvements include:

- Dual-Port RAM implementation
- UVM-based verification
- Functional coverage
- Assertion-based verification
- Burst read/write support
- Error injection testing
- Memory initialization files
- ECC implementation

---

# Applications

- FPGA Designs
- ASIC Design
- Embedded Systems
- Processor Memory
- Cache Memory
- Digital Signal Processing
- Communication Systems
- VLSI Verification Training

---

# Repository Structure

```
├── rtl/
│   ├── ram.sv
│
├── testbench/
│   ├── transaction.sv
│   ├── generator.sv
│   ├── driver.sv
│   ├── monitor.sv
│   ├── scoreboard.sv
│   ├── environment.sv
│   ├── interface.sv
│   └── testbench_top.sv
│
├── simulation/
│
├── docs/
│
└── README.md
```

---

# Author

**P. Meghana**  
B.Tech – Electronics and Communication Engineering (VLSI)  
National Institute of Technology Warangal

---

# Acknowledgement

This project was completed as part of the VLSI mini project under the guidance of **Prof. Atul Kumar Nishad**, Department of Electronics and Communication Engineering, National Institute of Technology Warangal. The project provided practical experience in digital design, SystemVerilog programming, and modern hardware verification techniques. :contentReference[oaicite:0]{index=0} :contentReference[oaicite:1]{index=1} :contentReference[oaicite:2]{index=2}
