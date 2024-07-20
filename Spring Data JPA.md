<< [README](./README.md)

# Spring Data and JPA

## Contents
- [Three Layers](#three-layers)
- [JDBC](#jdbc)
- [JPA](#jpa)
- [Example Stack](#example-stack)
- [Example Project Notes](#example-project-notes)
- [Cardinality](#cardinality)
- [Display Logging](#display-logging)
- [Startup Database Validation](#startup-database-validation)
- [Cyclical References](#cyclical-references)
- [See Also](#see-also)


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

![](Images/Pasted%20image%2020240718103150.png)

**Ports**
 - HTTP - 8080
 - DB - 5432
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

# Example Project Notes
Created a new project with these dependencies:
![](Images/Pasted%20image%2020240718101542.png)
`devtools` is also a good thing to add, prevents from constantly stopping/restarting by doing it automatically!

In pgAdmin4, create a new Database called `movies`. Right-click that database, select the `Query tool`, and run this code:

```
/* If the movies or directors table already exists, drop it so it can be remade */
drop table if exists MOVIES;
drop table if exists DIRECTORS;

create table DIRECTORS (
	id SERIAL PRIMARY KEY,
	first_name VARCHAR(50),
	last_name VARCHAR(50)
);

create table MOVIES (
	id SERIAL PRIMARY KEY,
	movie_title VARCHAR(50),
	rating INT,
	director_id INT,
	FOREIGN KEY (director_id) REFERENCES DIRECTORS(id)
);

/*

    used by the h2 database duing application startup

    populates table with data
    
*/

/* make sure to insert directors first */
insert into DIRECTORS (first_name, last_name) values ('Carma', 'Baine');
insert into DIRECTORS (first_name, last_name) values ('Isa', 'Phibb');
insert into DIRECTORS (first_name, last_name) values ('Karalynn', 'Caw');
insert into DIRECTORS (first_name, last_name) values ('Codie', 'Sally');
insert into DIRECTORS (first_name, last_name) values ('Rozamond', 'Rumbellow');

insert into MOVIES (movie_title, rating, director_id) values ('Friend Zone (Pagafantas)', 2, 2);
insert into MOVIES (movie_title, rating, director_id) values ('Kismet', 5, 1);
insert into MOVIES (movie_title, rating, director_id) values ('Casanova', 6, 2);
insert into MOVIES (movie_title, rating, director_id) values ('Extreme Ops', 2, 1);
insert into MOVIES (movie_title, rating, director_id) values ('Goodbye First Love', 7, 2);
insert into MOVIES (movie_title, rating, director_id) values ('Woman''s Face, A (En kvinnas ansikte) ', 8, 4);
insert into MOVIES (movie_title, rating, director_id) values ('French Film', 9, 1);
insert into MOVIES (movie_title, rating, director_id) values ('Hitting Home', 7, 1);
insert into MOVIES (movie_title, rating, director_id) values ('Contracted', 7, 3);
insert into MOVIES (movie_title, rating, director_id) values ('Room with a View, A', 3, 1);
insert into MOVIES (movie_title, rating, director_id) values ('40 Pounds of Trouble', 3, 1);
insert into MOVIES (movie_title, rating, director_id) values ('Easy A', 4, 4);
insert into MOVIES (movie_title, rating, director_id) values ('Grouse', 8, 5);
insert into MOVIES (movie_title, rating, director_id) values ('Mind Game', 4, 4);
insert into MOVIES (movie_title, rating, director_id) values ('Bye Bye Monkey (Ciao maschio)', 9, 3);
insert into MOVIES (movie_title, rating, director_id) values ('Three on a Weekend', 2, 1);
insert into MOVIES (movie_title, rating, director_id) values ('Legend of Hell House, The', 8, 5);
insert into MOVIES (movie_title, rating, director_id) values ('Teeth', 9, 4);
insert into MOVIES (movie_title, rating, director_id) values ('Kull the Conqueror', 3, 1);
insert into MOVIES (movie_title, rating, director_id) values ('Seconds Apart ', 9, 2);
insert into MOVIES (movie_title, rating, director_id) values ('Brain, The', 5, 4);
insert into MOVIES (movie_title, rating, director_id) values ('All Fall Down', 8, 4);
insert into MOVIES (movie_title, rating, director_id) values ('Bopha!', 4, 1);
insert into MOVIES (movie_title, rating, director_id) values ('Avengers: Infinity War', 10, 4);
insert into MOVIES (movie_title, rating, director_id) values ('Avengers: Endgame', 9, 2);
```

From there, under schemas -> public -> tables, you can right-click and view all the rows that have been added into the database.

Now, we're heading back to our `applications.properties` file under `src\main\resources\application.properties`.

```
# Setup the database connection

spring.datasource.url=jdbc:postgresql://localhost:5432/rottenpotato

spring.datasource.username=postgres

spring.datasource.password=<YOUR PASSWORD YOU SET UP>
```

For the password, we can also use Spring expression language, so its safe to push to Github later. To do this, you can use `${dp-pwd}` to read values from the environment, which will store the value for us.

To generate `launch.json`, you can do `ctrl+shift+d`, and then select the option to have VSCode generate it for you.

Making:
 - Folders controllers, services, repositories, models
 - Make java files Director.java and Movie.java

**Requirements for a POJO:**
 - Has a default constructor
 - Getters and setters for all private data

**CrudRepository**
Has methods for CRUD operations!

**PacingAndSortingRepository**
Extends CRUD operations with ability to specify limit and offset the data returned.

![](Images/Pasted%20image%2020240718114809.png)
**The lifecycle model for a JPA entity**

**Optional**
 - Holds what it found
 - Alternatively, has an "empty" state

[Spring Data Reference](https://docs.spring.io/spring-data/jpa/reference/#repositories.query-methods.details "https://docs.spring.io/spring-data/jpa/reference/#repositories.query-methods.details")

## Cardinality
![](Images/Pasted%20image%2020240718132831.png)

In our case-

![](Images/Pasted%20image%2020240718133425.png)

-is the relationship we have.

## Display Logging
*Shows relevant SQL in error logs when debugging.*
![](Images/Pasted%20image%2020240718134116.png)
```
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
```

When logging, don't use a print statement -- you'll want to use the relevant logs.


## Startup database validation

`spring.jpa.hibernate.ddl-auto=validate`

Ensures that the database schema is in sync with the JPA entities.
## Cyclical References

![](Images/Pasted%20image%2020240718135552.png)

## See Also
- [JPA](./More%20JPA.md)
