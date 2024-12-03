---
title: Normalization
aliases:
  - Normalization
draft: false
tags:
  - DataEngineering
author:
  - Sarthak Chandajkar
---
 **Normalization** is the process of organizing data in a database to reduce redundancy and improve data integrity. It involves dividing a database into smaller tables and defining relationships between them according to rules designed to protect the data and make it more flexible and efficient.

### **Objectives of Normalization**
1. **Eliminate Redundant Data**: Prevents the same piece of data from being stored in multiple places.
2. **Ensure Data Dependencies Make Sense**: Data is stored logically and is consistent.
3. **Improve Data Integrity**: Reduces the risk of anomalies during data manipulation operations like insertion, deletion, and updating.
4. **Optimize Storage**: Reduces the amount of space required by the database.

---

### **Normalization Forms**
Normalization is achieved in stages called **Normal Forms (NF)**, each with its own set of rules:

1. **First Normal Form (1NF)**:
   - Ensures that the values in each column of a table are atomic (indivisible).
   - Removes repeating groups or arrays.

1. **Second Normal Form (2NF)**:
   - Achieves 1NF.
   - Removes partial dependency, where non-primary key columns depend on part of a composite primary key.
   - Example:
     A table with composite primary key (OrderID, ProductID) has additional columns that depend only on OrderID or ProductID.
     Solution: Split the table into two tables.

3. **Third Normal Form (3NF)**:
   - Achieves 2NF.
   - Removes transitive dependency, where non-primary key columns depend indirectly on the primary key through another non-primary key column.
   - Example:
     If a table stores `StudentID`, `CourseID`, and `InstructorName`:
     - `InstructorName` depends on `CourseID`, not directly on `StudentID`.
     Solution: Move `InstructorName` to a separate table.

4. **Boyce-Codd Normal Form (BCNF)**:
   - A stricter version of 3NF.
   - Ensures that every determinant (a column or a set of columns that uniquely determines another column) is a candidate key.

5. **Fourth Normal Form (4NF)**:
   - Achieves BCNF.
   - Removes multi-valued dependencies, where a single primary key is associated with multiple independent sets of values.

6. **Fifth Normal Form (5NF)**:
   - Achieves 4NF.
   - Resolves complex join dependencies, ensuring that data is reconstructed without loss.

---

### **Advantages of Normalization**
1. **Reduces Data Redundancy**: Prevents duplicate data storage.
2. **Ensures Data Integrity**: Updates, deletions, and insertions do not introduce anomalies.
3. **Improves Query Efficiency**: Queries on normalized data are often faster due to reduced data duplication.
4. **Improves Data Consistency**: Keeps related data consistent across the database.

---

### **Drawbacks**
1. **Increased Complexity**: Requires additional tables and relationships, which can make queries more complex.
2. **Potential Performance Issues**: Joins across many tables can slow down read operations in highly normalized databases.

Normalization is a fundamental concept in relational database design and is often balanced with denormalization in real-world scenarios to achieve the right balance between performance and data integrity.

