<< [README](README.md)

# Title

## Contents
- [Register as a Bean](#register-as-a-bean)
- [Bean Scopes](#bean-scopes)
- [Resources](#resources)

## Register as a Bean
- @BEAN
    - register the bean inside the BeanFactory
    - this way spring can give you beans when you ask from them

## Bean Scopes

- @SCOPE - tells spring what kind of bean you want
    - BEAN SCOPES:
    - singleton - each bean will be the same (this is the default, if you dont specify a new scope)
    - prototype - each bean will be different
    - application - creates a bean for the lifespan of the entire app
    - request - creates a bean for the lifespan of an HTTP request
    - session - creates a bean for the lifespan of a user's session
    - websocket - creates a bean for the lifespan of a websocket

## Resources
- [Spring Beans Showdown: Unraveling the Mystery of @Component vs @Bean!](https://www.youtube.com/watch?v=CWEQ-1vff1o) - 🎥18:17 - Discussion and examples of Spring Beans including @Component and @Bean. He also mentions his 4-hour course on Spring Boot.

- [Spring ultimate basics: What are Spring Beans and what is the Spring Container↗️](https://www.youtube.com/watch?v=aS9SQITRocc) - 🎥16:30 - Discussion and example for Spring Beans and IOC container.