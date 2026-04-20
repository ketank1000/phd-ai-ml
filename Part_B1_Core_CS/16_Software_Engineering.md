# 16. Software Engineering

> **Part B1 — Core Computer Science** | SIU PET Complete Study Guide

---

## 16.1 Software Development Life Cycle (SDLC) Models

### Waterfall Model

Sequential, phase-by-phase development. Each phase must complete before the next begins.

```
Requirements → Design → Implementation → Testing → Deployment → Maintenance
```

| Pros | Cons |
|------|------|
| Simple, well-documented | Inflexible — can't go back easily |
| Good for stable, well-known requirements | Late discovery of defects (testing is at the end) |
| Clear milestones | Customer sees product only at the end |

**Best for:** Government projects, embedded systems, projects with very stable requirements.

### Agile Model

Iterative, incremental development in short cycles (sprints). Customer is involved throughout.

**Key Principles (from the Agile Manifesto):**
- Individuals and interactions over processes and tools
- Working software over comprehensive documentation
- Customer collaboration over contract negotiation
- Responding to change over following a plan

**Scrum Framework:**

```
Product Backlog → Sprint Planning → Sprint (2-4 weeks) → Sprint Review → Sprint Retrospective
                                       │
                                  Daily Standup
                                  (15 min: What I did, What I'll do, Blockers)
```

**Roles:** Product Owner (what to build), Scrum Master (process), Development Team (how to build)

**Kanban:** Visual board with columns: To Do → In Progress → Done. Limit Work-In-Progress (WIP).

| Pros | Cons |
|------|------|
| Flexible, adapts to changes | Less predictable timeline/budget |
| Early and continuous delivery | Requires active customer involvement |
| Frequent feedback | Poor documentation if not managed |

### Other Models

| Model | Key Feature | Best For |
|-------|-------------|----------|
| **Spiral** | Risk analysis at each iteration | Large, complex, high-risk projects |
| **V-Model** | Testing parallel to each dev phase | Safety-critical systems (medical, automotive) |
| **Iterative** | Build incrementally, refine each iteration | When requirements are partially known |
| **RAD (Rapid Application Development)** | Prototyping, quick turnaround | Small-medium projects with tight timelines |
| **DevOps** | Development + Operations merged; CI/CD | Modern software with frequent releases |

---

## 16.2 Requirements Engineering

### Types of Requirements

| Type | Definition | Examples |
|------|-----------|---------|
| **Functional** | What the system DOES | "User shall be able to upload images," "System shall classify images" |
| **Non-functional** | How the system PERFORMS | Performance, security, scalability, usability, reliability |

### Non-Functional Requirements Categories

| NFR | Example |
|-----|---------|
| **Performance** | Response time < 200ms for API calls |
| **Scalability** | Handle 10,000 concurrent users |
| **Security** | Data encrypted at rest and in transit |
| **Availability** | 99.9% uptime (< 8.7 hours downtime/year) |
| **Usability** | New users complete the task within 5 minutes |
| **Maintainability** | Modular code with > 80% unit test coverage |

### Use Cases vs. User Stories

| Use Case | User Story |
|----------|-----------|
| Detailed, formal | Brief, informal |
| Actor + steps + pre/post conditions | As a [role], I want [goal], so that [benefit] |
| UML use case diagrams | Written on index cards / Jira tickets |
| Used in Waterfall/V-Model | Used in Agile |

---

## 16.3 Software Design

### Design Principles

| Principle | Meaning |
|-----------|---------|
| **High Cohesion** | A module does ONE thing well (related functions grouped together) |
| **Low Coupling** | Modules are independent; changes in one don't ripple through others |
| **SOLID** (OOP principles) | Single responsibility, Open-closed, Liskov substitution, Interface segregation, Dependency inversion |
| **DRY** | Don't Repeat Yourself |
| **KISS** | Keep It Simple, Stupid |
| **YAGNI** | You Aren't Gonna Need It (don't build for hypothetical future) |

### Design Patterns (Gang of Four)

| Pattern | Category | Problem It Solves | Example |
|---------|----------|------------------|---------|
| **Singleton** | Creational | Ensure only ONE instance of a class | Database connection pool, Logger |
| **Factory** | Creational | Create objects without specifying exact class | Creating different model architectures: `ModelFactory.create("resnet50")` |
| **Observer** | Behavioral | One-to-many dependency (notify when state changes) | Event handling, pub-sub, UI updates |
| **Strategy** | Behavioral | Swap algorithms at runtime | Different sorting algorithms, different optimization strategies |
| **MVC** | Architectural | Separate Model (data), View (UI), Controller (logic) | Web frameworks (Django, Spring) |
| **Builder** | Creational | Construct complex objects step by step | Building neural network layers |
| **Adapter** | Structural | Make incompatible interfaces work together | Wrapping a legacy API |
| **Decorator** | Structural | Add behavior to objects dynamically | Python decorators, logging wrappers |

### Architectural Styles

| Style | Description | Pros | Cons |
|-------|-------------|------|------|
| **Monolithic** | Single deployable unit | Simple, easy to develop initially | Hard to scale, deploy, maintain |
| **Microservices** | Independent, loosely coupled services | Scalable, independent deployment | Complex to manage, network overhead |
| **Layered** | Presentation → Business → Data layers | Separation of concerns | Rigid, performance overhead |
| **Event-Driven** | Components communicate via events/messages | Loosely coupled, scalable | Hard to debug, eventual consistency |
| **Serverless** | Cloud functions triggered by events | No server management, pay-per-use | Cold start latency, vendor lock-in |

---

## 16.4 UML Diagrams

### Structural Diagrams

| Diagram | Shows | Key Elements |
|---------|-------|-------------|
| **Class Diagram** | Classes, attributes, methods, relationships | Classes, inheritance (triangle), association (line), composition (filled diamond), aggregation (empty diamond) |
| **Object Diagram** | Instance-level snapshot | Specific objects with current values |
| **Component Diagram** | System components and dependencies | Components, interfaces, connectors |

**Class Diagram Example:**
```
┌──────────────────┐         ┌──────────────────┐
│     Animal       │         │   Dog            │
├──────────────────┤         ├──────────────────┤
│ - name: String   │◁────────│ - breed: String  │
│ - age: int       │         ├──────────────────┤
├──────────────────┤         │ + fetch(): void  │
│ + eat(): void    │         └──────────────────┘
│ + sleep(): void  │
└──────────────────┘
  ◁ = Inheritance (Dog extends Animal)
```

### Behavioral Diagrams

| Diagram | Shows | Use Case |
|---------|-------|----------|
| **Use Case** | System functions from user perspective | Requirements gathering |
| **Sequence** | Object interactions over time (message flow) | API call flows, authentication sequences |
| **Activity** | Workflow/business process (like flowchart) | Order processing, data pipeline |
| **State Machine** | States and transitions of an object | Connection states, order lifecycle |

---

## 16.5 Testing

### Testing Levels

```
               ┌───────────────────────┐
               │  Acceptance Testing    │  ← Customer validates
               ├───────────────────────┤
               │    System Testing      │  ← Complete system tested
               ├───────────────────────┤
               │  Integration Testing   │  ← Components combined
               ├───────────────────────┤
               │    Unit Testing        │  ← Individual modules
               └───────────────────────┘
```

### Testing Types

| Type | Knowledge of Code? | What Is Tested? | Techniques |
|------|-------------------|-----------------|-----------|
| **Black-box** | No (treat as black box) | Input → output behavior | Equivalence partitioning, boundary value analysis |
| **White-box** | Yes (see the code) | Internal logic, paths | Statement coverage, branch coverage, path coverage |
| **Grey-box** | Partial | Both internal and external | Common in integration testing |

### Integration Testing Strategies

| Strategy | How It Works | Pros |
|----------|-------------|------|
| **Big Bang** | All modules integrated at once | Simple; hard to isolate faults |
| **Top-Down** | Start from main module, add sub-modules (stubs for missing) | Early testing of main architecture |
| **Bottom-Up** | Start from lowest modules, add upward (drivers for missing) | No stubs needed; late testing of top-level |
| **Sandwich** | Top-down + Bottom-up combined | Combines benefits |

### Code Coverage

| Metric | What It Measures |
|--------|-----------------|
| **Statement coverage** | % of statements executed at least once |
| **Branch coverage** | % of branches (if/else) taken at least once |
| **Path coverage** | % of all possible execution paths tested |

Path coverage ⊃ Branch coverage ⊃ Statement coverage (most to least thorough)

---

## 16.6 Software Metrics & Quality

### Cyclomatic Complexity (McCabe)

Measures the number of independent paths through a program's control flow graph.

$$V(G) = E - N + 2P$$

Where E = edges, N = nodes, P = connected components (usually 1)

**Shortcut:** V(G) = number of decision points (if, while, for, case) + 1

| V(G) | Risk |
|------|------|
| 1-10 | Low — simple, well-structured |
| 11-20 | Moderate — more complex |
| 21-50 | High — complex, hard to test |
| > 50 | Very high — untestable, refactor! |

### CMM / CMMI (Capability Maturity Model Integration)

| Level | Name | Description |
|-------|------|-------------|
| 1 | **Initial** | Ad-hoc, chaotic, unpredictable |
| 2 | **Managed** | Projects managed, basic processes |
| 3 | **Defined** | Organization-wide standard processes |
| 4 | **Quantitatively Managed** | Metrics-driven process control |
| 5 | **Optimizing** | Continuous improvement, innovation |

---

## 16.7 Practice Questions

**Q1.** Compare Waterfall and Agile approaches for developing an AI chatbot for a startup.
> **Answer:** **Agile is better** for this scenario. Reasons: (1) Chatbot requirements are likely to evolve based on user feedback, (2) Startups need to iterate quickly, (3) AI models improve with continuous user data, (4) Customer can test and provide feedback each sprint. Waterfall would be risky because freezing requirements upfront for an AI product where user needs aren't fully known would likely lead to a product that misses the mark.

**Q2.** What is the difference between high cohesion and low coupling? Why are both desirable?
> **Answer:** **High cohesion:** All elements within a module are closely related and serve a single purpose (e.g., a `DataPreprocessor` class that only handles data cleaning). **Low coupling:** Modules are independent; changing one doesn't require changing others. Both are desirable because they make code easier to understand, test, maintain, and reuse. A change in one module doesn't cascade through the system.

**Q3.** Explain the Singleton design pattern. When is it used, and what is its potential drawback?
> **Answer:** Singleton ensures only ONE instance of a class exists. Implementation: private constructor, static method `getInstance()` that creates the instance on first call and returns the same instance thereafter. **Used for:** database connections, loggers, configuration managers. **Drawback:** Makes unit testing difficult (hidden global state), violates single responsibility principle, can introduce tight coupling.

**Q4.** A program has 15 if-statements and 3 while-loops. What is its cyclomatic complexity?
> **Answer:** Decision points = 15 (if) + 3 (while) = 18. V(G) = 18 + 1 = **19**. This is in the moderate-high complexity range, suggesting it needs careful testing and might benefit from refactoring.

**Q5.** What is the difference between black-box and white-box testing? Give a practical example.
> **Answer:** **Black-box:** Tester doesn't know the code; tests inputs and expected outputs. Example: Testing a login page — enter valid/invalid credentials, check if it logs in/shows error. **White-box:** Tester has access to the code; tests internal logic and paths. Example: Testing a sorting function — ensure every branch is covered (empty array case, single element, duplicates, already sorted). Black-box verifies WHAT the software does; white-box verifies HOW it does it.

---

*Previous: [Chapter 15 — Computer Architecture](15_Computer_Architecture.md) | Next: [Chapter 17 — Programming & OOP](17_Programming_and_OOP.md)*
