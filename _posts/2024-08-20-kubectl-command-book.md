---
layout: post
title: kubectl Command Book.
date: 2024-08-20 20:39 -0500
categories: [Kubernetes]
tags: [Kubernetes, CLI]
---
This is my digital command book for  `kubectl` commands to interact with K8s clusters. This is a work in progress and will be updated with more detail + descriptions as I go.

## kubectl command book
Basic commands for managing Kubernetes contexts and configurations.

| Command                          | Description                                            |
|----------------------------------|--------------------------------------------------------|
| `kubectl config get-contexts`      | List all available contexts and show which one is currently active. |
| `kubectl config use-context $context$` | Switch to a different context. |

## Operations
Common operations for managing Kubernetes resources.

| Command                          | Description                                            |
|----------------------------------|--------------------------------------------------------|
| `kubectl apply`                    | Apply a configuration to a resource by file or stdin.  |
| `kubectl create`                   | Create a resource from a file or from stdin.           |
| `kubectl run`                      | Run a particular image on the cluster.                 |
| `kubectl explain`                  | Get documentation for a resource.                      |
| `kubectl get`                      | List one or more resources.                            |
| `kubectl get pods`                 | List all pods in the namespace.                        |
| `kubectl describe`                 | Show detailed information about a resource.            |
| `kubectl exec`                     | Execute a command in a container.                      |
| `kubectl logs`                     | Print the logs for a container in a pod.               |

## Resource Aliases
Shortcuts for commonly used Kubernetes resources.

| Resource  | Alias |
|-----------|-------|
| `nodes`     | `no`    |
| `pods`      | `po`    |
| `services`  | `svc`   |

## Output Options
**Options for formatting the output of kubectl commands.**
| Command | Description |
|---------|-------------|
| `-o wide` | Output additional information. |
| `-o yaml` | Output the resource in YAML format. |
| `-o json` | Output the resource in JSON format. |
| `-o dry-run` | Simulate the command without making any changes. |

**Options for adjusting verbosity in output**
| Verbosity | Description                                                                                                                                                                                                 |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --v=0     | Generally useful for this to ALWAYS be visible to an operator.                                                                                                                                               |
| --v=1     | A reasonable default log level if you don’t want verbosity.                                                                                                                                                  |
| --v=2     | Useful steady state information about the service and important log messages that may correlate to significant changes in the system. This is the recommended default log level for most systems.             |
| --v=3     | Extended information about changes.                                                                                                                                                                          |
| --v=4     | Debug level verbosity.                                                                                                                                                                                       |
| --v=6     | Display requested resources.                                                                                                                                                                                 |
| --v=7     | Display HTTP request headers. Application-Type and User Agent                                                                                                                                               |
| --v=8     | Display HTTP request contents.                                                                                                                                                                               |
| --v=9     | Display HTTP request contents without truncation of contents.                                                                                                                                                |


## Cluster Information
Commands for retrieving information about the Kubernetes cluster and its resources.

| Command                          | Description                                            |
|----------------------------------|--------------------------------------------------------|
| `kubectl cluster-info`             | Display cluster information.                           |
| `kubectl get nodes`                | List all nodes with their status, roles, age, and version. |
| `kubectl get nodes -o wide`        | List all nodes with additional information like IPs and kernel versions. |
| `kubectl get pods`                 | List all pods in the default namespace.                |
| `kubectl get pods --namespace redis` | List all pods in the redis namespace.            |
| `kubectl get all --all-namespaces` | List all resources in all namespaces.                  |
| `kubectl api-resources`            | List all available resource types.                     |
| `kubectl explain pod`              | Show detailed documentation for the pod resource.      |
| `kubectl explain pod.spec`         | Show detailed documentation for the pod spec.          |
| `kubectl explain pod.spec.containers` | Show detailed documentation for the pod containers spec. |
| `kubectl explain pod --recursive`  | Show detailed documentation for the pod resource and all its fields. |

## Node Information
Commands for retrieving detailed information about nodes in the cluster.

| Command                          | Description                                            | Example                                                 |
|----------------------------------|--------------------------------------------------------|---------------------------------------------------------|
| `kubectl describe nodes <node>`  | Show detailed information about a specific node.       | `kubectl describe nodes aks-nodepool1-30702851-vmss000000` |

## Help Commands
Commands for getting help and documentation for kubectl commands.

| Command           | Description                  | Example                |
|-------------------|------------------------------|------------------------|
| `kubectl -h`        | Show help for kubectl.       | `kubectl get -h`         |
| `kubectl create -h` | Show help for the create command. | `kubectl create -h`      |

## Deployment (Imperative)
Commands for creating and managing deployments imperatively.

| Command                          | Description                                            |
|----------------------------------|--------------------------------------------------------|
| `kubectl create deployment nginx --image=nginx` | Create a deployment named nginx with the nginx image. |
| `kubectl run nginx --image=nginx` | Start a pod named nginx with the nginx image. |

## Deployment (Declarative)
Define the desired state in code using a manifest in YAML or JSON, then use `kubectl apply -f deployment.yml`.

| Command                          | Description                                            |
|----------------------------------|--------------------------------------------------------|
| `kubectl apply -f deployment.yml`  | Apply the deployment configuration from a YAML file.   |

## Deploying Resources Imperatively
Commands for creating and managing resources imperatively.

| Command                                      | Description                           |
|----------------------------------------------|---------------------------------------|
| `kubectl create deployment hello-world --image=redis:alpine` | Create a deployment named hello-world with the redis:alpine image. |
| `kubectl run hello-world-pod --image=redis:alpine` | Start a pod named hello-world-pod with the redis:alpine image. |
| `kubectl create deployment hello-world --image=$image --dry-run=client -o yaml > deployment.yaml` | Generate a deployment YAML file without creating the deployment. |
| `kubectl get deployment hello-world`            | List the hello-world deployment.       |
| `kubectl get replicaset`                       | List all ReplicaSets.                  |
| `kubectl describe deployment hello-world`       | Show detailed information about the hello-world deployment. |
| `kubectl describe replicaset hello-world`       | Show detailed information about the hello-world ReplicaSet. |
| `kubectl describe pod hello-world`              | Show detailed information about the hello-world pod. |
| `kubectl expose deployment hello-world --port=80 --target-port=8080` | Expose the hello-world deployment as a service. |
| `kubectl get service hello-world`               | List the hello-world service.          |
| `kubectl describe service hello-world`          | Show detailed information about the hello-world service. |
| `curl http://$SERVICEIP:PORT`                   | Access the hello-world service inside the cluster. |
| `kubectl get endpoints hello-world`             | List the endpoints for the hello-world service. |
| `kubectl get deployment hello-world -o yaml`    | Output the hello-world deployment in YAML format. |
| `kubectl get deployment hello-world -o json`    | Output the hello-world deployment in JSON format. |

## Deployment Declaratively
Commands for creating and managing deployments declaratively.

| Command                                                          | Description                                      |
|------------------------------------------------------------------|--------------------------------------------------|
| `kubectl create deployment hello-world --image=redis:alpine --dry-run=client -o yaml` | Generate a deployment YAML file without creating the deployment. |
| `more deployment.yml`                                               | View the contents of the deployment.yml file.     |
| `kubectl deploy`                                                    | Deploy the resources defined in the YAML files.   |
| `kubectl expose > service.yml`                                      | Generate a service YAML file using the expose command. |
| `kubectl apply -f service.yml`                                      | Apply the service YAML file to create the service. |
| `kubectl get all`                                                   | List all resources including State, Deployment, ReplicaSet, Pod, and Service. |
| `kubectl get service hello-world`                                   | List the hello-world service.                     |
| `kubectl edit deployment hello-world`                               | Edit the hello-world deployment on the fly.       |
| `kubectl scale deployment hello-world --replicas=40`                | Scale the hello-world deployment to 40 replicas.  |
| `kubectl diff -f deployment-new.yaml`                               | Diff that with the current deployment file to narrow down where the changes are. |

## Logs
Commands for retrieving logs from containers and troubleshooting.

| Command                | Description               | Example                             |
|------------------------|---------------------------|-------------------------------------|
| `kubectl logs $podname$` | Print the logs for a specific pod. | `kubectl logs hello-world-pod`        |

```bash
# This is how you can remote into a container.
kubectl exec -it redis -- /bin/sh
hostname
ip addr
exit
```
