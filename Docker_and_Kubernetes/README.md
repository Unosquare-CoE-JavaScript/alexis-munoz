# Docker and Kubernetes

## What is Docker?

Docker is a platform for running containers on a Linux host. It is a lightweight, portable, and extensible system for running applications. A container is a piece of software that is packaged together with its dependencies.

## What are containers?

The industry standard today is to use Virtual Machines (VMs) to run software applications. VMs run applications inside a guest Operating System, which runs on virtual hardware powered by the server’s host OS.

## What is an image?

A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.

## Download a image from Docker Hub

`Docker pull busybox`

## List the images

`docker images`

## Run a container

`docker run busybox echo "hello from busybox"`

## Exec a container

Running the run command with the -it flags attaches us to an interactive tty in the container. Now we can run as many commands in the container as we want. Take some time to run your favorite commands.

`docker run -it busybox sh`

## Docker port forwarding

Docker port forwarding is a way to expose ports on the host to the container.

`docker run -p 8888:80 prakhar1989/static-site`

## Dockerfile

A Dockerfile is a text file that describes how to build a container image.

```Dockerfile
FROM node:alpine

WORKDIR /app

COPY ./package.json ./

RUN npm install

COPY . .

CMD ["npm","run", "start"]
```

## What is Kubernetes?

Kubernetes is a container orchestration system that is designed to be highly available, scalable, and fault-tolerant.

## What is a cluster?

A cluster is a group of machines that are connected to a shared network.

## What is a namespace?

A namespace is a collection of resources that are isolated from other resources in the same cluster.

## What is a pod?

Pods are containers that are deployed on a node.

### What is a pod template?

Pod templates are used to define the containers that will be deployed on each node.

## What is a node?

Nodes are machines that are part of a cluster.

## What is a service?

Services are used to expose ports to the outside world. They can be used to expose a web server, a database, or any other service.

## What is a deployment?

Deployments are used to scale a service. They are used to automatically scale a service to a specific number of replicas.

## What is a replication controller?

Replication controllers are used to manage the number of replicas of a service.

## Basic comands

    kubectl get nodes
    kubectl get pods
    kubectl get services
    kubectl get deployments
    kubectl get replicationcontrollers
    kubectl get pods --all-namespaces
    kubectl get pods --namespace=default
