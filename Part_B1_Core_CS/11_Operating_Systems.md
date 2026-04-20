# 11. Operating Systems

> **Part B1 — Core Computer Science** | SIU PET Study Guide

---

- [ ] **Process Management**
  - Process vs. Thread
  - Process states: new, ready, running, waiting, terminated
  - Process Control Block (PCB)
  - Context switching

- [ ] **CPU Scheduling Algorithms**

  | Algorithm | Preemptive? | Pros | Cons |
  |-----------|------------|------|------|
  | **FCFS** | No | Simple | Convoy effect |
  | **SJF** | No | Optimal avg. wait time | Starvation of long jobs |
  | **SRTF** | Yes | Better than SJF | Starvation, overhead |
  | **Round Robin** | Yes | Fair, good response time | Higher avg. turnaround |
  | **Priority** | Both | Priority-based | Starvation (use aging) |
  | **Multilevel Queue** | Both | Classification of processes | Inflexible |

- [ ] **Deadlock**
  - Conditions: Mutual exclusion, Hold & wait, No preemption, Circular wait
  - **Prevention**: Eliminate one condition
  - **Avoidance**: Banker's algorithm
  - **Detection**: Resource allocation graph, wait-for graph
  - **Recovery**: Process termination, resource preemption

- [ ] **Synchronization**
  - Critical section problem
  - **Mutex**: Binary lock (one thread at a time)
  - **Semaphore**: Counting (multiple resources), binary
  - **Monitors**: High-level synchronization construct
  - Classic problems: Producer-consumer, readers-writers, dining philosophers

- [ ] **Memory Management**
  - **Contiguous allocation**: First fit, best fit, worst fit
  - **Paging**: Fixed-size pages/frames, page table, TLB
  - **Segmentation**: Variable-size segments (code, data, stack)
  - **Virtual Memory**: Demand paging, page fault handling
  - **Page Replacement Algorithms**:
    - FIFO, Optimal (Belady's), LRU
    - Belady's anomaly (FIFO only)
  - Thrashing: High page-fault rate → excessive swapping

- [ ] **File Systems**
  - File allocation: contiguous, linked, indexed
  - Directory structure: single-level, two-level, tree, acyclic graph
  - Disk scheduling: FCFS, SSTF, SCAN, C-SCAN, LOOK

---

### Recommended Resources
- **Book**: *Operating System Concepts* — Silberschatz, Galvin, Gagne (Dinosaur Book)
- **Book**: *Modern Operating Systems* — Andrew Tanenbaum
