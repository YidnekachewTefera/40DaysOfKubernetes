# 40DaysOfKubernetes Day09

## Services in Kubernetes

The idea of a Service is to group a set of Pod endpoints into a single resource. You can configure various ways to access the grouping. By default, you get a stable cluster IP address that clients inside the cluster can use to contact Pods in the Service. A client sends a request to the stable IP address, and the request is routed to one of the Pods in the Service.

A Service identifies its member Pods with a selector. For a Pod to be a member of the Service, the Pod must have all of the labels specified in the selector.

## Why use a Kubernetes Service?

In a Kubernetes cluster, each Pod has an internal IP address. But the Pods in a Deployment come and go, and their IP addresses change. So it doesn't make sense to use Pod IP addresses directly. With a Service, you get a stable IP address that lasts for the life of the Service, even as the IP addresses of the member Pods change.

A Service also provides load balancing. Clients call a single, stable IP address, and their requests are balanced across the Pods that are members of the Service.

## Types of Kubernetes Services

ClusterIP (default): Internal clients send requests to a stable internal IP address.

NodePort: Clients send requests to the IP address of a node on one or more nodePort values that are specified by the Service.

LoadBalancer: Clients send requests to the IP address of a network load balancer.

ExternalName: Internal clients use the DNS name of a Service as an alias for an external DNS name.

# NodePort

In Kubernetes, a NodePort is a type of Service that exposes the Service on each Node's IP address at a static port (the NodePort). This makes the Service accessible from outside the Kubernetes cluster. Here are the key points about NodePort Services:

Static Port on Nodes: When you create a NodePort Service, Kubernetes allocates a port from a range (default is 30000-32767) and exposes it on each Node in the cluster. This port is the same across all Nodes.

Accessibility: The Service can be accessed from outside the cluster using the <NodeIP>:<NodePort> combination. This allows external clients to communicate with the Service.

ClusterIP and NodePort: A NodePort Service also creates a ClusterIP Service. The ClusterIP is used for internal communication within the cluster, while the NodePort is used for external communication.

Routing: When traffic is sent to the <NodeIP>:<NodePort>, Kubernetes routes the traffic to one of the Pods backing the Service, effectively load-balancing the incoming requests.

Configuration: You can specify a NodePort value manually in the Service definition, or let Kubernetes allocate one for you from the default port range. Here is an example of how to define a NodePort Service Example:

<pre>
yaml
Copy code
apiVersion: v1
kind: Service
metadata:
  name: my-nodeport-service
spec:
  type: NodePort
  selector:
    app: my-app
  ports:
    - port: 80           # The port that the Service will serve on
      targetPort: 80     # The port on the Pod that the traffic should be directed to
      nodePort: 30007
</pre>

          # The port exposed on each Node (optional)

Use Cases: NodePort Services are useful for exposing applications for development or testing purposes, or in scenarios where external load balancers are not available. However, for production environments, it's often recommended to use LoadBalancer Services or Ingress controllers for more robust and scalable solutions.

### Types of Ports in NodePort

Port (ClusterIP):

This is the port that other Services within the cluster use to communicate with this Service.
Defined as spec.ports.port.
Example: port: 80.
TargetPort:

This is the port on the container (Pod) where the application is listening.
Defined as spec.ports.targetPort.
Example: targetPort: 8080.
This can be the same as or different from the port value.
NodePort:

This is the port on each Node that maps to the Service's port.
Defined as spec.ports.nodePort.
The range for NodePort values is 30000-32767 by default, but this range can be configured in the Kubernetes API server.
Example: nodePort: 30007.

![alt text](image.png)

#### NodePort Demonestration

<pre>
apiVersion: v1
kind: Service
metadata:
  name: nodeport-svc
  labels:
    env: demo
spec:
  type: NodePort
  ports:
    - nodePort: 30001
      port: 80
      targetPort: 80
  selector:
    env: demo

</pre>

run `kubectl apply -f file-name(nodeport in my case).yaml`

after that try to access nginx by searching on your browser using the following URL `localhost:30001`
![alt text](image-1.png)
