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
