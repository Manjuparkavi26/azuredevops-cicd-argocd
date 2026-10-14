
# Example Voting App

A simple distributed application running across multiple Docker containers.

## Getting started

Download [Docker Desktop](https://www.docker.com/products/docker-desktop) for Mac or Windows. [Docker Compose](https://docs.docker.com/compose) will be automatically installed. On Linux, make sure you have the latest version of [Compose](https://docs.docker.com/compose/install/).

This solution uses Python, Node.js, .NET, with Redis for messaging and Postgres for storage.

Run in this directory to build and run the app:

shell
docker compose up

The vote app will be running at [http://localhost:8080](http://localhost:8080), and the results will be at [http://localhost:8081](http://localhost:8081).

Alternately, if you want to run it on a [Docker Swarm](https://docs.docker.com/engine/swarm/), first make sure you have a swarm. If you don't, run:
shell
docker swarm init

Once you have your swarm, in this directory run:

shell
docker stack deploy --compose-file docker-stack.yml vote


## Run the app in Kubernetes

The folder k8s-specifications contains the YAML specifications of the Voting App's services.

Run the following command to create the deployments and services. Note it will create these resources in your current namespace (default if you haven't changed it.)

shell
kubectl create -f k8s-specifications/


The vote web app is then available on port 31000 on each host of the cluster, the result web app is available on port 31001.

To remove them, run:

shell
kubectl delete -f k8s-specifications/


## Architecture

![Architecture diagram](architecture.excalidraw.png)

* A front-end web app in [Python](/vote) which lets you vote between two options
* A [Redis](https://hub.docker.com/_/redis/) which collects new votes
* A [.NET](/worker/) worker which consumes votes and stores them in…
* A [Postgres](https://hub.docker.com/_/postgres/) database backed by a Docker volume
* A [Node.js](/result) web app which shows the results of the voting in real time

## Notes

The voting application only accepts one vote per client browser. It does not register additional votes if a vote has already been submitted from a client.

This isn't an example of a properly architected perfectly designed distributed app it's just a simple
example of the various types of pieces and languages you might see (queues, persistent data, etc), and how to
deal with them in Docker at a basic level.

# azuredevops-cicd-argocd-voting-app
CI/CD pipeline using Azure DevOps, Docker, Kubernetes and Argo CD (Docker image,AKS,ACR,Yaml,Multi microservices-votingapp)


# Azure DevOps CI/CD with ArgoCD for a Multi-Microservice Voting App

This project demonstrates a complete CI/CD workflow for a multi-service application using:
- Azure DevOps for build and release automation
- Docker for containerization
- Azure Container Registry (ACR) for image storage
- Azure Kubernetes Service (AKS) for application hosting
- ArgoCD for GitOps-based continuous deployment

The application is based on a typical microservices voting app architecture and is designed to show how modern cloud-native deployments work in real-world enterprise environments.

---

## Overview

This repository is a hands-on DevOps learning project focused on:
- building Docker images for multiple services
- pushing them to ACR
- deploying to AKS
- managing continuous deployment using ArgoCD
- using YAML-based infrastructure and deployment definitions

The goal is to create a repeatable automated delivery pipeline from source code to production deployment.

---

## Project Objective

The main objective of this project is to implement a real-world CI/CD pipeline that helps:

- automate application builds
- package services into Docker containers
- store images in Azure Container Registry
- deploy microservices to Kubernetes
- manage deployments with ArgoCD
- make the project easier to maintain and scale

This is a practical example of DevOps and GitOps principles in Azure.

---

## Architecture

This project follows a multi-container application pattern, usually with services such as:

- Frontend application
- Backend/API service
- Worker service
- Redis as cache
- PostgreSQL or another database
- Result service / admin dashboard

Typical flow:

1. Developer pushes code to the repository
2. Azure DevOps pipeline triggers automatically
3. Docker images are built for each service
4. Images are pushed to Azure Container Registry
5. AKS receives deployment updates
6. ArgoCD syncs Kubernetes manifests or Helm values from Git
7. Application becomes live in the cluster

---

## Tech Stack

- Azure DevOps
- Azure Kubernetes Service (AKS)
- Azure Container Registry (ACR)
- Docker
- Kubernetes YAML manifests
- ArgoCD
- Git
- Microservices architecture

---

## Repository Structure

A typical layout for this project looks like this:

azuredevops-cicd-argocd/
├── app/
│   ├── frontend/
│   ├── backend/
│   ├── worker/
│   └── result/
├── docker/
│   ├── Dockerfile.frontend
│   ├── Dockerfile.backend
│   ├── Dockerfile.worker
│   └── Dockerfile.result
├── k8s/
│   ├── deployment/
│   ├── services/
│   ├── ingress/
│   └── config/
├── helm/
│   └── charts/
├── pipelines/
│   └── azure-pipelines.yml
├── scripts/
│   └── deploy.sh
├── README.md
├── .gitignore
└── docker-compose.yml





## CI/CD Flow

The normal pipeline flow is:

1. Code Commit

A developer updates source code and pushes it to Git.

2.Trigger Azure DevOps Pipeline

The Azure DevOps pipeline starts automatically after a commit or pull request.

3.Build Docker Images

Each microservice is built into a container image.

4.Push to ACR

Built images are tagged and placed in Azure Container Registry.

5.Deploy to AKS

The deployment manifests or Helm values are updated and applied to the Kubernetes cluster.

6.ArgoCD Sync

ArgoCD continuously monitors Git and synchronizes the cluster state with the desired application state.

7.Production Ready

The application is available through the cluster and external access configuration such as Ingress or LoadBalancer.



## Azure Resources Used

This project generally depends on the following Azure services:

1.Azure DevOps

2.Azure Container Registry (ACR)

3.Azure Kubernetes Service (AKS)

4.Azure Resource Group




## Example Deployment Flow

A typical path for this project:

Text
Developer Code Change
        |
        
Git Push
        |
        
Azure DevOps Pipeline
        |
        
Build Docker Images
        |
        
Push to Azure Container Registry
        |
        
Update Kubernetes manifests / Helm values
        |
        
ArgoCD Sync
        |
        
AKS Deployment Updated


## Conclusion

This repository is a practical implementation of Azure DevOps + Docker + AKS + ArgoCD for a multi-microservice application. It is useful for learning cloud-native DevOps workflows and understanding how modern software is deployed in enterprise environments.



