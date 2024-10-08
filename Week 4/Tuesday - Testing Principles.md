# Fundamentals of Testing
Before hopping into that, let's talk about software testing.

## Software Testing
 - The process in SDLC (software development lifecycle) that evaluates the quality of a component, system, or related work products.
	 - Meets the business and technical requirements
	 - Works as expected
	 - Can be implemented with the same characteristics
		 - There should be no difference between implementations across systems, needs to have a simple base

### Misconceptions of software testing
 - Testing only focuses on executing tests - **FALSE**
	 - Testing includes many other activities
		 - Reviews
		 - Designing tests
		 - Reporting
		 - Etc.
	 - Testing must be aligned with the software development lifecycle (e.g. waterfall vs agile)
 - Testing will only focus on testing the software object - **FALSE**
	 - It's important to remember we're also focusing on validation of the software for stakeholders
 - Testing can be fully automated - **FALSE**
	 - While we can automate a lot, it's also an intellectual process that the tester needs specialized knowledge about
		 - Needs to know about the business domain
 - Testing proves that software has no faults - **FALSE**
	 - It's impossible to prove that software will never have faults when you're looking for issues

A system is the product of the interaction of it's parts.
When we break down the different components of a bicycle, we have chains, wheels, a frame, etc. 
None of these make it a bike.
When all of these components interact, and are properly combined, then we have a working system.

## Test Objectives
 - Evaluating whether the software works as intended
 - Triggering failures and finding defects
 - Ensuring required coverage of a test objective
 - Reduce the risk of the software not being of high enough quality
	 - It's impossible to get the risk of errors to zero - but we can get *closer* with testing
 - Verify conformance to requirements
 - Verify compliance contractual, legal, or regulatory requirements
 - Provide enough information to stakeholders
	 - Should include progress and quality - *need to be confident about these* before sharing with stakeholders.
 - Build confidence in the quality of the test object
 - Validate whether the test object is complete and works as expected
	 - Important - stakeholders need to be assured that the software will do what it was designed to do.

Let's say we're on Target
We're logging in to our account, testing the Target login
We're searching for a way to break it, to find a failure of the system
The people who take care of these systems are the developers
Finding defects can be as small as a spelling mistake in a requirement document
This is a part of static testing - outside of the scope of the software
It also includes functionality of the website that is broken
That's part of dynamic testing - implemented within the code that needs to be fixed

## Testing and Debugging
 Testing can:
  - Trigger failures that are causes by defects, typically in-code or during execution, like a typo causing an error during execution (dynamic testing)
  - Find defects in the test objective, like a typo found in documentation (static testing)

Debugging is an activity that finds, analyzes, and eliminates the cause of the failure (the defect) found in dynamic testing.
Debugging a defect found in the static testing, debugging is simply removing the defect, no reproduction or diagnosis is needed.

![](../Images/Pasted%20image%2020240730094951.png)

A tester finds a failure, and reports it to the developer. The developer reproduces the failure, finds out why, fixes the issue, checks it on their end, and sends the fixed system back to the tester for re-validation.

SDET - Focuses on writing automated tests, goes more in-depth.
QA - Focuses more on the product and finding edge cases, manual testing.

## Why is testing necessary?
While ensuring stakeholders are receiving the product they expect is important, testing is also important, simply because it contributes to the success of the project.
 - It's also a cheap way of detecting defects, cheap in the sense that it doesn't compromise reputation in order to find out issues.

**Indirectly, testers represent the users.** When requirements are written and reviewed in static testing, testers make sure that the actual end user's needs are being fulfilled during development.

### Testing Reduces Risks
Reduces the risk of failure in operation by:
 - Being involved in reviews and refinements - preventing defects
 - Working together with designers - preventing design defects and early testing identification
 - Working with developers - increase understanding of code - reduce code and test defects
 - Verifying and validating the before you go live - gives time to detect and fix failures to meet stakeholder requirements

### Assessing Software Quality
If you have few faults, but very poor test quality, chances are you're missing a lot of faults in your testing.

If you have many faults, you can either have low or high test quality - If the test quality is low, then you're absolutely going to experience many more faults. If the test quality is high, over time, these faults can be addressed.

![](../Images/Pasted%20image%2020240730102513.png)

### How much testing is enough?
![](../Images/Pasted%20image%2020240730103419.png)

It depends on the *risks* for your system, and whether you are *confident* the system works as intended.

### Risk-based Testing
Test time will always be limited.

Use RISK to determine
 - What to test first
 - What to test most
 - How thoroughly to test each item, e.g. where to place emphasis
 - What not to test (this time)

### Testing and QA
![](../Images/Pasted%20image%2020240730104957.png)

Note that QC focuses on reaching a certain level of quality.
Testing is less on the organization-side of things, and is more happening at the product level.
 - Won't necessarily have a say in how the product is being made - but will be required to ensure that the product works.

# Errors, defects, failures, and root causes.
Error - a human action that produces an incorrect result.
Defect - a manifestation of an error in a software product.
 - Also known as a bug or a fault.
 - If executed, a defect may come to a failure.
Failure - deviation of the software from its expected delivery or service.

### Why do defects occur?
People make mistakes.
 - Time crunch
 - Complexity of work/infrastructure
 - Miscommunication
 - Inexperienced staff

Environmental conditions.
 - Radiation, pollution, etc.
 - Things that affect the hardware that code is running on

Bad assumptions, blind spots.
 - Reviewing your own code may make it hard to find bugs that you unknowingly introduced

### Where do defects occur?
**Documentation**
 - If defects are found in the requirement specifications, it's pretty cheap to edit the document to work around it.
 - If defects are found in test scripts, that makes it a little trickier.
**Source code**
**Supporting artifacts**

Again, it's cheaper to find bugs before they're put into production - and reputation is saved.

### Reliability vs Faults
Reliability - the probability that software will not cause failure of the system for a specified time under certain specified conditions.
 - Can software be fault-free? **No.**
 - Can software systems be reliable with faults? **Yes.**
 - Is a "fault-free" application always reliable? **No.**

Not every unexpected test result is a failure - the test itself can result in:
 - False negatives
 - False positives

### Root causes of defects and their effects
Root Cause
- A fundamental reason for the occurrence of a problem
- Earliest action/condition that created a defect
- Should be identified to avoid similar defects
- Root cause analysis can lead to process improvements to prevent defects

Identifying the root cause
 - "5 why's"

### 5 Why's
So it sounds like the code doing the bonus math was just bungled? Checking that out/testing it with test data and finding the output vs expected first sounds reasonable?

**Start with why the customer is complaining.**
 - Customer is complaining because the bonus calculation was wrong.

**Why is the calculation wrong?**
 - Code was incorrect.

**Why is the code incorrect?**
 - User story wasn't clear.

**Why was the user story not clear?**
 - PO misunderstood the requirements.

**Why did the product owner misunderstand the requirements?**
 - PO wasn't knowledgeable enough on how bonus calculations were done - ***ROOT CAUSE***

A **solution** could be to send the PO on training when it comes to bonus calculations. Further mistakes in this area could be avoided.

### Seven Testing Principles
1. **Testing shows the presence of defects - *not* their absence.**
 - Testing reduces the probability of undiscovered defects remaining in the software, but even finding no defects is not proof that they don't exist.
2. **Exhaustive testing is impossible.**
 - Testing everything (all combinations of inputs and preconditions) is not feasible. Instead, risk analysis and priorities should be used to focus on testing efforts.
3. **Early testing saves time and money**
 - To find defects early, testing activities should be started as early as possible in the software/system development lifecycle, and should focus on defined objectives.
4. **Defect cluster together**
 - Testing effort shall be focused proportionally to the expected and later observed defect density of modules.
5. **Pesticide Paradox - Tests wear out**
 - If the same tests are repeated over and over again, they will no longer find any new defects. To overcome this, test cases need to be reviewed and revised to exercise different parts of the software.
6. **Testing is context-dependent**
 - Testing is done differently in different contexts.
	 - Example: Safety-critical software is tested differently from an e-commerce site and Agile testing differs from sequential testing.
7. **Absence of errors fallacy**
 - Finding and fixing defects does not help if the system built is unusable and does not fulfill the users needs and expectations. Verification and validation should both be done.

### Test Process
 - Set of common test activities
 - Test strategy should state the proper test process followed
 - Not having common test activities - less likely to reach the test objectives
 - Decision of test activities are made in test planning
 - Test activities do not stand alone
 The essential goal is not to find bugs, but to fulfill the stakeholder's business needs - stakeholders *are* the ones paying. Customer is king.

### Test Process in Context
 - Test Strategy
 - Test Techniques used
 - Degree of test automation
 - Required level of coverage
 - Level of detail of test documentation
 - Reporting
	 - Does management want weekly progress reports, or just one at the end?

## Testware
 - Created as part of the test activities in the test process
 - Each test activity creates test work products
 - Type of work products vary as the test process varies
 - Much testware can be captured and managed using:
	 - Test management tools
	 - Defect management tools

Proper configuration management should be in place to ensure consistent testware.

### Fundamental Testware
**Organization Level**
 - Test Policy
 - Test Strategy
**On Project, Test Level**
 - Test Plan

### Test Planning - Testware
 **Test Plan(s)**
 Includes information on:
  - Test Basis
  - Traceability Information
  - Exit Criteria
	  - Used in test to monitor and control your test

==**-> REMEMBER WHAT THE TEST PLAN INCLUDES**==

### Test Monitoring and Control
![](../Images/Pasted%20image%2020240730114924.png)
(Next slides are covering these concepts in-order)
### Test Activities and Tasks
Test Monitoring
 - Ongoing checking of all test activities
 - Ongoing comparison of actual progress against the test plan using metrics
Test Control
 - Taking actions needed to mee the objectives of the testing
 - Updating the Test Plan according to feedback
Supported by the evaluation of Exit Criteria (definition of done)
 - Checking of test results and logs against coverage criteria
 - Assessing component or system quality based on the test results and logs
 - Determining if more tests are needed

### Testware
Various types of Test Reports:
 - Test progress reports
 - Test summary reports
 - Documentation of control directives
 - Risk information
These reports ... (missed it oops)

### Test Progress Report
 - Reporting period
 - Progress against the test plan
 - Factors blocking progress
 - Test measures
 - New and changed risks
 - Planned testing
You'll have a test progress report during a ... test phase? (Check this)

### Test Activities and Tasks
Answers "what to test" using measurable coverage criteria:

1. Analyzing the test basis to:
 - Identify testable features
 - Test bases including requirement specifications, design, and implementation information, risk analysis report, etc.
 2. Evaluating the Test Basis:
 - Ambiguities
 - Omissions
 - Inconsistencies
 3. Defining and prioritizing test conditions, their risks, and risk level per-feature based on:
 - Analysis of the test basis
 - Consideration of functional, non-functional and structural characteristics
 - Business and technical factors
 - Levels of risk

Black box, white box, and experience based testing techniques can be useful in test analysis to define more precise and accurate test conditions.

The fourth phase in the testing plan:
## Test Design
"How to test the test conditions."
 - Used to create higher-level test conditions in testware.

### Test Activities and Tasks
 - The test conditions are used to create high-level test cases and other testware, often involving test design techniques.
 - Answers "how to test"
 - Includes the following major activities:
	 - Identify coverage items
	 - Designing test cases and sets of test cases
	 - Defining the test data requirements to support test cases
	 - Designing the test environment
	 - Identifying required infrastructure and tools
 - Identification of defects during test design is a potential benefit
	 - At this stage (test design), it's cheap to find and fix defects.

### Good Test Case
Effective
- Finds faults
Exemplary
 - Represents others
Evolvable
 - Easy to maintain
Economic
 - Cheap to use

### Abstract (logical) vs Concrete Test Cases

Example 2
 - Application for calculating end-of-year bonuses
 - Bonuses depend on the time employees work for the company

![](../Images/Pasted%20image%2020240730141531.png)

### Testware (pt. 3)
There are just more than just tests from the test design phase that we need to focus on.
Consider:
 - Test characters, used for exploratory testing
 - Coverage items (satisfies the coverage criteria for the test analysis phase)
 - Test environment requirements
 - Test data requirements

Good practice to first design abstract test cases, and then create concrete test cases.

### Test Activities and Tasks
Includes the following major activities:
 - Organizing test cases into prioritized test procedures
 - Creating test suites needed for execution
 - Arranging the test procedures within a test execution schedule for efficient execution
 - Creating manual and automates test scripts
 - Building and verifying the test environment
 - Preparing test data and ensuring it is properly loaded into the test environment
 - Verifying and updating bi-directional traceability between the test bases, test conditions, test cases, test procedures, and test steps

Test procedure is a set of test scripts.
Arranging the test procedures for efficient execution: 
 - Let's say test case 2 is dependent on test case 1, test case 3 is dependent on test case 4
	 - Need to make sure you don't have blockers when scheduling test cases

![](../Images/Pasted%20image%2020240730142609.png)
Stubs are developed to replace a called component that's not there yet.
Drivers are the opposite of a stub - a substitute of a calling component, used in isolation.
Simulators are a component that behave like a certain component or system under certain conditions.
Service virtualizations enable virtual delivery of services that are going to be deployed, managed remotely.

### Test activities and Tasks
Tests are run in accordance with the test execution schedule.
Includes the following activities:
 - Executing tests in the planned sequence (manual or automated)
 - Comparing actual with expected results and log anomalies as incidents
 - Analyzing anomalies to find out their likely causes (defects, false positives, false negatives.)
 - Logging test results (pass, fail, blocked, etc.)
 - Repeating test activities when the incidents are solved (confirmation test, run corrected test, regression test)

More:
![](../Images/Pasted%20image%2020240730143727.png)

## Testware (ctd. further)
Work products report:
 - Test Completion Report
 - Action items for improvement
 - Documented lessons learned
	 - If you don't document, there's a chance you'll have to re-learn!
 - Change requests or product backlog items

# Testing Roles
 - **Test Management**
 - **Testing**

There will be situations where one role will be needed more than the other.
There is a division of activities between the two.

Activates and tasks per role depend on many factors:
 - The project
 - Product context
 - Skills of the people who are in the test management and testing roles
 - The organization

## Test Management Role
Responsible for:
 - Test Process
 - Test team
 - Leadership of test activities

Main focus:
 - Test planning
 - Test monitoring and control
 - Test completion

![](../Images/Pasted%20image%2020240730144325.png)
^ These orange steps are relevant for this role.

### Test Planning
 - Develop or review a test policy and test strategy for the organization
 - Plan the test activities
 - Write and update the test plans
 - Coordinate the test plans with stakeholders
 - Share testing perspective with other project activities such as integration planning
 - Initiate the analysis, design, implementation, and execution phases
 - Introduces suitable metrics for measuring test progress

### Test Monitoring and Control
 - Monitors test progress and results, checks the status of the exit criteria
 - Adapts test plan and planning based on test results, progress, and feedback
	 - If something isn't going to plan, we adjust based on the results/progress given

### Test Completion
 - Checks the status of the exit criteria - "is testing done?"
 - Prepare sand delivers the completion report
 - Initiates the archiving or handing over the testware to the appropriate team(s)
	 - Writes down the lessons learned

### Test Management Role - Additions
 - Supports the selection and implementation of tools to support the test process
	 - Budget
	 - Time
	 - Effort
 - Decides the implementation of test environments
 - Promotes and advocates the testers, test team, and the test profession within the org.
 - Develops the skills and careers of testing (training, evaluations, coaching, etc.)
 - The way in which the role is carried depends on the SDLC (software development lifecycle)

## Test Role - Activities
 - Reviews and contributes to test plans
 - Analyzes, reviews, and assesses requirements, user stories, and acceptance criteria
 - Identifies and documents test conditions and captures traceability between test cases, test conditions, and the test basis
 - Designs, sets up, and verifies test environments
 - Designs and implements test cases, test procedures and test data
 - Creates detailed test execution schedule
 - Executes tests, evaluates the results, and documents deviations
 - Automates tests as needed

### Test Role - Additional Activities
 - Evaluates non-functional characteristics such as performance, efficiency, reliability, usability, security, compatibility, portability
 - Reviews tests developed by others
 - Specialist roles can be related to test analysis, test design, specific test types or test automation
 - Different roles may take over the role of tester based on the risks related to the project and product and the SDLC used:
	 - Component - Integration Level - Developers
	 - Acceptance Level - Business experts and users
	 - System - Integration level - Independent test team
	 - Operational acceptance level - operators

### Role Division
Test Management Role
 - Team Leader
 - Test Manager
 - Development Manager
 - One person who has the test management and the testing role
Testing Role
 - Tester
 - DevOps
 - Customer support
 - Developer

