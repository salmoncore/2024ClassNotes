(Missed some notes prepping for Project 1 in the morning, my bad)

### Tester's Contribution to Iteration and Release Planning
Planning isn't a one-time event, it's ongoing.
In iterative lifecycles, two types of planning occur:
 - Release planning
 - Iteration planning

### Release Planning Process
 - Business representatives, together with the team, establish and prioritize the user stories for the release
 - Project and quality risks are identified and high-level effort estimation is performed
 - Testers are involved in release planning and particularly add value in a few key ways

### Iteration planning
 - Takes place before each iteration
 - Looks ahead to the end of a single iteration
 - Is concerned with the iteration backlog

### Iteration Planning Process
 - Team selects user stories from the prioritized release backlog
 - Team elaborates the user stories
 - Risk analysis for the user's stories is performed
 - Work needed for each story is estimated
 - All needs to be clear to the entire team or the team can refuse to accept it and take another item based on priority
 - Business representatives should answer any questions of the team about user stories to clarify
	 - What needs to be done
	 - How it should be implemented

### Iteration Planning Process
 - Number of stories selected is based on the story size and the velocity of the team
 - After the iteration content is final, the stories are broken up into tasks
 - Testers are involved in iteration planning an particularly add value in:
	 - Participating in the detailed risk analysis of user stories
	 - Determining the testability of the user stories
	 - Creating acceptance tests for the user stories
	 - Breaking down user stories into tasks
	 - etc she went really fast

### Typical Exit Criteria
When to safely stop testing, when to declare a certain test activity done? Should be a balance of quality, budget, schedule, and feature considerations.
 - Measures of thoroughness 
 - Completion criteria

Even without the exit criteria satisfied, test activities can also stop due to:
 - Testing budget being expended
 - Scheduled time being complete
 - Pressure to bring the product to market

### Definition of Done - Unit Testing
 - 100% decision coverage where possible
 - Static analysis performed on all code
 - No unresolved major defects (ranked based on priority and severity)
 - No known unacceptable technical debt remaining in the design and the code
 - All code, unit tests, and unit test results reviewed
 - All unit tests automated
 - Important characteristics are within the agreed limits. (e.g., performance)

### Definition of Done - System Testing
 - End-to-end tests of user stories, features, and functions
 - All user personas covered
 - The most important quality characteristics of the system covered (e.g., performance, robustness, reliability)
 - Testing done in a production-like environment(s)
 - All quality risks covered according to the agreed extent of testing
 - All regression tests automated, where possible
 - Etc.

### Definition of Done - User Story
 - The user stories selected for the iteration are complete, understood by the team, and have detailed, testable acceptance criteria
 - All the elements of the user story are specified and reviewed, including the user story acceptance test that has been completed
 - Tasks necessary to implement and test the selected (something she switched slides)

### Definition of Done - Feature
 - All user stories with acceptance criteria are defined and approved by the customer
 - The design is complete, with no known technical debt
 - The code is complete, with no known technical debt or unfinished refactoring
 - Unit tests have been performed and have achieved the defined level of coverage
 - Etc.

### Definition of Done - Iteration
 - All features for the iteration are ready and individually tested, according to the feature level criteria
 - Any non-critical defects that cannot be fixed within the constraints of the iteration added to the project backlog and prioritized 
 - Integration of all features for the iteration completed and tested
 - Documentation written, reviewed, and approved
Now the software is *potentially* releasable.
 - Not all iterations result in a potential release. It's a *potential*.

### Test Estimation Categories
Expert-based approach - estimating based on the experience of the owners of the testing tasks or by the experts and experienced staff members. Examples here are:
 - Wideband Delphi estimation
 - Planning poker in Agile
Metrics-based approach - estimating based on metrics of former or similar projects or based on typical values:
 - Dev-QA ratio
 - Project size and complexity
 - Defect removal models
 - Burndown charts and velocity

![](../Images/Pasted%20image%2020240802100848.png)
==Apparently the three-point estimation (or all of these?) is/are important to know?==

### Estimating Team Effort - Planning Poker
 - Takes place in release planning
 - Feature is discussed by the team (developers, testers, business)
 - Business answers questions from the team
 - For estimation it is great if there is the availability of:
	 - Risk Level
	 - Priority
 - In planning poker, 
	 - Business representatives present a user story
	 - After all questions and discussions, t he estimation can begin
	 - Each estimator (team member) privately selects a card to represent the estimate
	 - Everyone reveals their card at the same time
	 - (something)

### Three-Point Estimation - Example
![](../Images/Pasted%20image%2020240802102804.png)
==There may be a question on the exam where they expect you to calculate the three point estimation, and they will likely not give it to us.==

