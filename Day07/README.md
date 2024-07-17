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

## Creating a pod with Imperative Definition
`kubectl run nginx-pod --image=nginx:latest`

![image](https://github.com/user-attachments/assets/917dd254-68d4-4529-914c-2bc152b46b16)

Getting the status of the pods

`kubectl get pods`
![image](https://github.com/user-attachments/assets/2587ec44-600b-4dd8-98dc-1c40b0a9f094)


as you can see from the image the status of the pod is on creating the container stage, after completing creating the container the status will change to running.
![image](https://github.com/user-attachments/assets/e07b0586-955d-40d5-91be-bae3473a09e1)

### Deleting a pod 
`kubectl delete pod nginx-pod`
![image](https://github.com/user-attachments/assets/86a12209-432b-450f-936d-1200fbd62ac6)

## Creating a pod with Declarative Definition
use the following sample manifest to create a pod named nginx-pod

<pre>
  apiVersion: v1
  kind: Pod
  metadata:
    name: nginx-pod
    labels: 
      env: demo
      type: frontend
  spec:
    containers:
    - name: nginx-container
      image: nginx:
      ports:
      - containerPort: 80
</pre>
save this file as Yaml using `.yaml or .yml` extension.
go the the directory where you saved the file and open your terminal there then run the following command
`kubectl apply -f the-file-name.yaml or yml`
`kubectl apply -f nginx-pod.yaml`
![image](https://github.com/user-attachments/assets/2f57ded3-07f2-4c90-98f7-c4ad57226d37)

you can edit the configuration if you are facing an error with your pod by using the following command:
`kubectl edit pod pod-name`
`kubectl edit pod nginx-pod`

![image](https://github.com/user-attachments/assets/6e9442af-4a16-471f-ac31-258b2fc42a54)

If we want to run commands inside the pod we can use the following command
`kubectl exec -it nginx-pod -- sh`
![image](https://github.com/user-attachments/assets/66c388ec-ff4c-4f1f-af96-b3d163fe9c4d)

## Retriving a Declarative definition from an Imperative definition

### Dry Run
Dry Run is a feature provided by the kubectl command-line tool that allows you to simulate the application of a configuration file (usually YAML or JSON) without actually creating or modifying any resources in the cluster. This is particularly useful for testing and verifying Kubernetes resource configurations before applying them.

use the follwoing command to retrive the yaml file from the dry command:
`kubectl run nginx --image=nginx --dry-run=client -o yaml`
![image](https://github.com/user-attachments/assets/98fe00b7-623a-429a-b0eb-8de1c7e45004)
now you can edit and confgiure the yaml.
and If you want to redirect the output to a new file use the following command:
`kubectl run nginx --image=nginx --dry-run=client -o yaml > new-pod-manifest.yaml `
![image](https://github.com/user-attachments/assets/6598d434-db3f-4eff-a2a7-93882a01f632)

If you want to see details of the pod that is running, such as in which node it is raining and more, you can use the following command:
`kubectl describe pod nginx-pod`

![image](https://github.com/user-attachments/assets/5d644a71-610b-4ad1-a94f-7442fb26c80e)


If you want to see the labels:
`kubectl get pods nginx-pod --show-labels`
![image](https://github.com/user-attachments/assets/8d2d174d-9b27-492a-aa88-c1e40f526f31)

Task 3:
Apply the below YAML and fix the errors, including all the commands that you run during the troubleshooting and the error message

<pre>
apiVersion: v1
kind: Pod
metadata:
  labels:
    app: test
  name: redis
spec:
  containers:
  - image: rediss
    name: redis
</pre>  
to solve the issue with the above manifest
first apply the configuration:
`kubectl apply -f task3.yaml`
![image](https://github.com/user-attachments/assets/ace582cd-f186-4b2f-85ff-ebd1cd4a937e)
second se the details of the pod :
`kubectl describe pod redis`
![image](https://github.com/user-attachments/assets/f4c72b4f-df4d-4cc1-b8f6-8825d29ed152)
from the events we can see that there is a warning describing failure to pull an image, from this we have to check the image.
to edit and see the configuration of the image we can use the following command:
`kubectl edit pod redit`
![image](https://github.com/user-attachments/assets/1a71b892-cc1a-4142-ad09-03cb5c0af464)
as you can see from the image name "redis is with s double 'rediss' " so edit that to 'redis' and save it.
now by running the following command we can see the details of the pod:
`kubectl describe pod redis`
![image](https://github.com/user-attachments/assets/f8cdd469-147d-45d6-8fdc-78cde70e1c77)

Thank you very much
