Morning Pre-lecture Notes

New links added to canvas! One has practice tests and info for the ISTQB exam.
 - There's a 74 page-long syllabus thing about all of the separate thing we can go over.
 - There's also some practice exams that she's posted on canvas.
	 - **She said she would be taking questions from the practice exam for the ==Monday exam== - Review those!**

Friday presentation lengths are going to be 5-7 minutes. Try not to exceed 10 minutes.
 - Create warehouse
 - Create items
 - Do CRUD operations
 - Show code
 - Show requests going from the frontend to the backend to the DB
 - She may have other questions about the project

---

# Testing Throughout the SDLC
Testing heavily depends on the type of SDLC you use.

Some companies have one organizational lifecycle development lifecycle they always use, others have several depending on project. There's not a one-size-fits-all solution.

### Software Development Lifecycle Model
Abstract, high-level representation of the software development process.
Defines the relationship between development phases and types of activities.
 - Logically
 - Chronologically

### SDLC Models
Sequential
 - Waterfall model
 - V-model
 - W-model
Iterative
 - Spiral
 - Prototyping
Incremental
 - Unified Process

Specific Methods and Agile Practices
 - Acceptance-test driven development
 - Behavior-driven development
 - Domain-driven development
 - Extreme programming
 - Feature-driven development
 - KANBAN
 - Lean IT
 - Scrum
 - Test-driven development

### Impact of SDLC
Testing must be adapted to the SDLC.
Again, testing for one method may not be appropriate for another.
Testing has an impact on:
 - Scope and timing of test activities
 - Level of detail of Test Documentation
 - Choice of techniques and test approach
 - Extent of test automation
 - Role and responsibilities of a tester

It's assumed there may be changes in the software process, and that documentation would therefore be a lot less. With something like waterfall, you're documenting almost everything and you have strict requirements.

In Agile, it's assumed there will be changes. To keep regression testing possible, there's a large focus on test automation. If you wanted to release software really quickly, you'd push the test automation into a release pipeline, which will run checks on code before it is sent to the customer.

### Verification vs. Validation

May sound similar and be accidentally used interchangeably, but for testers, we need to know the difference.

**Software Verification**
 - Evaluating a work product, component, or system to determine whether it meets the requirements set.
 - "Is the product built according to the specification?"

**Software Validation**
 - Evaluating a work product, component, or system to determine whether it meets the user needs and requirements.
 - "Is the product fit for the purpose? Does it solve the problem?"

### Sequential Development
 - Entire system is built at once
 - Strict sequence of activities
	 - Define
	 - Implement
	 - Test
 - Each phase must be finished before the next phase starts
 - Testers start participating in requirement reviews, test analysis, and test design
 - Dynamic testing cannot start early in the SDLC

### Testing in the Waterfall Model
The most well-known sequential development model, where a solution needs to be built to solve a problem/fulfill a need.

 - User Requirements
	 - System Requirements
		 - Global Design
			 - Detailed Design
				 - Implementation
					 - Testing

**Issues:**
 - Testing at the end of the coding process
	 - Very late, doesn't detect issues earlier with design documents and etc.
 - Defects detected close to implementation
 - Difficult to pass feedback up the waterfall

### Testing in the V-Model
V for verification/validation.
 - Testing happens early, and are carried out in parallel with development activities.

![](../Images/Pasted%20image%2020240731093546.png)

Note that all our designs, global/detailed/etc, design is documented in a detailed way.
 - Component tests verifies the functionality of components that are separately testable.
 - Integration/component integreation tests, these are for different parts of the system communicating.
 - System tests ensures the system as a whole is working.
 - Acceptance tests - Does it solve the problem? Does it work with the other systems necessary?

### Advantages and Disadvantages of the V-Model
**Advantages**
 - Simple and easy
 - Systemic
 - Easy to track
 - Testing starts from the requirement phase
 - Detailed explanations of problems
 - Defects can be found early
 - Works well for small projects

**Disadvantages**
 - Not flexible
 - Regular updates required if the project changes
 - Can't be use in complex projects
 - No scope for risk management

### W-Model
The W doesn't stand for anything, just looks like one.

Combination of a model for development, and a model for testing.
Shows the two as parallel tracks instead of cross-arms.
Ensures each step is verified and validated.

![](../Images/Pasted%20image%2020240731094755.png)

### Advantages and Disadvantages of the W-Model
**Advantages**
 - Testing can run parallel with development tasks
 - No division between development and test tasks
 - Developers are often responsible for removing defects

**Disadvantages**
 - Complex to implement
 - Resource allocation might not be sufficient in most cases
 - Testing has equal weight as many activities in the development process

## Incremental and Iterative Models
Very often, these two are combined. It's possible to have them individually, but less common.

### What is incremental development?
System is built in pieces.
Pieces are called increments.
Generally, after each iteration there should be an increment or working prototype delivered.

Each part of the process is also done in pieces:
 - Establishing requirements
 - Designing
 - Building
 - Testing

### What is iterative development?
Builds are provided in iterations.
 - Changes in features/scope.

Each iteration involves cross-functional teams working simultaneously on different phases.
End of each iteration is a shippable product.
In each iteration, static and dynamic testing may be done on all test levels.

### Testing in Spiral Models
Based on prototyping, prototypes are used to design the system.
Development work passes through a sequence of prototypes that are:
 - Tested
 - Redesigned
 - Prototyped
 - Retested
 - Until all design decisions have been proven by testing

## Fundamentals of Agile
### Agile Manifesto
Some software development gurus decided they didn't like how software was being developed - the current development practice was slow, inflexible, and didn't have any system of feedback. They wanted to discover better ways of developing software, and published a manifesto with these details:

**Individuals and interactions** OVER process and tools
**Working software** OVER comprehensive documentation
**Customer collaboration** OVER contract negotiation
**Responding to change** OVER following a plan

The Agile Manifesto values the concepts on the right, but believes the ones on the left have a greater value.