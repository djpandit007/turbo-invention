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

## Noteworthy Commands

`kubectl logs -f <pod-name>` will live stream the logs for `<pod-name>`.

`kubectl logs -f <pod-name> <container-name>` will stream logs for `<container-name>`
within `<pod-name>`, if there are multiple containers running in a single pod.
