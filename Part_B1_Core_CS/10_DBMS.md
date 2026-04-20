# 10. Database Management Systems (DBMS)

> **Part B1 — Core Computer Science** | SIU PET Study Guide

---

- [ ] **Relational Model**
  - Tables (relations), rows (tuples), columns (attributes)
  - Keys: primary, candidate, super, foreign, composite
  - Relational algebra: select (σ), project (π), join (⋈), union, intersection, difference

- [ ] **ER Model & ER Diagrams**
  - Entities (strong, weak), attributes (simple, composite, derived, multivalued)
  - Relationships: one-to-one (1:1), one-to-many (1:N), many-to-many (M:N)
  - Participation: total, partial

- [ ] **Normalization**

  | Normal Form | Rule | Eliminates |
  |-------------|------|------------|
  | **1NF** | Atomic values, no repeating groups | Multi-valued attributes |
  | **2NF** | 1NF + no partial dependency | Partial dependency |
  | **3NF** | 2NF + no transitive dependency | Transitive dependency |
  | **BCNF** | Every determinant is a candidate key | Anomalies in 3NF |

- [ ] **SQL**
  - DDL: CREATE, ALTER, DROP, TRUNCATE
  - DML: SELECT, INSERT, UPDATE, DELETE
  - DCL: GRANT, REVOKE
  - TCL: COMMIT, ROLLBACK, SAVEPOINT
  - Joins: INNER, LEFT, RIGHT, FULL OUTER, CROSS, SELF
  - Aggregate functions: COUNT, SUM, AVG, MIN, MAX; GROUP BY, HAVING
  - Subqueries, views, stored procedures, triggers

- [ ] **Transactions & Concurrency**
  - **ACID Properties**:
    - **A**tomicity: All or nothing
    - **C**onsistency: Valid state to valid state
    - **I**solation: Transactions don't interfere
    - **D**urability: Committed changes persist
  - **Concurrency problems**: Lost update, dirty read, unrepeatable read, phantom read
  - **Locking**: shared/exclusive locks, two-phase locking (2PL)
  - **Serializability**: Conflict, view serializability
  - **Deadlock**: Prevention, detection, recovery

- [ ] **Indexing**
  - Primary index, secondary index, dense/sparse index
  - B-tree and B+ tree indexing
  - Hashing: static, dynamic (extendible hashing)

- [ ] **NoSQL Databases** (conceptual)
  - Key-Value: Redis, DynamoDB
  - Document: MongoDB, CouchDB
  - Column-Family: Cassandra, HBase
  - Graph: Neo4j
  - CAP theorem: Consistency, Availability, Partition tolerance (pick 2)

---

### Recommended Resources
- **Book**: *Database System Concepts* — Korth, Sudarshan, Silberschatz
- **Book**: *Fundamentals of Database Systems* — Elmasri & Navathe
