
https://github.com/bdgomey/JenkinsDemo

**CD/CD** - Continuous Integration, Continuous Deployment

**Delivery** - A user/human has to have a human confirm the deployment to production
**Deployment** - An integrated system automatically deploys code to production

# Jenkins

A CI/CD tool we can use to create pipelines.

### Installing Jenkins
 - Installer for Windows is apparently a pain
 - There's a `.war` file (Web Application Archive)
 - But we can also just get it through **Docker**

**Make a new directory and add a `.dockerfile`**

Add the following:

```
FROM jenkins/jenkins:2.462.1-jdk17
USER root
RUN apt-get update && apt-get install -y lsb-release maven zip
RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc \
  https://download.docker.com/linux/debian/gpg
RUN echo "deb [arch=$(dpkg --print-architecture) \
  signed-by=/usr/share/keyrings/docker-archive-keyring.asc] \
  https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list
RUN curl -fsSL https://deb.nodesource.com/setup_16.x | bash -
RUN apt-get update && apt-get install -y docker-ce-cli nodejs kubernetes-client
RUN export M2_HOME=/usr/bin/mvn; export MAVEN_HOME=/usr/bin/mvn
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
RUN unzip awscliv2.zip
RUN apt install docker.io -y
RUN ./aws/install
RUN jenkins-plugin-cli --plugins "maven-plugin workflow-aggregator git sonar nodejs kubernetes aws-credentials docker-workflow ssh-agent email-ext blueocean pipeline-aws docker-plugin"
```

**Now, we can create a Docker network using `docker network create jenkins`, and then set up the docker containers with:**

```
docker run --name jenkins --restart=on-failure --detach `
	--network jenkins `
	--volume /var/run/docker.sock:/var/run/docker.sock `
	--volume jenkins-data:/var/jenkins_home `
	--publish 8080:8080 --publish 50000:500000 myjenkins-blueocean
```
*If you're on a Mac, replace the backtic with backslash.*

**DIND** - Docker In Docker
*You need to allow a Docker container running within a Docker container access to the Host Operating System's Docker Socket (Sock), or else it won't work.*

![](../Images/Pasted%20image%2020240820093549.png)

**Now, we can navigate to localhost:8080, and you should see this:**

![](../Images/Pasted%20image%2020240820093855.png)

**Make sure to add all suggested plugins, you get the password from using `docker logs jenkins`**

When you create an admin user, use anything you want - your personal information is fine.

**Go to dashboard -> new item -> freestyle (name it whatever) -> Now we have some options!**

He advises us to discard old builds:
![](../Images/Pasted%20image%2020240820102348.png)

He advises we use Github and git stuff for automation, since that's where we're building.
We'll add a execute shell build step, and add in a bash script:
`echo "Hello World"`

![](../Images/Pasted%20image%2020240820102427.png)
![](../Images/Pasted%20image%2020240820102454.png)
And here we can see our output.

**Now, we'll be creating a Jenkins file, which will allow us to automate what we want to do!**

Make a new pipeline, go down and in the script area use the Hello World example:
```
pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
    }
}
```

And then in VSCode, make a new `Jenkinsfile`, with this:
```
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh "echo Building - Stage 1"
            }
        }

        stage('Test') {
            steps {
                sh "echo Testing - Stage 2"
            }
        }

        stage('Deploy') {
            steps {
                sh "echo Deployment - Stage 3"
            }
        }
    }
}
```

Make github repo
New pipeline
add github hook trigger for GITScm polling
select pipeline script from scm
![](../Images/Pasted%20image%2020240820110350.png)

Go to github repo -> settings -> webhook, and here's the thing - we're running locally, so it'll be a problem.

![](../Images/Pasted%20image%2020240820110729.png)

This tool will help us with that. 
Note: If you're on Windows you need chocolatey - it's pretty easy to setup if you don't have it.

Then we can do `ngrok http 8080`
Note - If you get an error, make an account https://dashboard.ngrok.com/get-started/your-authtoken here and copy the command for the authtoken

![](../Images/Pasted%20image%2020240820111321.png)

This address is what we're looking for.

Use `https://1c37-70-253-62-104.ngrok-free.app/github-webhook/` WITH the trailing slash when adding the github webhook

![](../Images/Pasted%20image%2020240820112817.png)

Should look something like this.

Once we push a change to the Jenkins file, or any other file in the repository - we should have a push go to the Jenkins instance and trigger a run of the tests.

![](../Images/Pasted%20image%2020240820113039.png)

We want to make a new react app using Vite
npm create vite@latest
cd frontend
npm install
npm run dev to test

Then we can edit our setup:

![](../Images/Pasted%20image%2020240820113821.png)

Now we'll make a new stage - 

```
stage('Deploy Frontend') {

            steps {

                sh "echo Deploying Frontend"

                sh "aws sync frontend/dist s3://inventoryman"

            }

        }
```

Now head to Jenkins, we need to add the AWS credentials

![](../Images/Pasted%20image%2020240820114341.png)

We're all using the same S3 key - find it somewhere.

```
pipeline {
    agent any

    stages {
        stage('Build Frontend') {
            steps {
                sh "echo Building Frontend"
                sh "cd frontend && npm install && npm run build"
            }
        }
        stage('Deploy Frontend') {
            steps {
                sh "echo Deploying Frontend"
                script{
                    withAWS(region: 'us-east-1', credentials: 'AWS_CREDENTIALS') {
                        sh "aws s3 sync frontend/dist s3://inventoryman-test"
                    }
                }
            }
        }
    }
}

```

```
pipeline {
    agent any

    stages{
        stage('Build Frontend'){
            steps{
                sh "echo Building frontend"
                sh "cd frontend && npm install && npm run build"
                
            }
        
            }
        stage('Deploy Frontend'){
            steps{
                script{
                    try {
                      withAWS(region: 'us-east-1', credentials: 'AWS_CREDENTIALS'){
                        sh "aws s3 sync frontend/dist s3://bjgomes-bucket-sdet" 
                        }
                    }catch (Exception e) {
                            echo "${e}"
                            throw e
                    }   
                }
            }
        }
        stage('Build Backend'){
            steps{
                sh "cd demo && mvn clean install && ls target/"
            }
        }
        stage('Test Backend'){
            steps{
                sh "cd demo && mvn test"
            }
        }
        stage('Deploy Backend'){
            steps{
                script{
                  withAWS(region: 'us-east-1', credentials: 'AWS_CREDENTIALS'){
                        sh 'pwd'
                        sh "aws s3 cp demo/target/demo-1.0-SNAPSHOT.jar s3://bjgomes-bucket-sdet-backend"
                        sh "echo 'aws elasticbeanstalk create-application-version --application-name myName --version-label 0.0.1 --source-bundle S3Bucket=\"bjgomes-bucket-sdet-backend\",S3Key=\"demo-1.0-SNAPSHOT.jar\"'"
                        sh "ech 'aws elasticbeanstalk update-environment --environment-name myName --version-label 0.0.1'"
                    }  
                }   
            }
        }
    }
}
```
^ his code for deploying front/backends

