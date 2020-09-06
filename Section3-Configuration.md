# Section 3: Configuration

## 35: Commands and Arguments in Kubernetes

The `command` field defines the operation/command to run on startup.
The `args` field defines the arguments passed to `command`.

## 42: Environment Variables

To set an environment variable use the `env` property.
`env` property is an array and each item in the array has a `name` and `value` property.
`name` is the name of the environment variable and the `value` is its value.

Shown above directly specifies the environment variables using a key-value pair.
Environment variables can also be set using config maps and secrets.

## 43: Config Maps

Config maps are used to pass configuration data in the form of key-value pairs.
There are 2 phases involved in configuring config maps:

1. Create a `ConfigMap`.
2. Inject them into the pod.

To inject an environment variable into a pod definition,
add a new **list** property called `envFrom`.

## 46: Secrets

Secrets are used to store sensitive information like password or keys.
Similar to a `ConfigMap`, we need to create the secret and inject into a pod.

The `generic` flag used while creating a secret
create a secret from a local file, directory or literal value.

To inject a secret into a pod definition, add a new **list** property called `envFrom`.

If we mount the secret as a volume in the pod, each attribute in the secret is
created as a file with the value of the secret as its content.
These files as stored under the directory `/opt/<secret-name>/`.

## 51: Security Contexts

We can define a set of security standards on a docker container.

These can be configured in Kubernetes as well.
We can configure the security settings at a container level or at a pod level.
Pod level settings will carry over to all the containers within the pod.
If configured at both the pod and the container, the settings on the container
will override the settings on the pod.

## 53: Service Account

There are 2 types of accounts on Kubernetes:

1. User Account: Used by humans

2. Service Account: Used by an application to interact with Kubernetes cluster.
   - Prometheus is used as a service account to pull Kubernetes API for
     performance metrics.
   - An automated build tool like Jenkins uses service accounts to deploy
     applications on the Kubernetes cluster.
   - A `default` service account is automatically created for each namespace.

When a service account is created, it automatically creates a token.
This token must be used by the external application while authenticating
to the Kubernetes API.
The token is stored as a secret object.
Service account of an existing pods cannot be edited.
We must delete and recreate the pod.

When a service account is created, the following things happen:

1. Create service account object.
2. Generate token for service account.
3. Create a secret object and stores the token inside the secret object.
4. Link secret object to the service account.

## 56: Resource Requirements

- Whenever a pod is placed on a node, it consumes resources available to that node.
- Kubernetes scheduler decides which node a pod goes to.
- If the resources requested by a pod aren't available on any pod,
Kubernetes holds back scheduling the pod.
  - The pod will remain in a "pending" state. The pod events will show the reason.

Resource `requests` define the minimum amount of compute resources required.
Resource `limits` define the maximum amount of compute resources allowed.

If the pod tries to go above the defined limits, Kubernetes will throttle the CPU.
If the pod consumes more memory than the limit, Kubernetes will let it do so.
However, if a pod is constantly using more memory than its limit, it'll be terminated.

### Resource Units

G: Gigabyte  | M: Megabyte  | K: Kilobyte

Gi: Gibibyte | Mi: Mebibyte | Ki: Kibibyte

1K  = 1,000 bytes | 1Ki = 1,024 bytes | 1Ki > 1K

## 59: Taints and Tolerations

Taints are applied to nodes. Tolerations are applied to pods.
Both these concepts together help us restrict nodes from accepting certain pods.
Taints and tolerations DO NOT guarantee a pod will end up in a particular node.
When Kubernetes cluster is setup, a taint is set on master node automatically.
This prevents any pods from being scheduled on the master node.
Best practice is to not run any application on the master node.

Taint Effects:

1. `NoSchedule`: Pod won't be scheduled on node. Guaranteed.
2. `PreferNoSchedule`: Pod will TRY not to be scheduled on node. No guarantees.
3. `NoExecute`: New pods won't be scheduled.
   Existing pods will be evicted if they don't tolerate the taint.
   These pods may have been scheduled before the taint was applied.

## Noteworthy Commands

```bash
kubectl create configmap \
  <config-name> --from-literal=<key>=<value> \
                --from-literal=<key_1>=<value_1>
```

will create a config map named `<config-name>`
with a key-value pair of `key: value` and `key_1: value_1`.

```bash
kubectl create configmap
  <config-name> --from-file=<path-to-file>
```

will create a config map named `<config-name>`
and the data from `<path-to-file>` is stored as environment variables.

`kubectl get configmaps` lists all config maps.

`kubectl describe configmaps` lists the configuration data for the config maps.

```bash
kubectl create secret generic \
  <secret-name> --from-literal=<key>=<value>
                --from-literal=<key_1>=<value_1>
```

will create a secret named `<secret-name>`
with a key-value pair of `key: value` and `key_1: value_1`.

```bash
kubectl create secret generic \
  <secret-name> --from-file=<path-to-file>
```

will create a secret name `<secret-name>`
and the data from `<path-to-file>` is read and stored under the name of the file.

`kubectl get secrets` lists all secrets.

`kubectl describe secrets` lists the secret attributes but hides the values.

`kubectl get secret <name> -o yaml` will show the secret definition with the values.

`echo -n '<value>' | base64` will convert `<value>` into base64 encoded string.

`echo -n '<value>' | base64 --decode` will decode the base64 `<value>` into string.

`kubectl exec <pod-name> -- <command>` will run `<command>` in `<pod-name>`.

`kubectl create serviceaccount <name>` will create a service account `<name>`.

`kubectl get serviceaccount` will list all service accounts.

`kubectl taint nodes <node-name> key=value:<taint-effect>`
will apply a taint `<node-name>` with `key=value` pair and `<taint-effect>`.

`kubectl taint nodes <node-name> key=value:<taint-effect>-`
will un-taint `<node-name>` with `key=value` pair and `<taint-effect>`.
Note the `-` sign at the very end of the command. This removes the taint.

`kubectl describe node <node-name> | grep Taint` shows taint applied to `<node-name>`.
