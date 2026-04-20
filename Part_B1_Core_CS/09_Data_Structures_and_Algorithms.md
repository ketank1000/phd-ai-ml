# 9. Data Structures & Algorithms

> **Part B1 — Core Computer Science** | SIU PET Study Guide

---

## 9.1 Linear Data Structures

- [ ] **Arrays**
  - 1D, 2D, dynamic arrays
  - Time: Access O(1), Search O(n), Insert/Delete O(n)

- [ ] **Linked Lists**
  - Singly, doubly, circular
  - Operations: insert, delete, reverse, detect cycle (Floyd's)
  - Time: Access O(n), Insert at head O(1)

- [ ] **Stacks**
  - LIFO | Operations: push, pop, peek
  - Applications: expression evaluation, parenthesis matching, function call stack, undo operations

- [ ] **Queues**
  - FIFO | Variants: circular queue, deque, priority queue
  - Applications: BFS, scheduling, buffering

---

## 9.2 Non-Linear Data Structures

- [ ] **Trees**
  - Binary tree, BST, AVL tree, Red-black tree
  - B-tree, B+ tree (used in databases/file systems)
  - Heap: max-heap, min-heap (priority queue implementation)
  - Trie (prefix tree — used in autocomplete, spell-check)
  - Traversals: inorder, preorder, postorder, level-order
  - BST operations: insert, delete, search — average O(log n), worst O(n)

- [ ] **Graphs**
  - Representation: adjacency matrix, adjacency list
  - Types: directed/undirected, weighted/unweighted, cyclic/acyclic, DAG
  - Traversals: BFS (O(V+E)), DFS (O(V+E))
  - Topological sort (DAG only)

- [ ] **Hash Tables**
  - Hash functions, collision resolution: chaining, open addressing (linear probing, quadratic probing, double hashing)
  - Average: O(1) for insert/search/delete
  - Load factor, rehashing

---

## 9.3 Sorting Algorithms

| Algorithm | Best | Average | Worst | Space | Stable? |
|-----------|------|---------|-------|-------|---------|
| **Bubble Sort** | O(n) | O(n²) | O(n²) | O(1) | Yes |
| **Selection Sort** | O(n²) | O(n²) | O(n²) | O(1) | No |
| **Insertion Sort** | O(n) | O(n²) | O(n²) | O(1) | Yes |
| **Merge Sort** | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |
| **Quick Sort** | O(n log n) | O(n log n) | O(n²) | O(log n) | No |
| **Heap Sort** | O(n log n) | O(n log n) | O(n log n) | O(1) | No |
| **Counting Sort** | O(n+k) | O(n+k) | O(n+k) | O(k) | Yes |
| **Radix Sort** | O(nk) | O(nk) | O(nk) | O(n+k) | Yes |

---

## 9.4 Algorithm Design Paradigms

- [ ] **Divide & Conquer**: Merge sort, quick sort, binary search, Strassen's matrix multiplication
- [ ] **Dynamic Programming**: Overlapping subproblems + optimal substructure
  - Examples: 0/1 knapsack, LCS, LIS, matrix chain multiplication, Fibonacci, edit distance, Floyd-Warshall
  - Memoization (top-down) vs. Tabulation (bottom-up)
- [ ] **Greedy Algorithms**: Locally optimal choices → globally optimal
  - Examples: Activity selection, Huffman coding, fractional knapsack, Kruskal's MST, Dijkstra's shortest path
- [ ] **Backtracking**: N-Queens, Sudoku solver, subset sum, graph coloring

---

## 9.5 Graph Algorithms

- [ ] **Shortest Path**:
  - Dijkstra's (non-negative weights, O(V² or (V+E)logV with heap))
  - Bellman-Ford (handles negative weights, O(VE))
  - Floyd-Warshall (all pairs, O(V³))
- [ ] **Minimum Spanning Tree**:
  - Prim's algorithm (O(V² or (V+E)logV))
  - Kruskal's algorithm (O(E log E))
- [ ] **Strongly Connected Components**: Tarjan's, Kosaraju's
- [ ] **Network Flow**: Ford-Fulkerson, max-flow min-cut theorem

---

## 9.6 Complexity Analysis

- [ ] **Asymptotic Notations**
  - Big-O (upper bound): O(f(n))
  - Big-Omega (lower bound): Ω(f(n))
  - Big-Theta (tight bound): Θ(f(n))
- [ ] **Common Complexities (fastest → slowest)**
  - O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(n³) < O(2ⁿ) < O(n!)
- [ ] **Master Theorem** for recurrences: $T(n) = aT(n/b) + f(n)$

---

### Recommended Resources
- **Book**: *Introduction to Algorithms* (CLRS) — Cormen et al.
- **Book**: *Data Structures and Algorithms Made Easy* — Narasimha Karumanchi
- **Practice**: LeetCode, GeeksforGeeks
