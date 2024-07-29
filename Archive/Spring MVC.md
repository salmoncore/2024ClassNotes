<< [README](README.md)

# Spring MVC

**Contents**
- [Spring MVC](#spring-mvc)
- [MVC Overview](#mvc-overview)
  - [MVC - Model View Controller](#mvc---model-view-controller)
  - [Serverlets](#serverlets)
  - [Front Controller](#front-controller)
- [Project 1 Structure](#project-1-structure)
- [Class Notes](#class-notes)
  - [Controller vs RestController](#controller-vs-restcontroller)
    - [RestController](#restcontroller)
    - [Controller](#controller)
  - [Returning via HTTP](#returning-via-http)
  - [Postman](#postman)
  - [See Also](#see-also)

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

### Other
 - `@AutoWired` - Asks spring boot to give us a service
 - `@PathVariable` - e.g. `user/[id]`, similar to `@RequestParam`
 - `@PostMapping` - Used for creating data via `POST` request
 - `@PutMapping` - Used to handle HTTP `PUT` requests for setting data
 - `@RequestMapping` - Can handle all types of requests
	 - Note that `POST` requests are used to send data
 - `@RequestBody` - Looks for the data in the body of your request
	 - Deserializes the JSON
 - `@RequestParam` - Finds the data for the parameter in the URL path
	 - `/users/firstName?firstName=[data]` - Everything after the `?` are the parameters
```
@GetMapping("/firstName")
public List<User> findByFirstName(@RequestParam String firstName) {
    return service.findUsersByFirstName(firstName);
}
```

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

## Postman

Install and make an account, and then hit the + button and add a new request at the port we specified!
![alt text](<PostMan.png>)

Start the `UserController.java` file, and once it's done loading, the GET request should return `Hello World!`.

![](Images/Postman%20Result.png)

### Requests
 - `GET` - Retrieves data
 - `POST` - Creates data
 - `PUT` - Updates data
 - `DELETE` - Deletes data

## Response Entity
 - An object that gives you more control over your HTTP response.
	 - Allows you to create objects
	 - Modify status codes, header, etc.

```
public ResponseEntity<User> createUser(@RequestBody User user) {
     User createdUser = service.createUser(user);
     return new ResponseEntity<User>(createdUser, HttpStatus.CREATED);
     // Should return with a 201 CREATED response
}
```

# DTOs

Data Transfer Object
 - Facilitate the transfer of data for your models
	 - More specifically, rather than transferring your model, you transfer its DTO
 - DTO isn't going to have everything a model would
	 - A hardcoded way to make sure that certain info in the model doesn't get passed to the frontend
		 - For example, passwords, or other sensitive information
		 - Not necessarily for security, though - it just ensures it doesn't get to the frontend
 - To work with a DTO, you need a Mapper!
	 - Converts the model to the DTO, and vice-versa
 - You might consider multiple DTOs
	 - Like a `UserCreateDto` that has a password, but no ID

   ## See Also
   [JPA > Spring MVC](More%20JPA.md#spring-mvc)



