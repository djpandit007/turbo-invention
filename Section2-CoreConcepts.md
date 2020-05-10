# 9: Recap - Kubernetes Architecture

## Node
- Machine - Physical or virtual on which k8s is installed
- Worker machine where containers will be launched by k8s
- Previously referred to as Minions.
- Need to have more than one node. Because if your only node fails, our app goes down
### Master Node
- Type of k8s node which is configured as "Master"
- Watches over the nodes in cluster
- Responsible for orchestration of nodes
- Has the kube-apiserver, which makes it the master
- Also has the controller/control manager and scheduler
### Worker Node
- Type of k8s node which is controlled by the master node
- Has the kubelet agent, which makes it the worker

## Cluster
- Number of nodes ground together

---

# 10: Recap - Pods

## Pods
- K8s <ins>**does not**</ins> deploy containers directly on the worker nodes
- Encapsulated within a pod - which is a <ins>single instance</ins> of an application
- Smallest object you can create in k8s
- We don't spin up a new instance of the app within an existing pod. We will create a new pod entirely and bring up our new app instance in it.
- Multiple pods <ins>**can be**</ins> within the same node
- **Pods have a 1:1 relationship with containers running your application**
### Multi-container Pods
- We can have multiple containers within the same pod however, these containers aren't the same. One container will be our app, the other container will be a "helper" container
- All containers within a pod will be killed if a pod goes down.
- This is a rare use case

---

# 12: Recap - Pods with YAML

## YAML Basics
- YAML denotes nesting through indentations
- Adding a hyphen `-` before a line indicates that the line is an element in a list/array

## Commands related to Pods
`kubectl get pods` will give us a list of pods currently available

`kubectl describe pod <pod-name>` will give us more details about a particular pod

`kubectl run nginx` deploys a docker container by creating a pod. First creates a pod automatically and deploys an instance of the `nginx` docker image

---

# 13: Recap - Demo - Creating Pods with YAML