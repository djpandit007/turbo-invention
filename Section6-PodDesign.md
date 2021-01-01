# Section 6: Pod Design

## 82: Labels, Selectors, and Annotations

Labels and selectors are used to group and select objects.
Annotations are used to record other details for information purposes.
For example, details like build version, owner details can be added as annotations.

## 85: Rolling Updates and Rollbacks in Deployments

There are 2 types of deployment strategies:

1. Recreate - Destroy all old versions and then create new versions.
This means there's some downtime involved. This isn't the default strategy.

2. Rolling Update - Create new version then take down old version, one by one.
This is the default deployment strategy.

## Noteworthy Commands

`kubectl get pods --selector app=App1` will show the pods for which are labeled
with `app: App1`.

`kubectl get pods --selector app=App1,env=prod` will show the pods for which are
labeled with `app: App1` AND `env=prod`.

`kubectl rollout status <deployment-name>` will show the status of the rollout
for the deployment named `<deployment-name>`.

`kubectl rollout history <deployment-name>` will show the history and revisions
of the deployment named `<deployment-name>`.

`kubectl rollout undo <deployment-name>` will revert the deployment named `<deployment-name>`
to its previous version.

`kubectl run <deployment-name> --image=<image-name>` will imperatively create a deployment
called `<deployment-name>` with the image specified in `<image-name>`.
Using a definition file is recommended approach.
