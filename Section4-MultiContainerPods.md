# Section 4: Multi-Container Pods

## 70: Multi-Container Pods

Multi-container pods share the same lifecycle which means they are created and
destroyed together. They share the same network space which means they can refer
to each other as local host and they have access to the same storage volumes.

There are different patterns of multi-container pods in Kubernetes:

- Ambassador: Outsourcing DB connection logic so that application always refers
  to a DB at local host and the Ambassador will proxy that request to the right
  database (dev, staging, prod).
- Adapter: Converting logs to a common format before sending it to the central server.
- Sidecar: Deploying a logging agent alongside a web server to collect logs and
  forwarding them to a central log server.
