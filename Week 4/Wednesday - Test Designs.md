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

## Fundamentals of [Agile](https://www.atlassian.com/agile)
### Agile Manifesto
Some software development gurus decided they didn't like how software was being developed - the current development practice was slow, inflexible, and didn't have any system of feedback. They wanted to discover better ways of developing software, and published a manifesto with these details:

**1. Individuals and interactions** OVER process and tools
**2. Working software** OVER comprehensive documentation
**3. Customer collaboration** OVER contract negotiation
**4. Responding to change** OVER following a plan

The Agile Manifesto values the concepts on the right, but believes the ones on the left have a greater value.

### Individuals and Interactions
Agile is people-centered
Teams build software - not processes
Continuous communication

### Working Software
Customers do not care about detailed documentation
Working software is the most useful and valuable
Enables rapid feedback to the development team
Availability of working software can result in time-to-market advantage

Agile is well-suited for environments where the solution isn't necessarily clear - for places where you might want to innovate.

### Customer Collaboration
Customer finds it difficult to specify requirements.
Working strictly on the original requirements might end up with useless software.
Collaboration results in better understanding of what the customer wants.
Contracts are important, working closely together with customers is more likely to bring success.

Sticking with your original plan the entire time can become useless as requirements change and feedback is exchanged.

### Responding to Change
Change is inevitable and should be responded to
 - Before Agile, change wasn't welcomed since it'd cause delays, higher costs, complications
Flexibility is more important than sticking to the plan
Smart and flexible planning is needed
Many factors can have a major influence on the project
 - Environment
 - Business domain
 - Legislation
 - Technological advances

### Whole-team Approach
Involving everyone with the needed skills and knowledge to ensure success
The team includes customer and other business representatives
Teams should be relatively small (3-9 people)
 - Larger teams should be split up
Approach is supported through daily stand-up meetings with the entire team
Promotes more effective and efficient team dynamics
 - Another one of the ideas behind Agile development

### Agile Testing Specifics
Changes will occur, so:
 - Use lightweight documentation
 - Implement extensive test automation
Use experience-based testing for manual test activities

### Agile Approach - SCRUM
![](../Images/Pasted%20image%2020240731104006.png)

In Agile, there are two approaches used a lot - SCRUM and KANBAN

**SCRUM**
The product organizer makes and ranks a list of required features/stories. **This is the Product Backlog.**

The team selects requirement items it commits to deliver by the end of the spring. **This is a Sprint Plan Meeting.**
 - Typically, sprints are a fixed-length.

Task Breakdown - **the Sprint Backlog.**

When you have a releasable product, that is going to be the product increment.
To ensure there is a releasable product at the end of a sprint, the SCRUM team defines an appropriate criteria for a sprint completion.

**Kanban**
![](../Images/Pasted%20image%2020240731104951.png)

Kanban utilizes three instruments:
 - Kanban Board
 - Work in progress limit
	 - Maximum number of tickets for a column
 - Lead time

Value chain is visualized by the board, each column focusing on an activity or related activity.
The main idea of Kanban is the board - it's more of an organization tool for visually knowing what's in progress and where it's at. It's not so much a development philosophy like Agile is.

### Kanban vs Scrum
**Similarities**
 - Visualization of active tasks
 - Transparency on content and progress
 - Inactive tasks are in the backlog
 - Tasks get placed on the backlog when there is capacity

**Differences**
- Iterations (sprints) are optional in Kanban\
- Deliverables are released item by item instead of in a release
- Timeboxing is optional, unlike in SCRUM

### Agile and Testing
**Benefits**
 - Focus on working software and good quality code
 - Testing as starting point of development
 - Business stakeholders accessible
 - Whole team responsible for the quality
 - Simple design is easier to test

**Challenges**
 - Less well-documented requirements
 - Testers feel less needed as dev does more component testing
 - More of a coaching role, can be difficult
 - Constant time pressure and less time to think on testing new features
 - Regression becomes extremely important and automation more beneficial

Regression - something broken in the system that now needs to be tested.

### Testing in a lifecycle model
Whichever development model is used, the below is always the case:
 - For each development activity, there is a corresponding testing activity
 - Each test level has test objectives specific to that level
 - Test analysis and design of tests for a given test level should begin during the corresponding development activity
 - Testers should be involved in reviewing documents as soon as drafts are available in the development lifecycle

### Testing as a Driver for Software Development
Approaches to produce quality products - introduce testing as early as possible:
 - Writing tests in advance, before the code
 - Focusing on early defect prevention, detection, and removal
 - Following a shift-left approach
 - Ensuring the right test types are run at the right time as part of the right test level
 - Use automated tests to ensure code quality in future adaptations or code refactoring

Agile testers play a key role in guiding the use of these testing practices.

### Test-Driven Development
 - Became popular through XP
 - Develop code guided by automated test cases
 - Mainly on unit-level and code-focused
 - CAN also be used on integration/system level
 - Used in Agile and sometimes in sequential
 - Helps developers focus on clearly expected results
 - Tests are automated

### Acceptance Test-Driven Development
 - Acceptance criteria and tests are defined during the creation of the user stories
 - Encourages collaboration amongst the business, developer, and tester
 - Every stakeholder should understand how the software component has to behave and what is needed to ensure this behavior
 - ATDD creates reusable tests for regression testing
 - Tools support creation and execution of tests (often in the CI process)
 - Helps determine the acceptance criteria are met for the feature

### Behavior-Driven Development
BDD helps developers collaborate with other stakeholders to define accurate tests focused on business needs

Allows a developer to focus on testing the code based on the desired behavior

As tests are based on the desired behavior, the tests are easier to understand

Specific frameworks to define acceptance criteria based on the "given/when/then" format:
 - **Given** some initial context
 - **When** an event occurs
 - **Then** ensure some outcomes

Test cases are automatically translated into executable tests

Example tool for Behavior-Driven Development: Cucumber
 - Translates test cases into executable tests

### TDD vs. BDD vs. ATDD
![](../Images/Pasted%20image%2020240731114558.png)

==**Important to know:**==
Explain the difference between behavior driven, test driven, and acceptance testing.

**Caroline Advice**
For the exam Monday, specifically for SDLC, with Agile, know the difference between product backlog, sprint backlog, (there was one I missed)

3 different sequential - waterfall, V, W.

Exam will be more in-tune with the testing side of things - SDLC questions will be more about the testing side. 

The practice exam that ISTQB offers will give us an idea for what to expect for both the Monday exam and the certification exam

**We'll be reimbursed for the cost of the exam - Date scheduled for Friday, August 9th**