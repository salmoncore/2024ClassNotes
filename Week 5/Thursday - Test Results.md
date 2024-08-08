
Exam tomorrow! Make sure to prep, run through [practice exams](https://stormsurge.skillstorm.com/courses/4068/pages/istqb-resources-2?module_item_id=39888), go through [flash cards](https://quizlet.com/931581916/week-4-review-flash-cards/), etc.!

---

Going back to the `Selenium` folder and the the `selenium_demo` project, we're adding a new file to `test\java\com\skillstorm\selenium_demo`, called `TestNG.java`.
 - **`TestNG`** is a testing framework used for automation testing 
	 - Widely used with Selenium
	 - Takes from both JUnit and NUnit
 - It overcomes some of the disadvantages of JUnit and makes E2E testing easier
 - If you have 5 different test cases, and you're not using TestNG, we could have 3 units execute successfully, and let's say the 4th one fails.
	 - We can fix the fourth case, but we traditionally can't just start at the 4th test case.
		 - This is what `TestNG` allows us to do - we can just start from the 4th test case now
	 - Also allows us to use annotations to define test methods and configurations
	 - Allows parallel testing (running tests at the same time)
	 - Allows for grouping of test cases
	 - Allows for the creation of reports
		 - Good for sharing with team, stakeholders, etc.

**Annotations include:**
 - `@Test` - used to let us know that the method is a test case
 - `@BeforeSuite` - runs before all test cases in this suite have run
 - `@AfterSuite` - runs after all test cases in this suite have run
 - `@BeforeTest` - runs before the execution of all test methods annotated with `@Test`
 - `@AfterTest` - runs after the execution of all test methods annotated with `@Test`
 - `@BeforeClass` - runs before the first test method in the current class have been run
 - `@AfterClass` - runs after all test methods in the current class have been run
 - `@BeforeMethod` - runs before each test method within a class
 - `@AfterMethod` - runs after each test method within a class
 - `@BeforeGroups` - runs before any test method belonging to the specified groups is executed
 - `@AfterGroups` - runs after any test method belonging to the specified groups is executed 

`BeforeSuite`, `BeforeTest`, `BeforeClass`, `BeforeMethod` will always run, regardless of what group it belongs to

*Adding the following...*

```
package ...

public class TestNG {
	@Test
	public void test1() {
		System.out.println("My first test case");
	}

	@Test
	public void test2() {
		System.out.println("My second test case");
	}
}
```

We then need to add [a new dependency](https://mvnrepository.com/artifact/org.testng/testng/7.10.2) to our `pom.xml`
 - https://mvnrepository.com/artifact/org.testng/testng/7.10.2

![](../Images/Pasted%20image%2020240808094001.png)

The import should be `import org.testng.annotations.Test`
 - IMPORTANT to use `TestNG`'s implementation, ***not*** `JUnit`'s.

Continuing on...

```
import org.testng.annotations.Test

public class TestNG {
	@Test
	public void test1() {
		System.out.println("My first test case");
	}

	@Test
	public void test2() {
		System.out.println("My second test case");
	}

	@BeforeMethod
	public void beforeMethod() {
		System.out.println("This will execute Before Method");
	}

	@AfterMethod
	public void afterMethod() {
		System.out.println("This will execute After Method");
	}

	@BeforeClass
	public void beforeClass() {
		System.out.println("This will execute Before Class execution");
	}

	@BeforeTest
	public class beforeTest() {
		System.out.println("This will execute Before Test");
	}

	@AfterTest
	public void afterTest() {
		System.out.println("This will execute After Test");
	}

	@AfterClass
	public void afterClass() {
		System.out.println("This will execute After Class execution");
	}

	@BeforeSuite
	public void beforeSuite() {
		System.out.println("This will execute Before Suite");
	}

	@AfterSuite
	public void afterSuite() {
		System.out.println("This will execute After Suite");
	}

	@BeforeGroups
	public void beforeGroups() {
		System.out.println("This will execute Before Groups");
	}

	@AfterGroups
	public void afterGroups() {
		System.out.println("This will execute After Groups");
	}
}
```

**To run:** There should be a run button next to the class name, that'll run the tests.

![](../Images/Pasted%20image%2020240808094837.png)

Output should look like this!

![](../Images/Pasted%20image%2020240808095034.png)

Note that additional cases will re-trigger `AfterMethod` and `BeforeMethod` for each case.

So, intuitively, when we want to open the browser in order to run the test cases...
**We would want to open the browser *before the tests run*.**

And for closing the browser after we're done running test cases...
**We would want to close the browser *after the tests run*.**

(Something like Group may be too late, the explanation was lost on me)

Making a new file called `MyTestNG.java`, we can add the following...

```
package ...

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.testng.annotations.Test;

public class MyTestNG {
	WebDriver driver;
	String baseUrl = "http://testfire.net/login.jsp";

	@Test
	public void login() {
		System.out.println("Test Case 1: Logging into Altoro Mutual as Admin");
		WebElement username = driver.findElement(By.id("uid"));
		WebElement password = driver.findElement(By.id("passw"));
		WebElement loginButton = driver.findElement(By.name("btnSubmit"));

		username.sendKeys("admin");
		password.sendKeys("admin");
		loginButton.click;
	}

	@BeforeTest
	public void launchBrowser() {
		System.out.println("Launching Chrome Browser");
		driver = new ChromeDriver();
		driver.get(baseUrl);
	}

	@BeforeClass
	public void beforeClass() {
		System.out.println("This will execute Before Class");
	}

	@BeforeMethod
	public void beforeMethod() { // Runs right before a test
		System.out.println("Before Method: Starting test on browser...");
	}

	@AfterMethod
	public void afterMethod() {
		System.out.println("After Method: Finished test on browser.");
	}

	@AfterClass
	public void afterClass() {
		System.out.println("This will execute After Class.");
	}

	@AfterTest
	public void afterTest() {
		System.out.println("All tests have finished - terminating browser");
		//driver.close();
		driver.quit(); // This may prevent the cause of errors -- ymmv
	}

	@BeforeSuite
	public void beforeSuite() {
		System.out.println("This will execute Before Suite");
	}

	@AfterSuite
	public void afterSuite() {
		System.out.println("This will execute After Suite");
	}
}
```

Output:
![](../Images/Pasted%20image%2020240808101359.png)
![](../Images/Pasted%20image%2020240808101413.png)

Adding even more code to `MyTestNG.java`...
```
package ...

import org.openqa.selenium.By;
...
<there are many imports i am missing now lol>

public class MyTestNG {
	WebDriver driver;
	String baseUrl = "http://testfire.net/login.jsp";

	@Test(priority = 1)
	public void login() {
		...
	}

	@Test(priority = 0)
	public void verifyTitle() {
		System.out.println("Test 2: Verifying the title");
		String expectedTitle = "Altoro Mutual";
		String actualTitle = driver.getTitle();
		Assert.assertsEquals(actualTitle, expectedTitle);
	}

	@Test(priority = 2)
	public void verifyGreeting() {
		System.out.println(x:"Test 3: Verifying the greeting when logged in");
		String expectedGreeting = "Hello Admin User";
		WebElement message = driver.findElement(By. tagName(tagName:"h1"));
		String actualGreeting = message.getText();
		Assert.assertEquals(actualGreeting, expectedGreeting);
	}
	...
}
```

Note that we're specifying a priority - this is another way to ensure the order in which tests run.
 - Priority ranges from 0-7?

Also, remember, we can now run parallel tests too!

```
@BeforeTest
public void launchEdgeBrowser() {
	System.out.println(x:"BeforeTest: Launching Edge Browser");
	System.out.println("Edge Thread : " + Thread.currentThread().getId());
	driver = new EdgeDriver();
	driver.get(baseUrl);
}

@BeforeTest
public void launchChromeBrowser() {
	System.out. println(x:"BeforeTest: Launching Chrome Browser");
	System.out.println("Chrome Thread : " + Thread.currentThread().getId();
	driver = new ChromeDriver();
	driver.get(baseUrl);
}
```

These two should be running on the same thread.

**For generating reports:**
This is typically easier done on IDEs such as Eclipse and SpringToolSuite, but there's a workaround for VSCode - **[the reportNG dependency](https://mvnrepository.com/artifact/org.testng/reportng/1.2.2)**

```
<dependency>
    <groupId>org.testng</groupId>
    <artifactId>reportng</artifactId>
    <version>1.2.2</version>
</dependency>
```

Running the tests again, we have 3 tests ran, 3 tests passed, and on the Explorer...

![](../Images/Pasted%20image%2020240808111238.png)

We have a new `test-output` folder with the test report.
It'll show how many failures, passed, errors, time passed, and more.
`index.html` will give us a prettier way to view the test report by opening it in a web browser.
**Note:** You may need the `Live Server` addon in VSCode to view the site, not sure.

![](../Images/Pasted%20image%2020240808111404.png)

![](../Images/Pasted%20image%2020240808111420.png)

Again, it's really just a prettier way to see the information we already got, but it's good to have.

![](../Images/Pasted%20image%2020240808111722.png)

It even gives us a nice output for errors!

```
@Test(priority = 2)
public void verifyGreeting() {
	System.out.println(x:"Test 3: Verifying the greeting once a user is logged in");
	String expectedGreeting = "Hello Admin User";
	WebElement message = driver.findElement(By.tagName(tagName:"h1"));
	String actualGreeting = message.getText();
	Assert.assertEquals(actualGreeting, expectedGreeting);
}

@Test(enabled = false) // Skipping
public void verifyTitle() {
	System.out.println(x:"Test 2: Verifying the title");
	String expectedTitle = "Altoro Mutual";
	String actualTitle = driver.getTitle();
	Assert.assertEquals(actualTitle, expectedTitle);
}
```

Note that, in the above, you can skip the test method by setting whether the test is enabled or not.

