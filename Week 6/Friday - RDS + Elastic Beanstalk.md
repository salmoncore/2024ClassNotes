Authentication vs Authorization
 - Authentication is verifying the user is who they say they are, 
 - Authorization is determining what services a user can access

AAA - Authentication, Authorization, and Accounting

IAM - Identity Access Management

---

## Temp
 - ID - Identity
	 - Needs to have access to a resource

**We do this by attaching permissions to a ==role==, and assigning the role to the user.**

**STS** - Simple Token Service
 - Looks to see if your ID is trusted, and if it is, it'll return a **session token** to the temp area with a time limit - usually 1-12 hours.
	 - Decoding the session token will show the information for the session time limit.
 - You also retrieve an access and secret key.
 - **With this, you can then access resources in EC2.**

**Why is it a good idea to have a time-based limit?**
 - If someone gets the session tokens, it's only a vulnerability for the duration of the token lifespan - after that, the attacker would have to re-gain the token,

---

# RDS

For our project, we're using the Aurora (PostgreSQL Compatible) database.

We'll be using the `Dev/Test` template.

Make sure to use `Serverless v2`

For capacity range, choose 0.5-2gb for the capacity range.

Don't create an Aurora replica.

He set public access to yes - ideally this would be no, but it's just for a project.

Within Additional Configuration, we can get the database automatically created when the project is created. Otherwise, it's just a pretty basic setup for getting RDS configured - do the same thing we did within PostgreSQL, essentially.

Going back into the settings, we will eventually have to connect a EC2 instance - make sure to use the cheap, non-IOP storage. That would be really bad.

There's two types of databases that live on Amazon that have different fault tolerance features - 
 - Non-aurora has a series of compute clusters, that if one went down, another would be promoted and traffic would be redistributed to it via the DNS. You wouldn't typically know a cluster went down because of this - uptime should be preserved.
 - Aurora has Read Replicas that will read across 6 different storage backups of the data, which is managed by the PR. It's faster and safer.

When attempting to access the database, if you have issues, remember to check and see if it's publicly accessible - you'll need that for connecting with postgres and postman, etc.


# Elastic Beanstalk

We can host an app, by providing the app code. With that, it can execute an environment to run the app, and we can tell it to pull the app from Github. 

With Maven, we build our backend via automations and the `.jar` file can be executed within this environment. 

When setting up the environment, we can use Coretto 17, which is just Amazon's version of Java.

We can set the elastic beanstalk to pull from an S3 bucket, but make sure that that bucket has public permissions! You can set that from the EC2 instance profile - if you make a role, consider making one like `S3FullEC2`, that'll allow full access to S3 from EC2.

We won't need load balancing for our app - it's very simple.

We can use up to t3 medium for our processing, but micro and small should also be available.

Using the application load balancer is a good idea.

For our API, we can add a listener port - like port 8080.

We shouldn't need to worry about health reporting, as we're developing, having health checks enabled may kill the process as we keep launching it, if it errors. May make debugging hard.

Once you've specified the `.jar` file in an S3 bucket and launch it, it should be able to create the backend.