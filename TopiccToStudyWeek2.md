<< [README](./README.md)

# Topics for Canas Exam and Mock Interview Monday (7/22/2024)

## Contents
- [Web API Development](#web-api-development)
- [HTTP Request](#http-request)
- [HTTP Response](#http-response)
- [Rest Architecture](#rest-architecture)
- [Spring Boot](#spring-boot)
- [Container, Dependency, IOC](#container-dependency-ioc)
- [Spring MVC](#spring-mvc)
- [Controllers](#controllers)
- [Design Patterns](#design-patterns)
- [Spring Data JPA](#spring-data-jpa)
- [Spring Data Repository interface](#spring-data-repository-interface)
- [Spring Data Repository interface](#spring-data-repository-interface-1)
- [Global Exception Handler](#global-exception-handler)
- [Aspect-Oriented Programming](#aspect-oriented-programming)
- [Resources](#resources)

### Web API Development
- Client-Server Architecture
- Web Servers (Tomcat)

## HTTP Request
- Http Methods(Get, Post, Put, Delete, Options)
- [Indempotent](./Idempotence.md) vs Safe Http Methods
- Path Variables and Request Parameters
- RequestBody

## HTTP Response
- Response Headers
- Status Codes
    - 200
    - 201
    - 204
    - 400
    - 401
    - 403
    - 404
    - 500
- Response Body and JSON format

## Rest Architecture
- Stateless
- Client-Server Architecture
- Layered
- Uniform interface
- catcheable

## [Spring Boot](./SpringBoot.md)
- start.spring.io / Spring Boot Initializr
- Spring Boot starter POMs
- SpringApplication.run & CommandLineRunner
- properties vs YML configuration
- Default application.properties location

## Container, Dependency, IOC
- [Bean](./Beans.md)Factory and ApplicationContext
- Instantiating an ApplicationContext
- Dependency injection
- Annotation Configuration
- @Configuration and @Bean
- @Autowired field, constructor, method injection
- @ComponentScan(basePackages)
- Stereotype annotations
- @Component, @Service, @Repository

## Spring MVC
- HandlerMapping and DispatcherServlet
- InternalResourceViewResolver (static HTML)

## Controllers
- @Controller and @RestController annotations
- @RequestMapping, @GetMapping, @PostMapping
- @ResponseBody, @RequestBody
- @RequestParam @PathVariable @CookieValue
- @ResponseStatus
- HTTP status codes, ResponseEntity

## Design Patterns
- Design Patterns: Front Controller
- Design Patterns: MVC

## Spring Data JPA
- Object Relational Mapping
- DataSource configuration
- Postresql connection properties

## Spring Data Repository interface
- JPA Annotations, @Entity, @Id
- Transient, persistent, detached
- Lazy & Eager fetching strategies
- @OneToMany, @OneToOne, @JoinColumn

## Spring Data Repository interface
- CrudRepository and JpaRepository
- Naming convention for query methods
- findByVariableName
- @Query and JPQL

## Global Exception Handler
- @ResponseStatus and @ControllerAdvice
- Bean Validation
- @Valid and @Min @Max @NotNull @NotBlank

## Aspect-Oriented Programming
- AOP and cross cutting concerns
- @EnableAspectJAutoproxy
- Pointcut, join point, advice, aspect, weaving
- Before, After, AfterReturning, AfterThrowing, Around
- Pointcut expressions
- @within, @target, @execution
- \* and .. parameters
- JoinPoint argument
- ProceedingJoinPoint and Around
- JDK Dynamic Proxy vs CGLIB proxy (theory)

## Resources
![](./Images/TopicsToStudyWeek2.png)