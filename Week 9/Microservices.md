***Presentation for Project 2***
 - Keep it around 10 minutes
 - Presentations will start at 11 on Friday
	 - 11-12:30 is the presentation timeframe
 - Keep it in a stand-up format more or less
	 - Go over milestones
	 - Nice documentation
	 - Demo the project
	 - For reports, we can add them in Canvas
	 - **We will submit the Github link to Canvas as well**
 - For something like SonarCloud, we could talk about the results in the presentation, but include the links to the results on the Github or attached to a project report - a README or something also works fine.
 
---

# Microservices

Everything we've worked with at this point has been monolithic - all code is in more or less one spot, one container. 

With microservices, we're breaking up these "services" and having them run in their own space.

*Microservices*
 - Loosely coupled architecture
 - Breaks down monolithic architecture
 - Easy to scale up/scale down services
 - Fault tolerant - if one service fails, it won't bring the whole thing down

![](../Images/Pasted%20image%2020240904101426.png)

*How might you split up a monolithic architecture?*
 - Domain Driven Design
	 - "We are going to split up our microservices - based on the domain of the company"

![](../Images/Pasted%20image%2020240904102013.png)

![](../Images/Pasted%20image%2020240904102506.png)

The frontend will send a HTTP request to the API gateway.
From the gateway, it'll forward the request to one of the services. 
Each request can then be forwarded to the other services, like this:

![](../Images/Pasted%20image%2020240904102600.png)

**Common Responsibilities @ API Gateway**
 - Load balancing
	 - Helps prevent services from being overrun
		 - Limits the number of requests sent to a service
		 - Resists DDoS attacks
 - Routing
	 - Ensures requests get routed properly
	 - E.g. paths, cookies, headers, methods
 - Handling CORS
	 - Done in `application.yml`
	 - "Who can get to your services?"
	 - SSL Termination
	 - Ensuring requests going to the service are secure
		 - HTTPS and verification needed for the API gateway, HTTP within the services

**Service Discovery**
 - "For the API gateway to keep track of all the services"
	 - Gateway is responsible for the service discovery, will be told by the Service Discovery where all the services are / if they are up and running
	 - Registry for all of the services
		 - What services are up or down
		 - Where they are
	 - Heartbeat requests
		 - A request with only a head - no body to the request
		 - Helps prevent cascading failure:
![](../Images/Pasted%20image%2020240904104415.png)
In this scenario, B is trying to send a request - but C is down. B will attempt to send multiple requests that won't go through, as they all fail.
 - How can we prevent cascading failure?

**Circuit Breaker**
 - A way to help prevent cascading failure
 - When a CB gets popped, it'll execute a fallback plan

Each service will have a circuit breaker attached with which it will communicate to the other services.
 - In the event of a service outage, the circuit breaker will **pop**, at which point a fallback plan can be executed:
![](../Images/Pasted%20image%2020240904105103.png)

---

For project 3, these microservices are going to be stored within different repositories - that makes it easier for CI/CD.

If we want to create a service for our microservice setup, we need to make different repositories.

Make a new folder for the microservices, and then use spring initalizr - create maven project.

Defaults for everything.

![](../Images/Pasted%20image%2020240904110857.png)

For dependencies, search for Eureka Server

![](../Images/Pasted%20image%2020240904110935.png)

![](../Images/Pasted%20image%2020240904111035.png)

This is the dependency needed to set up the Eureka server, included in the steps above.

All of our services are going to be connected to this Eureka server - the services will send heartbeat requests that will get picked up by the Eureka server.

![](../Images/Pasted%20image%2020240904111228.png)

Head here

![](../Images/Pasted%20image%2020240904111251.png)

Add the annotation `@EnableEurekaServer`. This makes sure the Eureka server is enabled on the application. Additionally, add `import org.springframework.cloud.netflix.eureka.server.EnableEurekaServer;` to the imports.
Under `resources`, rename `application.properties` to `application.yml`

Add the following:

```
server:
    port: 8761  # Standard port for Eureka server

spring:
    application:
        name: eureka  # ID for the Eureka discovery client
```

Note that we want *each* project to correspond to a different port - they can't share a port.

Now that we have it set under the name eureka, we need to ensure that it doesn't register itself. Add this below:

```
eureka:
    client:
        fetch-registry: false
        register-with-eureka: false
```

Make a new folder called `gateway` to initialize a new project into, call the project `spring-gateway`

![](../Images/Pasted%20image%2020240904112537.png)

Add these dependencies.

Again, change `application.properties` to `application.yml`, and add this:

```
server:
    port: 8125  # Standard port for api gateway
  
# Setting up eureka client for service discovery
eureka:
    client:
        service-url:
            defaultZone: http://localhost:8761/eureka/  # Location of Eureka server
  
spring:
    cloud:
        gateway:
            cors-configurations:
                '[/**]':
                    allowedOrigins: http://localhost:5173  # url allowed to gateway
                    allowedMethods:  # Allowed HTTP methods
                        - GET
                        - POST
                        - PUT
                        - DELETE
```

![](../Images/Pasted%20image%2020240904114059.png)

Heading here to the Gateway java file, add the `@EnableDiscoveryClient` annotation and the import `import org.springframework.cloud.client.discovery.EnableDiscoveryClient;`.

Hit ctrl+shift+p, make a new project with called accounts-service and give it these plugins:
![](../Images/Pasted%20image%2020240904114629.png)

Once again, rename `application.properties` to `application.yml`, and add the following:

```
server:
    port: 8081
  
spring:
    application:
        name: accounts-service  # used as the ID in the gateway routes
  
eureka:
    client:
        service-url:
            defaultZone: http://localhost:8761/eureka/ # Location of Eureka server
  
    # Configuring heartbeat frequency for the service
    instance:
        leaseRenewalIntervalInSeconds: 1
```

---

Back from lunch, we just continue on. I'll leave anything of note here.

We have:
 - Payment service
 - Account service
 - Eureka service
 - Gateway

We're having some issues

Note that when you start it up, start the server, then the gateway, then the other services.

---

*Notes for Thursday*

# Message Queues
 - Producer/consumer or publisher/subscriber model
	 - Publisher sends data to the exchange (RabbitMQ), where the subscriber is reading from
 - Can be an alternative to HTTP
 - Advantages - more decoupling
**RabbitMQ is an example of this type of service.**

## HTTP Requests
 - Synchronous
	 - Will wait for a response 
 - Point-to-point
	 - 1:1 relationship between devices

## MQ
 - Asynchronous 
	 - Sends messages and doesn't need a response
 - One-to-many
	 - One message can be sent to many queues

## Rabbit MQ
 - Built on AMQP (Advanced Message Queuing Protocol) in SpringBoot
 - Writes to an exchange or read from an exchange


*RabbitMQ is going to utilize Exchanges and Queues*
A publisher will send messages to our **Exchange** - there are several types that can be sent to.
### Exchanges
 - **Direct Exchange**
	 - Goes directly to the **queue** - ==point-to-point==
	 - Goes from the **queue** to the ***subscribers***
 - **Topic Exchange**
	 - Goes to some pattern of **queues** - a one-to-many relationship
		 - "==Pattern matching==" being the way for it to determine what queues to select
 - **Fanout Exchange**
	 - Goes to queues as based on name - one-to-many as well
		 - "==Based on name==" meaning it just gets sent to some named queues

![](../Images/Pasted%20image%2020240905101046.png)

---

*Class Example*

**Make a new project with spring initalizr**
 - Name it `demo-publisher`
 - For dependencies, add:
	 - Spring Web
	 - Spring for RabbitMQ
	 - Eureka Discovery Client

Head to Spring gateway, go to `application.yml`, uncomment ... and then start the application services, starting with the server, then the gateway and all the other services.

---

In-class Q's:
 - What class is used to listen to messages?
	 - RabbitListener - used to listen/read messages