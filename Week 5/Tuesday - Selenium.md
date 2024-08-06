
Exam Friday! Don't forget to run through practice exams!

---


# Selenium
**A test automation tool for webapps.**

"Your typical test automation tool"
 - Used for web apps
 - Can create selenium test scripts with almost any language
 - Scripts can do a lot of stuff

**Selenium's Structure**

*Selenium (The tool itself)*
 - Selenium IDE
 - Selenium Grid
	 - For running parallel tests by running mini-servers
 - Selenium RC
	 - Remote Control, allows control over web browsers locally or on other computers
 - ==Web Driver== *(what we're focusing on right now)*
	 - Allows automation scripts on a web browser

## Selenium's Web Driver
You can write your tests in whatever language you want.

**Contains:**
 - **Client Library**
	 - Java
	 - C#
	 - Python
	 - Connects to Browser Driver via JSON over HTTP
 - **Browser Driver** - Middleman between browser and client library
	 - Instantiate and communicate via HTTP
	 - Chrome
	 - Firefox
	 - Safari
	 - Communicates with Browsers
 - **Browsers**
	 - Sends back a response to the driver
	 - Chrome
	 - Firefox
	 - Safari
	 - Communicates back with the Browser Driver

![](../Images/Pasted%20image%2020240806092443.png)

## Why is Selenium useful for testing?

Selenium offers a lot of benefits:
 - Open source
	 - No licensing costs, free to use and download
 - Mimics user actions
	 - Web driver mimics user input, via automating keypresses, mouse clicks, drag and drop, selecting - pretty much any type of user input
 - Easy implementation
	 - Pretty user-friendly
 - Tool suite
 - Language support
	 - Supports pretty much any language you can think of
 - Framework support
	 - Supports maven, Junit, TestNG, gradle, etc. 
- Reusability
- Selenium community
	- Active, lots of resources and support

## Using Selenium
1. Create an instance of a web driver
	1. `WebDriver driver = new ChromeDriver();`
	2. There's drivers for Chrome, Firefox, etc.
2. Ask the driver to get the URL of the page to test
	1. `driver.get("<URL>");`
3. Find an element on the page to interact with
	1. `driver.FindByElement(By.name("<Name>"));`
4. Perform an action with the element
	1. Let's say we have a submit button that we want to click - 
	2. `SubmitBtn.click();`

## Page Object Model (POM)
 - Design pattern for test automation
	 - Creates an Object Repository for web elements
 - Reduces code duplication
 - Simplifies test creation
 - Improves readability
 - **Annotation** `@FindBy`

---

# Using Selenium

1. Open VSCode
2. Make new Selenium folder
3. Make a new Spring project
	1. We're calling it `selenium-demo`
	2. `jar` file
	3. For dependencies, select `none`
4. Go to the [Maven Repository](https://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-java) and copy/paste the Selenium dependency into `pom.xml`
	1. Paste into the dependencies, of course
5. Make a new file in `test\java\com\skillstorm\selenium_demo` called `MyFirstScript.java`
	1. If it freaks out over the package, make sure to `Clean Java Language Workspace`
6. Add the following:
	1. Note that `ChromeDriver()` will need to be swapped out with the drivers for whatever browser you're testing on - supported browser drivers are listed [here](selenium.dev/documentation/webdriver/browsers).
```
import org.openqa.selenium.WebDriver;

...

public static void main(String args[])
{
	WebDriver driver = new ChromeDriver();

	driver.get("https://www.selenium.dev/selenium/web/web-form.html");
}
```
7. Running this should then navigate to the link.
	1. In this case, to a test site that you can use to ensure the driver is working properly.
8. Add `String title = driver.getTitle();`
	1. With this, we have the title of the page.
	2. Adding `System.out.println(title);`, it'll load the website titled "Web form", and in the console you can see that title printed out as well.
9. Add `String currentUrl = driver.getCurrentUrl();`
	1. Similarly, using `System.out.println(currentUrl);` will get the URL and print it to the console!
10. To quit the website after it's done running the test, you can use `driver.quit();`.
11. Next, we'll add a **WebElement**
	1. A WebElement is an interface in the Selenium WebDriver API that represents an HTML element on a webpage
	2. `findByElement()` provides your WebDriver a way to find a single web element on the current page
	3. `By` is a class in your WebDriver that provides a mechanism for locating items
	4. `By.[<locator>](<identifier>)` finds elements with the same name attribute
	5. **Locators** are a way to find elements on a page, there are 8 of them:
		1. `className` - compound class names are not permitted!
		2. `cssSelector`
		3. `id`
		4. `name`
		5. `linkText`
		6. `partialLinkText`
		7. `tagName`
		8. `xpath` - locates elements matching an `xpath` expression
	6. Add `WebElement textbox = driver.findElement(By.name("my-text"));`
		1. Finds the textbox by getting the element with the name `my-text`![](../Images/Pasted%20image%2020240806102218.png)
		2. We can then insert text into the input field via automation by using `.sendKey`
	7. Add `textbox.sendKeys("This is my input");`
		1. Running this, you should immediately see "This is my input" added into the form
12. Interacting with Elements - 
	1. There are 5 basic commands you can execute on an element:
		1. `sendKeys` - only applies to text fields and context editable elements
		2. `click` - applied to any element
		3. `clear` - only applies to text fields and content editable elements
		4. `submit` - only applies to form elements
		5. `select` - only applies to select elements
	2. Let's say we want to interact with this checkbox:![](../Images/Pasted%20image%2020240806104658.png)
		1. Now we know we can interact with the `name`, or the `id`.
	3. We can get the element with `WebElement checkBox = driver.findElement(By.id("my-check-2"));`, and use `checkBox.check();` to automate checking it.
	4. Same thing with buttons - ![](../Images/Pasted%20image%2020240806104952.png)
		1. We can even use the CSS selector! `WebElement submitBtn = driver.findElement(By.cssSelector("button"));`, and then use `submitBtn.submit();` to automate submitting the form.
			1. Note that submitting the form is different from *clicking* the button.
			2. Also, note that you need to be careful when using something broad to do something like submitting a form - if you had multiple buttons that all had that button CSS style, the behavior may be unpredictable.
				1. Update: Britt tried it out, it only used the first one on the site?
	5. Another: `WebElement submitBtn2 = driver.findElement(By.tagName("a"));`
	6. Another yet: `WebElement checkRadio = driver.findElement(By.xpath("//input[@name='my-radio']"));`
		1. The `xpath` is found by inspecting the element and doing `Copy -> Copy XPath`![](../Images/Pasted%20image%2020240806111227.png)
	7. Note that all elements on the page need to actually load/render before it can be interacted with.
		1. Note that you can also set a wait time for the page to load/render before it throws a `No Such Element Exception`:
		2. `driver.manage().timeouts().implicitylyWait(Duration.ofMillis(1000));`
		3. The above essentially just makes it wait for a second before throwing.
		4. Using `implicitlyWait` isn't really good practice, but it's good for troubleshooting.
13. Making a new file called `HelloSelenium.java`, we're going to use annotations!
	1. Add the following code:
		1. Note that we're using [testfire.net](testfire.net) as a test site for this example.
		2. Additionally, note that the title of the website is `Altoro Mutual`
```
package com.skillstorm.selenium_demo;

import org.junit.jupiter.api.BeforeEach;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class HelloSelenium {

	WebDriver driver;

	@BeforeEach
	public void setup() {
		driver = new ChromeDriver();	
	}

	@Test
	public void login() {
		driver.manage().timeouts().implicitlyWait(Duration.ofMillis(1000));

		driver.get("http://testfire.net");
		String title = driver.getTitle(); // Title should be Altoro Mutual
		assertEquals("Altoro Mutual", title);
	}
}
```
14. The above gets the homepage, the title text, and tries to see if it equals our expected text, `Altoro Mutual`.
	1. Now, we'll try to access the login/password fields.
```
	// Simulating a login on a webpage!
	@Test
	public void login() {
		driver.manage().timeouts().implicitlyWait(Duration.ofMillis(1000));

		driver.get("http://testfire.net");
		String title = driver.getTitle(); // Title should be Altoro Mutual
		assertEquals("Altoro Mutual", title);

		driver.navigate().to("http://testfire.net/login.jsp");
		WebElement username = driver.findElement(By.id("uid"));
		WebElement password = driver.findElement(By.id("passw"));
		WebElement loginBtn = driver.findElement(By.name("btnSubmit"));

		username.sendKeys("jsmith");
		password.sendKeys("Demo1234");
		loginBtn.submit(); // Click should work here as well.
	}
```
15. For the above, we're also navigating from the homepage to the login page, entering text for the username and password, and then submitting the information.
```
@AfterEach
public void teardown() {
	driver.quit();
}
```
16. The above here ensures that the page closes automatically after the automation is complete.
```
@Test
public void navigation()
{
	driver.get("http://testfire.net");
	driver.navigate().to(url:"http://testfire.net/login.jsp");
	driver.navigate().to(url:"http://testfire.net/index.jsp?content=personal.htm");
	driver.navigate().back();
	driver.navigate().forward();
}
```
17. The above demonstrates navigation - even using the browser's `back` and `forward` buttons!