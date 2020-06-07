# Section 2: Core Concepts

## 9: Recap - Kubernetes Architecture

### Node

- Machine - Physical or virtual on which k8s is installed
- Worker machine where containers will be launched by k8s
- Previously referred to as Minions.
- Need to have more than one node. If your only node fails, our app goes down

#### Master Node

- Type of k8s node which is configured as "Master"
- Watches over the nodes in cluster
- Responsible for orchestration of nodes
- Has the kube-apiserver, which makes it the master
- Also has the controller/control manager and scheduler

#### Worker Node

- Type of k8s node which is controlled by the master node
- Has the kubelet agent, which makes it the worker

### Cluster

- Number of nodes ground together

---

## 10: Recap - Pods

### Pods

- K8s **does not** deploy containers directly on the worker nodes
- Encapsulated within a pod - which is a single instance of an application
- Smallest object you can create in k8s
- We don't spin up a new instance of the app within an existing pod.
  - We will create a new pod entirely and bring up our new app instance in it.
- Multiple pods **can be** within the same node
- **Pods have a 1:1 relationship with containers running your application**

#### Multi-container Pods

- We can have multiple containers within the same pod
  - However, these containers aren't the same.
  - One container will be our app, the other container will be a "helper" container
- All containers within a pod will be killed if a pod goes down.
- This is a rare use case

---

## 12: Recap - Pods with YAML

### YAML Basics

- YAML denotes nesting through indentations
- Adding a hyphen `-` before a line indicates that the line is an element in a list/array

### Commands related to Pods

`kubectl get pods` will give us a list of pods currently available

`kubectl describe pod <pod-name>` will give us more details about a particular pod

`kubectl run nginx` deploys a docker container by creating a pod.
First creates a pod automatically and deploys an instance of the `nginx` docker image

---

## 18: Practice Test - Pods

`kubectl get pods -o wide` gives us slightly more information about the pods

`kubectl delete pod <pod-name>` deletes the pod with name `<pod-name>`

`kubectl create -f <filename>` creates `kind` specified in the `<filename>`

`kubectl apply -f <filename>` updates existing `kind` and applies changes

`kubectl edit pod <pod-name>` edits `<pod-name>` config.
Changes are applied on file save/exit

`kubectl get pod <pod-name> -o yaml > pod-definition.yaml` extracts definition.
`<pod-name>` pod YAML definition will be extracted into `pod-definition.yaml`

[YAML file used](labs/18-redis.yml)

---

## 21: Recap - ReplicaSets

**Replica Set** allows us to have High Availability.
It is also used for Load Balancing and Scaling.

ReplicaSet MUST have a `selector` definition (required).
`selector` definition helps identify which pods fall under a replica set.
This is important because ReplicaSet can also manage pods which were not
created as part of the replica set creation.
Replica set uses labels and selectors to determine which pods to monitor.

ReplicationController does not need this (optional).

### Commands

`kubectl get replicaset` gives us a list of replica sets currently available.

`kubectl delete replicaset myapp-replicaset` deletes the replica set.
It will also delete all underlying Pods.

`kubectl replace -f <filename>` will replace/update `kind` specified in `filename`

`kubectl scale --replicas=<number> -f <filename>`
will scale `kind` specified in `filename`.
This will scale the `kind` from the command line without changing the contents
of `filename`.

---

## 22: Recap - Deployments

Pod deploys a single instance of our application.
Container is encapsulated in a pod.
Multiple pods are deployed using replication controller/replica set.
**Deployment** is a Kubernetes object that comes higher in this hierarchy.

Deployment provides us the capability to upgrade underlying instances seamlessly.
Deployment YAML file is similar to the Replica Set definition file.
Only the `kind` needs to be changed to `Deployment`.
