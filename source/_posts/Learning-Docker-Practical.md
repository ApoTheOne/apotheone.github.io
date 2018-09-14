---
title: Learning Docker - Practical
date: 2018-09-13 23:02:03
tags:
---

This post will be **hands on** session for working in Docker.

## Setup :

**To install Docker on Linux open the terminal and run following command**:  
`wget -qO- https://get.docker.com/ | sh`

To install docker in Windows 10 professional donwload binaries and install them.
If you are using a lower version like Windows home you will require Docker Toolbox and Oracle Virtual Box.

To update Docker in Windows:

```
> Install-Module DockerProvider -Force`
> Install-Package Docker -ProviderName DockerProvider -Force
```

Run the following command to restart the docker service  
`sudo service docker restart`

---

## Playing around with containers :

To run a container, type following command in the terminal:  
`docker run -it ubuntu bash`  
If the image is not present in your system's cache then it calls `docker pull` implicitly which downloads the image from Docker registry.  
`-it` here signifies interactive shell
and `bash` takes us to the ubuntu containers bash.  
Let's install curl utility in this container and then exit:

```
apt-get update
apt-get install curl
exit
```

To **check running containers**:  
`docker ps -a`

If we make some changes to a container and want to commit it to create a new image, we can use:  
`docker commit containerId`  
_Note 1_: "containerId" was retrieved from previous command.  
_Note 2_: Ideally We should create an image and then run container out of it but this is just to check out how `commit` works.

Let's check the output of commit by checking out new image:

```docker images
docker tag imageId myImageName
docker images
```

In order to **list running containers** type: `docker ps`  
To **list all the containers**: `docker ps -a`  
With Ids: `docker ps -aq`  
To check last run container: `docker ps -l`

Now let's **remove a container** by: `docker rm containerId`

What to do if one wants to list out the images residing in your system? Try this: `docker images`  
Now in order to **remove an image**: `docker rmi imageId`  
To **delete an image forcefully**: `docker rmi -f imageId`

Now, let's **create a Dockerfile** through which we can create an image, type this in terminal:

```
touch Dockerfile
vim Dockerfile
FROM ubuntu
RUN apt-get update
RUN apt-get install -y curl
```

`touch Dockerfile` creates a new file name Dockerfile.  
`vim Dockerfile` opens the file in the vim editor.  
Either copy paste all the content or by switching to INSERT mode in VIM by pressing `i` and then typing it.

Now let's save it by pressing escape key and then type in `:w` to save and `:q` to exit vim editor. Or to do save and quit in one go, press excape to get out of insert mode and then press `:wq`  
Now we have a docker file with following content:

```
FROM ubuntu
RUN apt-get update
RUN apt-get install -y curl
```

Now we will build an image from this dockerfile :  
`docker build -t newimagename .`  
_Note_: `.` in the command represents current folder.

Check new image using: `docker images`  
Now let's run the image which should have curl utility pre-installed in it.  
`docker run -it myubuntuimage bash`

In order to execute a command as soon as a container starts, we use **CMD** :

```
FROM ubuntu
RUN apt-get update
RUN apt-get install -y curl
CMD curl -i www.google.com
```

Build new image from this docker file:  
`docker build -t mycurlimage .`

If we need to build our image so that we can pass parameters in to it while running a container from it, we can use **entrypoints**

```
FROM ubuntu
RUN apt-get update
RUN apt-get install -y curl
ENTRYPOINT ["curl", "-i"]
```

Building image from updated dockerfile:  
`docker build -t mycurlimage .`

Now, test it by running these two commands one by one:  
`docker run mycurlimage www.google.com`  
`docker run mycurlimage https://reqres.in/api/users?page=1`

Let's try out one more scenario for entrypoint.  
Update dockerfile like this:

```
FROM ubuntu
RUN apt-get update
RUN apt-get install -y curl
ENTRYPOINT ["curl", "-i"]
CMD https://reqres.in/api/users?page=2
```

_Note_: If no parameter is passed while running `docker run`, then the CMD line's page 2 api will be called (think of it as a default value).  
Let's build new image from our updated docker file and then run the container:  
`docker build -t mycurlimage .`  
`docker run mycurlimage`  
This outputs response of https://reqres.in/api/users?page=2

`docker run mycurlimage https://reqres.in/api/users?page=1`  
This outputs response of https://reqres.in/api/users?page=1

`docker run mycurlimage https://reqres.in/api/users?page=3`  
This outputs response of https://reqres.in/api/users?page=3

To override entry point; let's replace curl with bash like this:  
`docker run -it --entrypoint bash mycurlimage`

---

We have some essential parameters which are used while running a container like `-d`, `-P` etc.

1. **daemon** `-d` is used to run a container in backgorund.

2. `--publish-all` or `-P` exposes it to others on random ports.  
   Lets try it out:  
   `docker run -d --publish-all imageNameOfAppOrApi`

Let's play around with **`-p`** for a while.  
We can expose/map localhost's (your system's) port 80 to container's port 8080 by:  
`docker run -d -p 80:8080 imagenameofwebapporapi`

---

In order to get IP address of the container:

```
docker inspect --format '{{ .NetworkSettings.IPAddress}}'
```

containerid returnedIp  
`ping returnedIp`

---

### SWARM

Now, let's create, download or clone a sample Node.js API (can refer to this [repo](https://github.com/apotheone/PPOC/tree/master/NodeJsApi))  
Create and run it's image from it's dockerfile(ex: [dockerfile](https://github.com/ApoTheOne/PPOC/blob/master/NodeJsApi/DockerFile)): `docker build -t username/imagename:tag .`

Now, let's initiate a swarm:  
$ `docker swarm init`  
Swarm initialized: current node (jfzjw0wo8p9rax7ofcy5XXXXX) is now a manager.

In order to add a worker to this swarm, run the following command:
`docker swarm join --token XXXXXXXXXXx-1-e2qregpnucqkzk6u87tgc0j08dnjp0zambwkg26p3ce8aovk-e8hb2xge 192.168.XX.X:PORTNO`

To add a manager to this swarm, run  
`docker swarm join-token manager`  
and follow the instructions.

Use a docker compose file from the given repo to deploy a stack:  
`docker stack deploy -c docker-compose.yml webapi`

Check running services using:
`docker service ls`
This should output webapi_web which is "webapi" appended with the service name in the docker-compose.yml file

##### TASK

A single container running in a service is called a task. Tasks are given unique IDs that numerically increment, up to the number of replicas you defined in docker-compose.yml.

To list all the tasks of your service:  
`docker service ps webapi_web`

`docker container ls -q`

`curl -5 http://localhost:8080/test`

To scale our service, we can change number of replicas in our docker-compose.yml and re run the stack:  
`docker stack deploy -c docker-compose.yml <appname>`

This doesn't require us to tear down a swarm or stop and re-run containers.  
`docker services ls -q`

In order to take down the app and the swarm:

1. Take the app down with docker swarm rm:  
   `docker stack rm webapi`
2. Take down the swarm.  
   `docker swarm leave --force`

---

### Various commands used:

```
docker stack ls
# List stacks or apps
docker stack deploy -c <composefile> <appname>
# Run the specified Compose file
docker service ls
# List running services associated with an app
docker service ps <service>
# List tasks associated with an app
docker inspect <task or container>
# Inspect task or container
docker container ls -q
# List container IDs
docker stack rm <appname>
# Tear down an application
docker swarm leave --force
# Take down a single node swarm from the manager

# //Create a Nw switch from HyperV Manager with eg: name myswitchname
//Creating VMs
docker-machine create -d hyperv --hyperv-virtual-switch "myswitchName" apovm1
docker-machine create -d hyperv --hyperv-virtual-switch "myswitchName" apovm2

docker-machine ssh apovm1 "docker swarm init --advertise-addr <ipadd:port>"

docker-machine env apovm1
# // configure your shell to talk to myvm1.
& "C:\Program Files\Docker\Docker\Resources\bin\docker-machine.exe" env apovm1 | Invoke-Expression

docker stack deploy -c docker-compose.yml apistack

docker stack rm apistack
docker-machine ssh apovm2 "docker swarm leave"
docker-machine ssh apovm1 "docker swarm leave --force"

// unset the docker-machine environment variables in your current shell with
& "C:\Program Files\Docker\Docker\Resources\bin\docker-machine.exe" env apovm1 -u | Invoke-Expression
```
