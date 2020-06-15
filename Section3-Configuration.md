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

## 41: Secrets

Secrets are used to store sensitive information like password or keys.
Similar to a `ConfigMap`, we need to create the secret and inject into a pod.

The `generic` flag used while creating a secret
create a secret from a local file, directory or literal value.

To inject a secret into a pod definition, add a new **list** property called `envFrom`.

If we mount the secret as a volume in the pod, each attribute in the secret is
created as a file with the value of the secret as its content.
These files as stored under the directory `/opt/<secret-name>/`.

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
