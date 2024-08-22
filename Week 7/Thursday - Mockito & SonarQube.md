# Mockito
Tool/framework for creating mock objects.

## Mocks
A clone of an object that we can use instead of real objects for use with dummy data.
 - If you have a class that depends on an object, we can use a mock of it.

(I was having a lot of PC trouble here, please check lecture recording for full notes.)

---

# SonarQube

Find downloads and steps [here](https://docs.sonarsource.com/sonarqube/latest/setup-and-upgrade/install-the-server/introduction/).

We're using PGAdmin with PostgreSQL 16, so we'll test it out.

Make a new user:

![](../Images/Pasted%20image%2020240822155115.png)

Name: sonaradmin
Password: admin
Privileges: ALL

Save it, and now you should see `sonaradmin` as a user.

Right-click postgres and disconnect from server:

![](../Images/Pasted%20image%2020240822155309.png)


Do this:

![](../Images/Pasted%20image%2020240822155520.png)

Change this to `sonaradmin`:

![](../Images/Pasted%20image%2020240822155537.png)

![](../Images/Pasted%20image%2020240822155622.png)

Go ahead and reconnect, put in the new password `admin`.

Now we need a sonarqube database:

![](../Images/Pasted%20image%2020240822160712.png)

![](../Images/Pasted%20image%2020240822160730.png)

Should look like this.

Heading back to the directory for sonarqube, head to the `conf` folder and open the `sonar` file AS ADMIN.

![](../Images/Pasted%20image%2020240822161101.png)

![](../Images/Pasted%20image%2020240822161133.png)

Make the above changes.

![](../Images/Pasted%20image%2020240822161725.png)

Additionally, add the `SONAR_JAVA_PATH` environment variable.

![](../Images/Pasted%20image%2020240822161752.png)

Should look like this.

Additionally, make sure the following is in PATH:

![](../Images/Pasted%20image%2020240822161839.png)

![](../Images/Pasted%20image%2020240822161907.png)

Should look like this.

Open up command prompt and run the `StartSonar.bat` file like this:

![](../Images/Pasted%20image%2020240822162327.png)

![](../Images/Pasted%20image%2020240822162507.png)

As long as we see the `SonarQube is operational` message, we should be good.

Head to `localhost:9000/`, and you should see this:

![](../Images/Pasted%20image%2020240822164519.png)

*Caroline is having some issues, so we're stopping here for today.*

https://docs.sonarsource.com/sonarqube/10.6/analyzing-source-code/scanners/sonarscanner-for-maven/

