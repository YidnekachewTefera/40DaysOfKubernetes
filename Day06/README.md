# Day 06 setting up K8s cluster using kind

Kind is a tool for running local Kubernetes clusters using Docker container nodes. It is primarily designed for testing Kubernetes itself, but it can also be used for local development and Continuous Integration (CI) workflows.

## Installation

pre-request
I. Ensure that you have docker installed on your machine and it is running.

II. Ensure you have chocolate installed on your windows system

2. Install Kind using a package manager

run the following command to install:

`choco install kind`

## Creating a Cluster

use the following syntax to create a cluster
`kind create cluster --name <cluster-name> --config <config-file> --image <image-name>`

The configuration file will contain the desired setup state of our cluster for example we can use the following the following command to create a k8s cluster that will have one master node and 2 worker nodes.

the config.yaml file looks as follows:

<pre>
```
```
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker
```
``` 
</pre>

`kind create cluster --image kindest/node:v1.30.0@sha256:047357ac0cfea04663786a612ba1eaba9702bef25227a794b52890dd8bcd692e --name cka1-cluster2 --config confnode:v1.30.0@sha256:047357ac0cfea04663786a612ba1eaba9702bef25227a794b52890dd8bcd692e --name day06-cluster2 --config config.yaml`

## Install Kubectl

Kubectl is the command-line tool for interacting with Kubernetes clusters. It allows users to manage and deploy applications, inspect and manage cluster resources, and view logs. Essentially, kubectl is the interface through which users interact with Kubernetes clusters to perform various tasks.

use Chocolate package manager for installing kubectl on windows

`choco install kubernetes-cli`

The following link contains cheat-sheet for kubectl commands https://spacelift.io/blog/kubernetes-cheat-sheet

### A, getting all the nodes

`kubectl get nodes`

### B, Listing all the clusters

`kubectl config get-contexts`

### C, Switching between

`kubectl config use-context cluster-name`

Thank you very much !!!
