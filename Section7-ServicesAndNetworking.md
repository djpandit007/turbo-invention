# Section 7: Services and Networking

## 93: Services

Kubernetes Services enable communication between various components within and outside of the application.

The following are the different types of services:

1. `NodePort`: Listens to a port on the node and forwards request on that port
to a pod on the node running the web application.
2. `ClusterIP`: Creates a virtual IP inside the cluster to enable communication between different services such as a set of front-end servers to a set of back-end servers.
3. `LoadBalancer`: Provisions a load balancer to distribute load across to different web servers in our front end tier.

The port on the pod where the actual web server is running is referred to as the **target port**. This is where the service forwards the request to. If empty, this is assumed to be the same as `port`.

The second port is the port on the service itself. It is simply referred to as the **port**. This should always be mentioned.

Lastly, we have the port on the node itself which we use to access the web server externally and that is known as the **node port**. The default valid range for this is 30,000  to 32,767. If left empty, a value in range is automatically assigned.

## Noteworthy Commands
