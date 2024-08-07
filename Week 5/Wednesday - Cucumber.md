# Cucumber
**Test automation tool**
 - Tests are written in the **Gherkin** language

1. **Feature File**
	1. Contains Gherkin code
2. **Step Definition File**
	1. Carries out the action that should be performed

## Behavior Driven Development
*Similar to Test Driven Development*, but focuses on the **behavior** of the feature.
 - Uses the Given/When/Then language for describing a scenario

![](../Images/Pasted%20image%2020240807092858.png)

**When we're using Selenium and Cucumber...**
 - Selenium lets us interact with websites.
	 - We went through some tests where we navigated through different pages
	 - Gave it some test data, end-to-end testing was possible
 - Cucumber is a way to split it up
	 - While Selenium gives us the ability to interact with the webpage, 
	 - Cucumber lets us create tests using Gherkin,
	 - which Selenium can use to know what tests to run

**Benefits**
 - Simple Setup
 - Code is reusable
 - Can work alongside many different frameworks,
 - and like Selenium, supports many different languages

---
# Using Cucumber

**Setting Up**
1. We're making a new folder called `cucumber`, right click the folder, hover over `Maven`, and select `New Project`. 
2. For the project archetype (may need to select "show more options"), use newest (7.11.1):
![](../Images/Pasted%20image%2020240807094516.png)
3. Save it to the folder, add your `com` and whatnot.
4. Within `pom.xml`, we can see there's a few dependencies for Cucumber.
	1. Make sure you have the `junit` dependency. If not, add it.
![](../Images/Pasted%20image%2020240807094805.png)

**Building an example project**
1. Note how we have `RunCucumberTest.java` and `StepDefinitions.java` in the main folder, and under `resources` we have the `example.feature` file.
	1. Note that in `RunCucumberTest.java`, the main annotation is `@Suite`. It allows us to run different tests together at the same time.
	2. `@Suite` - `Junit` test suite allows you to group and execute multiple tests
	3. `@IncludeEngines("cucumber")` - Specifies the test suite should use Cucumber's engine to run the tests
	4. `@SelectClasspathResource("com/skillstorm")` - Tells test suite to look for your feature file
	5. `@ConfigurationParameter(key = PLUGIN_PROPERTY_NAME, value = "pretty")` - Missed the first part, but also makes output human-readable

2. In `StepDefinitions.java`, we have an example, but we're going to delete most of these.

3. In `example.feature`, we're going to try and make an example where we're seeing if today is Friday. *Note: There's a lot of good examples on the Cucumber website*
	1. Rename `example.feature` to `is-it-friday-yet.feature`
	2. Add the "feature" at the top: `Feature: Is it Friday yet?`
	3. On the next line: `Everybody wants to know when it's Friday`
	4. For the Scenario, add the following: `Scenario: Sunday isn't Friday`
	5. `Given today is Sunday`
	6. `When I ask whether it's Friday yet`
	7. `Then I should be told "Nope"`
```
Feature: Is it Friday yet?
	Everybody wants to know when it's Friday

	Scenario: Sunday isn't Friday
		Given today is Sunday
		When I ask whether it's Friday yet
		Then I should be told "Nope"
```
-  Again, note that this Gherkin code is just describing the behavior without actually implementing it.
	- When we *do* implement it, we can use `Given`, `When`, and `Then`

4. Back to `StepDefinition.java`
	1. We're using Given/When/Then as annotations that match our feature -
	2. When we execute the below, it'll give us an error, since we haven't implemented anything.
```
public class StepDefinitions {

	@Given("today is Sunday")
	public void todayIsSunday() {
		throw new io.cucumber.java.PendingExecution(); // Placeholder for now
	}
	
	@When("I ask whether it's Friday yet")
	public void iAskWhetherItsFridayYet() {
		throw new io.cucumber.java.PendingExecution(); // Placeholder for now
	}
	
	@Then("I should be told {string}")
	public void iShouldBeTold(String string) {
		throw new io.cucumber.java.PendingExecution(); // Placeholder for now
	}
}
```
5. Make a new class for `ItsFriday`!
```
class IsItFriday {
	static String isItFriday(String today) {
		return "Nope";
	}
}
```

6. Revising our `StepDefinitions`...
	1. We're using behavior-driven-development testing
		1. We're focusing on the behavior of the feature
		2. We're using given/when/then to write step definitions to write **concrete actions**
	2. `@Given` - Maps to the step in the feature file that describes the **precondition**
	3. `@When` - Maps to the step in the feature file that describes the **action or event**
	4. `@Then` - Maps to the step in the feature file that describes the **expected outcome**
		1. Will take in a parameter of type String to compare whether the `expectedAnswer` and `actualAnswer` match
```
public class StepDefinitions {

	private String today;
	private String actualAnswer;

	@Given("today is Sunday")
	public void todayIsSunday() {
		today = "Sunday";
	}
	
	@When("I ask whether it's Friday yet")
	public void iAskWhetherItsFridayYet() {
		actualAnswer = IsItFriday.isItFriday(today);
	}
	
	@Then("I should be told {string}")
	public void iShouldBeTold(String expectedAnswer) {
		assertsEquals(expectedAnswer, actualAnswer);
	}
}
```

7. Note that when executed, this is fine and passes the test.
	1. Since we're saying today is Sunday, but `isItFriday` returns `Nope`, which is a response that we have defined in our `.feature` file, the `assertsEquals` evaluates as true and the test passes
![](../Images/Pasted%20image%2020240807103230.png)

8. Note that we can extend our `is-it-friday-yet.feature` file with additional scenarios:
	1. [Don't try and use variables in one of these, though - nightmare](https://stackoverflow.com/questions/33884027/using-variables-in-cucumber-feature-files) 
![](../Images/Pasted%20image%2020240807103952.png)
9. Adding a bit more to our `StepDefinition.java` file, we'll add another `@Given` for if it *is* Friday. 
	1. Note we **also** need to update `IsItFriday` to reflect whether `today` *is* Friday
```
class IsItFriday {
	static String isItFriday(String today) {
		return "Friday".equals(today) ? "YES" : "Nope";
		// Note that it's going to have to be "YES", all upper-case, since we were silly and made the scenario so that it was all upper-case
	}
}
```

```
public class StepDefinitions {

	private String today;
	private String actualAnswer;

	@Given("today is Sunday")
	public void todayIsSunday() {
		today = "Sunday";
	}

	@Given("today is Friday")
	public void todayIsSunday() {
		today = "Friday";
	}
	
	@When("I ask whether it's Friday yet")
	public void iAskWhetherItsFridayYet() {
		actualAnswer = IsItFriday.isItFriday(today);
	}
	
	@Then("I should be told {string}")
	public void iShouldBeTold(String expectedAnswer) {
		assertsEquals(expectedAnswer, actualAnswer);
	}
}
```

![](../Images/Pasted%20image%2020240807104809.png)

10. We can also add Scenario Outlines to our `.feature`!
	1. This is usually **preferred to writing individual scenarios**.
	2. Needs to be in this format below - the spacing between `|` doesn't matter.
	3. Note that it does need to be listed under `Examples:` and it does have to be called `Scenario Outline:`
	4. Off-topic note: Commenting is done using the `#` character
```
	Scenario Outline: Today is or is not Friday
		Given today is "<day>"
		When I ask whether it's Friday yet
		Then I should be told "<answer>" 

	Examples:
		| day    | answer  |
		| Friday | YES     |
		| Sunday | Nope    |
```

11. We can also add annotations to our `.feature` files to specify what tests we want to run - [see this Stack Overflow article](https://stackoverflow.com/questions/43493401/how-to-run-multiple-feature-files-using-the-cucumber-runner-class).
	1. For this example, we've commented our our earlier `Given` annotations.

13. We can now create new `Given` conditions:
	1. It'll run through all of the different examples given in the `.feature` file
```
@Given("today is {string}")
	public void todayIsSunday(String today) {
		this.today = today;
	}
```
