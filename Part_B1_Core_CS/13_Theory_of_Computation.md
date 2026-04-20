# 13. Theory of Computation

> **Part B1 — Core Computer Science** | SIU PET Study Guide

---

- [ ] **Finite Automata**
  - DFA (Deterministic): One transition per symbol per state
  - NFA (Non-deterministic): Multiple transitions, ε-transitions
  - DFA ↔ NFA equivalence (subset construction)
  - Regular expressions ↔ Finite automata equivalence

- [ ] **Regular Languages**
  - Closure properties: union, concatenation, Kleene star, intersection, complement
  - Pumping lemma for regular languages (used to prove a language is NOT regular)
  - Limitations: Can't count (e.g., aⁿbⁿ is not regular)

- [ ] **Context-Free Languages**
  - Context-Free Grammar (CFG): S → aSb | ε
  - Pushdown Automata (PDA): FA + stack
  - Chomsky Normal Form (CNF), Greibach Normal Form (GNF)
  - Pumping lemma for CFLs
  - CYK parsing algorithm

- [ ] **Turing Machines**
  - Deterministic Turing Machine (DTM)
  - Church-Turing thesis
  - Decidable vs. undecidable problems
  - **Halting problem**: Undecidable
  - Recursively enumerable vs. recursive languages

- [ ] **Computational Complexity**
  - **P**: Problems solvable in polynomial time
  - **NP**: Solutions verifiable in polynomial time
  - **NP-Hard**: At least as hard as NP problems
  - **NP-Complete**: In NP AND NP-Hard
  - P vs NP: Open question! (P ⊆ NP, but P = NP?)
  - NP-Complete examples: SAT, 3-SAT, Traveling Salesman (decision), Graph Coloring, Vertex Cover

---

### Recommended Resources
- **Book**: *Introduction to Automata Theory, Languages, and Computation* — Hopcroft, Motwani, Ullman
- **Book**: *Theory of Computation* — Michael Sipser
