<< [README](./README.md)
# Three Layers

**The Controller Layer**
 - We're taking in requests from a client (a PC/phone/etc.)
	 - Requests are coming in as HTTP requests
 - Using REST, the controller returns JSON, etc. back to the client

**The Service Layer**
 - Handles business logic
	 - Processing, etc.

**The Repository Layer**
 - Connects to database and model

*We do not want the frontend directly connecting to the database!*
 - Not only is this fragile if something changes, but that is a very poor security practice!
 
Additionally, we do not want Java making requests in SQL! We want a separation of concerns.

# JDBC
**Java Database Connectivity** 

*Hierarchy:*

JDK
 - JRE
	 - JDBC
	 - JVM

JDBC has interfaces and driver classes, that implement the statement interface.

![](Images/Pasted%20image%2020240718094210.png)

## JPA
**Java Persistency API**
- Standard describing how we interact with the database
- Abstraction layer over JDBC

**Hibernate**
 - Implementation of JPA
 - **ORM** Framework
	 - **Object Relational Mapping**

**Spring Data JPA**
 - Abstraction layer over Hibernate

### Example Stack:
![](Images/Pasted%20image%2020240718094740.png)

