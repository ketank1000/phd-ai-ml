# 11. Operating Systems

> **Part B1 — Core Computer Science** | SIU PET Complete Study Guide

---

## 11.1 Process Management

### Process vs. Thread

| Feature | Process | Thread |
|---------|---------|--------|
| **Definition** | An instance of a running program | A lightweight unit of execution within a process |
| **Memory** | Own address space (code, data, heap, stack) | Shares process memory; has own stack |
| **Creation** | Heavyweight (expensive) | Lightweight (cheap) |
| **Communication** | Inter-Process Communication (IPC): pipes, sockets, shared memory | Direct — share same memory space |
| **Failure impact** | One process crash doesn't affect others | One thread crash can kill the entire process |
| **Context switch** | Expensive (save/restore entire address space) | Cheap (share address space) |

### Process States

```
         ┌──────────┐   Admitted    ┌───────┐   Scheduler   ┌─────────┐
         │   New    │──────────────→│ Ready │──────────────→│ Running │
         └──────────┘               └───┬───┘               └────┬────┘
                                        │ ↑                      │ │
                                        │ │ I/O complete or      │ │
                                        │ │ event               │ │ Interrupt
                                        │ └──────────────────┐  │ │(preemption)
                                        │                    │  │ │
                                        │               ┌────┴──┴─↓──┐
                                        │               │  Waiting   │
                                        │               │ (Blocked)  │
                                        │               └────────────┘
                                        │                      │
                                        ↑                      ↓
                                    ┌────────────┐      Exit/
                                    │            │      Terminated
                                    └────────────┘
```

**Five states:** New → Ready → Running → Waiting/Terminated
- **New:** Process is being created
- **Ready:** Waiting for CPU (in the ready queue)
- **Running:** Currently executing on the CPU
- **Waiting:** Blocked on I/O or event
- **Terminated:** Finished execution

### Process Control Block (PCB)

Each process has a PCB containing:
- Process ID (PID)
- Process state (ready, running, etc.)
- Program counter (next instruction address)
- CPU registers (saved during context switch)
- Memory management info (page tables, segment tables)
- I/O status info (open files, devices)
- Scheduling info (priority, CPU time used)

### Context Switching

When the CPU switches from one process to another:
1. Save the state (PCB) of the current process
2. Load the state (PCB) of the next process
3. Resume the next process

**Overhead:** Context switching is "wasted" time — no useful work done during the switch.

---

## 11.2 CPU Scheduling Algorithms

### Key Metrics
- **Turnaround time:** Completion time − Arrival time
- **Waiting time:** Turnaround time − Burst time
- **Response time:** First CPU allocation − Arrival time
- **Throughput:** Number of processes completed per unit time
- **CPU Utilization:** Percentage of time CPU is busy

### Algorithms Explained

**1. FCFS (First Come, First Served)**
- Non-preemptive. Process that arrives first runs first.
- **Problem: Convoy Effect** — If a long process arrives first, all short processes wait behind it.

| Process | Arrival | Burst | Completion | Turnaround | Waiting |
|---------|---------|-------|------------|------------|---------|
| P1 | 0 | 24 | 24 | 24 | 0 |
| P2 | 0 | 3 | 27 | 27 | 24 |
| P3 | 0 | 3 | 30 | 30 | 27 |
| **Avg** | | | | **27** | **17** |

**2. SJF (Shortest Job First)**
- Non-preemptive. Pick the process with the shortest burst time.
- **Optimal** for average waiting time among non-preemptive algorithms.
- **Problem:** Starvation of long processes; requires knowing burst time in advance.

**3. SRTF (Shortest Remaining Time First)**
- Preemptive version of SJF.
- If a new process arrives with shorter remaining time than the currently running process, switch.

**4. Round Robin (RR)**
- Preemptive. Each process gets a fixed **time quantum** (q).
- After q units, the process is moved to the back of the ready queue.

```
Time quantum = 4
P1(10)  P2(4)  P3(6)

Gantt: |P1(4)|P2(4)|P3(4)|P1(4)|P3(2)|P1(2)|
       0     4    8    12   16   18   20
```

- **Small q:** More context switches (overhead), better response time
- **Large q:** Approaches FCFS behavior
- **Rule of thumb:** q should be large enough that 80% of CPU bursts are shorter than q

**5. Priority Scheduling**
- Each process has a priority. Higher priority → runs first.
- Can be preemptive or non-preemptive.
- **Problem:** Starvation (low-priority processes may never run)
- **Solution: Aging** — gradually increase priority of waiting processes

**6. Multilevel Queue**
- Multiple ready queues (e.g., foreground/interactive, background/batch)
- Each queue has its own scheduling algorithm
- Fixed priority between queues OR time-sliced

---

## 11.3 Deadlock

A situation where two or more processes are each waiting for resources held by each other, and none can proceed.

### Four Necessary Conditions (ALL must hold simultaneously)

| Condition | Meaning |
|-----------|---------|
| **Mutual Exclusion** | Resource can be used by only one process at a time |
| **Hold and Wait** | Process holds some resources while waiting for others |
| **No Preemption** | Resources cannot be forcibly taken from a process |
| **Circular Wait** | P1 waits for P2, P2 waits for P3, ..., Pn waits for P1 |

### Handling Deadlocks

**Prevention:** Ensure at least one of the four conditions can never hold.
- Eliminate hold-and-wait: request all resources at once
- Allow preemption: if a process can't get a resource, release what it holds
- Order resources: request resources in a fixed numerical order

**Avoidance — Banker's Algorithm:**
- Before allocating a resource, check if the system remains in a **safe state**
- Safe state: there exists a sequence of processes that can all finish
- Uses: Available, Max, Allocation, Need matrices

**Detection:** Build a resource allocation graph (or wait-for graph). If a cycle exists → deadlock.

**Recovery:**
- Terminate one or more deadlocked processes
- Preempt resources from some processes

---

## 11.4 Synchronization

### Critical Section Problem

A **critical section** is a code segment where a process accesses shared resources. Requirements:
1. **Mutual Exclusion:** Only one process in the critical section at a time
2. **Progress:** If no process is in the CS, a waiting process can enter
3. **Bounded Waiting:** A process won't wait forever

### Synchronization Mechanisms

**Mutex (Mutual Exclusion Lock):**
- Binary lock: locked (1) or unlocked (0)
- Only the thread that locked can unlock
- Ensures only one thread in the critical section

**Semaphore:**
- Integer variable accessed via atomic operations: `wait(S)` (P) and `signal(S)` (V)
- **Binary semaphore** (0 or 1): like a mutex
- **Counting semaphore** (0 to N): allows N processes to access the resource simultaneously

```
wait(S):
    while S <= 0: busy-wait
    S = S - 1

signal(S):
    S = S + 1
```

**Monitor:**
- High-level construct: encapsulates shared data + procedures + synchronization
- Only one process can be active inside a monitor at a time
- Uses **condition variables** with `wait()` and `signal()`

### Classic Synchronization Problems

| Problem | Description | Solution |
|---------|-------------|----------|
| **Producer-Consumer** | Producer adds items to buffer; consumer removes. Buffer can overflow/underflow | Semaphores: empty(N), full(0), mutex(1) |
| **Readers-Writers** | Multiple readers can read simultaneously but writers need exclusive access | Semaphores or reader-writer locks |
| **Dining Philosophers** | 5 philosophers, 5 forks; each needs 2 forks to eat; avoid deadlock | Order forks, use semaphores, or limit concurrent eaters |

---

## 11.5 Memory Management

### Contiguous Allocation

Entire process placed in a single contiguous block of memory.

| Strategy | How It Works | Problem |
|----------|-------------|---------|
| **First Fit** | Allocate first hole that is big enough | Fast; may leave many small fragments |
| **Best Fit** | Allocate smallest sufficient hole | Least waste per allocation; slow to search |
| **Worst Fit** | Allocate largest hole | Leaves largest remainder; not commonly used |

**Problem: External Fragmentation** — Free memory exists but is scattered in small holes.
**Solution: Compaction** — move processes to create one large free block (expensive).

### Paging

Divides memory into fixed-size blocks:
- **Pages** (logical memory) = **Frames** (physical memory)
- Typical page size: 4 KB

```
Logical Address:
┌──────────────────┬───────────────┐
│  Page Number (p) │  Offset (d)   │
└──────────────────┴───────────────┘

Page Table: maps page number → frame number
Physical Address = Frame Number × Page Size + Offset
```

**Advantages:** No external fragmentation. Process need not be contiguous.
**Disadvantage:** Internal fragmentation (last page may not be fully used). Page table overhead.

**TLB (Translation Lookaside Buffer):** Cache for page table entries. Makes address translation fast.
- TLB hit: O(1) lookup
- TLB miss: access page table in memory (slower)

### Segmentation

Divides memory by logical segments: code, data, stack, heap.
- Each segment has a base address and length
- Segments can vary in size
- **Advantage:** Matches logical structure of a program
- **Disadvantage:** External fragmentation (variable-size segments)

### Virtual Memory

Makes it appear that the system has more memory than physically available.

**Demand Paging:** Only load pages into memory when they're needed (on first access).

**Page Fault:** When a process accesses a page not in memory:
1. Trap to OS
2. Find the page on disk
3. Load it into a free frame
4. Update the page table
5. Resume the process

### Page Replacement Algorithms

When memory is full and a new page is needed, which page to evict?

| Algorithm | How It Works | Optimal? |
|-----------|-------------|----------|
| **FIFO** | Replace the oldest page | No. Suffers from Belady's anomaly |
| **Optimal (Belady's)** | Replace the page not used for longest time in the future | Yes, but impossible to implement (requires future knowledge) |
| **LRU (Least Recently Used)** | Replace the page that hasn't been used for the longest time | Near-optimal. Most commonly used |

**Belady's Anomaly:** With FIFO, increasing number of frames can INCREASE page faults (counterintuitive!). Does NOT occur with LRU or Optimal.

### Thrashing

When a process spends more time paging (swapping) than executing.
- Cause: too many processes competing for too little memory
- Solution: Reduce the degree of multiprogramming; use working set model

---

## 11.6 File Systems

### File Allocation Methods

| Method | How | Pros | Cons |
|--------|-----|------|------|
| **Contiguous** | File occupies consecutive disk blocks | Fast sequential & random access | External fragmentation, file growth difficult |
| **Linked** | Each block contains pointer to next block | No fragmentation, easy growth | Slow random access, pointer overhead |
| **Indexed** | Index block stores pointers to all file blocks | Fast random access, no fragmentation | Index block overhead |

### Disk Scheduling Algorithms

| Algorithm | Strategy | Advantage |
|-----------|----------|-----------|
| **FCFS** | Serve in order of request | Fair, simple |
| **SSTF** | Serve nearest request next | Low seek time, but starvation possible |
| **SCAN (Elevator)** | Move in one direction, then reverse | No starvation, uniform wait |
| **C-SCAN** | Like SCAN but only serves in one direction, then jumps back | More uniform wait time |
| **LOOK / C-LOOK** | Like SCAN/C-SCAN but reverses at last request, not disk end | Efficient, most commonly used |

---

## 11.7 Practice Questions

**Q1.** Three processes arrive at time 0 with burst times 6, 8, 7. Calculate average waiting time for FCFS and SJF.
> **Answer:** **FCFS** (order: P1, P2, P3): Waiting times = 0, 6, 14. Avg = (0+6+14)/3 = **6.67**. **SJF** (order: P1(6), P3(7), P2(8)): Waiting = 0, 6, 13. Avg = (0+6+13)/3 = **6.33**. SJF gives better average waiting time.

**Q2.** Given the page reference string: 7, 0, 1, 2, 0, 3, 0, 4, 2, 3 with 3 frames, calculate page faults using FIFO and LRU.
> **Answer:** **FIFO:** Frames after each access: {7},{7,0},{7,0,1},{2,0,1}(fault),{2,0,1},{2,3,1}(fault),{2,3,0}(fault),{4,3,0}(fault),{4,2,0}(fault),{4,2,3}(fault) = **9 page faults**. **LRU:** {7},{7,0},{7,0,1},{0,1,2}(fault),{0,1,2},{1,2,3}(fault),{2,3,0}(fault),{3,0,4}(fault),{0,4,2}(fault),{4,2,3}(fault) = **9 page faults**. (For this specific string both give 9; LRU often gives fewer faults for larger strings.)

**Q3.** What are the four necessary conditions for deadlock? Explain how the Banker's algorithm prevents deadlock.
> **Answer:** (1) Mutual Exclusion, (2) Hold and Wait, (3) No Preemption, (4) Circular Wait — ALL four must hold simultaneously. **Banker's Algorithm** prevents deadlock through **avoidance**: before granting a resource request, it checks if the resulting state is "safe" (i.e., all processes can eventually complete). If granting would lead to an unsafe state, the request is denied (process waits). It uses Max, Allocation, Available, and Need matrices.

**Q4.** Explain the difference between paging and segmentation.
> **Answer:** **Paging** divides memory into fixed-size blocks (pages/frames) — simple, eliminates external fragmentation but causes internal fragmentation. **Segmentation** divides memory by logical program segments (code, data, stack) of variable sizes — matches logical structure of programs but causes external fragmentation. Many real systems use **segmented paging** (a combination), like Intel x86 architecture.

**Q5.** What is thrashing? How can it be detected and resolved?
> **Answer:** **Thrashing** occurs when a process spends more time swapping pages between memory and disk than doing actual computation, because it doesn't have enough frames. **Detection:** If page fault rate is extremely high and CPU utilization drops despite high I/O. **Resolution:** (1) Reduce degree of multiprogramming (swap out some processes), (2) Use the working set model to allocate enough frames to each process, (3) Add more physical RAM.

---

*Previous: [Chapter 10 — DBMS](10_DBMS.md) | Next: [Chapter 12 — Computer Networks](12_Computer_Networks.md)*
