~~*Caroline is having computer trouble*~~
~~*We're going to install the [community edition of Burp Suite](https://portswigger.net/burp), should be pretty easy*~~
~~*Something about saving data in the appdata folder*~~
~~*There's also a Getting started page [here](https://portswigger.net/burp/documentation/desktop/getting-started)~~

![](../Images/Pasted%20image%2020240828091958.png)

Oh lol.
Apparently it was causing her computer troubles, we'll be joining another group for today.

---

*In new meeting with David Lazaro*
# Burp Suite

**What is it?**
 - Uses network interception to understand web vulnerabilities.

**OWASP Top 10**
 - Every 4 years, a group of web practitioners finds what "in the wild" has caused exploits with web applications.
![](../Images/Pasted%20image%2020240828093819.png)

What happens when you run `'or 1=1;-`
The `'` tells it to break out. The `or 1=1` is always true, where `;-` makes it break out.
This is a type of SQL vulnerability? CHECK THIS

Burp Suite is a Java framework. It captures and analyzes network traffic between a client and a server. 

Different components:
 - Proxy
	 - "Middleman"
	 - Intercept + modify
	 - Foxy Proxy
		 - Separate tool tied into Burp Suite
 - Repeater
	 - We resend things - "like a repeater in a Wi-Fi network"
	 - Capture, modify, and resend X times
	 - Useful for injecting/crafting a payload
 - Intruder
	 - "Fuzzing/Brute Force"
		 - Fuzzing - Using random inputs to see how an application responds
		 - Brute Forcing - Running every input possible to hopefully get one right
			 - RockYou - Passwords from a Yahoo data breach
 - Decoder
	 - Transforming data
	 - Encoding data
 - Comparer
	 - A byte level comparison of values
 - Sequencer
	 - Assesses tokens/session cookies
	 - HTTP - a stateless protocol
		 - Every time you reacquired the connection, you'd have to verify who you were

---

Okay, we're reinstalling Burp suite using the instructions at the top.
 - Download Community Edition.

Additionally, download FoxyProxy - https://chromewebstore.google.com/detail/foxyproxy/gcknhkkoolaabfmlnjonogaaifnjlfnp

![](../Images/Pasted%20image%2020240828100425.png)

We should be at this screen after installation. Hitting next is fine.

![](../Images/Pasted%20image%2020240828100831.png)

Then navigate to https://burpsuite/

Heading to Foxy Proxy, we're going to try this.

(We actually had to redo this in Firefox - it wasn't working in Chrome. It also works for the built-in Chrome browser in Burp suite, which I'll be using.)

![](../Images/Pasted%20image%2020240828101425.png)

---

**Proxy**
![](../Images/Pasted%20image%2020240828105006.png)

(was having issues but tldr proxy intercepts traffic)

**Repeater**
![](../Images/Pasted%20image%2020240828105325.png)
 - Allows you to send a request or a response, and lets you change the content of an existing request/response.
 - Note the target - you can send a response to a website.

You can copy/paste the info from the Proxy tab into the Request side of the Repeater in order to essentially "resend" the information that was sent - for a basic, static website, it'll send back the exact same stuff.

**Intruder**
 - It's our fuzzing tool!
	 - We take our incorrect data and apply it to some fields.
	 - We can fuzz for fields, subdirectories, etc.
 - Since we're using the community edition, we'll be rate-limited for our fuzzing attempts - this is to prevent the tool from being used maliciously for free.
 ![](../Images/Pasted%20image%2020240828110823.png)

We can:
 - Specify an attack type out of the four listed.
 - Specify a payload (passwords from a word list, etc)

If we're looking at a web form, we can find different fields under the "positions".

Code 302 - Redirected
 - If you have a short time needed for a redirect, then there's a good chance the system was aware of the connection/resource placement?
	 - "A regular at a restaurant may just wave hi to the owner and sit down at a table."
 - If it takes a long time, then you can assume that it needed to do more handoffs.
	 - "Uber eats at a restaurant has to give a code, tell them who they're with, etc."

**Decode**

Can be used to decode pretty simple HTML and Base64 encodings.

*We tried to use smart decode to translate a string that was in Base64, but it didn't seem to work.*

---

[https://portswigger.net/web-security](https://portswigger.net/web-security "https://portswigger.net/web-security")
