<< [README](./README.md)

# Spring MVC

**Contents**
- [Spring MCV](#spring-mvc)
- [MVC Overview](#mvc-overview)
  - [MVC - Model View Controller](#mvc---model-view-controller)
  - [Serverlets](#serverlets)
  - [Front Controller](#front-controller)
- [Project 1 Structure](#project-1-structure)

# MVC Overview

## MVC - Model View Controller

**View** - What the user sees

↑↓

**Controller** - A go-between

↑↓

**Model** - The structure of our data - or "pojos"

## Serverlets

 - Allow you to make HTTP requests
   - Uses Tomcat
     - The server for our project!

## Front Controller

 - Takes in many requests
   - Disperses HTTP requests to the specified controller as needed
 - Main dispatcher is the "Dispatcher Serverlet"

![alt text](<Images/Front Controller.png>)

# Project 1 Structure
 - Stereotype Annotations
 - `@Component`
   - `@Controller` - Takes in HTTP requests, and sends responses
   - `@Service` - Business logic, e.g. parsing data
   - `@Repository` - Talks to the DB - Sent back to the user

![[Model.png]]

---

# Class Notes

 - Don't store passwords in plaintext!

## Controller vs RestController

### RestController
 - Implicitly adds `@ResponseBody` to every method in the class.
 - `@ResponseBody` tells the controller that the object returned in serialized into JSON inside the body of the HTTP response.
	 - Needs to take in data from somewhere -- using `@RequestMapping`.

### Controller
 - More general.
	 - You'd have to add `@ResponseBody on every method`.


## Returning via HTTP
```
// Return is accessible on localhost:8080/users/helloworld

@RestController
@RequestMapping("/users")
public class UserController {
    @RequestMapping("/helloWorld")
    public String helloWorld() {
        return "Hello World!";
    }
}
```

