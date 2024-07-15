<< [README](./README.md)

# Week 1 Study Notes

## Contents
- [hashCode()](#hashcode)
- [equals()](#equals)
- [Arrays](#arrays)
- [Loops](#loops)
- [Lists](#lists)
- [ArrayLists](#array-lists)
- [LinkedLists](#linked-lists)
- [Maps](#maps)
- [Hashmaps](#hashmaps)
- [ETS](#ets)
- [Hashsets](#hashsets)
- [Iterators](#iterators)
- [Encapsulation](#encapsulation)
- [Abstraction](#abstraction)
- [Inheritance](#inheritance)
- [Factory Design Pattern](#factory-design-pattern)
- [Coupling and Cohesion](#coupling-and-cohesion)
- [Concurrent Collections](#concurrent-collections)
- [Anonymous Inner Class](#anonymous-inner-class)
- [Lambda Functions](#lambda-functions)
- [Singleton](#singleton)
- [Eager and Lazy Loading](#eager-and-lazy-loading)
- [Scanner](#scanner)
- [Print Writer](#print-writer)
- [Input/Output Streams](#inputoutput-streams)
- [Try-Catch](#try-catch)
- [Class Loader and Resource Stream](#class-loader-and-resource-stream)
- [Try With Resources](#try-with-resources)
- [Multi-Threading](#multi-threading)
- [Thread States](#thread-states)
- [Runnable Interface](#runnable-interface)
- [Customer Exceptions](#custom-exceptions)
- [JUNIT](#junit)
- [JUNIT Annotations](#junit-annotations)
- [Normalization](#normalization)
- [SQL Data Types](#sql-data-types)
- [SQL Basic Functions](#sql-basic-functions)
- [Relational Database](#relational-database)
    - [Entities](#entities)
    - [Attributes](#attributes)
    - [Keys](#keys)
    - [DDL and DML](#ddl-and-dml)


## hashCode()
Generates a unique hash value for an object
Hashing collections will use this function to determine locations
NEEDS to be overridden if you override equals

## equals()
Determines if two objects of this class are "equivalent"
Objects are equivelant if they refer to the same place in memory, or all values within the objects are equal

## ARRAYS
[Main topic](./Arrays.md)

Stores data in consecutive memory addresses
Access data via indices
Index starts at 0
Use square brackets to access an index []

## LOOPS
while
Executes while a condition is true.
do-while
Executes first, then continues execution if a condition is true.
for
Executes a specific number of times based on an iteration value, a condition, and an increment/decrement.
for-each
Iterates over each element in a collection or array, executing for each element.
iterators (not really a loop)
Provides a way to access elements of a collection without exposing the utilizing representation.

## LISTS
Are ordered and indexed
Part of the collections API in Java -- All lists will inherit from the Lists class
Only works with objects
Java gives you wrappers for the primitive types
e.g. int -> Integer, double -> Double, etc.

## ARRAY LISTS
[Main topic](./ArraysList.md)

Dynamic array, grows as you add more data to it
Doesn't shrink dynamically
Use trimToSize() method
Default starting capacity is 10
Grows by 50% if capacity is reached
Lookup is O(1) with the index
Insertion (with no resizing) is O(1) at the beginning and end of the array
Insertion with resizing or insertion within the list is O(n)

## LINKED LISTS
Non-consecutive memory locations
Each node contains a pointer to the next node, and the data at that node
No indexes - lookup is O(n)
Insertion at the front and end are O(1)
Insertion within the list is O(n)
Capacity always equals size
Java linked-lists are always doubly linked
Pointers for next and previous list elements

## MAPS
Unordered, operate on key-value pairs
Key has to be unique
Value can be anything

## HASHMAPS
Uses hashcode() to determine index location
O(1) lookup times
Collisions are possible, but unlikely
Happens when multiple keys have the same hashcode and get put into the same index
Under-the-hood, hashmaps are arrays of linked lists

## ETS
Unordered
Only unique values, no duplicates
No indexes -- use iterators to loop through them

## HASHSETS
Use hashcode to determine location

## ITERATORS
Allow you to move through a collection without a loop
You can move through a collection one step at a time using .next()

## ENCAPSULATION
Wraps up behaviors and data into a single class
Access modifiers allow for control over how behaviors/data are acccessed
Public: Everyone
Private: Class-only
Protected: Package-only
Getter/setter methods are commonly used
Useful for data security, simplicity, etc.
POLYMORPHISM
Assists with code reusability
Method Overriding
Changing the behavior of a method inherited from a superclass
Known as run-time polymorphism
Method Overloading
Changing the parameters of a method
Known as compile-time polymorphism
Every class inherits from the Object class
Covariance - a subclass may act in place of it's superclass
Contravariance - a superclass may act in place of its subclass

## ABSTRACTION
Only shows what needs to be shown -- abstracts complexity
Offers a blueprint for creating methods via an abstract method or interface
Abstract classes can contain abstract methods, implementations are not required
Subclasses of abstract classes must implement all abstract methods
Abstract classes cannot be instantiated directly

## INHERITANCE
The concept of a subclass accessing the behaviors and data of its superclass
For a class or abstract class, use the extends keyword
You can only extend one class
For an interface, use implements
You can implement multiple interfaces

## FACTORY DESIGN PATTERN
You don't create (instantiate) objects directly -- the factory does it for you
Factories have a general class with multiple child objects (subclasses)
Instead of the main class being dependent on all the child objects, it only depends on the factory
The factory takes care of deciding which subclasses to instantiate, depending on input
Helps reduce coupling and improves cohesion
Reduces dependency between main classes and subclasses, and centrailizes object creation logic

## COUPLING AND COHESION
Cohesion refers to relationships within classes
Low cohesion -- class performs many different tasks
High cohesion -- class performs a specific set of tasks
Coupling refers to relationships between classes
Low coupling -- dependent on few classes
High coupling -- dependent on many classes
We want high cohesion (class performs specific tasks), and low coupling (dependant on few classes)
PRODUCER CONSUMER MODEL
Something produces data, another thing consumes the data
Usually a thread that makes or reads data, consumed by another thread to be processed
Multithreading technique

## CONCURRENT COLLECTIONS
java.util.concurrent
Thread safe collections
Handle synchronization for us
Queues are first in, first out

## ANONYMOUS INNER CLASS
A class that isn't declared, but is defined
Only created with functional interfaces

## LAMBDA FUNCTIONS
Shorthand way to implement the method of a functional interface

## SINGLETON
When you only want ONE instance of an object that will stay consistant
Useful when working with threads -- ensures all threads are using the same object
Any two instances of a Singleton will point to the same address in memory

## EAGER AND LAZY LOADING
Eagar -- Instantiates an object as soon as possible
Faster, but memory is wasted if data isn't needed immediately
Lazy -- Only instantiates an object when it's asked for
Slower, but can save memory compared to eager

## SCANNER
All data has to be stored into a variable
As a primitive or a string
Use nextLine() to read in data

## PRINT WRITER
Allows for better formatting of print statements
Several prints can be queued before being "flushed" out all at once to the console
close() automatically invokes flush()

## INPUT/OUTPUT STREAMS
Allow for data to flow between files
Data is read in bytes
PATHS
Relative path -- path relative to the project file
Path -- the full path, beginning from the root of your drive

## TRY-CATCH
Put "risky" code in the try block
Any errors that occur can be handled in the catch block
Can only catch one error at a time
Multiple catch blocks can be used
Start with specific errors, then get more general

## CLASS LOADER AND RESOURCE STREAM
Class loader -- Dynamically loads java classes at runtime
Resource stream -- Method to access static resources within your project
Useful for apps not running on a local machine

## TRY WITH RESOURCES
Still a try-catch block, but is given a resource (e.g. a file stream) as an argument
Automatically closes it when done
Must implement the AutoClosable interface

## MULTI-THREADING
Splits different tasks across different threads to be done concurrently
By default, Java apps run Main on one thread
Performance is increased when using multithreading, at the cost of more power usage

## THREAD STATES
NEW -- Created but not yet started
RUNNABLE -- Thread has started
BLOCKED -- Thread is waiting on some lock before continuing
WAITING -- Thread is waiting indefinitely
TIMED-WAITING -- Thread is waiting for a specified amount of time
TERMINATED -- Thread is finished

## RUNNABLE INTERFACE
Defines a task to be run by a thread
Contains a single run() method, holding the code to be executed
Allows for multiple interfaces to be implemented, and for a class to be extended
Separates the task logic from thread management
THROWS AND THROW
throw -- "Method is literally throwing an exception right now"
throws -- "Method could throw an exception at any time"

## CUSTOM EXCEPTIONS
Needs to extend an existing exception class
Should have Exception at the end of its name
Allows for improved readability when error handling

## JUNIT
Unit testing framework
Unit testing -- Testing individual program components to ensure they work as intended

## JUNIT ANNOTATIONS

[Main topic](./JUNITAnnotations.md)
 
Note that multiple methods of the same annotation type may run in any order
BeforeClass -- Method should be run once before any of the test methods in the class
e.g. Setting up a database connection
Before -- Method should be run before each test method
e.g. Loading data from a database
Test -- Method is a test method
Tests either pass or fail, and only fail if an unhandled exception is thrown
After -- Method should be run after each test method
e.g. Used to delete/rollback things that were setup
AfterClass -- Method should be run once after all test methods in a class have been run
e.g. Final cleanup

## NORMALIZATION
[Main topic](./Normalization.md)

A way to structure your database table to remove redundant information
Makes it easier to understand, enhance, and extend
Protected from
Insertion Anomalies
Situation where inserting data is impossible
Update Anomalies
Situation where updating data leads to database inconsistencies
Deletion Anomalies
Situation where deleting data leads to unintended additional data loss
FIRST NORMAL FORM (1NF)
Prevents row from a unique column from ever being inserted
Not allowed:
Mixing data types within a column
Having a table without a Primary Key
Using row order to convey information
Repeating groups

SECOND NORMAL FORM (2NF)
Each non-key column on a table must be dependent on the entire PK
Conditions to satisfy:
Must be in first normal form
All non-key columns are fully dependent on primary key
No partial dependencies

THIRD NORMAL FORM (3NF)
Forbids dependency on a non-key attribute on another non-key attribute
Every non-key attribute in a table should depend on the key only
Must be in second normal form
No transitive dependencies

## SQL DATA TYPES
[Main topic](./SQLDataTypes.md)

SERIAL - Auto-incrementing integer data, often used for primary keys.
CHAR - A fixed-length character
VARCHAR - A variable-length character string
TEXT - A character string with no specific maximum length
INTEGER - A standard integer data type
SMALLINT - A smaller integer data type
BIGINT - A larger integer data type
DECIMAL or DEC - A fixed-point number with a variable precision and scale
FLOAT - A floating-point number
BOOLEAN or BOOL - A true/false value
DATE - Stores a formatted calendar date
TIME - Stores a formatted time
TIMESTAMP - Stores formatted date and time

## SQL BASIC FUNCTIONS
[Main topic](./SQLFunctions.md)

SELECT - Specifies a column to retrieve data from in a database
FROM - Specifies the table to retrieve data from in a database
ORDER BY - Sorts the result based on a column
WHERE - Used to filter records based on a condition, e.g. WHERE condition
AND - Used in conjunction with WHERE to have multiple filters
AS - Gives a column or table a temporary alias

[Main topic](./SQLJoins.md)

JOINS
INNER JOIN - Returns records with matching values in both tables
LEFT JOIN - Returns records from your left table and any matching records from the right table
RIGHT JOIN - Returns records from your right table and any matching records from the left table
FULL JOIN - Return all records from both tables

## RELATIONAL DATABASE

### ENTITIES
Tables
Strong Entity -- Don't rely on other entities
Weak Entity -- Has a Foriegn Key, relies on other entities

### ATTRIBUTES
Describe the properties of an entitiy
E.g. Columns

### KEYS
Primary Key
Unique identifier for a row in your table
Candidate key
Candidate Key
A set of one or more columns that can uniquely identify a row within a table
Simple candidate key
A Primary Key that is made up of a single column
Employee ID
Composite Candidate Key
A primary key that is made up of multiple columns
OrderID and CustomerID
Super Key
A set of one or more columns that uniquely identify a row
Can either be composite or simple
StudentID, CourseID, Grade
Surrogate Key
A primary key used specifically as a unique identifier for a row
E.g. Auto-incrementing number
Foriegn Key
A column or group of columns used to link data between tables
RELATIONSHIPS
One-to-one
A single table A relates to a single table B
Used to create critical relationships
E.g. ID number foriegn key linking names to liscense numbers between tables
One-to-many
A row (record) in table A that relates to one or more rows in table B
E.g. A customer ID in a customer table, linking to a Order table that also contains a customer ID forign key, but that uses an order ID as its primary key
Many-to-many
Where table A relates to one or more rows in table B, and vice-versa
E.g. An Author table and a Books table, both with distinct primary keys, relying on a Junction table to link the values together

## DDL AND DML
[Main topic](./DataDefinitionLanguage.md)

DDL -- Stands for Data Definition Language
SQL commands that are used to create, drop, and modify database objects
Not the data itself, but where it sits
CREATE - Creates a table
ALTER - Modified the structure of an existing table
DROP - Deletes a table and all of its data
TRUNCATE - Removes all the data from its table, but keeps the table

[Main topic](./DataManipulationLanguage.md)

DML -- Stands for Data Manipulation Language
SQL commands that are used to add, delete, and edit data in your tables
INSERT - Adds new data into your tables
UPDATE - Modifies data existing in your table