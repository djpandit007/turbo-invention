# Section 3: Configuration

## 35: Commands and Arguments in Kubernetes

The `command` field defines the operation/command to run on startup.
The `args` field defines the arguments passed to `command`.

## 38: Environment Variables

To set an environment variable use the `env` property.
`env` property is an array and each item in the array has a `name` and `value` property.
`name` is the name of the environment variable and the `value` is its value.

Shown above directly specifies the environment variables using a key-value pair.
Environment variables can also be set using config maps and secrets.

## 39: Config Maps

Config maps are used to pass configuration data in the form of key-value pairs.
There are 2 phases involved in configuring config maps:

1. Create a `ConfigMap`.
2. Inject them into the pod.

To inject an environment variable into a pod definition,
add a new **list** property called `envFrom`.

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
