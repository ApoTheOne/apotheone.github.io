---
title: Learning Docker - Theory
date: 2017-09-13 17:23:27
tags:
---

# Docker

---

#### Topics

-   Overview |
-   Dockerfile |
-   How to create a docker file? |
-   How to build a docker image? |
-   How to upload an image to Docker Hub? |

---

-   Docker Compose
-   Environment variables |
-   Port Mapping |
-   Links |
-   Volumes |

---

-   Network
-   Docker Swarm |
-   Services |
-   Stacks |
-   Tasks |

---

#### Overview

-   Docker is a platform for developers and sysadmins to develop, deploy, and run applications with containers.
-   The use of Linux containers to deploy applications is called containerization.

---

#### Virtual Machines to Docker containers.

Containerization makes CI/CD seamless.  
For example:

-   applications have no system dependencies
-   updates can be pushed to any part of a distributed application
-   resource density can be optimized.
    With Docker, scaling your application is a matter of spinning up new executables, not running heavy VM hosts.

---

##### Containers

-   Container is an isolated area of an OS with resource usage limits applied.
-   A container is launched by running an image.
-   A container is a runtime instance of an image what the image becomes in memory when executed.

---

##### Images

-   An image is an executable package that includes everything needed to run an application the code, a runtime, libraries, environment variables, and configuration files.
-   These portable images are defined by something called a Dockerfile.

---

### DEMO TIME

---

#### Networking

---

##### - Bridge network

-   Single host network
-   Each Bridge network is isolated from each others.
-   No communication between 2 containers in different bridge networks.

```
docker network create testnw
```

Create a network and run containers in those network using "--network"

```
docker create --name my-nginx --network testnw -p 8080:80 nginx:latest
docker network connect testnw my-nginx
```

---

##### - Overlay network

-   Multi-host network
-   Containers only network
-   Container to Container but not container to physical servers/virtual machines/EC2.

---

##### MACVLAN

-   In windows it is named as "Transparent" driver.
-   It assigns every container its own IP address and MAC address on existing network.
-   Requires promiscuous mode.

##### - IPVLAN: Similar to MACVLAN but doesn't requires promiscuous mode

---

### Swarm

A swarm is a group of machines that are running Docker and joined into a cluster.  
The machines in a swarm can be physical or virtual. After joining a swarm, they are referred to as nodes.  
Manager - worker pattern.

---

#### Services

In a distributed application, different pieces of the app are called “services.” For example, if you imagine a video sharing site, it probably includes a service for storing application data in a database, a service for video transcoding in the background after a user uploads something, a service for the front-end, and so on.
contd...

---

contd...
Services are really just “containers in production.” A service only runs one image, but it codifies the way that image runs—what ports it should use, how many replicas of the container should run so the service has the capacity it needs, and so on. Scaling a service changes the number of container instances running that piece of software, assigning more computing resources to the service in the process.
Luckily it’s very easy to define, run, and scale services with the Docker platform -- just write a docker-compose.yml file.
[Source](https://docs.docker.com/get-started/part3/#run-your-new-load-balanced-app)

---

To sum up: Services codify a container’s behavior in a Compose file, and this file can be used to scale, limit, and redeploy our app. Changes to the service can be applied in place, as it runs, using the same command that launched the service: docker stack deploy

---

#### Stack

Run your new load-balanced app
Before we can use the docker stack deploy command we first run:

```
docker swarm init
```

Now let’s run it. You need to give your app a name. Here, it is set to getstartedlab:

```
docker stack deploy -c docker-compose.yml getstartedlab
```

---

Our single service stack is running 5 container instances of our deployed image on one host. Let’s investigate.

Get the service ID for the one service in our application:

```
docker service ls
```

## [Source:Docker](https://docs.docker.com/get-started/part3/#run-your-new-load-balanced-app)

# Thank you!
