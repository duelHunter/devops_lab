# Phase 1: Kubernetes Foundations

## Why Kubernetes Exists

Running containers manually becomes difficult when an application grows.

Without Kubernetes, engineers must manually:

- Restart failed containers.
- Scale applications.
- manage container networking.
- Perform application updates.
- Balance traffic.
- Manage configuration.
- Manage persistent data.

Kubernetes automates these tasks using a desired-state model.

## Core Idea: Desired State

I describe what I want:

```text
Run three copies of my API.
```

Kubernetes continuously works to maintain that state:

```text
Desired replicas: 3
Running replicas: 3
```

If one Pod fails, Kubernetes creates a replacement.

## Architecture

```text
Kubernetes Cluster
│
├── Control Plane
│   ├── API Server
│   ├── Scheduler
│   ├── Controller Manager
│   └── etcd
│
└── Worker Nodes
    ├── kubelet
    ├── container runtime
    ├── kube-proxy
    └── application Pods
```

## Control Plane Components

### API Server

The main entry point for Kubernetes commands and API requests.

### Scheduler

Selects a suitable worker node for each new Pod.

### Controller Manager

Continuously checks whether the current cluster state matches the desired state.

### etcd

Stores Kubernetes cluster configuration and state.

## Worker Node Components

### kubelet

Ensures that the containers assigned to a node are running.

### Container Runtime

Runs containers. A common runtime is `containerd`.

### kube-proxy

Supports Kubernetes networking and Service traffic.

## Learning Checklist

- [ ] Explain why Kubernetes is used.
- [ ] Explain desired state.
- [ ] Explain the difference between the control plane and worker nodes.
- [ ] Explain the purpose of the API Server.
- [ ] Explain the purpose of the Scheduler.
- [ ] Explain the purpose of etcd.
- [ ] Explain the purpose of kubelet.

---

# Phase 2: Local Kubernetes Environment

Use a local Kubernetes cluster before moving to a managed cloud service.

Recommended options:

- Minikube
- Kind
- Docker Desktop Kubernetes

## Required Tools

- [ ] Docker
- [ ] kubectl
- [ ] Minikube or Kind

## Verify kubectl

```bash
kubectl version --client
```

## Start Minikube

```bash
minikube start
```

Verify the cluster:

```bash
kubectl get nodes
kubectl cluster-info
```

Expected node status:

```text
Ready
```

## Useful kubectl Commands

```bash
kubectl get nodes
kubectl get pods
kubectl get deployments
kubectl get services
kubectl get all
kubectl api-resources
```

## Practice Task

- [ ] Install `kubectl`.
- [ ] Install Minikube or Kind.
- [ ] Start a local cluster.
- [ ] Confirm that the node is ready.
- [ ] Explore the available Kubernetes resources.

---

# Phase 3: Pods

A Pod is the smallest deployable unit in Kubernetes.

A Pod normally contains one main application container, although it can contain multiple closely related containers.

## Create a Pod

Create `kubernetes/pods/nginx-pod.yaml`:

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: nginx-pod
  labels:
    app: nginx

spec:
  containers:
    - name: nginx
      image: nginx:alpine
      ports:
        - containerPort: 80
```

Apply it:

```bash
kubectl apply -f kubernetes/pods/nginx-pod.yaml
```

Check it:

```bash
kubectl get pods
kubectl get pods -o wide
kubectl describe pod nginx-pod
```

View logs:

```bash
kubectl logs nginx-pod
```

Open a shell inside the container:

```bash
kubectl exec -it nginx-pod -- sh
```

Delete the Pod:

```bash
kubectl delete -f kubernetes/pods/nginx-pod.yaml
```

## Pod Concepts

- [ ] Pod lifecycle.
- [ ] Pod labels.
- [ ] Container ports.
- [ ] Pod logs.
- [ ] Commands and arguments.
- [ ] Environment variables.
- [ ] Resource requests and limits.
- [ ] Liveness probes.
- [ ] Readiness probes.

## Resource Requests and Limits

```yaml
resources:
  requests:
    memory: "64Mi"
    cpu: "100m"
  limits:
    memory: "128Mi"
    cpu: "250m"
```

## Health Checks

```yaml
livenessProbe:
  httpGet:
    path: /health
    port: 8000
  initialDelaySeconds: 10
  periodSeconds: 10

readinessProbe:
  httpGet:
    path: /health
    port: 8000
  initialDelaySeconds: 5
  periodSeconds: 5
```

## Practice Task

Deploy the Dockerized FastAPI application as a Pod.

- [ ] Build the FastAPI image.
- [ ] Make the image available to the local cluster.
- [ ] Create the Pod manifest.
- [ ] Add labels.
- [ ] Add resource requests and limits.
- [ ] Add readiness and liveness probes.
- [ ] Check the logs.
- [ ] Enter the container using `kubectl exec`.

---

# Phase 4: Deployments

Pods are temporary. A Deployment manages Pods and maintains the required number of replicas.

## Create a Deployment

Create `kubernetes/deployments/api-deployment.yaml`:

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: ai-api-deployment

spec:
  replicas: 3

  selector:
    matchLabels:
      app: ai-api

  template:
    metadata:
      labels:
        app: ai-api

    spec:
      containers:
        - name: ai-api
          image: my-ai-api:v1
          ports:
            - containerPort: 8000

          resources:
            requests:
              memory: "128Mi"
              cpu: "100m"
            limits:
              memory: "256Mi"
              cpu: "500m"
```

Apply it:

```bash
kubectl apply -f kubernetes/deployments/api-deployment.yaml
```

Check the Deployment:

```bash
kubectl get deployments
kubectl get replicasets
kubectl get pods
```

Scale it:

```bash
kubectl scale deployment ai-api-deployment --replicas=5
```

Check rollout status:

```bash
kubectl rollout status deployment/ai-api-deployment
```

View rollout history:

```bash
kubectl rollout history deployment/ai-api-deployment
```

Undo an update:

```bash
kubectl rollout undo deployment/ai-api-deployment
```

## Deployment Concepts

- [ ] ReplicaSets.
- [ ] Desired replicas.
- [ ] Self-healing.
- [ ] Scaling.
- [ ] Rolling updates.
- [ ] Rollbacks.
- [ ] Image versions.
- [ ] Deployment strategies.

## Practice Task

- [ ] Deploy three API replicas.
- [ ] Delete one Pod manually.
- [ ] Observe Kubernetes recreate it.
- [ ] Scale the Deployment to five replicas.
- [ ] Update the application image.
- [ ] Observe the rolling update.
- [ ] Roll back to the previous version.

---

# Phase 5: Services and Networking

Pod IP addresses can change. A Service provides a stable network endpoint for a group of Pods.

## Service Types

### ClusterIP

Exposes an application inside the cluster.

### NodePort

Exposes an application using a port on each cluster node.

### LoadBalancer

Requests an external cloud load balancer when supported.

## Create a ClusterIP Service

Create `kubernetes/services/api-service.yaml`:

```yaml
apiVersion: v1
kind: Service

metadata:
  name: ai-api-service

spec:
  selector:
    app: ai-api

  ports:
    - protocol: TCP
      port: 80
      targetPort: 8000

  type: ClusterIP
```

Apply it:

```bash
kubectl apply -f kubernetes/services/api-service.yaml
```

Check Services:

```bash
kubectl get services
kubectl describe service ai-api-service
kubectl get endpoints
```

Access the Service locally:

```bash
kubectl port-forward service/ai-api-service 8080:80
```

Test it:

```bash
curl http://localhost:8080/health
```

## Important Networking Concepts

- [ ] Pod-to-Pod communication.
- [ ] Service discovery.
- [ ] DNS names.
- [ ] Selectors and labels.
- [ ] Service ports.
- [ ] Target ports.
- [ ] ClusterIP.
- [ ] NodePort.
- [ ] LoadBalancer.

## Practice Task

- [ ] Expose the API Deployment using ClusterIP.
- [ ] Access it using port forwarding.
- [ ] Create a temporary Pod.
- [ ] Call the Service using its DNS name from inside the cluster.
- [ ] Change the Service to NodePort.
- [ ] Observe how the access method changes.

Temporary test Pod:

```bash
kubectl run curl-test \
  --image=curlimages/curl \
  --restart=Never \
  -it --rm \
  -- curl http://ai-api-service/health
```

---

# Phase 6: ConfigMaps and Secrets

Application configuration should not be hardcoded into container images.

## ConfigMap

Use ConfigMaps for non-sensitive configuration.

Examples:

```text
APP_ENV=development
LOG_LEVEL=info
MODEL_NAME=small-model
```

Create `kubernetes/config/configmap.yaml`:

```yaml
apiVersion: v1
kind: ConfigMap

metadata:
  name: ai-api-config

data:
  APP_ENV: development
  LOG_LEVEL: info
  MODEL_NAME: small-model
```

Use it in a Deployment:

```yaml
envFrom:
  - configMapRef:
      name: ai-api-config
```

## Secret

Use Secrets for sensitive values.

Examples:

```text
DATABASE_PASSWORD
API_KEY
JWT_SECRET
```

Create a Secret from the command line:

```bash
kubectl create secret generic ai-api-secret \
  --from-literal=API_KEY=replace-me
```

Use it in a Deployment:

```yaml
envFrom:
  - secretRef:
      name: ai-api-secret
```

Read a Secret:

```bash
kubectl get secret ai-api-secret
kubectl describe secret ai-api-secret
```

## Security Note

Kubernetes Secrets should not be committed to a public repository in plain text.

Use one of these approaches in real projects:

- Environment-specific secret management.
- A cloud secret manager.
- Sealed Secrets.
- External Secrets Operator.
- A private CI/CD secret store.

## Practice Task

- [ ] Move application configuration into a ConfigMap.
- [ ] Move an API key into a Secret.
- [ ] Inject both into the Deployment.
- [ ] Read them inside the running Pod.
- [ ] Add secret files to `.gitignore`.

---

# Phase 7: Persistent Storage

Containers and Pods are temporary. Persistent storage keeps data after a Pod is restarted or replaced.

## Storage Concepts

- PersistentVolume
- PersistentVolumeClaim
- StorageClass
- Access modes
- Volume mounts

## PersistentVolumeClaim Example

Create `kubernetes/storage/model-pvc.yaml`:

```yaml
apiVersion: v1
kind: PersistentVolumeClaim

metadata:
  name: model-storage-pvc

spec:
  accessModes:
    - ReadWriteOnce

  resources:
    requests:
      storage: 5Gi
```

Mount it in a Deployment:

```yaml
volumeMounts:
  - name: model-storage
    mountPath: /models

volumes:
  - name: model-storage
    persistentVolumeClaim:
      claimName: model-storage-pvc
```

Check storage:

```bash
kubectl get pv
kubectl get pvc
kubectl describe pvc model-storage-pvc
```

## AI Storage Examples

Persistent storage can be used for:

- Downloaded AI model files.
- Uploaded documents.
- Vector database data.
- PostgreSQL data.
- Generated files.
- Cached datasets.

## Practice Task

- [ ] Create a PersistentVolumeClaim.
- [ ] Mount it into a Pod.
- [ ] Write a test file.
- [ ] Delete and recreate the Pod.
- [ ] Confirm that the file still exists.

---

# Phase 8: Ingress

Ingress manages incoming HTTP and HTTPS traffic.

It can route traffic based on hostnames or URL paths.

```text
User
  |
Ingress Controller
  |
  ├── /api      → FastAPI Service
  ├── /         → Frontend Service
  └── /qdrant   → Vector Database Service
```

## Ingress Resource Example

Create `kubernetes/ingress/app-ingress.yaml`:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress

metadata:
  name: ai-app-ingress

spec:
  rules:
    - host: ai-app.local
      http:
        paths:
          - path: /api
            pathType: Prefix
            backend:
              service:
                name: ai-api-service
                port:
                  number: 80
```

For Minikube:

```bash
minikube addons enable ingress
```

Check it:

```bash
kubectl get ingress
kubectl describe ingress ai-app-ingress
```

## Ingress Concepts

- [ ] Ingress resource.
- [ ] Ingress Controller.
- [ ] Host-based routing.
- [ ] Path-based routing.
- [ ] TLS termination.
- [ ] Domain names.
- [ ] Certificates.

## Practice Task

- [ ] Enable an Ingress Controller.
- [ ] Create an Ingress resource.
- [ ] Route `/api` to the FastAPI application.
- [ ] Add a local hostname.
- [ ] Test the route using a browser or `curl`.

---

# Phase 9: Helm

Helm is a package manager and templating system for Kubernetes applications.

A Helm chart can package:

```text
Deployment
Service
ConfigMap
Ingress
PersistentVolumeClaim
Other Kubernetes resources
```

## Basic Commands

```bash
helm version
helm create ai-app
helm lint ai-app
helm template ai-app
helm install ai-app ./ai-app
helm list
helm upgrade ai-app ./ai-app
helm rollback ai-app 1
helm uninstall ai-app
```

## Important Helm Files

```text
ai-app/
├── Chart.yaml
├── values.yaml
└── templates/
    ├── deployment.yaml
    ├── service.yaml
    ├── configmap.yaml
    ├── ingress.yaml
    └── pvc.yaml
```

## Example values.yaml

```yaml
replicaCount: 2

image:
  repository: my-ai-api
  tag: v1
  pullPolicy: IfNotPresent

service:
  type: ClusterIP
  port: 80

ingress:
  enabled: true
  host: ai-app.local

resources:
  requests:
    cpu: 100m
    memory: 128Mi
  limits:
    cpu: 500m
    memory: 512Mi
```

## Practice Task

- [ ] Create a Helm chart.
- [ ] Convert the Deployment into a Helm template.
- [ ] Convert the Service into a Helm template.
- [ ] Add configurable image tags.
- [ ] Add configurable replica counts.
- [ ] Add optional Ingress.
- [ ] Install the chart.
- [ ] Upgrade the application.
- [ ] Roll back the release.

---

# Phase 10: Troubleshooting

Troubleshooting is one of the most important Kubernetes skills.

## Essential Commands

Check resources:

```bash
kubectl get pods
kubectl get deployments
kubectl get services
kubectl get ingress
kubectl get pvc
kubectl get events
```

Inspect a resource:

```bash
kubectl describe pod <pod-name>
kubectl describe deployment <deployment-name>
kubectl describe service <service-name>
```

Read logs:

```bash
kubectl logs <pod-name>
kubectl logs <pod-name> --previous
kubectl logs -f <pod-name>
```

Read logs from a specific container:

```bash
kubectl logs <pod-name> -c <container-name>
```

Enter a container:

```bash
kubectl exec -it <pod-name> -- sh
```

Inspect YAML:

```bash
kubectl get pod <pod-name> -o yaml
```

## Common Problems

### ImagePullBackOff

Possible causes:

- Incorrect image name.
- Incorrect image tag.
- Private registry authentication failure.
- Image is unavailable to the local cluster.

### CrashLoopBackOff

Possible causes:

- Application crashes during startup.
- Missing environment variables.
- Incorrect command.
- Dependency connection failure.
- Failed liveness probe.

### Pending Pod

Possible causes:

- Insufficient CPU or memory.
- PersistentVolumeClaim is not bound.
- Node selector cannot be satisfied.
- Scheduling constraints cannot be satisfied.

### Service Not Reachable

Possible causes:

- Incorrect Service selector.
- Incorrect target port.
- Application listens only on `localhost`.
- Pods are not ready.
- Network policy blocks traffic.

## Troubleshooting Workflow

```text
1. kubectl get
2. kubectl describe
3. kubectl logs
4. kubectl get events
5. Check labels and selectors
6. Check ports
7. Check environment variables
8. Test connectivity from inside the cluster
```

## Practice Task

Intentionally create and fix these failures:

- [ ] Wrong image name.
- [ ] Missing environment variable.
- [ ] Incorrect container port.
- [ ] Incorrect Service selector.
- [ ] Failing readiness probe.
- [ ] Failing liveness probe.
- [ ] Unbound PersistentVolumeClaim.

Document each issue in:

```text
docs/troubleshooting.md
```

For every issue, record:

```text
Problem:
Observed status:
Commands used:
Root cause:
Solution:
What I learned:
```

---

# Phase 11: AI Application Deployment

Build a small production-style AI system.

## Suggested Architecture

```text
User
  |
Ingress
  |
Frontend
  |
FastAPI AI Service
  |
  ├── Redis
  ├── PostgreSQL
  ├── Qdrant
  └── Ollama or another model service
```

## Components

### FastAPI

Responsibilities:

- Receive API requests.
- Validate inputs.
- Call the AI model.
- Search the vector database.
- Store application data.
- Use Redis caching.

### Redis

Responsibilities:

- Cache repeated responses.
- Store temporary conversation state.
- Support rate limiting.
- Support background task queues.

### PostgreSQL

Responsibilities:

- Store users.
- Store document metadata.
- Store conversation records.
- Store application settings.

### Qdrant

Responsibilities:

- Store embeddings.
- Perform vector similarity search.
- Support Retrieval-Augmented Generation.

### Ollama or Model Service

Responsibilities:

- Serve the language model.
- Generate responses.
- Create embeddings when supported.

## Deployment Checklist

- [ ] Containerize every application component.
- [ ] Create Kubernetes Deployments.
- [ ] Create Services.
- [ ] Add ConfigMaps.
- [ ] Add Secrets.
- [ ] Add persistent storage.
- [ ] Add readiness probes.
- [ ] Add liveness probes.
- [ ] Add resource requests.
- [ ] Add resource limits.
- [ ] Add Ingress routing.
- [ ] Package the application using Helm.
- [ ] Write deployment documentation.
- [ ] Write troubleshooting documentation.

---

# Final Portfolio Project

## Project Name

**Kubernetes AI Application Platform**

## Minimum Features

- [ ] FastAPI backend.
- [ ] `/health` endpoint.
- [ ] AI chat or document question-answering endpoint.
- [ ] Redis response caching.
- [ ] PostgreSQL data storage.
- [ ] Qdrant vector search.
- [ ] Local LLM or external model integration.
- [ ] Docker Compose development environment.
- [ ] Kubernetes manifests.
- [ ] Helm chart.
- [ ] Ingress configuration.
- [ ] Persistent storage.
- [ ] Configuration management.
- [ ] Secret management.
- [ ] Health probes.
- [ ] Resource limits.
- [ ] Troubleshooting guide.
- [ ] Architecture diagram.
- [ ] Screenshots or demo GIF.
- [ ] GitHub Actions CI pipeline.

## Suggested Repository Structure

```text
kubernetes-ai-roadmap/
├── README.md
├── .gitignore
├── LICENSE
├── Makefile
│
├── app/
│   ├── main.py
│   ├── requirements.txt
│   ├── Dockerfile
│   └── tests/
│
├── docker/
│   └── docker-compose.yml
│
├── kubernetes/
│   ├── namespace.yaml
│   ├── pods/
│   ├── deployments/
│   ├── services/
│   ├── config/
│   ├── storage/
│   └── ingress/
│
├── helm/
│   └── ai-app/
│       ├── Chart.yaml
│       ├── values.yaml
│       └── templates/
│
├── docs/
│   ├── architecture.md
│   ├── setup.md
│   ├── troubleshooting.md
│   └── screenshots/
│
└── .github/
    └── workflows/
        └── ci.yml
```

---

# Suggested Three-Week Schedule

## Week 1: Core Kubernetes

### Day 1

- [ ] Understand Kubernetes architecture.
- [ ] Install kubectl.
- [ ] Start a local cluster.

### Day 2

- [ ] Create Pods.
- [ ] Inspect logs.
- [ ] Use `kubectl exec`.

### Day 3

- [ ] Create Deployments.
- [ ] Scale replicas.
- [ ] Test self-healing.

### Day 4

- [ ] Perform rolling updates.
- [ ] Perform rollbacks.

### Day 5

- [ ] Create Services.
- [ ] Understand ClusterIP, NodePort, and LoadBalancer.

### Weekend Project

Deploy a Dockerized FastAPI application using a Deployment and Service.

## Week 2: Application Configuration

### Day 6

- [ ] Create ConfigMaps.
- [ ] Inject environment variables.

### Day 7

- [ ] Create Secrets.
- [ ] Learn safe secret-handling practices.

### Day 8

- [ ] Create persistent storage.
- [ ] Test data persistence.

### Day 9

- [ ] Configure Ingress.
- [ ] Add path-based routing.

### Day 10

- [ ] Learn Helm fundamentals.
- [ ] Create a simple chart.

### Weekend Project

Deploy FastAPI, Redis, PostgreSQL, and Qdrant.

## Week 3: Production Skills

### Day 11

- [ ] Add readiness and liveness probes.

### Day 12

- [ ] Add resource requests and limits.

### Day 13

- [ ] Practice troubleshooting failures.

### Day 14

- [ ] Package the complete application using Helm.

### Day 15

- [ ] Add CI checks.
- [ ] Improve documentation.
- [ ] Record a demo.

### Weekend Project

Complete and publish the Kubernetes AI Application Platform.

---

# GitHub Practice Workflow

Use one branch for each learning phase.

```bash
git checkout -b phase-01-foundations
git checkout -b phase-02-local-cluster
git checkout -b phase-03-pods
git checkout -b phase-04-deployments
git checkout -b phase-05-services
git checkout -b phase-06-configuration
git checkout -b phase-07-storage
git checkout -b phase-08-ingress
git checkout -b phase-09-helm
git checkout -b phase-10-troubleshooting
git checkout -b phase-11-ai-project
```

Recommended commit style:

```text
docs: add Kubernetes architecture notes
feat: deploy FastAPI Pod
feat: add API Deployment
feat: expose API using ClusterIP Service
feat: add ConfigMap and Secret
feat: add persistent model storage
feat: configure Ingress
feat: create Helm chart
fix: correct Service selector
test: add API health endpoint test
```

---

# Documentation Template

Create one Markdown file for every phase.

Example:

```markdown
# Phase 3: Pods

## What I Learned

## Commands I Used

## YAML Files I Created

## Problems I Faced

## How I Solved Them

## Screenshots

## Key Takeaways
```

---

# Skills Validation Checklist

I am ready to claim Kubernetes fundamentals when I can complete these tasks without copying a full tutorial:

- [ ] Explain Kubernetes architecture.
- [ ] Create a Pod manifest.
- [ ] Create and scale a Deployment.
- [ ] Expose an application using a Service.
- [ ] Debug labels and selectors.
- [ ] Inject configuration using a ConfigMap.
- [ ] Inject sensitive values using a Secret.
- [ ] Mount persistent storage.
- [ ] Route traffic using Ingress.
- [ ] Create and install a Helm chart.
- [ ] Investigate `CrashLoopBackOff`.
- [ ] Investigate `ImagePullBackOff`.
- [ ] Investigate a Pending Pod.
- [ ] Perform a rolling update.
- [ ] Perform a rollback.
- [ ] Deploy a multi-service AI application.

---

# Useful Command Cheat Sheet

```bash
# Cluster
kubectl cluster-info
kubectl get nodes

# Resources
kubectl get all
kubectl get pods
kubectl get deployments
kubectl get services
kubectl get ingress
kubectl get configmaps
kubectl get secrets
kubectl get pv
kubectl get pvc

# Apply and delete
kubectl apply -f file.yaml
kubectl delete -f file.yaml

# Debugging
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl logs <pod-name> --previous
kubectl exec -it <pod-name> -- sh
kubectl get events --sort-by=.metadata.creationTimestamp

# Deployments
kubectl scale deployment <name> --replicas=3
kubectl rollout status deployment/<name>
kubectl rollout history deployment/<name>
kubectl rollout undo deployment/<name>

# Local access
kubectl port-forward service/<service-name> 8080:80

# Context
kubectl config get-contexts
kubectl config current-context
kubectl config use-context <context-name>

# Minikube
minikube start
minikube stop
minikube status
minikube dashboard
minikube addons enable ingress

# Helm
helm create <chart-name>
helm lint <chart-directory>
helm template <release-name> <chart-directory>
helm install <release-name> <chart-directory>
helm upgrade <release-name> <chart-directory>
helm rollback <release-name> <revision>
helm uninstall <release-name>
```

---

# Learning Rule

For every concept:

```text
Learn → Build → Break → Debug → Document → Commit
```

Watching tutorials is not enough. Each phase should produce code, YAML files, troubleshooting notes, and Git commits.

---

# Completion Criteria

This roadmap is complete when:

- [ ] All progress checkboxes are completed.
- [ ] The final AI application runs in Kubernetes.
- [ ] The application can be installed using Helm.
- [ ] The repository contains clear setup instructions.
- [ ] Common failures and fixes are documented.
- [ ] The project includes a working demonstration.
- [ ] I can explain every major design decision.

---

## License

This learning repository may use the MIT License.
