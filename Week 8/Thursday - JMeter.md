# JMeter
A tool to measure the performance of your app.
 - Performance testing
	 - Create test plans to determine what's expected of the best possible performance
 - Stress test tools
	 - Seeing how the system performs under intense load
	 - Determining at what point the system is overwhelmed
 - Load test tools
	 - Giving your system a payload to process
	 - Checking to see if the system can handle the load
 - Can be used via command line, or the GUI
 - Java-based (only for Java)

### Test Plan
 - Contains all of your tests
	 - Thread Group
		 - A starting point for a test plan
		 - Where we have different requests we make
		 - A thread is the amount of time a request is sent/ran
			 - Can be increased/decreased, e.g. 1-?? requests
		 - Different types of requests
			 - Can have a timer before another iteration is ran, stuff like that
	 - Types of tests:

---

https://jmeter.apache.org/download_jmeter.cgi
We downloaded JMeter from here - select the binary, not the source.

![](../Images/Pasted%20image%2020240829094125.png)

We extracted jmeter into program files, and we can run this to open the GUI.

![](../Images/Pasted%20image%2020240829094416.png)

To make it easier in the future, we can also add it to our PATH and run it using `jmeter` in the terminal.

Note that whatever directory you open with jmeter is where your tests will be saved by default - we can organize this by making a folder in your user directory.

![](../Images/Pasted%20image%2020240829095042.png)

To start off, let's create a thread group. Note that a thread is essentially like a simulated user.

![](../Images/Pasted%20image%2020240829095236.png)

We see some options - for example, we can choose the number of threads (users), the number of times we want to simulate a request being made, etc.

![](../Images/Pasted%20image%2020240829095529.png)

If we add an HTTP request...

![](../Images/Pasted%20image%2020240829100117.png)

https://reqres.in/ - We're using this site, which is essentially a test site for this type of tool.

Hit ctrl-s to save, and then you can run it.

![](../Images/Pasted%20image%2020240829100328.png)

Hm, no output. That's because we need a *listener*.

![](../Images/Pasted%20image%2020240829100426.png)

![](../Images/Pasted%20image%2020240829100437.png)

Add these two.

![](../Images/Pasted%20image%2020240829100937.png)

We can now view the results in the two different views.

![](../Images/Pasted%20image%2020240829101854.png)

Adding another HTTP request...

oh ps to clear the logs you can use this broom button 

![](../Images/Pasted%20image%2020240829102525.png)


Note that JMeter *can* be integrated into Jenkins to allow us to capture performance metrics.

---

**Project 3 Notes**
 - 3 weeks
 - Starting off of another cohort's project 3
 - We'll be implementing a bunch of tests into the software
	 - The project is already deployed to AWS, has a Jenkins CI/CD pipeline
 - We'll likely be split up into groups to work on implementing different testing components

---

If you're having trouble sending information like this:

![](../Images/Pasted%20image%2020240829114540.png)

Remember you may need to use a HTTP header manager - 

![](../Images/Pasted%20image%2020240829114524.png)

Think of it as the header that we use in Postman - it's like the content-type (application/json).

Cookies can also be added via other managers - it just depends.

![](../Images/Pasted%20image%2020240829114944.png)

Using a graph result, we can view information plotted out.

We can also use a Timer to delay a thread by a set amount of time - if we added a thread delay of 3000 milliseconds, it'd have to wait 3 second before running a thread action.

---

To summarize:

 - You need a thread group
 - Need some type of sampler to communicate with the network