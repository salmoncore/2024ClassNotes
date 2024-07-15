<< [README](./README.md)

# SQL Keys

## Contents
- [Keys](#keys)
- [Resources](#resources)

## Keys
- Primary key - Unique identifier for a row in your table
    - Primary key is also a candidate key

- Candidate Key - A set of 1 or more columns that can uniquely identify a row within a table.
    - Ensures a row in the table is unique.
    - Can be one or more columns to form a candidate key.
    - can be `simple` or `composite`
    - Simple - a primary key that is made up of a single column
        e.g. Employee ID
    - Composite candidate key - More than one column
        - A primary key that is made up of multiple columns
        e. g. OrderID and Customer ID in one table

- Super Key
    - Can be simple or composite.
    - A set of 1 or more columns that uniquely idenrify a row
    - Can either be composite or simple.

- Surrogate Key
    - A primary key (pk) used to specifically as a unique idenfitier
    - Typically auto-generated
    - e. g. Auto-incrementing number

- Foreign Key
    - A column or gorup of columns used to link data between tables.

## Resources
- [Geeks for Geeks, Difference between Super Key and Candidate Key↗️](https://www.geeksforgeeks.org/difference-between-super-key-and-candidate-key) - 📄