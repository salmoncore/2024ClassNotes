## Image
 - "A copy of the code"
 - Libraries
	 - Needed for execution
 - Binaries
	 - The executables

## VM
 - Applications
 - Libraries
 - Binaries
 - **Operating system**
 - **Hypervisor**
	 - *Manages resource for our VM operating system*
	 - *Acts as a barrier between the VM OS and the OS it's running on*(?)
	 - RAM
	 - CPU
	 - Storage
	 - Networking

## Container
 - "Runs the image"
 - The image needs to "enter" into the container
	 - This is done by exposing a port - telling it what port it needs to listen on

---

## Docker Example

Docker docs: https://docs.docker.com/manuals/

Note that signing into Docker desktop is signing into the Docker Hub - a repository for Docker images.
 - A docker image is a set of pre-requisites and scripts needed for running an application - it can include anything from app code to dependencies and etc.

In our case - we're trying to run Java. Therefore, we need the dependencies to run a Java executable - we're looking for one to run the Java Runtime Environment (JRE). 

You can specify versions of an image from docker hub using something like:
```
docker pull java
java: latest
// java: 1.0.1
```

There's a Docker workshop we'll be working through [here](https://docs.docker.com/guides/workshop/).

### Terminal Walkthrough
Make sure that Docker is open, and we'll be going through a few things:

1. `docker ps`
This should show us a buncha docker things - more on this later.

2. `docker run ubuntu` - Docker pulls an image from Docker Hub, in this case, ubuntu.
	1. This will download it in "layers", essentially parts - any subsequent update will only require a small update.
![](../Images/Pasted%20image%2020240813102201.png)

3. Run `docker ps -a`
	1. We get the output saying something ran not too long ago - it was our Ubuntu image. However, the image had no executables - it isn't executing anything. If nothing is running, it automatically closes it.
	2. We can force it to run for a while using `docker run ubuntu sleep 15` - it'll keep executing for the duration of the sleep task.
	3. If we run `docker run -d ubuntu sleep 30` - the `-d` places the docker container into the background, and we can use `docker ps -a` to show the running container.

4. `docker images`
	1. This shows us our images that we have installed - `ubuntu` should be listed.

5. `git clone https://github.com/docker/getting-started-app.git`
	1. We're containerizing this application. 
	2. `docker build -t todo-app .` will do it, but we need a `dockerfile` to instruct it on *how*

![](../Images/Pasted%20image%2020240813103105.png)

We make the `dockerfile` in this directory - and add the following:
 - Note: If you're working in a Windows/M-series Mac team, you need to instruct it to use the same instruction set when building.

```
FROM node:18-alpine

WORKDIR /app

COPY . .

RUN yarn install --production

CMD ["node", "src/index.js"]
```

 - `node:18-alpine` specifies Node 18, running on Alpine Linux
 - `WORKDIR` specifies the directory we're working in - note that we're working off of the directory that the `dockerfile` is in
 - We copy everything using `COPY . .`, and in our case, we're using a `.dockerignore` to exclude everything we don't want - so this is fine.
 - We can have as many `RUN` commands as we'd like, but only one `CMD` - which takes a list of strings of dependencies it needs.
	 - `CMD` is where it runs the application.

6. Back to `docker build -t todo-app .`
	1. This builds the docker image into the root directory
	2. Any additional change should be faster, thanks to layers!

8. `docker run -d -p 3000:3000 todo-app`
	1. Can use `-dp`, but needs to specify the `p` last
	2. `3000:3000` specifies the ports being used to communicate into Docker
	3. Now that it's running, we can go to `http://localhost:3000/` to view the application


**Our Computer** (localhost:3000)-> *Port 3000* <--> *Port 3000* <-(Application Port) **Docker Container**

Note that something like `3000:8080` is valid, as long as they're all opened up properly - when we have it on something like a Kubernetes cluster, we need to have a little more consideration.

9. When closing it down when it's in the background, we can use `docker stop`, with the container ID:
![](../Images/Pasted%20image%2020240813105409.png)

We can also use the "name", which fun fact, is an adjective and the name of a scientist.

10. To clean up (since all images we make take up space):
	1. `docker container prune -f`

*Back from morning break*

Again, if we edit something, we then have to stop the Docker container, make a change, and then re-build the docker container. So far, that's not a great workflow. We'll get to that, but first, we'll start by **doing a simple push to our Docker Hub.**

11. `docker tag todo-app salmonline/todo-app`
	1. `salmonline` is my username - use whatever your Docker hub username is!
	2. We can then use `docker push salmonline/todo-app` to push it to an repo!
	3. You can find the image and ensure it worked [here](https://hub.docker.com/): https://hub.docker.com/
	4. If you have trouble signing in via the Docker desktop app - go to account settings on the web -> security -> personal access token, set any name, allow read/write/delete, and follow the steps to sign in via the console. From there, docker push should work just fine.

![](../Images/Pasted%20image%2020240813112126.png)

12. Containers are stateless - if you make something new within them during execution, it won't persist on the next run. We manage persistent storage via **volumes.**
	1. We can either use the `docker volume create` tool, or the command line `docker run -it -v ubuntuvolume:/mnt ubuntu /bin/bash`, where we're making a volume `ubuntuvolume` located within `/mnt` within the container.
	2. **We can also set our working directory as a volume!** This makes development easier. The command is pretty long:

```
docker run -dp 3000:3000 skillstorm/todo-app
```
*oh no! it failed! it says the port is already allocated by our earlier todo app!*
We can either stop the container, or change the port number. In our case, we just stopped the old container. Back to the **ACTUAL** string:

```
docker run -dp 3000:3000 skillstorm/todo-app -w /app -v {$pwd}:/app node:18-alpine sh -c "yarn install && yarn run dev"
```
*oh no, this might also fail! dunno why, here's one that fr will work:*

```
POWERSHELL:
docker run -dp 127.0.0.1:3000:3000 `
    -w /app --mount "type=bind,src=$pwd,target=/app" `
    node:18-alpine `
    sh -c "yarn install && yarn run dev"

MAC/LINUX:
docker run -dp 127.0.0.1:3000:3000 \
    -w /app --mount type=bind,src="$(pwd)",target=/app \
    node:18-alpine \
    sh -c "yarn install && yarn run dev"
```
**MAKE SURE TO PASTE AS ONE LINE!**
If you have issues loading `localhost:3000`, try `127.0.0.1:3000` instead. If that doesn't work, remove the 

https://docs.docker.com/guides/workshop/06_bind_mounts/ 
Here's the link for this command for other systems/consoles.

*Resuming from after lunch*

To force all Docker containers to stop all at once:
`docker stop $(docker ps -q)`

To remove all images at once:
`docker rmi $(docker images -q)`

13. `docker network ls`

![](../Images/Pasted%20image%2020240813131200.png)

This shows us all the networks that are currently attached
 - The bridge is the connection to the internet(?)

We want to create a new network connection:

14. `docker network create todo-app`
If we do `docker network ls` again, we can see our new network. Let's go ahead and use it:

`docker run -d --network todo-app --network-alias mysql -v mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=secret -e MYSQL_DATABASE=todos mysql:8.0`
 - The network name is a reference so that we don't use IP addresses - these addresses *can* change, even in our demo project. We want to use DNS, not the IP. In this example, `mysql` is our DNS.

![](../Images/Pasted%20image%2020240813132053.png)

Get the container ID using `docker ps`

15. `exec -it <id> mysql -u root -p`
`dig mysql` will show you the IP address that the todo app is using.

16. Here's the next script, we'll go over it in a moment:

```
docker run -dp 3000:3000 `
  -w /app -v "$(pwd):/app" `
  --network todo-app `
  -e MYSQL_HOST=mysql `
  -e MYSQL_USER=root `
  -e MYSQL_PASSWORD=secret `
  -e MYSQL_DB=todos `
  node:18-alpine `
  sh -c "yarn install && yarn run dev"
```
Note that this is for PowerShell-

```
docker run -dp 3000:3000 \
  -w /app -v "$(pwd):/app" \
  --network todo-app \
  -e MYSQL_HOST=mysql \
  -e MYSQL_USER=root \
  -e MYSQL_PASSWORD=secret \
  -e MYSQL_DB=todos \
  node:18-alpine \
  sh -c "yarn install && yarn run dev"
```
-and this is for Mac.

The purpose of all of this is so we set up a separate MySQL database to hold the to-do's. They now persist between container shutdown and more!

![](../Images/Pasted%20image%2020240813134614.png)

Here's the cycle for shutting everything down, and then the two steps to get everything brought back up.

17. Docker Compose
It's a `.yaml` file that describes services, volumes, configuration, secrets, networking, etc.

Make the file here:

![](../Images/Pasted%20image%2020240813140509.png)

```
services:

  app:

    image: node:18-alpine

    ports:

      - 3000:3000

    working_dir: /app

    volumes:

      - ./:/app

    networks:

      - todo-app

    environment:

      - MYSQL_HOST=mysql

      - MYSQL_USER=root

      - MYSQL_PASSWORD=secret

      - MYSQL_DB=todos

    command: sh -c "yarn install && yarn run dev"

  

  mysql:

    image: mysql:8.0

    networks:

      - todo-app

    volumes:

      - todo-mysql:/var/lib/mysql

    environment:

      - MYSQL_ROOT_PASSWORD=secret

      - MYSQL_DB=todos

  

volumes:

  todo-mysql:

  

networks:

  todo-app:
```

18. `docker compose up -d`

Runs the Docker setup - and we're done!

***LEARN WHAT KUBERNETES STANDS FOR OR SOMETHING LOL***

