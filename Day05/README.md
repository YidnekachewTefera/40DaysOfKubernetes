# Kubernetes Architecture

Kubernetes is a powerful open-source platform designed for automating the deployment, scaling, and operation of application containers.

There are 2 types of nodes in Kubernetes which are the Master(Controller) nodes and the Worker nodes.

## Master(Controller) node:

Them master node mainly contain four components that are tasked for administrating the cluster, they provide instructions to the worker nodes, these are:

### I. API Server

Acts as the front-end for the Kubernetes control plane.
Exposes the Kubernetes API.
Interacts with etcd to read and write cluster data.
Handles REST operations and provides the interface for all the other components to interact.
It is the main entry point inside the cluster.

### II. etcd

A consistent and highly-available key-value store used as Kubernetes’ backing store for all cluster data.
Stores the configuration data and the state of the cluster.

### III. Controller Manager

Runs controllers, which are background threads that handle routine tasks.
Includes various controllers such as Node Controller, Replication Controller, Endpoints Controller, and Service Account & Token Controllers.
It ensures all the controllers are running properly, and everything is monitored.

### IV. Scheduler

Assigns nodes to newly created pods.
Considers resource requirements, policy constraints, and other factors when making scheduling decisions.

## 2. Worker Node Components:

They are Virtual Machines these could be VPS or any Virtual machines on the Cloud, it is the place where all the actual works happening such as running pods which encapsulate a list of containers, you may have a single or multiple containers encapsulated inside a Pod.

### I. Kubelet

An agent that runs on each node in the cluster.
Ensures that containers are running in a Pod.
Takes a set of PodSpecs and ensures that the described containers are running and healthy.
it receives instructions from master node through api server and ensure the instructions are applied on the worker node. and based on the response API server will update the etcd about the status of cluster.

### II. Kube-proxy

Maintains network rules on nodes.
it creates a route table
It is also responsible for maintaining Pod-to-Pod relation.
Facilitates network communication inside the cluster by forwarding requests to the correct Pod across different nodes.

### III. Container Runtime

The software responsible for running containers.
Examples include Docker, containerd, and CRI-O.

## 2. Additional Components

### A. Pod:

The smallest and simplest Kubernetes object.
Represents a single instance of a running process in the cluster.
Can contain one or more containers.
Containers within a pod share the same IP address and port space and can communicate with each other using localhost.

### B. Service:

An abstract way to expose an application running on a set of Pods as a network service.
Can be of several types: ClusterIP, NodePort, LoadBalancer, and ExternalName.

### C. ConfigMap and Secret:

ConfigMap: Used to store non-confidential configuration data in key-value pairs.
Secret: Used to store and manage sensitive information, such as passwords, OAuth tokens, and SSH keys.

### D. Deployment:

Provides declarative updates to applications.
Manages the creation and scaling of Pods.
Can roll out changes and roll back to previous versions if necessary.

### E. ReplicaSet:

Ensures that a specified number of pod replicas are running at any given time.
A Deployment is used to manage ReplicaSets.

### F. StatefulSet:

Manages the deployment and scaling of a set of Pods with unique, persistent identities and stable hostnames.

### G. DaemonSet:

Ensures that a copy of a Pod runs on all or some of the nodes in the cluster.

### H. Job and CronJob:

#### Job: Creates one or more Pods and ensures that a specified number of them successfully terminate.

#### CronJob: Creates Jobs on a time-based schedule.

### I. Ingress:

Manages external access to the services in a cluster, typically HTTP.
Provides load balancing, SSL termination, and name-based virtual hosting.
These components work together to provide a robust platform for container orchestration, making it easier to manage and scale applications.
