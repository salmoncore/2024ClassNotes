She wants cucumber/selenium integrated with the project:
 - Wants to see some test cases
 - Wants to see some JUnit test cases covered
	 - She wants us to be more comfortable using testNG?
 - Wants project 2 deployed to AWS

---

## Quality Gates
A checkpoint in the development process that must be passed before moving on to the next step.

*Two Types:*
### Automated
- Will read every line of code you have
	- Statement testing - sees what code lines have executed
- **Advantages**
	- Consistent, scalable, fast
- "Checkpoints that are automatically checked by automation tools"
	- JaCoCo
	- SonarQube
	- Mockito
- *If you can only do one, this one has more advantages*

### Manual
 - Some human intervention that would be happening
	 - Code reviews, inspecting it for issues, design reviews, UAT
	 - Any manual process is included in this category
 - **Advantages**
	 - More flexible than automated tests
	 - Pulls from your experience with the project - expert testers can catch issues
	 - More user-centric
 - "Checkpoints that involve human interaction to check criteria is met"

### Hybrid
 - Using both is preferred 

We believe our code is ready for deployment - so we pass it through a quality gate before building.
We believe our build is ready for testing - so we pass it through another quality gate.
After testing, we pass it through another quality gate before deployment.

# JaCoCo
*Java Code Coverage*
A library for Java that will read and execute parts of your code, when you run a test.
- Line Coverage
- Branch Coverage
- Method Coverage
- Class Coverage

To allow for us to do this, we'll be using our `age-validator` project.

![](../Images/Pasted%20image%2020240821110601.png)
First, add the dependency for JaCoCo, and then we'll be adding a plugin:

```
<build>
      <plugins>
            <plugin>
                <groupId>org.jacoco</groupId>
                <artifactId>jacoco-maven-plugin</artifactId>
                <version>0.8.5</version>
                <executions>
                    <execution>
                        <goals>
                            <goal>prepare-agent</goal>
                        </goals>
                    </execution>
                    <!-- attached to Maven test phase -->
                    <execution>
                        <id>report</id>
                        <phase>test</phase>
                        <goals>
                            <goal>report</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
  </build>
```

Should look something like this.

![](../Images/Pasted%20image%2020240821111446.png)

Then, we should be able to use these button to select what we want to do with our code - in our example, we can `clean` to set it up, and `test` to test the code. **We can also just use `mvn test`.**

We also have new `site\jacoco` and (something) folders, the `index.html` file within the `jacoco` folder will then show us our test statement/branch coverage results.

![](../Images/Pasted%20image%2020240821112005.png)

Note the `Cxty` column - this is how many test cases needed to cover a piece of code.

![](../Images/Pasted%20image%2020240821112538.png)

We can even see what statements are executed, and which are missed!

We can also set a minimum for the percentage of statements/branches that need to be tested:

```
<build>
      <plugins>
            <plugin>
                <groupId>org.jacoco</groupId>
                <artifactId>jacoco-maven-plugin</artifactId>
                <version>0.8.5</version>
                <executions>
                    <execution>
                        <goals>
                            <goal>prepare-agent</goal>
                        </goals>
                    </execution>
                    <!-- attached to Maven test phase -->
                    <execution>
                        <id>report</id>
                        <phase>test</phase>
                        <goals>
                            <goal>report</goal>
                            <goal>check</goal>
                        </goals>
                        <configuration>
                          <rules>
                            <rule>
                              <limits>
                                <limit>
                                  <counter>LINE</counter>
                                  <value>COVEREDRATIO</value>
                                  <minimum>0.50</minimum>
                                </limit>
                              </limits>
                            </rule>
                          </rules>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
  </build>
</project>
```

Note: If we have 100% code coverage, we have executed it, but that's it. **We still need to be checking for logic issues.**

