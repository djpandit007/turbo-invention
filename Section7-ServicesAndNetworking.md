# Section 7: Services and Networking

## 93: Services

Kubernetes Services enable communication between various components
within and outside of the application.

The following are the different types of services:

1. `NodePort`: Listens to a port on the node and forwards request on that port
to a pod on the node running the web application.
2. `ClusterIP`: Creates a virtual IP inside the cluster to enable communication
between different services such as front-end and back-end servers.
3. `LoadBalancer`: Provisions a load balancer to distribute load across to
different web servers in our front end tier.

The port on the pod where the actual web server is running is referred to as
the **target port**. This is where the service forwards the request to.
If empty, this is assumed to be the same as `port`.

The second port is the port on the service itself. It is simply referred to as
the **port**. This should always be mentioned.

Lastly, we have the port on the node itself which we use to access the web server
externally and that is known as the **node port**.
The default valid range for this is 30,000  to 32,767.
If left empty, a value in range is automatically assigned.

## 94: Services - Cluster IP

`ClusterIP` service allows us to group the pods together and provide a single
interface to access the pods in a group. The service allows each layer to scale
or move as required without impacting communication between the various services.
Each service gets an IP and name assigned to it inside the cluster and
that is the name that should be used by other pods to access the service.

## 97: Ingress Networking

_**Kubernetes cluster does not come with an Ingress controller by default.**_

Ingress helps users access our application using a single externally accessible URL
that we can configure to route to different services within our cluster
based on that URL path.
Ingress can implement SSL security as well.
Simply put Ingress is a layer 7 load balancer built in to the Kubernetes cluster
that can be configured using native Kubernetes primitives.
Ingress controllers have additional intelligence built into them to monitor the
the Kubernetes cluster for ingress resources and configure the underlying
NGINX server when something has changed.

## 103: Network Policies

One of the prerequisites for networking in Kubernetes is, whatever solution we implement,
the pods should be able to communicate with each other without having to configure
any additional settings like routes.
Kubernetes is configured by default with an **"All Allow"** rule that allows traffic
from any pod to any other pod or services within the cluster.

## Noteworthy Commands
