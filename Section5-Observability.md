# Section 5: Observability

## 73: Readiness and Liveness Probes

A pod is said to be ready once all the required images have been pulled.
This can be misleading as the app itself may take some time to start.
So the Ready condition is just a check of the pod status and
may not tell us the true state of our application.
Thus, it is important for developers to define Readiness Probes,
which tie into the state of the application.

## Noteworthy Commands
