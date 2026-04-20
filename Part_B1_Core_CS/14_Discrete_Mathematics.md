# 14. Discrete Mathematics

> **Part B1 — Core Computer Science** | SIU PET Complete Study Guide

---

## 14.1 Set Theory

### Basic Concepts

A **set** is an unordered collection of distinct elements. 

**Notation:** A = {1, 2, 3}, B = {x | x is even and x > 0}

| Concept | Notation | Example |
|---------|----------|---------|
| **Membership** | x ∈ A | 2 ∈ {1, 2, 3} |
| **Subset** | A ⊆ B | {1, 2} ⊆ {1, 2, 3} |
| **Proper Subset** | A ⊂ B | {1, 2} ⊂ {1, 2, 3} |
| **Empty Set** | ∅ or {} | Set with no elements |
| **Universal Set** | U | All elements under consideration |
| **Cardinality** | \|A\| | \|{1, 2, 3}\| = 3 |
| **Power Set** | P(A) | P({1,2}) = {∅, {1}, {2}, {1,2}} — has 2ⁿ elements |

### Set Operations

| Operation | Symbol | Definition | Example (A={1,2,3}, B={2,3,4}) |
|-----------|--------|-----------|-------------------------------|
| **Union** | A ∪ B | Elements in A OR B (or both) | {1, 2, 3, 4} |
| **Intersection** | A ∩ B | Elements in BOTH A and B | {2, 3} |
| **Difference** | A − B | Elements in A but NOT in B | {1} |
| **Complement** | A' or Ā | Elements NOT in A (relative to U) | U − A |
| **Symmetric Difference** | A △ B | Elements in A or B but NOT both | {1, 4} |
| **Cartesian Product** | A × B | All ordered pairs (a, b) | {(1,2),(1,3),(1,4),(2,2),...} — 12 pairs |

### De Morgan's Laws

$$(A \cup B)' = A' \cap B'$$
$$(A \cap B)' = A' \cup B'$$

> "The complement of the union is the intersection of complements" (and vice versa).
> These also apply to logic: ¬(p ∨ q) ≡ (¬p) ∧ (¬q)

---

## 14.2 Relations

A **relation** R from set A to set B is a subset of A × B. If (a, b) ∈ R, we write aRb.

### Properties of Relations (on a set A)

| Property | Definition | Example on {1,2,3} |
|----------|-----------|-------------------|
| **Reflexive** | ∀a ∈ A: (a,a) ∈ R | ≤ is reflexive (1≤1, 2≤2, 3≤3) |
| **Irreflexive** | ∀a ∈ A: (a,a) ∉ R | < is irreflexive |
| **Symmetric** | If (a,b) ∈ R then (b,a) ∈ R | "is sibling of" |
| **Antisymmetric** | If (a,b) ∈ R and (b,a) ∈ R then a = b | ≤ (if a≤b and b≤a then a=b) |
| **Transitive** | If (a,b) ∈ R and (b,c) ∈ R then (a,c) ∈ R | < (if a<b and b<c then a<c) |

### Special Relations

| Type | Properties | Example |
|------|-----------|---------|
| **Equivalence Relation** | Reflexive + Symmetric + Transitive | "Same age as," "congruent modulo n" |
| **Partial Order** | Reflexive + Antisymmetric + Transitive | ≤ on integers, ⊆ on sets |
| **Total Order** | Partial order where every pair is comparable | ≤ on real numbers |

**Equivalence classes** partition the set into disjoint subsets.
> Example: Mod 3 equivalence on {0,1,2,3,4,5}: Classes are {0,3}, {1,4}, {2,5}

**Hasse Diagram:** Visual representation of a partial order (draw lines for direct relationships, remove redundant edges and direction).

---

## 14.3 Functions

A **function** f: A → B maps every element of A to exactly one element of B.

| Type | Definition | Example |
|------|-----------|---------|
| **Injective (One-to-one)** | f(a₁) = f(a₂) → a₁ = a₂ (different inputs → different outputs) | f(x) = 2x |
| **Surjective (Onto)** | For every b ∈ B, ∃ a ∈ A such that f(a) = b (every element in B is "hit") | f: ℤ → ℤ, f(x) = x+1 |
| **Bijective** | Both injective AND surjective (one-to-one correspondence) | f(x) = x+1 from ℤ to ℤ |

**Composition:** (g ∘ f)(x) = g(f(x)) — apply f first, then g
**Inverse:** f⁻¹ exists if and only if f is bijective

### Pigeonhole Principle

If n items are placed into m containers and n > m, then at least one container must hold more than one item.

> **Example:** In any group of 367 people, at least two share a birthday (367 people, 366 possible days).
> **CS Example:** A hash table with 100 slots and 101 keys must have at least one collision.

---

## 14.4 Propositional Logic

### Logical Operators

| Operator | Symbol | Name | Truth |
|----------|--------|------|-------|
| NOT | ¬p | Negation | True when p is false |
| AND | p ∧ q | Conjunction | True when BOTH true |
| OR | p ∨ q | Disjunction | True when at LEAST one true |
| IMPLIES | p → q | Conditional | False ONLY when p=T, q=F |
| BICONDITIONAL | p ↔ q | Biconditional | True when both same value |
| XOR | p ⊕ q | Exclusive OR | True when exactly one true |

### Truth Table for p → q (IMPORTANT — counterintuitive!)

| p | q | p → q |
|---|---|-------|
| T | T | **T** |
| T | F | **F** ← Only this is false |
| F | T | **T** |
| F | F | **T** |

> "If it rains, then the ground is wet." Only false when it rains (T) but ground is NOT wet (F).

### Key Equivalences

| Name | Equivalence |
|------|------------|
| **Double Negation** | ¬(¬p) ≡ p |
| **De Morgan's** | ¬(p ∧ q) ≡ ¬p ∨ ¬q; ¬(p ∨ q) ≡ ¬p ∧ ¬q |
| **Contrapositive** | p → q ≡ ¬q → ¬p |
| **Implication** | p → q ≡ ¬p ∨ q |
| **Distributive** | p ∧ (q ∨ r) ≡ (p ∧ q) ∨ (p ∧ r) |
| **Absorption** | p ∨ (p ∧ q) ≡ p |

### Normal Forms

| Form | Structure | Example |
|------|-----------|---------|
| **CNF (Conjunctive Normal Form)** | AND of ORs | (p ∨ q) ∧ (¬p ∨ r) |
| **DNF (Disjunctive Normal Form)** | OR of ANDs | (p ∧ q) ∨ (¬p ∧ r) |

### Special Formulas

| Type | Definition | Example |
|------|-----------|---------|
| **Tautology** | Always true regardless of values | p ∨ ¬p |
| **Contradiction** | Always false | p ∧ ¬p |
| **Contingency** | Sometimes true, sometimes false | p ∨ q |

---

## 14.5 Predicate Logic

Extends propositional logic with **variables**, **predicates**, and **quantifiers**.

**Predicate:** P(x) = "x is greater than 5" (becomes a proposition when x has a value)

### Quantifiers

| Quantifier | Symbol | Meaning | Negation |
|-----------|--------|---------|----------|
| **Universal** | ∀x P(x) | "For ALL x, P(x) holds" | ¬(∀x P(x)) ≡ ∃x ¬P(x) |
| **Existential** | ∃x P(x) | "There EXISTS at least one x for which P(x) holds" | ¬(∃x P(x)) ≡ ∀x ¬P(x) |

> **Example:** "Every student passed" = ∀x (Student(x) → Passed(x))
> Negation: "There exists a student who didn't pass" = ∃x (Student(x) ∧ ¬Passed(x))

---

## 14.6 Graph Theory

### Basic Concepts

- **Graph** G = (V, E) where V = vertices, E = edges
- **Degree** of vertex v: Number of edges incident on v, denoted deg(v)
- **Handshaking Lemma:** $\sum_{v \in V} deg(v) = 2|E|$ (each edge contributes 2 to total degree)

### Euler Paths and Circuits

| Concept | Visits | Condition |
|---------|--------|-----------|
| **Euler Path** | Every EDGE exactly once | Exactly 0 or 2 vertices have odd degree |
| **Euler Circuit** | Every edge once, returns to start | ALL vertices have even degree |
| **Hamiltonian Path** | Every VERTEX exactly once | No simple condition (NP-complete to decide) |
| **Hamiltonian Cycle** | Every vertex once, returns to start | No simple condition (NP-complete) |

### Graph Coloring

Assign colors to vertices such that no two adjacent vertices share a color.

**Chromatic Number** χ(G): Minimum colors needed.
- Complete graph Kₙ: χ = n
- Tree: χ = 2 (bipartite)
- Cycle (even length): χ = 2
- Cycle (odd length): χ = 3
- Planar graph: χ ≤ 4 (Four Color Theorem)

### Planar Graphs

A graph that can be drawn on a plane without edge crossings.

**Euler's Formula:** $V - E + F = 2$ (where F = faces, including the outer face)

For a connected planar graph with V ≥ 3: $E ≤ 3V - 6$

**Kuratowski's Theorem:** A graph is planar iff it contains no subgraph homeomorphic to K₅ or K₃,₃.

### Trees

| Property | Value |
|----------|-------|
| Edges | n − 1 (for n vertices) |
| Connected? | Yes |
| Cycles? | No |
| Path between any two vertices | Unique |

---

## 14.7 Combinatorics

### Counting Principles

| Principle | Description |
|-----------|------------|
| **Addition** | If task can be done in n₁ OR n₂ ways → n₁ + n₂ total |
| **Multiplication** | If task has stages done in n₁ AND n₂ ways → n₁ × n₂ total |

### Permutations and Combinations

| | Formula | Order Matters? | Example |
|-|---------|---------------|---------|
| **Permutation** | $P(n,r) = \frac{n!}{(n-r)!}$ | Yes | Arranging 3 books from 5: P(5,3) = 60 |
| **Combination** | $C(n,r) = \binom{n}{r} = \frac{n!}{r!(n-r)!}$ | No | Choosing 3 books from 5: C(5,3) = 10 |

### Binomial Theorem

$$(x + y)^n = \sum_{k=0}^{n} \binom{n}{k} x^{n-k} y^k$$

> $(1+x)^4 = 1 + 4x + 6x^2 + 4x^3 + x^4$

### Inclusion-Exclusion Principle

$$|A \cup B| = |A| + |B| - |A \cap B|$$

For three sets:
$$|A \cup B \cup C| = |A| + |B| + |C| - |A \cap B| - |A \cap C| - |B \cap C| + |A \cap B \cap C|$$

---

## 14.8 Number Theory

### GCD and Euclidean Algorithm

**GCD** (Greatest Common Divisor): Largest number that divides both a and b.

**Euclidean Algorithm:**
```
GCD(252, 105):
252 = 2 × 105 + 42
105 = 2 × 42  + 21
42  = 2 × 21  + 0
GCD = 21
```

**Relation:** $GCD(a,b) \times LCM(a,b) = a \times b$

### Modular Arithmetic

$$a \equiv b \pmod{m} \text{ means } m \text{ divides } (a-b)$$

**Key properties:**
- $(a + b) \mod m = ((a \mod m) + (b \mod m)) \mod m$
- $(a \times b) \mod m = ((a \mod m) \times (b \mod m)) \mod m$

### Fermat's Little Theorem

If p is prime and gcd(a, p) = 1:
$$a^{p-1} \equiv 1 \pmod{p}$$

> Used in RSA encryption and primality testing.

### Euler's Totient Function φ(n)

Counts integers from 1 to n that are coprime to n.
- φ(p) = p − 1 for prime p
- φ(p × q) = (p−1)(q−1) for distinct primes p, q (used in RSA!)

---

## 14.9 Practice Questions

**Q1.** A = {1,2,3,4,5}, B = {3,4,5,6,7}. Find A ∪ B, A ∩ B, A − B, and |P(A ∩ B)|.
> **Answer:** A ∪ B = {1,2,3,4,5,6,7}. A ∩ B = {3,4,5}. A − B = {1,2}. |A ∩ B| = 3, so |P(A ∩ B)| = 2³ = **8**.

**Q2.** Is the relation R = {(1,1),(2,2),(3,3),(1,2),(2,1)} on {1,2,3} an equivalence relation?
> **Answer:** Reflexive: (1,1),(2,2),(3,3) ∈ R ✓. Symmetric: (1,2) ∈ R and (2,1) ∈ R ✓. Transitive: (1,2) and (2,1) → need (1,1) — yes ✓; (2,1) and (1,2) → need (2,2) — yes ✓. **Yes, it is an equivalence relation.** Equivalence classes: {1,2} and {3}.

**Q3.** How many ways can you choose a committee of 4 from 10 people, if 2 specific people must be on the committee?
> **Answer:** The 2 specific people are already chosen. We need to choose 2 more from the remaining 8: $\binom{8}{2} = \frac{8!}{2!6!} = 28$.

**Q4.** Prove using truth table: p → q ≡ ¬p ∨ q.
> **Answer:** | p | q | p→q | ¬p | ¬p∨q |
> |---|---|-----|-----|------|
> | T | T | T | F | T |
> | T | F | F | F | F |
> | F | T | T | T | T |
> | F | F | T | T | T |
> Columns for p→q and ¬p∨q are identical → **equivalent** ✓

**Q5.** Find GCD(462, 1071) using the Euclidean algorithm.
> **Answer:** 1071 = 2 × 462 + 147. 462 = 3 × 147 + 21. 147 = 7 × 21 + 0. **GCD = 21**.

---

*Previous: [Chapter 13 — Theory of Computation](13_Theory_of_Computation.md) | Next: [Chapter 15 — Computer Architecture](15_Computer_Architecture.md)*
