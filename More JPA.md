<< [README](./README.md)

# JPA
## Contents
- [Recap](#recap)
- [Potential Exam Topics](#potential-exam-topics)
- [Web API Development](#web-api-development)
- [Spring Boot](#spring-boot)
- [Spring MVC](#spring-mvc)
- [Spring Data JPA](#spring-data-jpa)
- [Transactions](#transactions)
- [Aspect-Oriented Programming](#aspect-oriented-programming)
- [Global Exception Handler](#global-exception-handler)
- [Indempotence](#idempotence)
- [Validation Checks](#validation-checks)
- [Transient Objects](#transient-objects)
- [Advice and Aspect Oriented Programming](#advice-and-aspect-oriented-programming)
# Recap
- `DirectorController`
	- REST controller managing HTTP requests related to `Director` entities.
		- Annotated with `@RestController`, marking it as a controller where every method returns a domain object instead of a view.
		- Mapped to `/directors` URL path.
	- `getMethodName(@PathVariable int id)` retrieves a `Director` by its ID within `DirectorRepository`.
- `MovieController`
	- Another REST controller, this time for `Movie` entities.
		- Mapped to `/movies`
		- `findAll()` - Returns a list of all movies from `MovieRepository`
		- `findById`, `create`, etc. are placeholders for now.
- `DirectorRepository` and `MovieRepository`
	- Interfaces extend `JpaRepository` to provide JPA methods, such as `findAll()`.
		- Makes it easier to perform **CRUD** operations on the database.
			- **Create, Read, Update, Delete**
 - POM File
	 - Includes build settings, dependencies, etc.
- Configuration
	- Spring MVC
		- Handles HTTP requests, dispatching them to their controller method
	- Spring Data JPA
		- Abstracts out database interaction
	- Hibernate
		- Acts as the JPA implementation
			- Converts entity states into database operations

---
# Potential Exam Topics
![](Images/Pasted%20image%2020240719104756.png)

### Web API Development

- Client-Server Architecture
- Web Servers (Tomcat)
- HTTP Fundamentals
    - HTTP Request (Methods: Get, Post, Put, Delete, Options)
    - Path Variables and Request Parameters
    - Request Body
- HTTP Response
    - Response Headers
    - Status Codes (200, 201, 204, 400, 401, 403, 404, 500)
    - Response Body
- REST Architecture
    - Stateful vs Stateless (sessions, tokens, JWT)

### Spring Boot

- Spring boot.io / Spring Boot Initializer
- Spring Boot starter POMs

### Spring MVC

- HandlerMapping and DispatcherServlet
- InternalResourceViewResolver (static HTML)
- `@Controller` and `@RestController` annotations
    - `@RequestMapping`, `@GetMapping`, `@PostMapping`
    - `@ResponseBody`, `@RequestBody`
    - `@RequestParam`, `@PathVariable`, `@CookieValue`
- JSR-303 Validation / `@Valid`
- HTTP status codes, `ResponseEntity`
- Design Patterns: Front Controller
- Design Patterns: MVC

### Spring Data JPA

- Object Relational Mapping
- DataSource and connection pooling
- Spring Data Repository interface
    - JPA Annotations, `@Entity`, `@Id`
    - Transient, persistent, detached
    - Lazy & Eager fetching strategies
    - `@OneToMany`, `@OneToOne`, `@JoinColumn`
- `CrudRepository` and `JpaRepository`
- Naming convention for query methods
    - findByVariableName
    - Sorting and Where
    - `@Repository`
    - `@Query` and JPQL
    - `@Param` vs ?1
    - Joining Nested Objects
- PostgreSQL connection properties
- Pagination & `PagingAndSortingRepository`
- Design Patterns: Data Access Object
- Design Patterns: Data Transfer Object
- Design Patterns: Repository
- H2 Embedded database, data/schema.sql

### Transactions

- Local and global transactions
- `@Transactional` annotation
- Declarative transaction management
- Default rollback policy
- Transaction propagation
- Transaction isolation levels

### Aspect-Oriented Programming

- AOP and cross cutting concerns
- `@EnableAspectJAutoProxy`
- Pointcut, join point, advice, aspect, weaving
    - Before, After, AfterReturning, AfterThrowing, Around
- Pointcut expressions
    - `@within`, `@target`, `@execution`
    - `*` and `..` parameters
- JoinPoint argument
- ProceedingJoinPoint and Around
- JDK Dynamic Proxy vs CGLIB proxy (theory)

### Global Exception Handler

- `@ResponseStatus` and `@ControllerAdvice`
---
# Back to JPA

### Idempotence
- [Indempotence Main Document](./Idempotence.md)
![](Images/Pasted%20image%2020240719110934.png)
 - HTTP put/delete requests should be idempotent?

### Validation Checks
 - `@Min` - Only for numeric types
 - `@Max` - Only for numeric types
 - `@NotNull`
 - `@NotBlank` - Only for Strings

### Transient Objects
 - Lifecycle
	 - **Instantiation** - Object is created using `new`
	 - **Transient state** - Object exists in memory, with no persistent representation in the database, and is not managed by the persistence context
	 - **Persistence** - If you persist a transient object (e.g. using `persist()` in JPA), it transitions from being transient to managed, where JPA starts tracking changes to the object and will sync it with the database 

`@Cascade(CascadeType.PERSIST)`
 - Makes sure the persist (save) operation on the parent entity also triggers a persist operation on the child entity associated with it.
- e.g. if `Movie` entity contains a `Director`, the `Director` will automatically be persisted as well if its not already in the database.

### Advice and Aspect Oriented Programming
 - Problem: Certain aspects of our code get tangled together 
	 - Separation of concerns is violated!
![](Images/Pasted%20image%2020240719115744.png)

 - Cross-cutting concerns:
	 - Logging
	 - Exception handling
	 - Security
	 - Caching

**We want to separate and modularize the Cross-cutting concerns.**
 - How does the code get invoked?
	 - Depends on the AOP framework
		 - Some will inject try-catch at compile time
		 - Some do a similar approach at runtime
	 - Spring AOP 
		 - Dynamically inject code during runtime via a proxy
	 - AspectJ
		 - Weaves the code together at compile time (injecting bytecode into bytecode)
![](Images/Pasted%20image%2020240719120833.png)

Examples:
 - `@RestControllerAdvice`
	 - Terminology "advice" 
		 - The code used to run when a cross-cutting concern needs to be handled
		 - Think of how the code is being spliced as a film reel with new film being inserted - we're just marking where new code should be spliced in, and where we want our code to resume
	 - To describe when it should run - use `PointcutExpressions`
	 - These points in our code are called `JoinPoint`
		 - A point in the execution of a program as a method call or exception thrown
		 - `Pointcut`
			 - An expression that selects one or more Join Points
		 - Advice
			 - Code to be executed at each selected Join Point
		 - Aspect
			 - A module that encapsulates pointcuts and advice
		 - Weaving
			 - Technique by which aspects are combined with main code

Types of Advice:
 - `@Before`
 - `@After`
 - `@AfterReturning`
 - `@AfterThrowing`
 - `@Around`

![](Images/Pasted%20image%2020240719140518.png)
![](Images/Pasted%20image%2020240719140541.png)
![](Images/Pasted%20image%2020240719140635.png)

What are the types of advice?
What are the types of mapping?
What are the different states?
How do you make a field a primary/foreign key?
Explain one to many/many to one?