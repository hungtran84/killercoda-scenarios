# Create Kubernetes Privileged Pod

In this example we will create a simple pod using centos image with all the privilege and Linux Capabilities

- Create privileged pod

```
cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Pod
metadata:
  name: privileged-pod
  namespace: default
spec:
  containers:
  - name: centos
    image: centos
    command: ['sh', '-c', 'sleep 999']
    securityContext:
       privileged: true
EOF
```

- Polaris blocked pod creation

```
Error from server (
Polaris prevented this deployment due to configuration problems:
- Container centos: Should not be allowed to run as root
- Container centos: Image tag should be specified
- Container centos: Privilege escalation should not be allowed
- Container centos: Should not be running as privileged
): error when creating "STDIN": admission webhook "polaris.fairwinds.com" denied the request: 
Polaris prevented this deployment due to configuration problems:
- Container centos: Should not be allowed to run as root
- Container centos: Image tag should be specified
- Container centos: Privilege escalation should not be allowed
- Container centos: Should not be running as privileged
```

- Let modify the pod manifest to meet security baseline

```
cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Pod
metadata:
  name: privileged-pod
  namespace: default
spec:
  containers:
  - name: centos
    image: centos:7
    command: ['sh', '-c', 'sleep 999']
    securityContext:
      privileged: false # disallow running as privileged
      allowPrivilegeEscalation: false # disallow privilege escalation
      runAsUser: 1000 # Run containter as non-root user
EOF
```
