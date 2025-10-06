
<div align="center">

# 🐳 Docker for Developers

A comprehensive guide to Docker commands and configurations for various application components

## 📋 Table of Contents

| About | Contents | Description |
|---|---|---|
| Project | [Summary](#-summary) | |
| Docker | [Introduction](#-introduction) | |
| Docker | [Docker Principles](#-docker-principles) | Four principles of docker |
| Docker | [Essential Docker Commands](#-essential-docker-commands) | Docker commands |
| Docker | [Docker Compose Commands](#-docker-compose-commands) | Docker commands |
| Swarm | [Overview of Swarm](#-overview-of-swarm) | Started Swarm |
| Swarm | [Commands of Swarm](#-commands-of-swarm) | Swarm commands |
| K8S | [Overview of Kubernetes](#-overview-of-kubernetes) | Started K8S |
| K8S | [Installing K8S](#-installing-k8s) | Installing Kubernetes on macOS |
| K8S | [Deploy to the cluster](#-deploy-to-the-cluster) | Deploy to the cluster |
| Project | [Project Architecture](#-project-architecture) | |
| Project | [Resources](#-resources) | |

</div>

<div align="center">

## 🔍 Summary

</div>

This repository contains Docker configurations and commands for various application components, including backend services, frontend applications, and fullstack setups. It provides a practical guide for containerizing different parts of a web application using Docker and Docker Compose.

The project includes:
- Backend service with Node.js and MongoDB
- Frontend application with React
- Fullstack setup with Docker Compose

Each component has its own Dockerfile and configuration, demonstrating best practices for containerizing web applications.

<div align="center">

## 🚀 Introduction

</div>

Docker is a platform for developing, shipping, and running applications in containers. Containers allow developers to package an application with all its dependencies and ship it as a single unit.

> **Note:** When working with Docker, always start by finding an appropriate base image on Docker Hub that matches your application's requirements.

The first step in creating a Dockerfile is to look for a base image on Docker Hub and copy the specific name.

Docker Hub website for searching images: [https://hub.docker.com/](https://hub.docker.com/)

<div align="center">

## 🌴 Docker Principles

</div>

Docker has four principles.

### 1. Image 💿

An image refers to the configuration of a container, it is the base image to run the container. The image contains the configuration base and/or an application and its entire environment.

### 2. Container 🧰

A container is the coupled image running in execution, and can be accessed.

### 3. Newtwork 🛜

It is the network used by the application running in the container, this includes the port and the docker network settings created for the application to run on top.

### 4. Volume 🎲

A volume refers to a data allocation created and managed by Docker. It is not deleted when deleting a container or image. Volumes can be created for databases, file storage, or similar purposes for running containers.

<div align="center">

## 🖥️ Essential Docker Commands

</div>

This section covers fundamental Docker commands for building, managing, and running containers and images.

### Build an Image

Use this command to build a Docker image from a Dockerfile in the current directory. Replace `[image_name]` with your desired image name.

```bash
docker build -t [image_name] .
```

Example for backend:
```bash
docker build -t jonathasrochadesouza/backend .
```

Example for frontend:
```bash
docker build -t jonathasrochadesouza/frontend .
```

### List Images

Displays all locally available Docker images.

```bash
docker images
```

### Run a Container

Starts a new container from an image. The `-p` flag maps ports (host:container), and `-d` runs the container in the background (detached mode).

```bash
docker run -p [host_port]:[container_port] [image_name]
```

To free the console CLI, add the `-d` flag:
```bash
docker run -d -p [host_port]:[container_port] [image_name]
```

If an error occurs due to version (e.g., Node.js):
```bash
docker run -e "NODE_OPTIONS=--openssl-legacy-provider" -p [host_port]:[container_port] [image_name]
```

Example for backend:
```bash
docker run -p 4000:4000 jonathasrochadesouza/backend
```

Example for frontend:
```bash
docker run -p 3000:3000 jonathasrochadesouza/frontend
```

### Check Running Containers

Lists all currently running Docker containers.

```bash
docker ps
```

### Stop a Container

Stops a running container using its ID or name.

```bash
docker stop <container_id_or_name>
```

### Remove an Image

Removes a Docker image. Ensure no containers are using the image before removing it.

```bash
docker rmi <image_id_or_name>
```

### Force Stop a Container and Remove Image

Forces a container to stop and, if necessary, removes the associated image.

```bash
docker kill <container_id_or_name>
```

<div align="center">

## 🖥️ Docker Compose Commands

</div>

This section details commands for managing multi-container applications using Docker Compose.

### Build Images (Compose)

Builds or rebuilds services defined in `docker-compose.yml`.

For all services:
```bash
docker-compose build
```

For individual services (e.g., `mongo`, `app`, `client`):
```bash
docker-compose build [service_name]
```

Example:
```bash
docker-compose build mongo
```

### Start Services (Compose)

Creates and starts containers for all services defined in `docker-compose.yml`. The `-d` flag runs in the background.

For all services:
```bash
docker-compose up -d
```

For individual services:
```bash
docker-compose up -d [service_name]
```

Example:
```bash
docker-compose up -d app
```

### Stop Services (Compose)

Stops running services without removing the containers.

```bash
docker-compose stop
```

### Stop and Remove Services (Compose)

Stops and removes containers, networks, and volumes created by `up`.

```bash
docker-compose down
```

### View Logs (Compose)

Displays logs for all services or a specific service.

For all services:
```bash
docker-compose logs
```

For a specific service:
```bash
docker-compose logs [service_name]
```

<div align="center">

## 📦 Overview of Swarm

</div>

Docker Swarm is Docker's native orchestration tool, designed to group and manage multiple hosts (called nodes) into a single, cohesive cluster. As the default solution, it comes installed and enabled by default with Docker.

The primary feature of Swarm is the creation of an overlay network that connects all nodes. This allows containers, even if running on different physical machines, to communicate transparently and securely as if they were on the same local network. Nodes can connect to each other. A container within a node can connect to a container on another node.

SSH into the new machine, use the join command that was displayed when the swarm was initialized to join the new node to the swarm, and then deploy the stack using the Docker compose file.

## 👨🏾‍💻 Commands of Swarm

Initializes a new swarm. This command sets up your current machine as the manager node of the swarm.
```bash
docker swarm init
```

Provides detailed information about your Docker installation, including the status of the swarm, containers, and images.
```bash
docker info
```

Lists all the nodes in the swarm, showing their IDs and roles (e.g., manager or worker).
```bash
docker node ls
```

**These commands above help you set up and manage a Docker swarm, which is a cluster of Docker nodes that can be used to deploy and manage applications.**

Deploys a new stack to the swarm using the specified Docker Compose file. This command sets up the services defined in the compose file within the swarm.
```bash
docker stack deploy -c docker-compose.yml <stack_name>
```

Adds a new node to the swarm. This command is run on the machine you want to add as a worker or manager node, using the token and manager IP address provided when the swarm was initialized.
```bash
docker swarm join --token <token> <manager_ip>:<port>
```

**These commands above help you manage and expand your Docker swarm by adding new nodes and deploying services.**

Creates a new service in the swarm with one replica. The service is named node_server2 and uses the node image from Docker Hub.
```bash
docker service create --replicas 1 --name nodeserver2 node ping docker.com
```

Lists all the services currently running in the swarm, showing their names, IDs, and statuses.
```bash
docker service ls
```

**These commands help you deploy and manage services within a Docker swarm, allowing you to scale and inspect your applications efficiently.**

<div align="center">

## 🗃️ Overview of Kubernetes

</div>

* Tool for container orchestration.
* Built by Google and open-sourced.
* More extensible compared to Docker Swarm.
* Same concepts of nodes.

Features:

* Clustering
* Scaling
* Scheduling
* Deployment

Nodes:

* Uses the concept of nodes to manage multiple containers.
* Can scale to thousands of nodes if needed.

Comparison with Docker Swarm:

* Swarm is tightly integrated with Docker.
* Kubernetes is more customizable and an industry standard.

## 📥 Installing K8S

### 1. Homebrew

To install Kubernetes on macOS, you can use a tool like Minikube or Docker Desktop, which simplifies the process. Here’s a general outline of the steps you can follow:

Install Homebrew: If you haven't already, install Homebrew, which is a package manager for macOS. You can do this by running the following command in your terminal:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### 2. Kubectl

Install kubectl: This is the command-line tool for interacting with Kubernetes. You can install it using Homebrew as well:

```bash
brew install kubectl
```

Verify Installation: After installation, you can verify that everything is working by running:

```bash
kubectl version --client
```

### 3. Minikube

Install Minikube: Use Homebrew to install Minikube:

```bash
brew install minikube
```

Verify Installation: After installation, you can verify that everything is working by running:

```bash
minikube version
```

Start Minikube: Once installed, you can start Minikube with:

```bash
minikube start
```

Access the Kubernetes Dashboard: If you want to access the Kubernetes dashboard, you can enable it with:

```bash
minikube dashboard
```

### About installations

Minikube: A tool that creates a single-node Kubernetes cluster on your local machine for learning and development purposes.

Kubectl: A command-line interface (CLI) used to run commands and manage resources within a Kubernetes cluster.

All have allows flag `--help`, for show all commands and obtain helping!

<div align="center">

## 👨🏾‍💻  Deploy to the cluster

### 1. Creating your first cluster

</div>

Start Minikube:
```bash
minikube start
```

This command initializes and starts your first Kubernetes cluster using Minikube. It might take longer if you don't have all the necessary images downloaded.

Check Cluster Info:
```bash
kubectl cluster-info
```

This command provides information about the cluster, including the control plane (master) and CoreDNS, confirming that your cluster is up and running.

Verify Control Plane:

The output will include the IP address of the control plane, which you can use to SSH into the cluster or add services.

### Deploy to the cluster

Create Deployment:
```bash
kubectl create deployment <deploy-name-here> --image=<image_here>
```

This command creates a new deployment in the Kubernetes cluster. For example, to create a deployment named nodeapplication using the Node.js image, you would use:
```bash
kubectl create deployment nodeapplication --image=node
```

Specify Image:

When creating a deployment, you can specify the image from Docker Hub or any other repository by providing the full URL. For example:

```bash
kubectl create deployment nodeapplication --image=docker.io/library/node
```

Check Deployments:
```bash
kubectl get deployments
```

This command lists all the deployments in your cluster, showing the status of each deployment.

These commands help you deploy an application to your Kubernetes cluster and verify its deployment.

<div align="center">

## 🏗️ Project Architecture

</div>

The project is organized into several components, each with its own Docker configuration:

```
docker_for_developers_linkedIn/
|
|-- README.md                 # Main documentation
|
|-- backend/                  # Backend service
|   |-- Dockerfile            # Backend container configuration
|   |-- docker-compose.yml    # Compose for backend with MongoDB
|   |-- index.js              # Main backend application file
|   |-- package.json          # Node.js dependencies
|   |-- README.md             # Backend documentation
|   |-- src/                  # Source code
|   |   |-- controllers/      # API controllers
|   |   |-- models/           # Data models
|   |   |-- routes/           # API routes
|   |-- public/               # Static files
|   |-- data/                 # MongoDB data
|
|-- frontend/                 # Frontend application
|   |-- Dockerfile            # Frontend container configuration
|   |-- package.json          # Node.js dependencies
|   |-- README.md             # Frontend documentation
|   |-- public/               # Static files
|   |-- src/                  # Source code
|
|-- fullstack/                # Fullstack application
|   |-- docker-compose.yml    # Compose for all services
|   |-- README.md             # Fullstack documentation
|   |-- api/                  # Backend API
|   |   |-- Dockerfile        # API container configuration
|   |   |-- index.js          # Main API file
|   |   |-- package.json      # Node.js dependencies
|   |-- client/               # Frontend client
|   |   |-- Dockerfile        # Client container configuration
|   |   |-- package.json      # Node.js dependencies
|   |-- data/                 # MongoDB data
```

<div align="center">

## 📚 Resources

</div>

### Docker Install and Started

Visit the official Docker documentation:
[https://www.docker.com/get-started/](https://www.docker.com/get-started/)

### Docker CLI References

For more detailed information about Docker commands, visit the official Docker CLI documentation:
[https://docs.docker.com/reference/cli/docker/](https://docs.docker.com/reference/cli/docker/)

### Docker Image Search

Docker Hub website for searching images:
[https://hub.docker.com/](https://hub.docker.com/)

---

<div align="center">

*From Jonathas* 🤎

</div>

