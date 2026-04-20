# 15. Computer Architecture & Organization

> **Part B1 — Core Computer Science** | SIU PET Study Guide

---

- [ ] **Basic Concepts**
  - Von Neumann architecture vs. Harvard architecture
  - CPU: ALU, Control Unit, Registers
  - Instruction cycle: Fetch → Decode → Execute → Memory → Write-back

- [ ] **Instruction Set Architecture**
  - RISC (Reduced): Simple instructions, fixed length, more registers (ARM, MIPS)
  - CISC (Complex): Complex instructions, variable length, fewer registers (x86)
  - Addressing modes: immediate, register, direct, indirect, indexed

- [ ] **Pipelining**
  - Stages: IF → ID → EX → MEM → WB
  - Hazards: structural, data (RAW, WAR, WAW), control
  - Solutions: forwarding, stalling, branch prediction

- [ ] **Memory Hierarchy**
  - Registers → Cache (L1, L2, L3) → Main Memory (RAM) → Secondary Storage (SSD/HDD)
  - Cache: direct-mapped, fully associative, set-associative
  - Cache replacement: LRU, FIFO, random
  - Cache performance: hit rate, miss rate, average access time

- [ ] **I/O Organization**
  - Programmed I/O, interrupt-driven I/O, DMA (Direct Memory Access)
  - I/O interfaces: serial, parallel

- [ ] **Parallel Processing**
  - Flynn's classification: SISD, SIMD, MISD, MIMD
  - Multi-core processors
  - Amdahl's Law: Speedup $= \frac{1}{(1-P) + \frac{P}{N}}$ where P = parallelizable fraction, N = processors

---

### Recommended Resources
- **Book**: *Computer Organization and Design* — Patterson & Hennessy
- **Book**: *Computer Architecture* — Morris Mano
