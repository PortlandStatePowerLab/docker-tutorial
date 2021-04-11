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

```shell
git clone https://github.com/PortlandStatePowerLab/docker-tutorial
cd docker-tutorial
docker build --tag psu-dev .
docker run -id psu-dev
```
