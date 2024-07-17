# Pods and YAML

Pod is the smallest and simplest unit in the Kubernetes object model that you can create or deploy. A Pod represents a single instance of a running process in your cluster and can contain one or more containers, such as Docker containers. Pods provide an environment for running containers, and they are designed to run a single application.

A Pod can encapsulate an application composed of multiple co-located containers that are tightly coupled and need to share resources.

Most commonly, Pods contain a single container, but they can include multiple containers that need to work together. These containers can share the same network namespace and storage volumes.

Containers in a Pod share an IP address and port space, which allows them to communicate with each other using localhost.

Containers can also share storage volumes, making it easy to share data between containers in the same Pod.

Pods are ephemeral. They are created, destroyed, and re-created as needed. When a Pod is terminated, it cannot be brought back; instead, a new Pod with a new UID is created.

Pods can be managed and orchestrated by higher-level Kubernetes objects like Deployments, StatefulSets, and DaemonSets, which handle the creation, scaling, and management of Pods.

Pods can be defined in imperative or declarative way using YAML or JSON configuration files. A typical declarative Pod configuration includes information about the containers it runs, their resource requirements, environment variables, and volume mounts.

The imperative definition of Pods involves using command-line instructions to directly create and manage Pods, rather than defining their desired state in a configuration file. This approach focuses on issuing commands to perform actions immediately.

A declarative definition of a Pod is a YAML (or JSON) file that specifies the desired state of the Pod. The Kubernetes control plane ensures that the actual state of the Pod matches this desired state. The declarative approach focuses on what the final state should be, rather than the steps to get there.

use the following syntax to create a pod using a Declarative definition

`kubectl run pod-name --image=image:image-tag`

### Use Cases for Pods:

Single Application Instance: Running a single instance of an application or microservice.
Sidecar Containers: Deploying auxiliary containers that enhance or add functionality to the main application container, such as logging, monitoring, or proxying.
Initialization: Using init containers to set up the environment before the main application containers start.
Tightly Coupled Applications: Running multiple tightly coupled applications or processes that need to share resources and communicate efficiently.

## Creating a pod with Declarative Definition
