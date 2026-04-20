# 9. Data Structures & Algorithms

> **Part B1 — Core Computer Science** | SIU PET Complete Study Guide

---

## 9.1 Linear Data Structures

### 9.1.1 Arrays

An **array** is a contiguous block of memory storing elements of the same type.

```
Index:   0     1     2     3     4
       ┌─────┬─────┬─────┬─────┬─────┐
Value: │  10  │  20  │  30  │  40  │  50  │
       └─────┴─────┴─────┴─────┴─────┘
```

**Types:**
- **1D Array:** Linear list — `int arr[5] = {10, 20, 30, 40, 50};`
- **2D Array:** Matrix — `int matrix[3][3]` — stored row-major (C/C++) or column-major (Fortran)
- **Dynamic Array:** Resizable — `ArrayList` (Java), `list` (Python), `vector` (C++)
  - When full, allocates a new array of 2× size and copies elements
  - Amortized O(1) for append

**Time Complexity:**

| Operation | Time | Explanation |
|-----------|------|-------------|
| Access by index | O(1) | Direct calculation: `base_address + index × size` |
| Search (unsorted) | O(n) | Must check every element |
| Search (sorted) | O(log n) | Binary search |
| Insert at end | O(1) amortized | Just place at next available slot |
| Insert at position i | O(n) | Must shift elements right |
| Delete at position i | O(n) | Must shift elements left |

### 9.1.2 Linked Lists

A collection of **nodes** where each node stores data and a pointer to the next node. Unlike arrays, elements are NOT in contiguous memory.

**Singly Linked List:**
```
[10|→] → [20|→] → [30|→] → [40|→] → NULL
 head
```

**Doubly Linked List:**
```
NULL ← [←|10|→] ⇄ [←|20|→] ⇄ [←|30|→] → NULL
         head
```

**Circular Linked List:** Last node points back to the head (instead of NULL).

**Key Operations:**

| Operation | Singly LL | Doubly LL |
|-----------|----------|----------|
| Insert at head | O(1) | O(1) |
| Insert at tail | O(n) [O(1) with tail pointer] | O(1) with tail pointer |
| Delete at head | O(1) | O(1) |
| Delete specific node | O(n) — need to find predecessor | O(1) — if you have the node pointer |
| Search | O(n) | O(n) |
| Reverse | O(n) | O(n) |

**Important Algorithm — Floyd's Cycle Detection:**
Use two pointers: slow (moves 1 step) and fast (moves 2 steps). If they meet → cycle exists.

```
slow → 1 → 2 → 3 → 4
fast → 1 → 3 → (meets slow at some node if cycle exists)
```

**Array vs Linked List:**

| Feature | Array | Linked List |
|---------|-------|-------------|
| Access | O(1) — random access | O(n) — sequential only |
| Insert/Delete | O(n) — shifting | O(1) — pointer manipulation |
| Memory | Contiguous, no overhead | Extra pointer per node |
| Cache performance | Excellent (locality) | Poor (scattered memory) |
| Size | Fixed (or amortized resize) | Dynamic, grows one node at a time |

### 9.1.3 Stacks (LIFO — Last In, First Out)

```
        ┌─────┐
push →  │  30 │  ← top (pop from here)
        ├─────┤
        │  20 │
        ├─────┤
        │  10 │
        └─────┘
```

**Operations:** All O(1)
- `push(x)` — add element to top
- `pop()` — remove and return top element
- `peek()/top()` — view top element without removing
- `isEmpty()` — check if stack is empty

**Applications:**
1. **Function call stack** — each function call pushes a frame; return pops it
2. **Expression evaluation** — infix to postfix conversion, postfix evaluation
3. **Parenthesis matching** — push opening brackets, pop on closing
4. **Undo/Redo** — undo stack and redo stack
5. **DFS traversal** — iterative DFS uses a stack
6. **Browser back button** — pages stored in a stack

### 9.1.4 Queues (FIFO — First In, First Out)

```
Enqueue →  [10] [20] [30] [40]  → Dequeue
           front              rear
```

**Operations:** All O(1)
- `enqueue(x)` — add to rear
- `dequeue()` — remove from front
- `front()` — view front element
- `isEmpty()` — check if empty

**Variants:**

| Variant | Description | Use Case |
|---------|-------------|----------|
| **Circular Queue** | Rear wraps around to the beginning | Fixed-size buffer (ring buffer) |
| **Deque (Double-Ended)** | Insert/delete from both ends | Sliding window problems |
| **Priority Queue** | Elements dequeued by priority (not order of arrival) | Dijkstra's, task scheduling, Huffman coding |

**Priority Queue Implementation:** Usually implemented using a **heap** (binary heap).

---

## 9.2 Non-Linear Data Structures

### 9.2.1 Trees

A tree is a hierarchical data structure with a root node and child nodes forming a parent-child relationship.

**Key Terminology:**

| Term | Definition |
|------|-----------|
| **Root** | Top node (no parent) |
| **Leaf** | Node with no children |
| **Height** | Longest path from root to a leaf |
| **Depth** | Distance from root to a node |
| **Degree** | Number of children of a node |

**Binary Tree:** Each node has at most 2 children (left and right).

```
        1
       / \
      2   3
     / \   \
    4   5   6
```

**Binary Search Tree (BST):**
- Left subtree values < node value
- Right subtree values > node value

```
        50
       /  \
      30    70
     / \   / \
    20  40 60  80
```

- **Search/Insert/Delete:** Average O(log n), Worst O(n) (degenerate/skewed tree)

**Tree Traversals:**

| Traversal | Order | Example Output (above BST) | Use Case |
|-----------|-------|---------------------------|----------|
| **Inorder** (LNR) | Left → Node → Right | 20, 30, 40, 50, 60, 70, 80 | Sorted output from BST |
| **Preorder** (NLR) | Node → Left → Right | 50, 30, 20, 40, 70, 60, 80 | Copy tree, prefix expression |
| **Postorder** (LRN) | Left → Right → Node | 20, 40, 30, 60, 80, 70, 50 | Delete tree, postfix expression |
| **Level-order** | Level by level (BFS) | 50, 30, 70, 20, 40, 60, 80 | BFS, print by level |

**Self-Balancing BSTs:**

| Tree | Balance Condition | Operations | Use Case |
|------|------------------|-----------|----------|
| **AVL Tree** | Height difference of left and right subtrees ≤ 1 | O(log n) guaranteed | When frequent lookups needed |
| **Red-Black Tree** | Coloring rules ensure approximate balance | O(log n) guaranteed | Java TreeMap, C++ std::map |

**Rotations in AVL:** Used to restore balance after insert/delete.
- **Left Rotation (LL):** Right child becomes parent
- **Right Rotation (RR):** Left child becomes parent
- **Left-Right (LR):** Left rotate left child, then right rotate root
- **Right-Left (RL):** Right rotate right child, then left rotate root

**B-Tree and B+ Tree (for databases/file systems):**

| Feature | B-Tree | B+ Tree |
|---------|--------|---------|
| Keys in | All nodes | All nodes (copies in internal, originals in leaves) |
| Data in | All nodes | Only leaf nodes |
| Leaf linking | Not linked | Leaves linked (sequential access) |
| Use case | General purpose | Database indices (MySQL InnoDB) |

**Heap (Binary Heap):**
- **Max-Heap:** Parent ≥ Children
- **Min-Heap:** Parent ≤ Children
- Stored as an array: parent at `i`, children at `2i+1` and `2i+2`
- Insert: O(log n), Extract min/max: O(log n), Build heap: O(n)
- Used for: Priority queues, heap sort

**Trie (Prefix Tree):**
```
       root
      / | \
     c  d  t
     |  |  |
     a  o  h
    /|  |  |
   r t  g  e
   |
   d
Words: car, card, cat, dog, the
```
- Insert/Search: O(L) where L = length of the word
- Used for: Autocomplete, spell-check, IP routing

### 9.2.2 Graphs

A graph G = (V, E) consists of vertices (V) and edges (E).

**Types:**

| Type | Description |
|------|-------------|
| **Directed** | Edges have direction (A → B ≠ B → A) |
| **Undirected** | Edges are bidirectional (A — B = B — A) |
| **Weighted** | Edges have costs/weights |
| **Unweighted** | All edges have equal weight |
| **Cyclic** | Contains at least one cycle |
| **Acyclic** | No cycles |
| **DAG** | Directed Acyclic Graph (used in scheduling, topological sort) |

**Representations:**

| | Adjacency Matrix | Adjacency List |
|-|------------------|----------------|
| **Space** | O(V²) | O(V + E) |
| **Check if edge exists** | O(1) | O(degree of vertex) |
| **List all neighbors** | O(V) | O(degree of vertex) |
| **Best for** | Dense graphs | Sparse graphs (most real-world graphs) |

**BFS (Breadth-First Search):**
- Uses a **queue**
- Visits level by level (shortest path in unweighted graph)
- Time: O(V + E)

**DFS (Depth-First Search):**
- Uses a **stack** (or recursion)
- Goes deep first, then backtracks
- Time: O(V + E)
- Used for: cycle detection, topological sort, connected components

**Topological Sort:** Linear ordering of vertices in a DAG such that for every directed edge (u, v), u comes before v.
- Used for: build systems, course prerequisites, task scheduling

### 9.2.3 Hash Tables

Store key-value pairs for O(1) average-case lookup.

**Hash Function:** Maps a key to an index: `index = hash(key) % table_size`

**Collision Resolution:**

| Method | How It Works | Pros/Cons |
|--------|-------------|-----------|
| **Chaining** | Each bucket stores a linked list of collisions | Simple; extra memory for pointers |
| **Linear Probing** | If slot occupied, try next slot | Cache-friendly; clustering problem |
| **Quadratic Probing** | Try slots: h+1², h+2², h+3²... | Less clustering than linear |
| **Double Hashing** | Use a second hash function for step size | Best distribution; more computation |

**Load Factor:** $\alpha = n/m$ (number of elements / table size)
- When α exceeds threshold (e.g., 0.75), **rehash** — double the table size and reinsert all elements

---

## 9.3 Sorting Algorithms

### Comparison Table

| Algorithm | Best | Average | Worst | Space | Stable? | Method |
|-----------|------|---------|-------|-------|---------|--------|
| **Bubble Sort** | O(n) | O(n²) | O(n²) | O(1) | Yes | Compare adjacent, swap |
| **Selection Sort** | O(n²) | O(n²) | O(n²) | O(1) | No | Find min, place at front |
| **Insertion Sort** | O(n) | O(n²) | O(n²) | O(1) | Yes | Insert each into sorted portion |
| **Merge Sort** | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes | Divide, sort halves, merge |
| **Quick Sort** | O(n log n) | O(n log n) | O(n²) | O(log n) | No | Partition around pivot |
| **Heap Sort** | O(n log n) | O(n log n) | O(n log n) | O(1) | No | Build heap, extract max |
| **Counting Sort** | O(n+k) | O(n+k) | O(n+k) | O(k) | Yes | Count occurrences |
| **Radix Sort** | O(d·(n+k)) | O(d·(n+k)) | O(d·(n+k)) | O(n+k) | Yes | Sort by each digit |

**Stability:** A stable sort preserves the relative order of equal elements. Important when sorting by multiple keys.

### Key Algorithms Explained

**Merge Sort (Divide & Conquer):**
```
[38, 27, 43, 3, 9, 82, 10]
         Split
[38, 27, 43, 3]  [9, 82, 10]
    Split              Split
[38, 27] [43, 3]  [9, 82] [10]
  Split    Split     Split
[38][27] [43][3]  [9][82] [10]
  Merge    Merge    Merge
[27, 38] [3, 43]  [9, 82] [10]
    Merge              Merge
[3, 27, 38, 43]  [9, 10, 82]
         Merge
[3, 9, 10, 27, 38, 43, 82]
```

**Quick Sort (Divide & Conquer):**
1. Choose a **pivot** element
2. **Partition:** elements < pivot go left, elements > pivot go right
3. Recursively sort left and right

**Why O(n²) worst case?** If pivot is always the smallest/largest element (already sorted array with first/last element as pivot), each partition removes only 1 element.

**When to Use Which Sort?**

| Situation | Best Choice | Why |
|-----------|-------------|-----|
| Small arrays (n < 50) | Insertion Sort | Low overhead, fast for small n |
| General purpose | Quick Sort | Fastest average case, in-place |
| Need stability + guaranteed O(n log n) | Merge Sort | Stable, always O(n log n) |
| Memory constrained | Heap Sort | O(1) extra space, O(n log n) |
| Integers in small range | Counting Sort | O(n + k) — linear time |
| Nearly sorted | Insertion Sort | O(n) best case |

---

## 9.4 Algorithm Design Paradigms

### 9.4.1 Divide and Conquer

**Principle:** Break problem into smaller subproblems, solve each recursively, combine solutions.

| Problem | Divide | Conquer | Combine |
|---------|--------|---------|---------|
| Merge Sort | Split array in half | Sort each half | Merge sorted halves |
| Quick Sort | Partition around pivot | Sort partitions | Already in place |
| Binary Search | Check middle element | Search left or right half | Return result |
| Strassen's Matrix Mult. | Split into sub-matrices | Multiply sub-matrices | Combine results |

### 9.4.2 Dynamic Programming (DP)

**Principle:** When a problem has **overlapping subproblems** (same subproblem solved repeatedly) AND **optimal substructure** (optimal solution built from optimal sub-solutions).

**Two approaches:**
- **Memoization (top-down):** Recursive + cache results in a table
- **Tabulation (bottom-up):** Iterative, fill table from base cases up

**Classic Example — Fibonacci:**

Without DP: $T(n) = T(n-1) + T(n-2)$ → O(2ⁿ) (exponential!)

With memoization:
```
fib(5)
├── fib(4) [compute]
│   ├── fib(3) [compute]
│   │   ├── fib(2) [compute] = 1
│   │   └── fib(1) [cached] = 1
│   └── fib(2) [cached] = 1
└── fib(3) [cached] = 2
```
Time: O(n), Space: O(n)

**Important DP Problems:**

| Problem | Description | Time |
|---------|-------------|------|
| **0/1 Knapsack** | Select items with max value, limited capacity | O(nW) |
| **Longest Common Subsequence (LCS)** | Longest subsequence common to two strings | O(mn) |
| **Longest Increasing Subsequence (LIS)** | Longest strictly increasing subsequence | O(n²) or O(n log n) |
| **Edit Distance** | Min operations to convert one string to another | O(mn) |
| **Matrix Chain Multiplication** | Optimal parenthesization for matrix products | O(n³) |
| **Floyd-Warshall** | All-pairs shortest paths | O(V³) |
| **Coin Change** | Min coins to make a given amount | O(n·amount) |

### 9.4.3 Greedy Algorithms

**Principle:** At each step, make the **locally optimal** choice, hoping it leads to the global optimum. Does NOT always work — must prove "greedy choice property."

| Problem | Greedy Strategy | Does It Work? |
|---------|----------------|--------------|
| **Activity Selection** | Always pick earliest finishing activity | Yes (proven optimal) |
| **Fractional Knapsack** | Take item with highest value/weight ratio | Yes |
| **0/1 Knapsack** | Take item with highest value/weight ratio | NO — DP required |
| **Huffman Coding** | Combine two lowest-frequency nodes | Yes |
| **Dijkstra's Shortest Path** | Always expand nearest unvisited vertex | Yes (non-negative weights) |
| **Kruskal's MST** | Pick cheapest edge that doesn't create a cycle | Yes |
| **Prim's MST** | Grow tree by adding cheapest adjacent edge | Yes |

### 9.4.4 Backtracking

**Principle:** Build solution incrementally; abandon a candidate as soon as it violates constraints ("prune").

```
               Start
              / | \
             Q  Q  Q  ...  (place Queen in column 1)
            /|\
           Q Q Q  ...      (place Queen in column 2)
           ✗ ✓ ...         (check: does it attack? if yes, backtrack)
```

**Classic Problems:** N-Queens, Sudoku solver, subset sum, graph coloring, maze solving.

---

## 9.5 Graph Algorithms

### 9.5.1 Shortest Path Algorithms

| Algorithm | Type | Handles Negative Weights? | Time |
|-----------|------|--------------------------|------|
| **Dijkstra's** | Single-source | No | O((V+E) log V) with min-heap |
| **Bellman-Ford** | Single-source | Yes (detects negative cycles) | O(VE) |
| **Floyd-Warshall** | All-pairs | Yes (no negative cycles) | O(V³) |

**Dijkstra's Algorithm (Key for exam):**
1. Set distance to source = 0, all others = ∞
2. Visit the unvisited node with smallest distance
3. Update distances to its neighbors
4. Mark node as visited
5. Repeat until all nodes visited

### 9.5.2 Minimum Spanning Tree (MST)

A spanning tree that connects all vertices with minimum total edge weight.

| Algorithm | Strategy | Time |
|-----------|----------|------|
| **Kruskal's** | Sort all edges by weight; add cheapest edge that doesn't create a cycle (Union-Find) | O(E log E) |
| **Prim's** | Start from any node; grow tree by adding cheapest edge to an unvisited node | O((V+E) log V) |

### 9.5.3 Other Graph Algorithms

| Algorithm | Purpose | Time |
|-----------|---------|------|
| **Topological Sort** | Order tasks with dependencies (DAG only) | O(V + E) |
| **Tarjan's / Kosaraju's** | Find Strongly Connected Components | O(V + E) |
| **Ford-Fulkerson** | Maximum flow in a network | O(V · E²) |

---

## 9.6 Complexity Analysis

### Asymptotic Notations

| Notation | Meaning | Formal Definition | Analogy |
|----------|---------|-------------------|---------|
| **O(f(n))** — Big-O | Upper bound (worst case ≤) | g(n) ≤ c·f(n) for large n | "At most this slow" |
| **Ω(f(n))** — Big-Omega | Lower bound (best case ≥) | g(n) ≥ c·f(n) for large n | "At least this fast" |
| **Θ(f(n))** — Big-Theta | Tight bound (exact order) | c₁·f(n) ≤ g(n) ≤ c₂·f(n) | "Exactly this speed" |

### Common Complexities (ranked fastest to slowest)

$$O(1) < O(\log n) < O(\sqrt{n}) < O(n) < O(n \log n) < O(n^2) < O(n^3) < O(2^n) < O(n!)$$

| Complexity | Name | Example |
|-----------|------|---------|
| O(1) | Constant | Array access, hash table lookup |
| O(log n) | Logarithmic | Binary search |
| O(n) | Linear | Linear search, single pass |
| O(n log n) | Linearithmic | Merge sort, heap sort |
| O(n²) | Quadratic | Bubble sort, nested loops |
| O(n³) | Cubic | Floyd-Warshall, matrix multiplication |
| O(2ⁿ) | Exponential | Recursive Fibonacci (without DP), subset generation |
| O(n!) | Factorial | Permutation generation, brute-force TSP |

### Master Theorem

For recurrences of the form: $T(n) = aT(n/b) + f(n)$
where $a ≥ 1$, $b > 1$

Let $c = \log_b a$

| Case | Condition | T(n) |
|------|-----------|------|
| Case 1 | $f(n) = O(n^{c-\epsilon})$ for some ε > 0 | $\Theta(n^c)$ |
| Case 2 | $f(n) = \Theta(n^c)$ | $\Theta(n^c \log n)$ |
| Case 3 | $f(n) = \Omega(n^{c+\epsilon})$ for some ε > 0 | $\Theta(f(n))$ |

**Example:** Merge Sort: $T(n) = 2T(n/2) + n$
- a = 2, b = 2, f(n) = n
- $c = \log_2 2 = 1$
- f(n) = n = Θ(n¹) → Case 2
- $T(n) = \Theta(n \log n)$ ✓

---

## 9.7 Practice Questions

**Q1.** Compare array and linked list for: (a) random access, (b) insertion at the beginning, (c) memory usage.
> **Answer:** (a) Array: O(1), Linked List: O(n) — arrays win for random access. (b) Array: O(n) — must shift all elements, Linked List: O(1) — just update head pointer. (c) Arrays use less memory per element (just the data), while linked lists require extra pointer(s) per node (4-8 bytes each). For a doubly linked list, overhead is even higher.

**Q2.** You need to find the top-K elements from a stream of N numbers where N is very large and K is small. Which data structure and algorithm would you use?
> **Answer:** Use a **min-heap of size K**. For each new number: if it's larger than the heap's minimum, remove the minimum and insert the new number. After processing all N numbers, the heap contains the top-K elements. Time: O(N log K). This is much better than sorting (O(N log N)) when K << N.

**Q3.** What is the difference between Dijkstra's and Bellman-Ford? When would you choose Bellman-Ford?
> **Answer:** Dijkstra's is faster — O((V+E) log V) but only works with **non-negative edge weights**. Bellman-Ford is slower — O(VE) but handles **negative edge weights** and can detect **negative cycles**. Choose Bellman-Ford when the graph may have negative edges (e.g., in financial arbitrage detection).

**Q4.** Explain the difference between memoization and tabulation in Dynamic Programming.
> **Answer:** **Memoization (top-down):** Uses recursion; stores results of already-solved subproblems in a cache; solves only the subproblems that are needed. **Tabulation (bottom-up):** Uses iteration; fills a table starting from base cases up to the desired answer; solves ALL subproblems. Tabulation is generally faster (no recursion overhead) and uses predictable memory, while memoization is easier to implement and naturally avoids solving unnecessary subproblems.

**Q5.** Apply the Master Theorem to: $T(n) = 4T(n/2) + n$
> **Answer:** a = 4, b = 2, f(n) = n. $c = \log_2 4 = 2$. Compare f(n) = n with $n^c = n^2$. Since $n = O(n^{2-1})$, this is Case 1 with ε = 1. Therefore, $T(n) = \Theta(n^2)$.

---

*Previous: [Chapter 8 — Report Writing](../Part_A_Research_Methodology/08_Report_Writing_and_Thesis_Structure.md) | Next: [Chapter 10 — DBMS](10_DBMS.md)*
