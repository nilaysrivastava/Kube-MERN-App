# Kube-MERN-App

This repository contains Kubernetes manifests for deploying a MongoDB database and a Mongo Express web application using Docker images, ConfigMaps, and Secrets for configuration management.

## Overview

The project consists of deploying two main components using Kubernetes:

1. **MongoDB**: A popular NoSQL database.
2. **Mongo Express**: A web-based MongoDB admin interface.

Both components are deployed using their official Docker images:
- MongoDB: `mongo:latest`
- Mongo Express: `mongo-express:latest`

## Files

- `mongo-app.yaml`: Deployment and Service definition for MongoDB.
- `mongo-config.yaml`: ConfigMap for MongoDB configuration.
- `secret.yaml`: Secret for storing MongoDB credentials.
- `web-app.yaml`: Deployment and Service definition for Mongo Express.

## Prerequisites

- Kubernetes cluster
- `kubectl` command-line tool configured to interact with your Kubernetes cluster

## Setup

### 1. Clone the repository

```bash
git clone <repository-url>
cd Kube-MERN-App
```

### 2. Create Secrets and ConfigMaps

Create the Secret for MongoDB credentials:

```bash
kubectl apply -f secret.yaml
```

Create the ConfigMap for MongoDB configuration:

```bash
kubectl apply -f mongo-config.yaml
```

### 3. Deploy MongoDB

Deploy the MongoDB instance using the following command:

```bash
kubectl apply -f mongo-app.yaml
```

Verify the MongoDB deployment and service:

```bash
kubectl get deployments
kubectl get services
```

### 4. Deploy Mongo Express

Deploy the Mongo Express web application using the following command:

```bash
kubectl apply -f web-app.yaml
```

Verify the Mongo Express deployment and service:

```bash
kubectl get deployments
kubectl get services
```

### 5. Access Mongo Express

Find the NodePort assigned to Mongo Express:

```bash
kubectl get services
```

Access Mongo Express using your browser and the IP address of any node in your cluster along with the NodePort. For example:

```
http://<node-ip>:30100
```

## Files Details

### `mongo-app.yaml`

Defines the MongoDB deployment and service. The MongoDB container is configured with environment variables that retrieve values from the `mongo-secret`.

### `mongo-config.yaml`

Defines a ConfigMap that contains the MongoDB service URL.

### `secret.yaml`

Defines a Secret that stores the MongoDB root username and password in base64 encoded format.

### `web-app.yaml`

Defines the Mongo Express deployment and service. The Mongo Express container is configured with environment variables that retrieve values from the `mongo-config` ConfigMap and `mongo-secret`.

## Clean Up

To delete all the resources created by this project, run:

```bash
kubectl delete -f web-app.yaml
kubectl delete -f mongo-app.yaml
kubectl delete -f secret.yaml
kubectl delete -f mongo-config.yaml
```

## Contributing

Contributions are welcome! Please fork this repository and submit a pull request with your changes.
