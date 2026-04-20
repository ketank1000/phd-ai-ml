# 13. Theory of Computation

> **Part B1 — Core Computer Science** | SIU PET Complete Study Guide

---

## 13.1 Finite Automata

### 13.1.1 DFA (Deterministic Finite Automaton)

A mathematical model of computation with a finite number of states. For every state and input symbol, there is **exactly one** transition.

**Formal Definition:** A DFA is a 5-tuple (Q, Σ, δ, q₀, F) where:
- Q = finite set of states
- Σ = input alphabet
- δ = transition function: Q × Σ → Q
- q₀ = start state
- F = set of accepting (final) states

**Example:** DFA that accepts strings ending in "01":

```
           0        1        0        1
→ (q0) ──────→ (q1) ──────→ (q0) ──────→ (q1) ──────→ ((q2))
    ↑                                                      │
    └──── 0 ──────────────────────────────────────────────┘
                            1
```

| State | Input 0 | Input 1 |
|-------|---------|---------|
| →q0 | q1 | q0 |
| q1 | q1 | q2 |
| *q2 | q1 | q0 |

### 13.1.2 NFA (Non-deterministic Finite Automaton)

Like DFA but allows:
- Multiple transitions for the same input from a state
- **ε-transitions** (transitions without consuming input)
- A string is accepted if ANY path leads to an accepting state

**Key Result:** Every NFA can be converted to an equivalent DFA (subset construction). However, the DFA may have up to 2ⁿ states if the NFA has n states.

### 13.1.3 Regular Expressions

Concise notation for describing regular languages.

| Operation | Symbol | Meaning | Example |
|-----------|--------|---------|---------|
| **Concatenation** | ab | a followed by b | "ab" |
| **Union** | a\|b (or a+b) | a or b | "a or b" |
| **Kleene Star** | a* | Zero or more a's | "", "a", "aa", "aaa", ... |
| **Kleene Plus** | a⁺ | One or more a's | "a", "aa", "aaa", ... |
| **Optional** | a? | Zero or one a | "", "a" |

**Equivalence:** Regular expressions = DFAs = NFAs (all describe exactly the class of regular languages).

---

## 13.2 Regular Languages

### Closure Properties

Regular languages are closed under:
- **Union** (L₁ ∪ L₂)
- **Concatenation** (L₁ · L₂)
- **Kleene Star** (L*)
- **Intersection** (L₁ ∩ L₂)
- **Complement** (L̄)
- **Difference** (L₁ − L₂)
- **Reversal** (Lᴿ)

### Pumping Lemma for Regular Languages

Used to **prove** a language is **NOT regular** (proof by contradiction).

**Statement:** If L is regular, then there exists a pumping length p such that any string s ∈ L with |s| ≥ p can be split as s = xyz where:
1. |y| > 0 (y is non-empty)
2. |xy| ≤ p
3. For all i ≥ 0, xy^iz ∈ L (pumping y any number of times still gives a string in L)

**Classic Example:** Prove L = {aⁿbⁿ | n ≥ 0} is NOT regular.
- Assume L is regular with pumping length p
- Choose s = aᵖbᵖ (length 2p ≥ p) ✓
- s = xyz where |xy| ≤ p → y = aᵏ for some k > 0 (all in the a-part)
- Pump: xy²z = aᵖ⁺ᵏbᵖ — more a's than b's → NOT in L
- Contradiction! → L is not regular ✓

### What Regular Languages CAN'T Do

- Cannot count (aⁿbⁿ)
- Cannot match patterns (palindromes)
- Cannot nest (balanced parentheses)
- Limited to **finite memory** (finite number of states)

---

## 13.3 Context-Free Languages

### Context-Free Grammar (CFG)

**Definition:** A 4-tuple (V, Σ, R, S) where:
- V = set of variables (non-terminals)
- Σ = set of terminals
- R = production rules: V → (V ∪ Σ)*
- S = start variable

**Example:** L = {aⁿbⁿ | n ≥ 1}
```
S → aSb | ab
```

**Derivation of "aaabbb":**
```
S → aSb → aaSbb → aaabbb
```

### Pushdown Automata (PDA)

A finite automaton with an additional **stack** (infinite memory, but LIFO access only).

PDA = FA + Stack → accepts exactly the context-free languages.

**Why the stack helps:** It can count! Push a's onto the stack, then pop one a for each b → matches aⁿbⁿ.

### Normal Forms

| Form | Rule | Purpose |
|------|------|---------|
| **Chomsky Normal Form (CNF)** | Every rule is A → BC or A → a | CYK parsing algorithm |
| **Greibach Normal Form (GNF)** | Every rule is A → aα (starts with a terminal) | LL parsing |

### Pumping Lemma for CFLs

Similar to the regular pumping lemma but splits string s = uvxyz with:
1. |vy| > 0
2. |vxy| ≤ p
3. For all i ≥ 0, uv^ixy^iz ∈ L

Used to prove languages like {aⁿbⁿcⁿ} are NOT context-free.

---

## 13.4 Turing Machines

### Definition

A Turing Machine (TM) is a theoretical model of computation with:
- An infinite tape (read/write head)
- A finite set of states
- A transition function that can read, write, and move left or right

A TM can compute anything that any computer can compute (**Church-Turing Thesis**).

### Language Classification

| Language Type | Recognized By | Example |
|--------------|--------------|---------|
| **Regular** | DFA/NFA | a*b* |
| **Context-Free** | PDA | aⁿbⁿ |
| **Context-Sensitive** | Linear Bounded Automaton | aⁿbⁿcⁿ |
| **Recursively Enumerable** | Turing Machine | Any TM-recognizable language |
| **Recursive (Decidable)** | TM that always halts | Languages where TM says Yes or No |

### Chomsky Hierarchy

```
┌───────────────────────────────────────────┐
│  Type 0: Recursively Enumerable (TM)      │
│  ┌────────────────────────────────────┐   │
│  │  Type 1: Context-Sensitive (LBA)   │   │
│  │  ┌─────────────────────────────┐   │   │
│  │  │  Type 2: Context-Free (PDA) │   │   │
│  │  │  ┌──────────────────────┐   │   │   │
│  │  │  │  Type 3: Regular (FA)│   │   │   │
│  │  │  └──────────────────────┘   │   │   │
│  │  └─────────────────────────────┘   │   │
│  └────────────────────────────────────┘   │
└───────────────────────────────────────────┘
```

### Decidability

| Problem | Decidable? | Explanation |
|---------|-----------|-------------|
| "Does this DFA accept string w?" | Yes | Simulate DFA on w |
| "Is this CFL empty?" | Yes | Check if start variable generates any string |
| "Does this TM halt on input w?" | **No** (Halting Problem) | Undecidable — proven by Alan Turing via diagonalization |
| "Are two CFGs equivalent?" | **No** | Undecidable |

---

## 13.5 Computational Complexity

### Complexity Classes

| Class | Definition | Examples |
|-------|-----------|----------|
| **P** | Problems solvable in polynomial time O(nᵏ) by a deterministic TM | Sorting, shortest path, primality testing |
| **NP** | Problems whose solutions can be **verified** in polynomial time | SAT, graph coloring, TSP (decision version) |
| **NP-Hard** | At least as hard as any NP problem | Halting problem, TSP (optimization) |
| **NP-Complete** | In NP AND NP-Hard; the "hardest" problems in NP | SAT, 3-SAT, vertex cover, Hamiltonian cycle |

### P vs. NP

The most famous open question in CS: **Is P = NP?**

```
If P ≠ NP (believed):        If P = NP:
┌──────────── NP ──────────┐  ┌──────────────┐
│  ┌── NP-Complete ──┐     │  │   P = NP     │
│  │  SAT, TSP,      │     │  │  (everything  │
│  │  Graph Coloring  │     │  │   is easy)   │
│  └──────────────────┘     │  └──────────────┘
│  ┌──── P ────┐            │
│  │ Sorting,   │            │
│  │ Shortest   │            │
│  │ Path       │            │
│  └────────────┘            │
└───────────────────────────┘
```

**If P = NP were proven:** All NP problems could be solved efficiently. Cryptography would break. This is considered extremely unlikely.

### NP-Complete Problems (Important Examples)

| Problem | Description |
|---------|------------|
| **SAT** | Is there an assignment of variables that satisfies a Boolean formula? (First NP-Complete problem, Cook-Levin theorem) |
| **3-SAT** | SAT restricted to clauses with exactly 3 literals |
| **Vertex Cover** | Find minimum set of vertices that covers all edges |
| **Graph Coloring** | Can the graph be colored with k colors such that no adjacent vertices share a color? |
| **Hamiltonian Cycle** | Does a cycle visiting every vertex exactly once exist? |
| **Traveling Salesman (Decision)** | Is there a tour of total cost ≤ k? |
| **Subset Sum** | Is there a subset that sums to target value? |

**Reduction:** To prove a problem X is NP-Complete:
1. Show X is in NP (solution verifiable in polynomial time)
2. Reduce a known NP-Complete problem to X in polynomial time

---

## 13.6 Practice Questions

**Q1.** Construct a DFA that accepts binary strings divisible by 3.
> **Answer:** States: q0 (remainder 0, start & accept), q1 (remainder 1), q2 (remainder 2). Transitions: From q0: 0→q0, 1→q1. From q1: 0→q2, 1→q0. From q2: 0→q1, 1→q2. The DFA tracks the running remainder when dividing by 3 in binary. String "110" (6 in decimal): q0→q1→q0→q0 → accepted ✓

**Q2.** Use the pumping lemma to prove L = {ww | w ∈ {a,b}*} is not regular.
> **Answer:** Assume L is regular with pumping length p. Choose s = aᵖbaᵖb (which is in L since w = aᵖb). s = xyz with |xy| ≤ p, so y = aᵏ for some k > 0 (within the first aᵖ). Pump: xy⁰z = aᵖ⁻ᵏbaᵖb. The first half would be aᵖ⁻ᵏb and the second half aᵖb — they're not equal. So xy⁰z ∉ L. Contradiction → L is not regular.

**Q3.** What is the difference between P, NP, and NP-Complete?
> **Answer:** **P:** Problems solvable in polynomial time (efficient algorithms exist). **NP:** Problems whose solutions can be verified in polynomial time (but finding the solution may be hard). **NP-Complete:** The hardest problems in NP — if any NP-Complete problem can be solved in polynomial time, then ALL NP problems can be (P = NP). Every problem in P is also in NP (P ⊆ NP), but whether P = NP is unknown.

**Q4.** Is the Halting Problem decidable? Explain.
> **Answer:** No. The Halting Problem ("Given a TM M and input w, does M halt on w?") is **undecidable**. Proof by contradiction: Assume a TM H decides it. Construct a TM D that runs H on itself: if H says "halts," D loops forever; if H says "doesn't halt," D halts. Running D on itself leads to a contradiction (halts ↔ doesn't halt). Therefore, no such H can exist.

**Q5.** What is the Chomsky Hierarchy? Name all four types with their recognizers.
> **Answer:** Type 3: Regular languages → Finite Automata (DFA/NFA). Type 2: Context-Free languages → Pushdown Automata. Type 1: Context-Sensitive languages → Linear Bounded Automata. Type 0: Recursively Enumerable languages → Turing Machines. Each level strictly includes the ones below it.

---

*Previous: [Chapter 12 — Computer Networks](12_Computer_Networks.md) | Next: [Chapter 14 — Discrete Mathematics](14_Discrete_Mathematics.md)*
