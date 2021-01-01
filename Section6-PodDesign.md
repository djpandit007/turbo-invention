# Section 6: Pod Design

## 82: Labels, Selectors, and Annotations

Labels and selectors are used to group and select objects.
Annotations are used to record other details for information purposes.
For example, details like build version, owner details can be added as annotations.

## Noteworthy Commands

`kubectl get pods --selector app=App1` will show the pods for which are labeled
with `app: App1`.
