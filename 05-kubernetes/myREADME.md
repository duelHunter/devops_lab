Run this in CMD or PowerShell:
```bash
kubectl version --client
```

You will get, 
```bash
C:\Users\MSI>kubectl version --client
Client Version: v1.32.2
Kustomize Version: v5.5.0
```

If you want to get the client information in YAML format:
```bash
PS D:\devops_lab\05-kubernetes> kubectl version --client --output=yaml
clientVersion:
  buildDate: "2025-02-12T21:26:09Z"
  compiler: gc
  gitCommit: 67a30c0adcf52bd3f56ff0893ce19966be12991f
  gitTreeState: clean
  gitVersion: v1.32.2
  goVersion: go1.23.6
  major: "1"
  minor: "32"
  platform: windows/amd64
kustomizeVersion: v5.5.0
```
Why we need this YAML format?
Suppose you want to extract the version automatically in a script. Then YAML format make it easier.

Start minikube:
```bash
minikube start --driver=docker
```
Minikube will:

1. Create a Docker container for the Kubernetes node.
2. Install the Kubernetes components.
3. Start the control plane.
4. Create or update your kubeconfig.
5. Configure kubectl to use the Minikube cluster.


Check the minikube status:
```bash
PS D:\devops_lab\05-kubernetes> minikube status
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured
```

![Kubernetes cluster architecture](kubernetes-cluster-architecture.svg)


```bash
kubectl get nodes
```
```bash
kubectl get nodes -o wide
```
This displays:

- Internal IP address
- Operating system
- Kernel version
- Container runtime
- Kubernetes version