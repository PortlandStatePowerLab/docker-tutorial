# docker-tutorial
In an attempt to create a standard development environment to reduce setup time and debugging the PSU Power Lab has adopted the use of docker. If you are unfamiliar with docker and containers in general I highly recommend watching [docker's get started](https://docs.docker.com/get-started/). Following the tutorials you will know docker works as well as the general setup of a dockerfile for your development environment.

# Dockerfile
Our dockerfile consists of all project dependancies required to run each of our projects. This means that the container takes some time to install, but once it is installed each project can seemlessly be cloned and worked on within. 

## Building Dockerfile.buster
- Download and install docker on your machine following the instructions specific to your Operating System. *see the get started link above*
- Clone this repository to your machine
- Change directory to the docker-tutorial folder
- Build the Dockerfile.buster and wait for the process to finish
- Run the docker image as *-id* interactive and detached so it is running in the background
- Note: Read below section on RAM use before running for the first time!

```shell
git clone https://github.com/PortlandStatePowerLab/docker-tutorial
cd docker-tutorial
docker build --file Dockerfile.buster --tag psu-dev .
docker run -id psu-dev
```
### Creeping Host Machine RAM Use
Note: It is a well-documented problem that docker containers will "creep," their use of the host machine's RAM. To solve this problem, you can specify a limit to the RAM used by the container. This link contains more details: https://docs.docker.com/config/containers/resource_constraints/

To do this for the above instructions, you can try replacing `docker run -id psu-dev` with the following:

```shell
docker run -id -m "4g" psu-dev
```
Where the `"4g"` in quotes is the RAM ceiling for the container (in gigabytes, as specified by the g).

## Saving/Loading Image
I have found that my machine will delete images after a system update. This is actually a common issue that will hopefully be fixed soon. If you have room on your machine, approximatly 3 GB, I recommend saving the image to a tar file so that you can always reload the image if something happens. 

```shell
cd docker-tutorial
docker save --output psu-dev.tar psu-dev
docker load < psu-dev.tar
```

# Development Environment
Now that we have a docker container running we can set up our editor to attach to it and program from our local machine as if it was the container. Each IDE or Editor has its own setup, but we will show how to setup using Visual Studio Code as it is cross-platform and fairly straight forward. 

## Visual Studio Code
Download VS Code from https://code.visualstudio.com/ and install according to your operating system.

### Extensions
Once VS Code is installed you will need a few extensions to make developing in your project much easier. This only lists C++ specific extensions, but you can find extensions for any language you are working in. The most important are **Docker and Remote - Container** as these are what allows VS Code to attach to a container and act as if your local machine is the container. 

- C/C++
- C++ Helper
- CMake
- Docker
- Remote - Container
- Remote - SSH

### Attach VS Code
The following link shows you how to simply connect to a container to start development. And off you go!

https://code.visualstudio.com/docs/remote/attach-container
