# 10. Database Management Systems (DBMS)

> **Part B1 — Core Computer Science** | SIU PET Complete Study Guide

---

## 10.1 Relational Model

### Basic Terminology

| Term | Formal Name | Informal Equivalent |
|------|------------|-------------------|
| **Relation** | R | Table |
| **Tuple** | t | Row / Record |
| **Attribute** | A | Column / Field |
| **Domain** | D | Set of allowed values for an attribute |
| **Schema** | R(A₁, A₂, ..., Aₙ) | Table structure (column names + types) |
| **Instance** | r(R) | Actual data in the table at a given time |
| **Degree** | — | Number of attributes (columns) |
| **Cardinality** | — | Number of tuples (rows) |

### Keys

| Key Type | Definition | Example |
|----------|-----------|---------|
| **Super Key** | Any set of attributes that uniquely identifies a tuple | {StudentID}, {StudentID, Name}, {StudentID, Name, Email} |
| **Candidate Key** | Minimal super key (no proper subset is a super key) | {StudentID}, {Email} — both uniquely identify |
| **Primary Key** | The chosen candidate key | StudentID |
| **Foreign Key** | Attribute in one table that references the primary key of another table | CourseID in Enrollment table → references Courses(CourseID) |
| **Composite Key** | Primary key with 2+ attributes | {StudentID, CourseID} in Enrollment table |
| **Alternate Key** | Candidate key that is NOT the primary key | Email (if StudentID is primary) |

### Relational Algebra

The theoretical query language for relational databases. SQL is based on it.

| Operation | Symbol | Description | SQL Equivalent |
|-----------|--------|-------------|---------------|
| **Select** | σ (sigma) | Filter rows based on condition | WHERE |
| **Project** | π (pi) | Select specific columns | SELECT col1, col2 |
| **Union** | ∪ | Combine rows from two compatible relations | UNION |
| **Intersection** | ∩ | Common rows in two relations | INTERSECT |
| **Difference** | − | Rows in R1 but not in R2 | EXCEPT |
| **Cartesian Product** | × | All combinations of rows | CROSS JOIN |
| **Natural Join** | ⋈ | Join on common attributes | NATURAL JOIN |
| **Rename** | ρ (rho) | Rename relation or attribute | AS |

**Example:**
"Find names of students enrolled in course CS101":
$$\pi_{Name}(\sigma_{CourseID='CS101'}(Student \bowtie Enrollment))$$

---

## 10.2 ER Model & ER Diagrams

Entity-Relationship model is used for **conceptual database design** (before creating tables).

### Components

**Entities:** Real-world objects or concepts stored in the database.
- **Strong entity:** Exists independently. Has its own primary key. (e.g., Student, Course)
- **Weak entity:** Depends on a strong entity. No primary key of its own — uses a partial key + owner's key. (e.g., Dependent of an Employee)

**Attributes:**

| Type | Description | Example |
|------|-------------|---------|
| **Simple** | Atomic, cannot be divided | Age, Roll Number |
| **Composite** | Can be divided into sub-parts | Name → {First, Middle, Last} |
| **Derived** | Calculated from other attributes | Age (derived from Date of Birth) |
| **Multivalued** | Can have multiple values | Phone numbers, skills |
| **Key attribute** | Uniquely identifies entity | StudentID |

**Relationships:**

| Cardinality | Meaning | Example |
|-------------|---------|---------|
| **1:1** | One entity of A relates to one of B | Student — has — AdmissionCard |
| **1:N** | One entity of A relates to many of B | Department — has — Employees |
| **M:N** | Many of A relate to many of B | Students — enroll in — Courses |

**Participation:**
- **Total:** Every entity MUST participate in the relationship (double line in ER diagram)
- **Partial:** Some entities MAY participate (single line)

> *Example:* Every Employee MUST belong to a Department (total participation of Employee in "works_in"). But not every Department must have a Manager specifically (partial participation).

---

## 10.3 Normalization

Normalization eliminates data redundancy and anomalies (insert, update, delete anomalies).

### Step by Step

**1NF (First Normal Form):**
- All attributes must have **atomic** (indivisible) values
- No repeating groups or arrays within a field

| Before 1NF ❌ | After 1NF ✅ |
|--------------|-------------|
| Student(ID, Courses="CS101,CS102") | Enrollment(ID, Course) |
| | Row 1: (1, CS101) |
| | Row 2: (1, CS102) |

**2NF (Second Normal Form):**
- Must be in 1NF
- No **partial dependency** — every non-key attribute must depend on the WHOLE primary key (not just part of a composite key)

| Problem ❌ | Explanation |
|-----------|------------|
| Table: Enrollment(StudentID, CourseID, CourseName, Grade) | CourseName depends only on CourseID, not on {StudentID, CourseID} |
| **Fix:** | Split into Enrollment(StudentID, CourseID, Grade) and Course(CourseID, CourseName) |

**3NF (Third Normal Form):**
- Must be in 2NF
- No **transitive dependency** — non-key attributes must not depend on other non-key attributes

| Problem ❌ | Explanation |
|-----------|------------|
| Student(ID, DeptID, DeptName) | DeptName depends on DeptID (not directly on ID). ID → DeptID → DeptName is transitive. |
| **Fix:** | Student(ID, DeptID) and Department(DeptID, DeptName) |

**BCNF (Boyce-Codd Normal Form):**
- Must be in 3NF
- For every functional dependency X → Y, X must be a **superkey**
- Stricter than 3NF — handles edge cases where a non-candidate-key determines part of a candidate key

### Quick Summary

```
Unnormalized → Remove multi-valued attributes → 1NF
1NF → Remove partial dependencies → 2NF
2NF → Remove transitive dependencies → 3NF
3NF → Every determinant is a candidate key → BCNF
```

---

## 10.4 SQL (Structured Query Language)

### SQL Command Categories

| Category | Commands | Purpose |
|----------|---------|---------|
| **DDL** (Data Definition) | CREATE, ALTER, DROP, TRUNCATE | Define/modify schema |
| **DML** (Data Manipulation) | SELECT, INSERT, UPDATE, DELETE | Query/modify data |
| **DCL** (Data Control) | GRANT, REVOKE | Manage permissions |
| **TCL** (Transaction Control) | COMMIT, ROLLBACK, SAVEPOINT | Manage transactions |

### Essential SQL Operations

**CREATE TABLE:**
```sql
CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Email VARCHAR(100) UNIQUE,
    DeptID INT,
    FOREIGN KEY (DeptID) REFERENCES Department(DeptID)
);
```

**JOINs:**

```
Table A        Table B
┌────┬───┐    ┌────┬───┐
│ ID │ X │    │ ID │ Y │
├────┼───┤    ├────┼───┤
│  1 │ a │    │  1 │ p │
│  2 │ b │    │  3 │ q │
│  3 │ c │    │  4 │ r │
└────┴───┘    └────┴───┘
```

| Join Type | Result | Rows Included |
|-----------|--------|---------------|
| **INNER JOIN** | 1-a-p, 3-c-q | Only matching rows from both tables |
| **LEFT JOIN** | 1-a-p, 2-b-NULL, 3-c-q | All from A + matching from B |
| **RIGHT JOIN** | 1-a-p, 3-c-q, 4-NULL-r | All from B + matching from A |
| **FULL OUTER JOIN** | 1-a-p, 2-b-NULL, 3-c-q, 4-NULL-r | All from both tables |
| **CROSS JOIN** | All combinations (3×3 = 9 rows) | Cartesian product |

**Aggregate Functions:**
```sql
SELECT DeptID, COUNT(*) AS NumStudents, AVG(GPA) AS AvgGPA
FROM Student
GROUP BY DeptID
HAVING COUNT(*) > 5
ORDER BY AvgGPA DESC;
```

- `GROUP BY` — groups rows by a column
- `HAVING` — filters groups (like WHERE but for aggregated results)
- `ORDER BY` — sorts results (ASC default, DESC for descending)

**Subqueries:**
```sql
-- Find students with above-average GPA
SELECT Name FROM Student
WHERE GPA > (SELECT AVG(GPA) FROM Student);
```

---

## 10.5 Transactions & Concurrency

### ACID Properties

| Property | Meaning | Example |
|----------|---------|---------|
| **Atomicity** | Transaction is all-or-nothing | Bank transfer: debit AND credit both succeed, or both fail |
| **Consistency** | Database goes from one valid state to another | Total money before = total money after |
| **Isolation** | Concurrent transactions don't interfere | Two people booking the same seat won't see each other's partial work |
| **Durability** | Committed changes survive crashes | Power failure after COMMIT → data is safe |

### Concurrency Problems

| Problem | Description | Example |
|---------|-------------|---------|
| **Lost Update** | T1 and T2 both read, then write — one update is lost | Both users read balance=1000, both add 500, write 1500 (should be 2000) |
| **Dirty Read** | T1 reads data that T2 hasn't committed (and T2 may rollback) | T1 reads balance=500 after T2's uncommitted debit; T2 rolls back → T1 used wrong data |
| **Unrepeatable Read** | T1 reads same data twice, gets different values (T2 modified in between) | T1 reads salary=50K, T2 updates to 60K, T1 reads again: salary=60K |
| **Phantom Read** | T1 re-runs a query and gets different rows (T2 inserted/deleted rows) | T1 counts 10 employees, T2 adds one, T1 recounts: 11 |

### Locking

| Lock Type | Alias | Allows |
|-----------|-------|--------|
| **Shared Lock (S)** | Read lock | Multiple readers, no writers |
| **Exclusive Lock (X)** | Write lock | Only one writer, no readers |

**Two-Phase Locking (2PL):**
1. **Growing Phase:** Acquire locks, never release
2. **Shrinking Phase:** Release locks, never acquire new ones

Guarantees **serializability** (transactions appear to execute one after another).

### Serializability

A schedule of concurrent transactions is **serializable** if its result is equivalent to some serial execution of those transactions.

- **Conflict serializable:** Can be transformed into a serial schedule by swapping non-conflicting operations
- **View serializable:** Every read produces the same value as in some serial schedule

### Deadlock

Two or more transactions waiting for each other's locks → none can proceed.

**Prevention strategies:**
- Wait-Die / Wound-Wait timestamps
- Lock ordering (always acquire locks in the same order)

**Detection:** Wait-for graph — if cycle exists → deadlock

**Recovery:** Abort (rollback) one of the transactions

---

## 10.6 Indexing

Indexes speed up data retrieval (like a book's index).

| Index Type | Description |
|-----------|-------------|
| **Primary Index** | On the primary key of a sorted file (1 entry per block) |
| **Secondary Index** | On a non-ordering field (1 entry per record or per unique value) |
| **Dense Index** | One index entry per record |
| **Sparse Index** | One index entry per data block |
| **Clustered** | Records physically sorted by the index key |
| **Non-clustered** | Index order ≠ physical order (pointers) |

**B+ Tree Index (Most Common):**
- Internal nodes store keys for routing
- Leaf nodes store actual data pointers
- Leaf nodes are linked → great for range queries
- All operations: O(log n)
- Used by MySQL (InnoDB), PostgreSQL, Oracle

---

## 10.7 NoSQL Databases

| Type | Data Model | Examples | Best For |
|------|-----------|----------|----------|
| **Key-Value** | Simple key → value pairs | Redis, DynamoDB | Caching, sessions, simple lookups |
| **Document** | JSON/BSON documents | MongoDB, CouchDB | Semi-structured data, content management |
| **Column-Family** | Columns grouped into families | Cassandra, HBase | Time-series, wide rows, analytics |
| **Graph** | Nodes + edges + properties | Neo4j, Amazon Neptune | Social networks, knowledge graphs, recommendations |

### CAP Theorem (Brewer's Theorem)

A distributed system can guarantee at most **2 out of 3**:

| Property | Meaning |
|----------|---------|
| **Consistency** | Every read returns the most recent write |
| **Availability** | Every request gets a response (even if not the latest) |
| **Partition Tolerance** | System works despite network failures between nodes |

Since network partitions are inevitable in distributed systems, the real choice is between **CP** (consistent but may be unavailable) and **AP** (available but may be inconsistent).

| System | CAP Choice | Example |
|--------|-----------|---------|
| **CP** | Consistency + Partition Tolerance | HBase, MongoDB (default) |
| **AP** | Availability + Partition Tolerance | Cassandra, DynamoDB |
| **CA** | Consistency + Availability (theoretical — no partition tolerance) | Traditional RDBMS on single node |

### SQL vs. NoSQL

| Aspect | SQL (RDBMS) | NoSQL |
|--------|-------------|-------|
| Schema | Fixed, predefined | Flexible, schema-less |
| Scaling | Vertical (bigger machine) | Horizontal (more machines) |
| ACID | Full support | BASE (Basically Available, Soft state, Eventually consistent) |
| Joins | Rich join support | Limited or no joins |
| Best for | Structured data, complex queries | Unstructured data, high throughput, scale |

---

## 10.8 Practice Questions

**Q1.** Given a table Student(StudentID, Name, DeptID, DeptName, HOD), identify the highest normal form and normalize it to 3NF.
> **Answer:** Current: 1NF (all atomic). Issue: DeptName and HOD depend on DeptID (transitive dependency through StudentID → DeptID → DeptName, HOD). Not even 2NF if DeptID is not part of the key. **3NF solution:** Student(StudentID, Name, DeptID) and Department(DeptID, DeptName, HOD). Now StudentID → {Name, DeptID} and DeptID → {DeptName, HOD}.

**Q2.** What is the difference between HAVING and WHERE in SQL?
> **Answer:** `WHERE` filters individual rows BEFORE grouping. `HAVING` filters groups AFTER GROUP BY and aggregation. Example: `WHERE salary > 50000` filters rows; `HAVING COUNT(*) > 5` filters groups with more than 5 records. You cannot use aggregate functions in WHERE.

**Q3.** Explain the difference between a clustered and non-clustered index.
> **Answer:** A **clustered index** determines the physical order of data in the table — there can be only ONE per table (like a book organized alphabetically by topic). A **non-clustered index** is a separate structure with pointers to the data rows — there can be many per table (like a book's index at the back). Clustered is faster for range queries; non-clustered is more flexible.

**Q4.** Two transactions T1 and T2 operate on the same data. T1: Read(X), X=X+100, Write(X). T2: Read(X), X=X×2, Write(X). If X=500 initially, what happens with a lost update?
> **Answer:** T1 reads X=500, T2 reads X=500. T1 writes X=600 (500+100). T2 writes X=1000 (500×2). T1's update is **lost** — final value is 1000 instead of 1200 (the correct serial result). **Fix:** Use locking or proper isolation level.

**Q5.** When would you choose MongoDB over MySQL for an AI/ML application?
> **Answer:** MongoDB when: (1) Data has varying structure (different ML experiments store different metadata), (2) Need to store unstructured data like JSON, images metadata, log entries, (3) Need horizontal scaling for large datasets, (4) Rapid prototyping where schema changes frequently. MySQL when: (5) Data is highly structured with relationships, (6) Need complex joins and ACID transactions, (7) Need strong consistency guarantees.

---

*Previous: [Chapter 9 — DSA](09_Data_Structures_and_Algorithms.md) | Next: [Chapter 11 — Operating Systems](11_Operating_Systems.md)*
