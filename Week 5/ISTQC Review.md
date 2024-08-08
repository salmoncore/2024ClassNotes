**Entry vs Exit Criteria**
 - Entry - Definition of "ready"
 - Exit - Definition of "done"

**Whole-team approach**
 - Involves business-side synergy

**Exploratory testing**
 - If you have domain knowledge and a lack of time, this may be helpful

**Decision-based testing**
 - Test cases are derived from a decision table? REVIEW

**Equivalence Partitioning**
 - Partitioning input ranges to explore edge cases
 - Black-box technique

**What black-box technique will get you different outcomes based on previous state**
 - State transition testing

**Role of a Tester**
 - Test analysis and design

**Branch testing vs branch coverage**
 - Branch testing - Checking each fork at a decision point to evaluate it's outcome
 - Branch coverage - The % of tested branches / total # of branches
	 - 100% statement coverage **does not** mean it covers all branches, 100% branch coverage **does** cover all statements

**Checklist based testing**
 - How do you create checklist items?
	 - They are usually phrased as a question, they're based on requirements

**What is a way that you can control and minimize the cost of testing and development?**
 - Starting early
	 - You want to be able to detect defects as early as possible
		 - Static testing, reviews, that kinda thing
	 - Shift-left approach!

**What is one way that can be used to develop user stories when collaborating with developers and business stakeholders.**
 - Brainstorming

**When you add a new feature, what needs to come up?**
 - Maintenance testing
	 - Confirmation/maintenance testing works here

**Confirmation vs Regression**
 - Regression - Detects whether defects have been introduced in unchanged parts of software
	 - Checking to make sure that a solution that you have is not causing problems elsewhere
 - Confirmation - Detects whether a fixed piece of software does not again have a fault
 - Maintenance - Detects whether the system changing or the environment a system runs in changing has caused issues
	 - In the below problem, the answer is maintenance testing. 
	 - The system has likely changed since the migration feature was implemented?
![](../Images/Pasted%20image%2020240808133112.png)

**What is static testing?**
 - You aren't executing the code

**Is static testing something you would do during your test plan?**
 - A test plan contains 
	 - Info about budget, schedule, resources, **test objectives**
	 - *Anything before any code is done.*
 - Static testing is any testing before code is being executed

**What is the opposite of static testing?**
- Dynamic testing
	- We have the code, we're executing it, we're finding bugs and having faults

**What type of exploratory testing technique is this:**
 - You are to create a list of possible defects and errors, and you design tests to address each one.
 - Error guessing - you are *aware* of the potential defects and errors

**Fault Attack**
 - The approach to the implementation of error guessing

**How is branch coverage determined?**
 - (The % of branches executed / total # of branches) * 100%

**What are two risk response actions that will help with the control of product risk?**
1. Risk Delegation
	1. Giving it to someone else - transferring the risk
2. Risk Acceptance
	1. Literally just accepting it
3. Risk Mitigation
	1. Testing
4. Contingency Plan

**BDD Format**
 - Given/When/Then

**Q: Which is a valid test objective?**
 - Code Review
 - Debugging
 - Finding failure/defects in the test object
**A: Finding failures/defects**

**Q: What is an example of a test work product?**
 - Codebase
 - Test platform selection
 - Test tool selection
 - Test plan
**A: Test Plan**