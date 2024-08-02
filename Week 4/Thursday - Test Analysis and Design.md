This chapter will be very comprehensive!
**There will be questions about these techniques on the exam.**

### Test Techniques
Test techniques are used in test analysis ("what to test") and test design ("how to test").
Test techniques help the tester in defining test conditions, identifying coverage items in test data.

### Choosing Test Techniques
You want to be able to choose the most effective test technique for what you would be testing.
Some are more applicable to certain test levels than others, and some are applicable in almost all scenarios.
In general, a combination of white box/black box and experience testing usually receives the best results.

![](../Images/Pasted%20image%2020240801092155.png)

### Black-Box Test Techniques
Test conditions, test case and test data are derived from a test basis that may include: 
 - Software requirements
 - Specifications
 - User cases
 - User stories

Think of black box testing as a closed box - the system itself is closed off. We care about the input and expected output, not whatever goes on inside the box.

### Equivalence Partitioning
A black-box technique. May save a lot of time and have relatively high test coverage.
It can be applied to all testing levels - from system to system integration, unit testing to components, etc.

**Idea is to divide (partition) data into groups or sets for which the behavior is assumed to be the same (test object should handle each value in a partition equivalently).**
 - Equivalent partitions are known as equivalence classes
 - Test cases are designed to execute representatives from ALL equivalence partitions
	 - Valid values are values that should be accepted by the component or system and are in a valid equivalence parititon
	 - Invalid values are values that should NOT be accepted by the component or system and are in an invalid equivalence partition

Test cases are designed to cover each partition **ONCE AND ONLY ONCE**

If one condition in a partition works (or doesn't work), we assume they all work (or don't work) - no need to test more conditions.

Each partition can be divided into sub-partitions if needed
 - Partitions can be identified for any data element related to the test object

Coverage is calculated as:
`(number of equivalence partitions tested by at least one value / Total of nr identified equivalence paritions) * 100%`

### Points of Attention
For Equivalence Partitioning, partitions must NOT overlap and must NOT be empty
Partitions do NOT have to be ordered, they can be:
 - Continuous or discrete
 - Ordered or not ordered
 - Finite or infinite

In simple test objects, the test technique is not hard
Can be very powerful if done carefully.

### Valid or Invalid Partitions?
A partition containing VALID values is a VALID partition
A partition containing INVALID values is an INVALID partition

BUT

Companies and teams have different definitions of valid and invalid
 - Valid values could be:
	 - Values that should be processed by the test object
	 - Values for which the processing is defines in the specification
 - Invalid values could be:
	 - Values that should be ignored or rejected by the test object
	 - Values for which the processing is not defined in the specification

**Scenario**
For every child, parents get a certain amount of money from the government for the support of that child or children.
 - If no children, parents get nothing
 - For 1-2 children, $50/child
 - For 3-5 children, $75/child
 - For 6-8 children, $100/child

![](../Images/Pasted%20image%2020240801094057.png)

All partitions are invalid except for the case of 8 or greater. This doesn't have a specified value, or return a result. Since this last partition is invalid, the entire table is invalid.

### Multiple sets of Partitions
 - Multiple sets of partitions are common in test objects
 - A test case will then cover multiple partitions from different EP tables
 - How to measure coverage?
	 - Each Choice Coverage

### Each Choice Coverage Example

![](../Images/Pasted%20image%2020240801094638.png)

This *is* valid. 
We can split the tables into two:

![](../Images/Pasted%20image%2020240801094824.png)

Now, what is the minimum number of additional test cases that are needed to ensure full coverage of all valid INPUT equivalence partitions?

For T1 - 1.5 hours at very low, we can say we have completed, for the bottom two charts, valid for less than 3 hours, and valid for very low. Essentially, everything that gets touched on already is valid. Since we 

High and low intensity still need to be checked, and one for a time range between 3-6 hours. Since we can't accomplish high and low simultaneously, we need a minimum of two tests. 
 - If we just needed to accomplish 3-6 and high intensity, we could validate both of those in one test.

### Boundary Value Analysis
Another black-box test.

Can be applied to all test levels
Extension of EP, generally used to test requirements that call for a range of numbers.
 - Can ONLY be used when the partitions are ordered
We're exercising the boundaries of equivalence partitions
 - Behavior at the boundaries of the equivalence partitions are more likely to be incorrect than within the partitions

2 elements (values) belonging to the same partition
 - All values in-between must also belong to that partition
Boundary values are the MIN and MAX values of EP

Coverage is calculated as:
`(num of coverage items tested / total # of identified coverage items) * 100%`

### Identifying Boundary Values
1. Divide a set of test conditions into groups or sets for which the behavior is assumed to be the same
2. Draw up your EP table
3. Identify the min and max values for each partition
 - These are the boundary values
 - It's possible to only have 1 BV in a partition

![](../Images/Pasted%20image%2020240801100347.png)

Let's say the lower BV is 0.00, higher BV is 50.00

![](../Images/Pasted%20image%2020240801100939.png)

Savings Account in a bank
 - Earns different interest percentages depending on balance
Balance between 0 and 50 earns 2%
Balance more than 50 but less than 1000 earns 3%
Balance of 1000 or more earns 5%

### Decision Table Testing
Combinatorial test technique that can be applied at all test levels

Useful to test implementation of system requirements that specify how different combinations of conditions resulting in different outcomes

Effective way to record complex logic such as business rules

Helps identify all the important combinations of conditions
Technique is to:
 - Identify all inputs (conditions) and outputs (actions) and put them in a table as rows
 - List all True-False combinations for each of the conditions (mostly Boolean)
 - Identify the correct outcome for each combination - each column is a decision rule
 - Write tests to exercise each of the rules (columns) in the decision table at least once

![](../Images/Pasted%20image%2020240801103148.png)
If an action should occur, you can fill it in with an X.
### Decision Table Testing
Systematic way to identify all combinations of conditions
Find any gaps or contradictions in the requirements
Exercising ALL decision rules may be very time consuming if there are a lot of conditions
If a lot of combinations, or having multiple types of input that are not binary, use risk assessment or a minimized decision table to decide which rules to execute
Table can be collapsed by deleting business rules (columns) that are not possible

Normal notation is:
- Conditions: T if true, F if not true (false), - if the condition is irrelevant, N/A indicates an infeasible condition for a given rule column
 - Actions: X if action should occur (or a value, color, etc), blank if the action should not occur (or -)

### State Transition Testing
In a decision table, the action in each state can transition to a different state, so if you want to manage multiple states with different branches with different responses, this may be a way to do it

State Transition Testing - Used when an aspect of the system is in a "finite state machine"
 - Limited number of states
 - State is determined by the rules of the machine
 - Different response on an event depending on the current conditions and previous history

Test cases can be designed to execute valid and invalid state transitions

![](../Images/Pasted%20image%2020240801105117.png)

Behavior in a system is shown in a state transition diagram model, which shows:
 - Possible states and transitions
 - Events that cause or result in a transition from one state to another
 - Actions that result from a transition

If one event from the same state can result in 2 or more different transitions, the event may be qualified by a guard condition (precondition for an event), standard syntax is 'event (guard condition) / action'

Transitions are assumed to be instantaneous
Transitions may occur in a software crash? (Check this i missed it)

### State Transition Testing
State transition tables are often used to identify valid and invalid transitions

Tests can be designed to:
 - Cover a typical sequence of states
 - Excercise specific sequences of transitions
 - Exercise all states
 - Exercise all valid transitions
 - Exercise all transitions
 - Test invalid transitions

Rows represent states, columns represent events (with/without guard conditions)
Cell entries represent transition and contain the target state and possible actions

![](../Images/Pasted%20image%2020240801105533.png)

If a cell is empty, that's an invalid transition

### State Transition Testing Coverage
==We'll need to know the theory and how to apply it for the exam!==

If you want 100% of all states covered, all states need to be covered.
 - Calculation is `(the total number of exercises states / total number of valid/invalid transitions) * 100%`

![](../Images/Pasted%20image%2020240801110007.png)

![](../Images/Pasted%20image%2020240801110329.png)

Note that all transitions with a `-` are invalid, examples being:
 - Trying to add an item from the summary and cost state
 - Trying to remove an item from an empty shopping cart
 - Try to enter okay while in the shopping state or when having an empty basket

### White-Box Techniques
Differs from black-box, since we are aware of the internals during testing.

![](../Images/Pasted%20image%2020240801111315.png)
**Testing Techniques**
 - All of these will POSSIBLY be on the exam.

White-box is based on how the software is constructed and designed
 - Can be used at all test levels, mainly on the **component level**

Serves 2 purposes:
 - Test coverage measurement (from specification-based techniques)
 - Structural test case design (to increase test coverage)

100% coverage does NOT equal 100% tested

Drawback is that code coverage measurement ONLY covers what has BEEN written, the structure that's already there
 - Specified function not implemented - Specification-based techniques
 - Specification missing a function - Experience-based testing

Branch testing focuses on the percentage of branches that have been executed by a test suite.

![](../Images/Pasted%20image%2020240801111948.png)

In the psuedocode, we perform a few actions to read a, read b, and then we come across a condition.
 - If false, we're following the green branch to endif.
	 - We then read D, with another branch. If that is true, we assign C and end.
 - If true, we're following the red branch to endif
	 - We then follow the same path, but the red branch still follows along the false branch, hitting endif

Just to clarify - we're not testing every possible option, we just want to follow every branch path. 
 - Red could evaluate as true both times and green could evaluate as false both times, and that'd still be full coverage.

### Why White-Box Testing?
Provides an objective measurement of code coverage, information needed to create additional tests to increase the coverage and increasing the confidence in the code

The entire software implementation is considered, defects can be found even if the software specs are:
 - Vague
 - Outdated
 - Incomplete
However, missing requirements will not be found by white-box testing

Can also be used in static testing:
 - Dry runs of the code
 - Reviewing: Code that is not ready for execution, pseudo-code, high-level or top-down logic that can be modeled with a Control Flow Graph.

### Experience-Based Testing
The test conditions, the test cases and test data are derived from a test basis that may include the knowledge and expertise of:
 - Testers
 - Developers
 - Users
 - Other stakeholders

Knowledge generally includes:
- The expected use of the software
- It's environment
- Likely defects and the distribution of the software

**Techniques**
 - Based on knowledge, experience, imagination and intuition
 - Some defects are hard to find using more systematic approaches
 - Should in general be used as a compliment to more formal techniques
 - Effectiveness and coverage purely depends on the testers' approach and experience
 - Coverage can be difficult to assess and may not be measurable 

**Three Main Techniques:**
 - Error guessing
 - Exploratory testing
 - Checklist-based testing

### Error Guessing
A technique that anticipates the occurrence of mistakes, defects and failures, based on the knowledge of the tester:
 - How the application worked in the past
 - What types of mistakes the developers tend to make
 - The type of defects that result from these errors made by developers
 - Failures that have occurred in other applications
 - No rules, tester is encouraged to think of situations the software will not be able to cope with:
	 - Division by zero
	 - Empty files
	 - Etc.

**Fault Attacks**
Methodical and focused way of error guessing
List possible errors, defects and failures based on experience 
Lists can be based on:
 - Experience
 - Defects and faulure data
 - Knowledge on why software fails

Design tests that will:
 - Identify associated defects associated with the errors
 - Expose the defects or
 - Cause the failures

**The process of error guessing**
Imagine you are testing a web application's login functionality. The application allows users to log in with their username and password to access their account dashboard.

1. Identification of Potential Errors
	1. Begin by identifying potential errors or faults that could occur in the login functionality based on your experience and knowledge of common issues in authentication systems. Some potential errors might include:
		1. Invalid username/password combination
		2. Empty username or password fields
		3. Username or password containing special characters
		4. Long username or password exceeding character limits
		5. SQL injection attacks by entering special characters in the username or password fields
2. Based on the identified potential errors, design test cases to systematically test each scenario. For example:
	1. Test Case 1: Attempt to login with a valid username and an incorrect password.
	2. Test Case 2: Attempt to login with a valid username and a valid password.
	3. Test Case 3: Attempt to login with an empty username and a valid password.
	4. Test Case 4: Attempt to login with a valid username and an empty password.
	5. Test Case 5: Attempt to login with a username containing special characters.
	6. Test Case 6: Attempt to login with a password containing special characters.
	7. Test Case 7: Attempt to login with a long username (exceeding character limit).
	8. Test Case 8: Attempt to login with a long password (exceeding character limit).
	9. Test Case 9: Attempt to login with SQL injection attempt in the username or password fields.
3. Execute test cases
	1. Execute each test case against the login functionality, recording all the results and any deviations from the expected behavior
4. Analyze results
	1. Analyze the results of each test case to identify any errors or unexpected behavior encountered during the testing process. Pay attention to any discrepancies between the expected and actual outcomes
5. Report and document findings
	1. Document the findings, including any errors or faults identified during the testing process. Report the details of each issue, including steps to reproduce
6. Retest and verify fixes
	1. After developers address the reported issues, retest the affected areas to ensure the fixes have been successful, and that no new issues have been introduced.

---
# Project 1 Presentations from 11-12

---

### Exploratory Testing
Investigating and being creative in finding ways to test.
It's more informal.

(Missed some notes, thanks teams)

![](../Images/Pasted%20image%2020240801131033.png)

### When and how to use Exploratory Testing?
Most useful when there are:
 - Few or inadequate specifications
 - Severe time pressure
 - As complement to more formal techniques

Strongly associated with reactive testing strategies
Effectiveness grows with the knowledge, skills, and experience of the tester
Can include the use of black-box (something else i missed it)

**Example**
Shopping website - what do you expect?
 - Maybe you're able to select some items, check out, and pay for it?
Maybe you learn that:
 - The website has a feature for having an in-home-trial for a product

You're looking to make sure the website functions as expected.

### Test Automation in Exploratory Testing
Exploratory testing cannot be replaced by test automation.
You also can't automate:
 - Creativity
 - Human curiosity
 - Random inventions
Combining exploratory testing and test automations, though...
You CAN automate:
 - The creation of random test data
 - The execution of functional tests
 - Output logging and reporting

**Common Pitfalls**
- Lack of test coverage
- Limited time and resources
- Documentation and reporting
- Adapting to agile
- Subjectivity in testing
- Skill and knowledge gaps
- Defect reproducibility
- Managing test data
- Collaboration and communication 

### Checklist-Based Testing Example
A checklist to make sure none of the software modules are forgotten

A checklist to make sure that none of the non-functional quality characteristics are forgotten:
 - Performance & stress
 - Usability
 - Portability

A checklist to make sure all parts of a workflow have been tested:
 - Login, open record, close record, create record, save record, edit record, close record, delete record

With more experience the generic checklists can become more specific and clearer. They are guidelines rather than test cases.

### Benefits and Risks
**Benefits**
 - Structured approach to testing
 - Promotes consistency and repeatability 
 - Improve communication between team members
 - Helps new testers teste new products more confidently and efficiently
**Risks**
 - Checklist becomes gradually less effective - developers learn from their mistakes
 - Constant maintenance is needed
	 - To add newly found effects
	 - To update based on defect analysis
 - Checklists easily become too long
 - Interpretation is subjective

