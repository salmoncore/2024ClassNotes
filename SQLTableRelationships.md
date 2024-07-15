<< [README](./README.md)

# SQL Table Relationships

## Contents
- [Relationships](#relationships)
## Relationships
- One-to-one
    - A single table A relates to a single table B
    - Used to create critical relationships
-    E.g. ID number foriegn key linking names to liscense numbers between tables
- One-to-many
    - A row (record) in table A that relates to one or more rows in table B
    - E.g. A customer ID in a customer table, linking to a Order table that also contains a customer ID forign key, but that uses an order ID as its primary key
- Many-to-many
    - Where table A relates to one or more rows in table B, and vice-versa
    - E.g. An Author table and a Books table, both with distinct primary keys, relying on a Junction table to link the values together