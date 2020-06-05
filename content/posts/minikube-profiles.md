---
title: "Minikube Profiles"
date: 2020-05-02
categories:
- Dev
tags:
- kubernetes
---

Every new release of Kuberentes introduces many new changes. Some API's graduate into stable, few move into beta from alpha, few gets deprecated and few might be removed.

<!--more-->

For example, here is an excerpt from [kubernetes 1.18 release notes](https://kubernetes.io/blog/2020/03/25/kubernetes-1-18-release-announcement/)

> We’re pleased to announce the delivery of Kubernetes 1.18, our first release of 2020! Kubernetes 1.18 consists of 38 enhancements: 15 enhancements are moving to stable, 11 enhancements in beta, and 12 enhancements in alpha.

Sometimes it really helps to actually login to the cluster and see it for ourselves. This is where [minikube](https://github.com/kubernetes/minikube) [profiles](https://minikube.sigs.k8s.io/docs/commands/profile/) come in handy. They offer a quick way to spin up a specific version of kubernetes or multiple instances. Using which we can use to quickly test or check if some API is avaialable or even compare the behaviour between different versions.

### Start an instance with a profile

These are some example commands to spin up a instance with a specific kubernetes version.

```bash
$ minikube start -p v1.14 --kubernetes-version v1.14.10
$ minikube start -p v1.15 --kubernetes-version v1.15.12
$ minikube start -p v1.16 --kubernetes-version v1.16.10
$ minikube start -p v1.17 --kubernetes-version v1.17.6
$ minikube start -p v1.18 --kubernetes-version v1.18.3
```

* `--kubernetes-version` flag specifies which kubernetes version we want to spin up.
* `-p, --profile` flag is the name for the minikube instance

You can find more kuberetes versions in the [github releases](https://github.com/kubernetes/kubernetes/releases)

### List Profiles

```bash
$ minikube profile list
|---------|-----------|---------|---------------|------|----------------|---------|
| Profile | VM Driver | Runtime |      IP       | Port |    Version     | Status  |
|---------|-----------|---------|---------------|------|----------------|---------|
| v1.14   | hyperkit  | docker  | 192.168.64.16 | 8443 | v1.14.10       | Running |
| v1.15   | hyperkit  | docker  | 192.168.64.15 | 8443 | v1.15.12       | Stopped |
| v1.16   | hyperkit  | docker  | 192.168.64.14 | 8443 | v1.16.10       | Running |
| v1.18   | hyperkit  | docker  | 192.168.64.17 | 8443 | v1.18.3        | Running |
|---------|-----------|---------|---------------|------|----------------|---------|
```

### Switch Profiles

To switch between instances, the minikube profile command can be used to set or switch to a particular profile. This also changes the current kubectl context.

```bash
$ minikube profile v1.15
✅  minikube profile was successfully set to v1.15
$ kubectl config current-context
v1.15
$ minikube profile v1.16
✅  minikube profile was successfully set to v1.16
$ kubectl config current-context
v1.16
```

### Stopping and Deleting Instance

To stop a running instance associated with the profile

```bash
$ minikube stop -p v1.16
```

To delete the local cluster associated with the profile

```bash
$ minikube delete -p v1.16
```

### References

* [Minikube](https://minikube.sigs.k8s.io/docs/)
* [Kuberneres](https://github.com/kubernetes/kubernetes)
