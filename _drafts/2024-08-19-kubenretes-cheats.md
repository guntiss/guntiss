---
title: "Kubernetes cheats"
date: 2024-08-19
---

This article will be collection of my Kubernetes shortcuts.

### Dlete namespace stuck in terminating phase
```
sdh
for ns in $(kubectl get ns --field-selector status.phase=Terminating -o jsonpath='{.items[*].metadata.name}')
do
  kubectl get ns $ns -ojson | jq '.spec.finalizers = []' | kubectl replace --raw "/api/v1/namespaces/$ns/finalize" -f -
done

for ns in $(kubectl get ns --field-selector status.phase=Terminating -o jsonpath='{.items[*].metadata.name}')
do
  kubectl get ns $ns -ojson | jq '.metadata.finalizers = []' | kubectl replace --raw "/api/v1/namespaces/$ns/finalize" -f -
done
```

### Sanitize (Remove not running pods)
```
kubectl get pods -A | grep -E 'ImagePullBackOff|ErrImagePull|Evicted|Error|Completed|OOMKilled|ContainerStatusUnknown' | awk '{print $2 " --namespace=" $1}' | xargs -n2 -t kubectl delete pod
```