# Section 5: Observability

## 73: Readiness and Liveness Probes

A pod is said to be ready once all the required images have been pulled.
This can be misleading as the app itself may take some time to start.
So the Ready condition is just a check of the pod status and
may not tell us the true state of our application.
Thus, it is important for developers to define Readiness Probes,
which tie into the state of the application.

## 74: Liveness

Let's say our application is stuck in an infinite loop due to a bug in our code.
The container is up but the users are seeing errors. Container needs to be restarted.
This is where Liveness probes can help us. Liveness probe can be configured on the
container to periodically test whether the application within the container is healthy.

## 76: Container Logging

Once a pod is running, we can see the logs it generates.
If there are multiple containers running inside a single pod, we should specify
the name of the container for which we want to see the logs.

## 79: Monitor and Debug Applications

Heapster enabled monitoring and analysis features for Kubernetes. It is deprecated.
Metric Server is a slimmed down version of Heapster.
You can have one metric server per Kubernetes cluster.
The Metrics Server retrieves metrics from each of the Kubernetes nodes and pods,
aggregates them and store them **_in memory_**.
Being an in-memory monitoring solution, we cannot see historical performance data.

Kubernetes runs an agent on each node known as the kubelet which is responsible
for receiving instructions from the kubernetes API Master server and running Pods
on the nodes. The Kubelet also contains a sub-component known as the cAdvisor or
Container Advisor. cAdvisor is responsible for retrieving performance metrics
from pods and exposing them through the kubelet API to meet the metrics available
for the metrics server.

## Noteworthy Commands

`kubectl logs -f <pod-name>` will live stream the logs for `<pod-name>`.

`kubectl logs -f <pod-name> <container-name>` will stream logs for `<container-name>`
within `<pod-name>`, if there are multiple containers running in a single pod.

`kubectl top node` provides CPU and memory usage of each node.

`kubectl top pod` provides CPU and memory usage of each pod.
