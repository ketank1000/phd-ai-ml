# 15. Computer Architecture & Organization

> **Part B1 — Core Computer Science** | SIU PET Complete Study Guide

---

## 15.1 Basic Concepts

### Von Neumann vs. Harvard Architecture

| Feature | Von Neumann | Harvard |
|---------|-------------|---------|
| **Memory** | Shared memory for instructions AND data | Separate memory for instructions and data |
| **Bus** | Single bus for both | Separate buses (parallel access) |
| **Speed** | Slower (bottleneck on shared bus) | Faster (can fetch instruction and data simultaneously) |
| **Used in** | General-purpose CPUs (x86, most PCs) | DSPs, microcontrollers (ARM Cortex-M), some embedded systems |
| **Flexibility** | Easy self-modifying code | Safer (code can't accidentally overwrite data) |

### CPU Components

```
┌────────────────────────── CPU ──────────────────────────┐
│                                                          │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │  Control Unit │  │     ALU      │  │  Registers   │  │
│  │  (CU)        │  │ (Arithmetic  │  │ PC, IR, MAR, │  │
│  │  Decodes &   │  │  Logic Unit) │  │ MDR, ACC,    │  │
│  │  coordinates │  │  +, -, ×, /, │  │ General-     │  │
│  │  operations  │  │  AND, OR,    │  │ purpose      │  │
│  │              │  │  NOT, shift  │  │              │  │
│  └──────────────┘  └──────────────┘  └──────────────┘  │
│                                                          │
└────────────────────── System Bus ───────────────────────┘
                    ┌──────┬──────┬──────┐
                    │ Data │ Addr │ Ctrl │
                    │ Bus  │ Bus  │ Bus  │
                    └──────┴──────┴──────┘
```

**Key Registers:**

| Register | Full Name | Purpose |
|----------|----------|---------|
| **PC** | Program Counter | Address of NEXT instruction to fetch |
| **IR** | Instruction Register | Currently executing instruction |
| **MAR** | Memory Address Register | Address to read from/write to memory |
| **MDR** | Memory Data Register | Data read from/to be written to memory |
| **ACC** | Accumulator | Stores intermediate ALU results |
| **SP** | Stack Pointer | Points to top of stack |

### Instruction Cycle

```
┌────────┐    ┌────────┐    ┌─────────┐    ┌────────┐    ┌────────────┐
│ FETCH  │ →  │ DECODE │ →  │ EXECUTE │ →  │ MEMORY │ →  │ WRITE-BACK │
│        │    │        │    │         │    │ ACCESS │    │            │
│ Get    │    │ What   │    │ Do the  │    │ Load/  │    │ Store      │
│ instr  │    │ does   │    │ oper-   │    │ Store  │    │ result in  │
│ from   │    │ it say │    │ ation   │    │ data   │    │ register   │
│ memory │    │ to do? │    │ (ALU)   │    │        │    │            │
└────────┘    └────────┘    └─────────┘    └────────┘    └────────────┘
```

---

## 15.2 Instruction Set Architecture (ISA)

### RISC vs. CISC

| Feature | RISC | CISC |
|---------|------|------|
| **Full name** | Reduced Instruction Set Computer | Complex Instruction Set Computer |
| **Instructions** | Simple, fixed format, fixed length | Complex, variable length |
| **Execution** | Most in 1 clock cycle | May take multiple cycles |
| **Registers** | Many (32+) | Fewer |
| **Memory access** | Load/Store architecture (only LW, SW access memory) | Any instruction can access memory |
| **Pipelining** | Easy to pipeline | Harder to pipeline |
| **Examples** | ARM, MIPS, RISC-V | x86, Intel, AMD |
| **Used in** | Mobile (ARM in phones), embedded | Desktop, laptop, servers |

### Addressing Modes

| Mode | Operand Location | Example | Effective Address |
|------|-----------------|---------|-------------------|
| **Immediate** | In the instruction itself | ADD R1, #5 | Value = 5 |
| **Register** | In a register | ADD R1, R2 | EA = R2 |
| **Direct** | At a specific memory address | LOAD R1, [1000] | EA = 1000 |
| **Indirect** | Address in the instruction points to address of operand | LOAD R1, @1000 | EA = M[1000] |
| **Register Indirect** | Register contains the address | LOAD R1, (R2) | EA = R2 contents |
| **Indexed** | Base address + offset | LOAD R1, 100(R2) | EA = R2 + 100 |
| **Base-Register** | Similar to indexed | — | EA = Base + Offset |

---

## 15.3 Pipelining

### Concept

Execute multiple instructions simultaneously by overlapping their stages.

**Without pipelining (sequential):**
```
Instruction 1: IF  ID  EX  MEM  WB
Instruction 2:                    IF  ID  EX  MEM  WB
Time: 10 cycles for 2 instructions
```

**With pipelining:**
```
Instruction 1: IF  ID  EX  MEM  WB
Instruction 2:     IF  ID  EX  MEM  WB
Instruction 3:         IF  ID  EX  MEM  WB
Time: 7 cycles for 3 instructions (vs 15 sequential)
```

**Stages:** IF (Instruction Fetch) → ID (Instruction Decode) → EX (Execute) → MEM (Memory Access) → WB (Write Back)

**Speedup:** Ideally k× for k stages, but limited by the slowest stage.

### Pipeline Hazards

| Hazard Type | Description | Example |
|-------------|-------------|---------|
| **Structural** | Two instructions need the same hardware simultaneously | Both need memory access in the same cycle |
| **Data (RAW)** | Read After Write — instruction needs result not yet computed | ADD R1, R2, R3; SUB R4, R1, R5 (SUB needs R1 from ADD) |
| **Data (WAR)** | Write After Read — writing before a previous read | Rare in simple pipelines |
| **Data (WAW)** | Write After Write — two writes to same register out of order | Rare in simple pipelines |
| **Control** | Branch instruction — don't know which instruction to fetch next | BEQ label (if equal, go to label — but next instruction already fetched) |

### Solutions to Hazards

| Solution | For Which Hazard | How It Works |
|----------|-----------------|-------------|
| **Forwarding (Bypassing)** | Data (RAW) | Pass ALU result directly to next instruction without waiting for WB |
| **Stalling (Pipeline Bubble)** | Data | Insert NOPs (idle cycles) until the result is available |
| **Branch Prediction** | Control | Guess whether branch is taken; flush pipeline if wrong |
| **Reordering** | Data | Compiler rearranges instructions to avoid hazards |

---

## 15.4 Memory Hierarchy

```
Speed ↑        ┌──────────┐         Cost ↑
               │ Registers│ (< 1ns)
               │  (~1 KB) │
               ├──────────┤
               │ L1 Cache │ (1-2 ns)
               │ (32-64KB)│
               ├──────────┤
               │ L2 Cache │ (3-10 ns)
               │(256KB-1MB│
               ├──────────┤
               │ L3 Cache │ (10-30 ns)
               │ (4-64 MB)│
               ├──────────┤
               │   RAM    │ (50-100 ns)
               │ (8-64 GB)│
               ├──────────┤
               │   SSD    │ (100 μs)
               │(256GB-4TB│
               ├──────────┤
               │   HDD    │ (5-10 ms)
               │ (1-16 TB)│
               └──────────┘
Size ↑                              Speed ↓
```

### Cache Memory

A small, fast memory between CPU and main memory that stores recently/frequently accessed data.

**Principle of Locality:**
- **Temporal locality:** If data was accessed recently, it will likely be accessed again soon
- **Spatial locality:** If data at address X was accessed, addresses near X will likely be accessed soon

### Cache Mapping Techniques

| Technique | How It Maps | Hit Check | Pros | Cons |
|-----------|-------------|-----------|------|------|
| **Direct Mapped** | Each memory block maps to exactly one cache line | Compare 1 tag | Simple, fast | Conflict misses |
| **Fully Associative** | Any block can go in any cache line | Compare ALL tags | No conflict misses | Expensive (need to search all lines) |
| **Set Associative** | Each block maps to a SET of lines (e.g., 4-way) | Compare tags in the set | Good balance | Moderate complexity |

**N-way set-associative:** The cache is divided into sets, each containing N lines. A block maps to one set but can go in any of the N lines within that set.

### Cache Performance

$$\text{Average Access Time} = \text{Hit Time} + \text{Miss Rate} \times \text{Miss Penalty}$$

**Types of cache misses (3 C's):**
- **Compulsory:** First access to a block (cold start)
- **Capacity:** Cache is too small to hold all needed blocks
- **Conflict:** Blocks map to the same cache line (direct-mapped/set-associative)

### Cache Replacement Policies

| Policy | How It Chooses Block to Replace |
|--------|-------------------------------|
| **LRU (Least Recently Used)** | Replace the block not used for the longest time |
| **FIFO (First In, First Out)** | Replace the oldest block |
| **Random** | Replace a random block |

---

## 15.5 I/O Organization

| Method | How It Works | CPU Involvement | Speed |
|--------|-------------|----------------|-------|
| **Programmed I/O** | CPU constantly checks I/O device status (polling/busy-waiting) | 100% — CPU does nothing else | Slowest |
| **Interrupt-driven I/O** | Device sends interrupt when ready; CPU handles it | Moderate — CPU does other work until interrupt | Medium |
| **DMA (Direct Memory Access)** | DMA controller transfers data directly between I/O device and memory | Minimal — CPU just initiates, DMA does the transfer | Fastest |

---

## 15.6 Parallel Processing

### Flynn's Classification

| Category | Instructions | Data | Description | Example |
|----------|-------------|------|-------------|---------|
| **SISD** | Single | Single | Traditional sequential CPU | Classic von Neumann machine |
| **SIMD** | Single | Multiple | Same operation on multiple data points | GPU (apply same shader to millions of pixels), vector processors |
| **MISD** | Multiple | Single | Multiple operations on same data | Fault-tolerant systems (rare) |
| **MIMD** | Multiple | Multiple | Multiple independent processors | Multi-core CPUs, clusters, supercomputers |

> **For AI/ML:** GPUs use SIMD (or more precisely SIMT) for parallel matrix operations. This is why GPUs are essential for deep learning.

### Amdahl's Law

$$\text{Speedup} = \frac{1}{(1-P) + \frac{P}{N}}$$

Where:
- P = fraction of program that can be parallelized
- N = number of processors

**Example:** If 90% of a program is parallelizable (P = 0.9):
- With 2 processors: Speedup = 1/(0.1 + 0.45) = 1/0.55 = **1.82×**
- With 10 processors: Speedup = 1/(0.1 + 0.09) = 1/0.19 = **5.26×**
- With ∞ processors: Speedup = 1/0.1 = **10×** (limited by serial portion!)

**Key Insight:** Even with infinite processors, speedup is limited by the sequential (non-parallelizable) portion. A program that is 95% parallel can achieve at most 20× speedup.

---

## 15.7 Practice Questions

**Q1.** What is the key difference between Von Neumann and Harvard architecture? Which is used in most modern PCs?
> **Answer:** Von Neumann uses a **single shared memory** for both instructions and data with a shared bus (bottleneck). Harvard uses **separate memories and buses** for instructions and data (faster). Most modern PCs use Von Neumann, but many use a **modified Harvard architecture** where L1 cache is split into instruction cache and data cache (Harvard-like) while main memory is shared (Von Neumann-like).

**Q2.** A 5-stage pipeline has 100 instructions to execute. How many cycles does it take? What is the speedup over non-pipelined execution?
> **Answer:** Pipelined: **104 cycles** (first instruction takes 5 stages, then 99 more instructions, one per cycle = 5 + 99 = 104). Non-pipelined: 100 × 5 = 500 cycles. **Speedup = 500/104 ≈ 4.81×** (approaches 5× for large numbers of instructions). 

**Q3.** A system has a cache with hit rate 95%, hit time 2 ns, and miss penalty 100 ns. What is the average memory access time?
> **Answer:** AMAT = Hit Time + Miss Rate × Miss Penalty = 2 + (0.05 × 100) = 2 + 5 = **7 ns**. Without cache, every access would take ~100 ns. The cache provides 100/7 ≈ 14× speedup.

**Q4.** Using Amdahl's Law, if 80% of a program is parallelizable and you have 4 processors, what is the speedup?
> **Answer:** Speedup = 1/(0.2 + 0.8/4) = 1/(0.2 + 0.2) = 1/0.4 = **2.5×**. Maximum possible speedup (∞ processors): 1/0.2 = 5×.

**Q5.** Explain the RAW data hazard with an example. How does forwarding solve it?
> **Answer:** **RAW (Read After Write):** A later instruction tries to read a register before a previous instruction has written to it. Example: `ADD R1, R2, R3` (writes R1), then `SUB R4, R1, R5` (reads R1). SUB needs the result of ADD, but in a pipeline, ADD hasn't written R1 back to the register file when SUB reads it. **Forwarding:** The ALU output from ADD's Execute stage is directly forwarded to SUB's Execute stage input, bypassing the need to wait for the Write-Back stage.

---

*Previous: [Chapter 14 — Discrete Mathematics](14_Discrete_Mathematics.md) | Next: [Chapter 16 — Software Engineering](16_Software_Engineering.md)*
