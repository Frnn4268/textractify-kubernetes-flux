# Textractify Kubernetes Project with Flux

This repository contains the setup for deploying the Textractify application using Kubernetes with Flux for continuous delivery. The application consists of multiple services: a client, a server, and a Textractify client, all managed in a Kubernetes environment.

## Table of Contents

- Prerequisites
- Installation
- Configuration
- Deployment
- Verification
- Troubleshooting

## Prerequisites

Before getting started, ensure you have the following installed:

- Docker: Install Docker
- Kubernetes (kind): Install kind
- kubectl: Install kubectl
- Flux CLI: Install Flux CLI

## Installation

1. Clone the Repository

	Clone the repository to your local machine:

	```bash
 	git clone https://github.com/Frnn4268/textractify-kubernetes-flux.git
	cd textractify-kubernetes-flux
 	```

2. Create a Kind Cluster 

	Create a new Kubernetes cluster using kind:

	```bash
	kind create cluster --name "your_cluster_name"
	```

3. Install Flux

	Bootstrap Flux into your Git repository:

	```bash
    flux bootstrap github \
 	--owner="your_github_username" \
	--repository=textractify-kubernetes-flux \
	--branch=master \
	--path=clusters/textractify \
	--personal
    ```

4. Update Docker Images

	Push your Docker images to Docker Hub. Ensure your images are tagged correctly. Example:

	```bash
    docker build -t your-dockerhub-username/client:latest ./client
	docker push your-dockerhub-username/client:latest

	docker build -t your-dockerhub-username/server:latest ./server
	docker push your-dockerhub-username/server:latest

	docker build -t your-dockerhub-username/textractify-client:latest ./textractify-client
	docker push your-dockerhub-username/textractify-client:latest
    ```

## Deployment

After the configurations are set up, Flux will automatically monitor the Git repository for changes. To apply the initial configuration, run:
```bash
kubectl apply -f clusters/textractify
   ```

## Verification
