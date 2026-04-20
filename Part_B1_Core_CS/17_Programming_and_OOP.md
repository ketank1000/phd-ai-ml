# 17. Programming & OOP Concepts

> **Part B1 — Core Computer Science** | SIU PET Complete Study Guide

---

## 17.1 Object-Oriented Programming (OOP) Principles

### 17.1.1 Encapsulation

**Bundling data (attributes) and methods (functions) that operate on that data into a single unit (class), and restricting direct access to internal state.**

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  # Private attribute (name mangling in Python)
    
    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount
    
    def get_balance(self):
        return self.__balance  # Controlled access via getter
```

**Access Modifiers:**

| Modifier | Accessible From | Python Convention |
|----------|----------------|-------------------|
| **public** | Anywhere | `self.name` (no underscore) |
| **protected** | Same class + subclasses | `self._name` (single underscore) |
| **private** | Same class only | `self.__name` (double underscore) |

**Benefits:** Data validation (prevent invalid states), implementation hiding (change internals without breaking external code), security.

### 17.1.2 Inheritance

**Creating new classes (child/derived) from existing classes (parent/base), inheriting their properties and methods.**

```python
class Animal:
    def __init__(self, name):
        self.name = name
    def speak(self):
        pass

class Dog(Animal):       # Dog inherits from Animal
    def speak(self):
        return "Woof!"

class Cat(Animal):       # Cat inherits from Animal
    def speak(self):
        return "Meow!"
```

**Types of Inheritance:**

| Type | Description | Example |
|------|-------------|---------|
| **Single** | One parent, one child | Dog → Animal |
| **Multi-level** | Chain of inheritance | Puppy → Dog → Animal |
| **Hierarchical** | One parent, multiple children | Animal → Dog, Cat, Bird |
| **Multiple** | Multiple parents (supported in Python, via interfaces in Java) | `class FlyingCar(Car, Aircraft)` |

**Diamond Problem:** In multiple inheritance, if both parents inherit from the same grandparent, which version of a method is used? Python resolves this using **MRO (Method Resolution Order)** — C3 linearization.

### 17.1.3 Polymorphism

**"Many forms" — same interface, different implementations.**

| Type | Mechanism | When Decided | Example |
|------|-----------|-------------|---------|
| **Compile-time (Static)** | Method overloading | Compile time | `add(int, int)` vs `add(float, float)` in Java/C++ |
| **Runtime (Dynamic)** | Method overriding | Runtime | `dog.speak()` returns "Woof", `cat.speak()` returns "Meow" |

```python
# Runtime polymorphism
animals = [Dog("Rex"), Cat("Whiskers")]
for animal in animals:
    print(animal.speak())  # Same method call, different behavior
# Output: Woof!  Meow!
```

**In Python:** Duck typing ("If it walks like a duck and quacks like a duck, it's a duck"). Python doesn't check the type — it checks if the method exists.

### 17.1.4 Abstraction

**Hiding complex implementation details and showing only the essential interface.**

```python
from abc import ABC, abstractmethod

class Shape(ABC):      # Abstract class — cannot be instantiated
    @abstractmethod
    def area(self):     # Abstract method — must be implemented by subclass
        pass

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    def area(self):     # Concrete implementation
        return 3.14159 * self.radius ** 2
```

**Abstract Class vs Interface:**

| Feature | Abstract Class | Interface (Python Protocol) |
|---------|---------------|----------------------------|
| Methods | Can have both abstract and concrete | Typically only abstract methods |
| Instantiation | Cannot be instantiated | Cannot be instantiated |
| Inheritance | Single (in Java) | Multiple |
| State | Can have attributes | No state (in pure interfaces) |

---

## 17.2 SOLID Principles

| Principle | Full Name | Meaning |
|-----------|----------|---------|
| **S** | Single Responsibility | A class should have only ONE reason to change |
| **O** | Open/Closed | Open for extension, closed for modification |
| **L** | Liskov Substitution | Subclass should be usable wherever parent class is expected |
| **I** | Interface Segregation | Don't force clients to depend on methods they don't use |
| **D** | Dependency Inversion | Depend on abstractions, not concrete implementations |

---

## 17.3 Key Programming Concepts

### Memory: Stack vs. Heap

| Feature | Stack | Heap |
|---------|-------|------|
| **What's stored** | Local variables, function calls | Dynamically allocated objects |
| **Allocation** | Automatic (LIFO) | Manual (C/C++) or garbage-collected (Python/Java) |
| **Speed** | Very fast | Slower (fragmentation, GC) |
| **Size** | Limited (usually 1-8 MB) | Large (limited by available RAM) |
| **Lifetime** | Destroyed when function returns | Until explicitly freed or GC collects |

### Garbage Collection

Automatic memory management — the runtime reclaims memory of objects that are no longer referenced.

| Strategy | How It Works | Used By |
|----------|-------------|---------|
| **Reference Counting** | Track number of references; free when count = 0 | Python (primary), Swift |
| **Mark and Sweep** | Mark all reachable objects, sweep unreachable ones | Java, Go |
| **Generational GC** | Objects that survive longer are checked less often | Java (young gen, old gen), Python (gen 0, 1, 2) |

### Recursion vs. Iteration

| Feature | Recursion | Iteration |
|---------|-----------|-----------|
| **Mechanism** | Function calls itself | Loops (for, while) |
| **Memory** | Uses call stack (risk of stack overflow) | Constant extra memory |
| **Readability** | Often more elegant for tree/graph problems | Often simpler for linear problems |
| **Performance** | Function call overhead | Generally faster |
| **Example** | Fibonacci, tree traversal, merge sort | List processing, searching |

**Tail recursion:** When the recursive call is the LAST operation. Can be optimized by the compiler into iteration (tail-call optimization). Python does NOT optimize tail calls.

### Exception Handling

```python
try:
    result = 10 / 0          # Code that might fail
except ZeroDivisionError as e:
    print(f"Error: {e}")     # Handle specific error
except Exception as e:
    print(f"General: {e}")   # Handle any other error
else:
    print("Success!")         # Runs if NO exception
finally:
    print("Cleanup")         # ALWAYS runs (closing files, connections)
```

### Generics / Templates

Write code that works with ANY type:

```python
from typing import TypeVar, List
T = TypeVar('T')

def first_element(lst: List[T]) -> T:
    return lst[0]

# Works with any type:
first_element([1, 2, 3])      # int
first_element(["a", "b"])     # str
```

### Lambda Functions

Anonymous, single-expression functions:

```python
# Regular function
def square(x):
    return x * x

# Lambda equivalent
square = lambda x: x * x

# Common use: sorting, filtering
sorted(students, key=lambda s: s.gpa)
filtered = list(filter(lambda x: x > 5, [1, 3, 5, 7, 9]))
```

---

## 17.4 Python-Specific Concepts (Important for AI/ML)

### List Comprehensions

```python
# Traditional loop
squares = []
for x in range(10):
    squares.append(x**2)

# List comprehension (Pythonic)
squares = [x**2 for x in range(10)]

# With condition
even_squares = [x**2 for x in range(10) if x % 2 == 0]

# Nested
matrix = [[1,2,3],[4,5,6]]
flat = [x for row in matrix for x in row]  # [1,2,3,4,5,6]
```

### Generators

Produce values lazily (one at a time, on demand) — memory efficient for large datasets.

```python
def fibonacci():
    a, b = 0, 1
    while True:
        yield a      # yield instead of return — pauses function
        a, b = b, a + b

gen = fibonacci()
print(next(gen))  # 0
print(next(gen))  # 1
print(next(gen))  # 1

# Generator expression (like list comprehension but lazy)
sum_of_squares = sum(x**2 for x in range(1000000))  # Doesn't create list in memory
```

### Decorators

Functions that modify other functions:

```python
def timer(func):
    import time
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        print(f"{func.__name__} took {time.time()-start:.2f}s")
        return result
    return wrapper

@timer
def train_model(data):
    # training logic here
    pass

# Calling train_model() now automatically times it
```

### Pass by Object Reference

Python passes references to objects (not values, not pointers):

```python
def modify(lst):
    lst.append(4)    # Modifies the original list (mutable)

def reassign(lst):
    lst = [5, 6, 7]  # Creates new local variable — original unchanged

my_list = [1, 2, 3]
modify(my_list)       # my_list = [1, 2, 3, 4]
reassign(my_list)     # my_list = [1, 2, 3, 4] — unchanged!
```

**Rule:** Mutable objects (lists, dicts, sets) can be modified in place. Immutable objects (int, str, tuple) create new objects on modification.

### GIL (Global Interpreter Lock)

- Python (CPython) has a GIL that allows only ONE thread to execute Python bytecode at a time
- **Impact:** Multi-threading does NOT give true parallelism for CPU-bound tasks
- **Solutions:** Use `multiprocessing` (separate processes) or C extensions (NumPy operations release the GIL)
- **For ML:** NumPy, TensorFlow, and PyTorch release the GIL internally, so matrix operations are truly parallel

---

## 17.5 Practice Questions

**Q1.** Explain the difference between method overloading and method overriding with examples.
> **Answer:** **Overloading (compile-time polymorphism):** Multiple methods with the same name but different parameters in the same class. Example in Java: `add(int, int)` and `add(double, double)`. Python doesn't natively support overloading (last definition wins), but you can use `*args` or `@singledispatch`. **Overriding (runtime polymorphism):** Subclass provides its own implementation of a parent method. Example: `Dog.speak()` overrides `Animal.speak()`. The correct version is called based on the actual object type at runtime.

**Q2.** What is the diamond problem in multiple inheritance? How does Python solve it?
> **Answer:** If class D inherits from both B and C, and both B and C inherit from A, calling a method defined in A is ambiguous — which path (D→B→A or D→C→A)? Python solves this using **MRO (Method Resolution Order)** with C3 linearization. You can check it with `D.__mro__`. Python follows a left-to-right, depth-first order with duplicate removal.

**Q3.** What is the difference between a list and a generator in Python? When would you use a generator?
> **Answer:** A **list** stores ALL elements in memory at once. A **generator** produces elements one at a time (lazy evaluation) and doesn't store them all. Use generators when: (1) dealing with very large datasets that don't fit in memory, (2) you only need to iterate once, (3) you want to implement infinite sequences (like Fibonacci). Example: Reading a 100GB log file line by line — a generator processes one line at a time; a list would try to load everything.

**Q4.** Explain encapsulation and why `self.__balance` is not truly private in Python.
> **Answer:** Encapsulation bundles data and methods together and restricts access to internals. `self.__balance` uses **name mangling** — Python renames it to `_ClassName__balance`. It's NOT truly private because you can still access it via `obj._BankAccount__balance`. This is "name mangling" for accidental access prevention, not security. Python's philosophy is "we're all consenting adults" — trust developers to respect conventions.

**Q5.** What is the GIL and why is it relevant for AI/ML developers using Python?
> **Answer:** The **Global Interpreter Lock** is a mutex in CPython that allows only one thread to execute Python code at a time, preventing true parallel execution of Python threads. For AI/ML: (1) NumPy, TensorFlow, and PyTorch release the GIL during C/CUDA operations, so matrix computations ARE parallel. (2) For data loading, use `multiprocessing` (PyTorch `DataLoader` with `num_workers > 0`). (3) The GIL doesn't affect I/O-bound tasks (network, disk), only CPU-bound Python code.

---

*Previous: [Chapter 16 — Software Engineering](16_Software_Engineering.md) | Next: [Chapter 18 — Math Foundations for ML](../Part_B2_AI_ML_Specialization/18_Math_Foundations_for_ML.md)*
