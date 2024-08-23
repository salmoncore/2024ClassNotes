To sign in on the login page, use the username/password `admin`. Afterwards, set a new password!

Select local project, and we'll be using this one:

![](../Images/Pasted%20image%2020240823093624.png)

We're going to be using the global setting on the next page.

We can analyze the project with Github actions or Jenkins, but for now, we'll be using "locally".

Generate a token - I believe we set ours not to expire. Copy the command containing the token on the next page, it'll have Maven and we're using that.

Also, we'll need to add this plugin to our project: [https://mvnrepository.com/artifact/org.sonarsource.scanner.maven/sonar-maven-plugin](https://mvnrepository.com/artifact/org.sonarsource.scanner.maven/sonar-maven-plugin "https://mvnrepository.com/artifact/org.sonarsource.scanner.maven/sonar-maven-plugin")

POM should look like this:

```
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.skillstorm</groupId>
  <artifactId>age-validator</artifactId>
  <version>1.0.0</version>
  <name>age-validator</name>
  <url>http://www.example.com</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source> 
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>

  <dependencies>
    <!-- JUNIT 4-->
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.13.2</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
  
  <build>
    <plugins>
      <plugin>
        <groupId>org.jacoco</groupId>
        <artifactId>jacoco-maven-plugin</artifactId>
        <version>0.8.12</version>
        <executions>
          <execution>
            <goals>
              <goal>prepare-agent</goal>
              <goal>report</goal>
            </goals>
          </execution>
        </executions>
      </plugin>

      <plugin>
        <groupId>org.sonarsource.scanner.maven</groupId>
        <artifactId>sonar-maven-plugin</artifactId>
        <version>4.0.0.4121</version>
      </plugin>
    </plugins>
  </build>
</project>
```

```
mvn clean verify sonar:sonar `-Dsonar.projectKey=age-validator `-Dsonar.projectName=age-validator `-Dsonar.host.url=http://localhost:9000 `-Dsonar.login=<your token>
```

The above code worked for me. YMMV.

---

We're doing the same thing for the CucumberDemo - Modify the POM with the necessary dependencies, and then run:

```
mvn clean verify sonar:sonar `-Dsonar.projectKey=cucumberdemo `-Dsonar.projectName=cucumberdemo `-Dsonar.host.url=http://localhost:9000 `-Dsonar.login=<your token>
```

...from the folder with CucumberDemo in it.

---

When we set this up for our own project...

When we create a new configuration, we will be using Github for this.

Go to your profile, select developer settings, and create a new Github app.

For the name, just name it whatever your project name is. For the homepage, put in the homepage of the app we've deployed. 

---

We may end up having it so that ngrock will be running on EC2 - this will simplify our CI/CD portion. 

---

Frontend almost done, if not all the way done
Try to get Jenkins put together - this one is pending some potential changes for EC2
Mockito underway
Try to get on SonarQube