<< [README](./README.md)

# Contents
- [Overview](#overview)
- [1st Normal Form](#1st-normal-form)
- [2nd Normal Form](#2nd-normal-form)
- [Resources](#resources)

# Overview
- A way to structure your database table to remove redundant information 
    - Makes it easier to understand, enhance, and extend 
- Protected from 
    - Insertion Anomalies 
        - Situation where inserting data is impossible 
    - Update Anomalies 
        - Situation where updating data leads to database inconsistencies 
    - Deletion Anomalies 
        - Situation where deleting data leads to unintended additional data loss 

## 1st Normal Form
- FIRST NORMAL FORM (1NF) Prevents row from a unique column from ever being inserted
- Not allowed: 
    - Mixing data types within a column 
    - Having a table without a Primary Key 
    - Using row order to convey information 
    - Repeating groups

## 2nd Normal Form
- SECOND NORMAL FORM (2NF) Each non-key column on a table must be dependent on the entire PK 
- Conditions to satisfy: 
    - Must be in first normal form 
    - All non-key columns are fully dependent on primary key 
    - No partial dependencies

## 3rd Normal Form
THIRD NORMAL FORM (3NF) Forbids dependency on a non-key attribute on another non-key attribute 
- Every non-key attribute in a table should depend on the key only 
    - Must be in second normal form 
    - No transitive dependencies

## Resources
- [Database Normalization - Simple Explanation for Beginners](https://www.youtube.com/watch?v=xoTyrdT9SZI) - 🎥 YouTube Video