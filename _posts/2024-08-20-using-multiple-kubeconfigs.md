---
title: "Using multiple kubeconfig files"
date: 2024-08-20
---

On a daily basis I'm working with multiple Kuberetes cluster. I also use [Kubernetes tools VSCode extension](https://marketplace.visualstudio.com/items?itemName=ms-kubernetes-tools.vscode-kubernetes-tools). Extension allows to easily change current context from within VSCode.

## Generating common kubeconfig

In order to switch contexts you need to merge multiple kubeconfig files into single yaml file. To do that I have created a script at `/home/guntis/.kube/merge.sh` that looks something like:
```sh
KUBECONFIG=\
~/.kube/abc-test.yaml:\
~/.kube/abc-staging.yaml:\
~/.kube/abc-prod.yaml:\
 kubectl config view --flatten > ~/.kube/config
```

When you run this script it will merge all listed files into one.

Important rule is that each kubeconfig must have unique keys. For example `abc-test.yaml` file would look like this:
```yaml
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JS...ZJQ0FURS0tLS0tCg==
    server: https://kubernetes.docker.internal:6443
  name: abc-test
contexts:
- context:
    cluster: abc-test
    user: abc-test
  name: abc-test
current-context: abc-test
kind: Config
preferences: {}
users:
- name: abc-test
  user:
    client-certificate-data: LS0tLS...S0tCg==
    client-key-data: LS0tL..0tCg==
```

## Switch contexts using VSCode
![VScode Kubernetes extension](/assets/k8s-contexts.png)

## Switch contexts using k9s

K9s is super convenvient utility that also allows switching contexts, by typing `:ctx` command.
![K9s contexts](/assets/k9s-contexts.png)