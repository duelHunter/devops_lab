# Cloud & DevOps Engineering Practice Repository

This repository is my hands-on learning workspace for mastering the core skills required for a **Cloud and DevOps Engineer** role.

Each major topic has its own folder containing notes, commands, configuration files, scripts, exercises, screenshots, and mini-projects.

---

## Repository Goals

- Build strong Linux and networking fundamentals
- Learn containerization with Docker
- Deploy and manage applications with Kubernetes
- Practice AWS cloud services
- Build CI/CD pipelines
- Provision infrastructure using Terraform and CloudFormation
- Automate server configuration using Ansible
- Monitor applications and infrastructure
- Apply DevSecOps security practices
- Improve Bash, Python, and Node.js automation skills
- Create a public portfolio that demonstrates practical DevOps experience

---

## Repository Structure

```text
cloud-devops-engineering-roadmap/
│
├── 01-linux/
│   ├── commands/
│   ├── permissions/
│   ├── users-and-groups/
│   ├── systemd/
│   ├── networking/
│   ├── bash-scripting/
│   ├── process-management/
│   ├── logs/
│   └── README.md
│
├── 02-networking/
│   ├── tcp-ip/
│   ├── dns/
│   ├── http-https/
│   ├── ssh/
│   ├── firewalls/
│   ├── load-balancers/
│   ├── nginx-reverse-proxy/
│   └── README.md
│
├── 03-git/
│   ├── branching/
│   ├── merge-and-rebase/
│   ├── pull-requests/
│   ├── workflows/
│   └── README.md
│
├── 04-docker/
│   ├── images-and-containers/
│   ├── dockerfiles/
│   ├── volumes/
│   ├── networks/
│   ├── docker-compose/
│   ├── multi-stage-builds/
│   ├── security/
│   └── README.md
│
├── 05-kubernetes/
│   ├── pods/
│   ├── deployments/
│   ├── services/
│   ├── configmaps/
│   ├── secrets/
│   ├── ingress/
│   ├── persistent-volumes/
│   ├── helm/
│   ├── troubleshooting/
│   └── README.md
│
├── 06-aws/
│   ├── ec2/
│   ├── vpc/
│   ├── iam/
│   ├── s3/
│   ├── rds/
│   ├── ecs/
│   ├── eks/
│   ├── route53/
│   ├── cloudwatch/
│   ├── auto-scaling/
│   ├── load-balancer/
│   ├── lambda/
│   └── README.md
│
├── 07-ci-cd/
│   ├── jenkins/
│   ├── github-actions/
│   ├── gitlab-ci/
│   ├── automated-testing/
│   ├── deployment-pipelines/
│   └── README.md
│
├── 08-infrastructure-as-code/
│   ├── terraform/
│   ├── cloudformation/
│   └── README.md
│
├── 09-configuration-management/
│   ├── ansible/
│   ├── inventory/
│   ├── playbooks/
│   ├── roles/
│   └── README.md
│
├── 10-monitoring-and-logging/
│   ├── prometheus/
│   ├── grafana/
│   ├── loki/
│   ├── elk-stack/
│   └── README.md
│
├── 11-devsecops/
│   ├── iam-best-practices/
│   ├── secrets-management/
│   ├── tls-ssl/
│   ├── vulnerability-scanning/
│   ├── least-privilege/
│   └── README.md
│
├── 12-programming/
│   ├── bash/
│   ├── python/
│   ├── nodejs/
│   └── README.md
│
├── projects/
│   ├── 01-dockerized-web-app/
│   ├── 02-ci-cd-pipeline/
│   ├── 03-terraform-aws-infrastructure/
│   ├── 04-kubernetes-deployment/
│   ├── 05-monitoring-stack/
│   └── 06-end-to-end-devops-project/
│
├── diagrams/
├── notes/
├── resources/
├── .gitignore
├── LICENSE
└── README.md
```

---

# Learning Roadmap

## 1. Linux

**Folder:** [`01-linux/`](./01-linux/)

### Topics

- [ ] Essential Linux commands
- [ ] Files and directories
- [ ] File permissions
- [ ] Users and groups
- [ ] Package management
- [ ] Environment variables
- [ ] Systemd services
- [ ] Linux networking commands
- [ ] Bash scripting
- [ ] Process management
- [ ] Log management
- [ ] `journalctl`
- [ ] `/var/log`

### Practice Tasks

- [ ] Create, move, copy, and delete files using the terminal
- [ ] Create users and groups
- [ ] Configure file ownership and permissions
- [ ] Create and manage a custom systemd service
- [ ] Write Bash scripts for system health checks
- [ ] Monitor CPU, memory, storage, and processes
- [ ] Search and filter log files
- [ ] Schedule a script using cron

### Useful Commands

```bash
pwd
ls -la
cd
mkdir
touch
cp
mv
rm
cat
less
grep
find
chmod
chown
ps
top
htop
kill
systemctl
journalctl
df -h
du -sh
free -m
ip addr
ss -tulpn
```

---

## 2. Networking

**Folder:** [`02-networking/`](./02-networking/)

### Topics

- [ ] OSI and TCP/IP models
- [ ] IP addresses and subnetting
- [ ] Ports and protocols
- [ ] DNS
- [ ] HTTP and HTTPS
- [ ] SSH
- [ ] Firewalls
- [ ] Load balancers
- [ ] Reverse proxies
- [ ] Nginx

### Practice Tasks

- [ ] Identify private and public IP addresses
- [ ] Practice basic subnet calculations
- [ ] Test DNS resolution using `nslookup` and `dig`
- [ ] Inspect HTTP requests using `curl`
- [ ] Configure SSH key authentication
- [ ] Configure UFW firewall rules
- [ ] Configure Nginx as a reverse proxy
- [ ] Load balance traffic between two application instances

### Useful Commands

```bash
ping
traceroute
nslookup
dig
curl
wget
ip addr
ip route
ss -tulpn
netstat
ssh
scp
```

---

## 3. Git

**Folder:** [`03-git/`](./03-git/)

### Topics

- [ ] Repository initialization
- [ ] Staging and commits
- [ ] Branching
- [ ] Merging
- [ ] Rebasing
- [ ] Resolving merge conflicts
- [ ] Pull requests
- [ ] Tags and releases
- [ ] Git workflows

### Practice Tasks

- [ ] Create a repository and push it to GitHub
- [ ] Create and merge feature branches
- [ ] Rebase a feature branch
- [ ] Resolve a merge conflict
- [ ] Create a pull request
- [ ] Add release tags
- [ ] Practice GitHub Flow

### Useful Commands

```bash
git init
git clone
git status
git add .
git commit -m "message"
git branch
git switch
git checkout
git merge
git rebase
git pull
git push
git log
git tag
```

---

## 4. Docker

**Folder:** [`04-docker/`](./04-docker/)

### Topics

- [ ] Images and containers
- [ ] Dockerfiles
- [ ] Image layers
- [ ] Volumes
- [ ] Networks
- [ ] Docker Compose
- [ ] Multi-stage builds
- [ ] Image optimization
- [ ] Container security
- [ ] Container registries

### Practice Tasks

- [ ] Run Nginx, Redis, and PostgreSQL containers
- [ ] Containerize a Python or Node.js application
- [ ] Mount a persistent volume
- [ ] Create a custom Docker network
- [ ] Connect an application container to a database container
- [ ] Build a multi-container environment using Docker Compose
- [ ] Create a multi-stage Dockerfile
- [ ] Scan an image for vulnerabilities
- [ ] Push an image to Docker Hub or GitHub Container Registry

### Example

```bash
docker build -t my-app .
docker run -d -p 8080:8080 --name my-app my-app
docker ps
docker logs my-app
docker exec -it my-app sh
docker compose up -d
docker compose down
```

---

## 5. Kubernetes

**Folder:** [`05-kubernetes/`](./05-kubernetes/)

### Topics

- [ ] Kubernetes architecture
- [ ] Pods
- [ ] ReplicaSets
- [ ] Deployments
- [ ] Services
- [ ] ConfigMaps
- [ ] Secrets
- [ ] Ingress
- [ ] Namespaces
- [ ] Persistent Volumes
- [ ] Persistent Volume Claims
- [ ] Resource requests and limits
- [ ] Health checks
- [ ] Helm
- [ ] Troubleshooting

### Practice Tasks

- [ ] Create a local cluster using Minikube or Kind
- [ ] Deploy an Nginx pod
- [ ] Create a deployment with multiple replicas
- [ ] Expose the deployment using a service
- [ ] Add application configuration using a ConfigMap
- [ ] Add credentials using a Secret
- [ ] Configure readiness and liveness probes
- [ ] Configure persistent storage
- [ ] Expose an application using Ingress
- [ ] Package an application using Helm
- [ ] Troubleshoot `CrashLoopBackOff`
- [ ] Troubleshoot `ImagePullBackOff`

### Useful Commands

```bash
kubectl get nodes
kubectl get pods
kubectl get deployments
kubectl get services
kubectl apply -f file.yaml
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl exec -it <pod-name> -- sh
kubectl delete -f file.yaml
```

---

## 6. AWS Cloud

**Folder:** [`06-aws/`](./06-aws/)

### Topics

- [ ] EC2
- [ ] VPC
- [ ] Subnets
- [ ] Route tables
- [ ] Security groups
- [ ] IAM
- [ ] S3
- [ ] RDS
- [ ] ECS
- [ ] EKS
- [ ] Route 53
- [ ] CloudWatch
- [ ] Auto Scaling
- [ ] Elastic Load Balancer
- [ ] Lambda

### Practice Tasks

- [ ] Launch and connect to an EC2 instance
- [ ] Host a static website in S3
- [ ] Create an IAM user and role
- [ ] Apply least-privilege IAM permissions
- [ ] Build a VPC with public and private subnets
- [ ] Deploy a database using RDS
- [ ] Configure an Application Load Balancer
- [ ] Configure Auto Scaling
- [ ] Send logs and metrics to CloudWatch
- [ ] Deploy a container using ECS
- [ ] Deploy an application using EKS
- [ ] Create a basic Lambda function
- [ ] Configure DNS using Route 53

> Delete unused cloud resources after practice to avoid unexpected charges.

---

## 7. CI/CD

**Folder:** [`07-ci-cd/`](./07-ci-cd/)

### Topics

- [ ] Continuous Integration
- [ ] Continuous Delivery
- [ ] Continuous Deployment
- [ ] Jenkins
- [ ] GitHub Actions
- [ ] GitLab CI
- [ ] Automated testing
- [ ] Artifact management
- [ ] Deployment pipelines
- [ ] Rollback strategies

### Practice Tasks

- [ ] Run tests automatically when code is pushed
- [ ] Build a Docker image in a pipeline
- [ ] Push an image to a container registry
- [ ] Deploy an application to a server
- [ ] Deploy an application to Kubernetes
- [ ] Configure pipeline secrets
- [ ] Add manual approval before production deployment
- [ ] Add rollback steps
- [ ] Send pipeline success and failure notifications

### Example GitHub Actions Workflow

```yaml
name: CI

on:
  push:
    branches:
      - main
  pull_request:

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Run tests
        run: echo "Run application tests here"
```

---

## 8. Infrastructure as Code

**Folder:** [`08-infrastructure-as-code/`](./08-infrastructure-as-code/)

### Topics

- [ ] Terraform providers
- [ ] Resources
- [ ] Variables
- [ ] Outputs
- [ ] State files
- [ ] Remote state
- [ ] Modules
- [ ] Workspaces
- [ ] Terraform lifecycle
- [ ] AWS CloudFormation basics

### Practice Tasks

- [ ] Provision an EC2 instance using Terraform
- [ ] Create a VPC using Terraform
- [ ] Create reusable Terraform modules
- [ ] Store Terraform state remotely
- [ ] Use variables and outputs
- [ ] Import an existing resource
- [ ] Create an S3 bucket using CloudFormation
- [ ] Add Terraform validation to CI/CD

### Useful Commands

```bash
terraform init
terraform fmt
terraform validate
terraform plan
terraform apply
terraform destroy
terraform output
terraform state list
```

---

## 9. Configuration Management

**Folder:** [`09-configuration-management/`](./09-configuration-management/)

### Topics

- [ ] Ansible installation
- [ ] Inventory
- [ ] Ad hoc commands
- [ ] Playbooks
- [ ] Variables
- [ ] Templates
- [ ] Handlers
- [ ] Roles
- [ ] Ansible Vault

### Practice Tasks

- [ ] Connect Ansible to a Linux VM
- [ ] Install packages using a playbook
- [ ] Create users using a playbook
- [ ] Configure Nginx automatically
- [ ] Deploy an application
- [ ] Create a reusable Ansible role
- [ ] Store secrets using Ansible Vault

### Useful Commands

```bash
ansible all -m ping
ansible all -a "uptime"
ansible-playbook playbook.yml
ansible-inventory --list
ansible-vault create secrets.yml
```

---

## 10. Monitoring and Logging

**Folder:** [`10-monitoring-and-logging/`](./10-monitoring-and-logging/)

### Topics

- [ ] Metrics
- [ ] Logs
- [ ] Alerts
- [ ] Prometheus
- [ ] Grafana
- [ ] Loki
- [ ] Elasticsearch
- [ ] Logstash
- [ ] Kibana
- [ ] Application monitoring
- [ ] Infrastructure monitoring

### Practice Tasks

- [ ] Run Prometheus and Grafana using Docker Compose
- [ ] Monitor a Linux server using Node Exporter
- [ ] Monitor a containerized application
- [ ] Create a Grafana dashboard
- [ ] Create alerting rules
- [ ] Collect logs using Loki
- [ ] Build an ELK stack
- [ ] Search and visualize application logs

---

## 11. DevSecOps

**Folder:** [`11-devsecops/`](./11-devsecops/)

### Topics

- [ ] IAM best practices
- [ ] Least privilege
- [ ] Secrets management
- [ ] TLS and SSL
- [ ] Dependency scanning
- [ ] Container image scanning
- [ ] Static application security testing
- [ ] Infrastructure security
- [ ] Secure CI/CD pipelines

### Practice Tasks

- [ ] Remove hard-coded credentials from source code
- [ ] Store secrets in GitHub Actions Secrets
- [ ] Configure HTTPS using TLS certificates
- [ ] Scan dependencies for vulnerabilities
- [ ] Scan Docker images
- [ ] Scan Terraform files
- [ ] Add security checks to CI/CD
- [ ] Create restricted IAM policies
- [ ] Enable logging and auditing

### Tools to Explore

```text
Trivy
SonarQube
OWASP Dependency-Check
Checkov
tfsec
Gitleaks
AWS Secrets Manager
HashiCorp Vault
```

---

## 12. Programming and Automation

**Folder:** [`12-programming/`](./12-programming/)

### Languages

- [ ] Bash
- [ ] Python
- [ ] JavaScript
- [ ] Node.js

### Practice Tasks

- [ ] Write a Bash backup script
- [ ] Write a system health monitoring script
- [ ] Write a Python script that calls an API
- [ ] Write a Python script that reads and writes JSON
- [ ] Automate AWS tasks using Boto3
- [ ] Create a simple REST API using Python or Node.js
- [ ] Add logging and error handling
- [ ] Create command-line tools
- [ ] Write unit tests

---

# Portfolio Projects

## Project 1: Dockerized Web Application

**Folder:** [`projects/01-dockerized-web-app/`](./projects/01-dockerized-web-app/)

Build a small Python or Node.js web application.

### Requirements

- [ ] Application source code
- [ ] Dockerfile
- [ ] `.dockerignore`
- [ ] Docker Compose
- [ ] PostgreSQL or Redis
- [ ] Environment variables
- [ ] Health check
- [ ] Setup documentation

---

## Project 2: CI/CD Pipeline

**Folder:** [`projects/02-ci-cd-pipeline/`](./projects/02-ci-cd-pipeline/)

### Requirements

- [ ] Run tests
- [ ] Build a Docker image
- [ ] Scan the image
- [ ] Push the image to a registry
- [ ] Deploy the application
- [ ] Store secrets securely
- [ ] Add failure notifications

---

## Project 3: AWS Infrastructure with Terraform

**Folder:** [`projects/03-terraform-aws-infrastructure/`](./projects/03-terraform-aws-infrastructure/)

### Requirements

- [ ] VPC
- [ ] Public and private subnets
- [ ] Internet gateway
- [ ] Route tables
- [ ] Security groups
- [ ] EC2 instance
- [ ] Load balancer
- [ ] RDS database
- [ ] Terraform modules
- [ ] Remote state
- [ ] Architecture diagram

---

## Project 4: Kubernetes Deployment

**Folder:** [`projects/04-kubernetes-deployment/`](./projects/04-kubernetes-deployment/)

### Requirements

- [ ] Deployment
- [ ] Service
- [ ] ConfigMap
- [ ] Secret
- [ ] Ingress
- [ ] Persistent storage
- [ ] Health probes
- [ ] Resource limits
- [ ] Helm chart
- [ ] Troubleshooting guide

---

## Project 5: Monitoring Stack

**Folder:** [`projects/05-monitoring-stack/`](./projects/05-monitoring-stack/)

### Requirements

- [ ] Prometheus
- [ ] Grafana
- [ ] Node Exporter
- [ ] Application metrics
- [ ] Loki
- [ ] Dashboard
- [ ] Alert rules
- [ ] Docker Compose or Kubernetes deployment

---

## Project 6: End-to-End DevOps Project

**Folder:** [`projects/06-end-to-end-devops-project/`](./projects/06-end-to-end-devops-project/)

Build and deploy a complete application using:

```text
GitHub
  ↓
GitHub Actions or Jenkins
  ↓
Automated Tests
  ↓
Docker Build
  ↓
Security Scan
  ↓
Container Registry
  ↓
Terraform
  ↓
AWS
  ↓
Kubernetes
  ↓
Prometheus and Grafana
```

### Requirements

- [ ] Application source code
- [ ] Git branching workflow
- [ ] Automated tests
- [ ] Docker image
- [ ] CI/CD pipeline
- [ ] Terraform infrastructure
- [ ] Ansible configuration
- [ ] Kubernetes manifests
- [ ] Helm chart
- [ ] Monitoring dashboard
- [ ] Centralized logging
- [ ] Security scanning
- [ ] Architecture diagram
- [ ] Deployment documentation
- [ ] Troubleshooting documentation

---

# Suggested Learning Order

```text
Linux
  ↓
Networking
  ↓
Git
  ↓
Programming and Scripting
  ↓
Docker
  ↓
AWS
  ↓
CI/CD
  ↓
Terraform
  ↓
Ansible
  ↓
Kubernetes
  ↓
Monitoring and Logging
  ↓
DevSecOps
  ↓
End-to-End Project
```

---

# Progress Tracker

| Area | Status | Notes |
|---|---|---|
| Linux | Not Started | |
| Networking | Not Started | |
| Git | Not Started | |
| Docker | Not Started | |
| Kubernetes | Not Started | |
| AWS | Not Started | |
| CI/CD | Not Started | |
| Terraform | Not Started | |
| CloudFormation | Not Started | |
| Ansible | Not Started | |
| Monitoring | Not Started | |
| Logging | Not Started | |
| DevSecOps | Not Started | |
| Bash | Not Started | |
| Python | Not Started | |
| Node.js | Not Started | |
| Portfolio Projects | Not Started | |

Suggested status values:

```text
Not Started
Learning
Practicing
Completed
Needs Review
```

---

# How I Will Document Each Topic

Each topic folder should contain its own `README.md`.

Recommended format:

```markdown
# Topic Name

## Objective

Explain what I want to learn.

## Concepts

Document the important theory.

## Commands

List useful commands with explanations.

## Practice

Describe the exercises completed.

## Files

Explain the purpose of each file.

## Problems Faced

Document errors and troubleshooting steps.

## What I Learned

Summarize the main lessons.

## References

Add useful documentation links.
```

---

# Recommended Commit Style

Use clear commit messages:

```text
docs: add Linux permission notes
feat: add Dockerized Node.js application
fix: correct Kubernetes service selector
ci: add GitHub Actions workflow
infra: add Terraform VPC module
security: add Trivy image scanning
monitoring: add Grafana dashboard
```

---

# Git Workflow

```bash
git switch -c feature/linux-permissions

git add .
git commit -m "docs: add Linux permissions practice"

git push -u origin feature/linux-permissions
```

Create a pull request, review the changes, and merge them into `main`.

---

# Documentation Rules

For every exercise:

1. Explain the objective.
2. Include the commands used.
3. Add the configuration files.
4. Record errors and solutions.
5. Include screenshots when useful.
6. Explain what was learned.
7. Never commit passwords, tokens, private keys, or cloud credentials.

---

# Security Notes

Do not commit files such as:

```text
.env
*.pem
*.key
terraform.tfstate
terraform.tfstate.backup
credentials
secrets.yml
kubeconfig
```

Example `.gitignore` entries:

```gitignore
.env
.env.*
*.pem
*.key
*.crt
terraform.tfstate
terraform.tfstate.*
.terraform/
*.tfvars
ansible/secrets.yml
node_modules/
venv/
.venv/
__pycache__/
*.log
```

---

# Definition of Done

A topic is considered complete when:

- [ ] I understand the main concepts
- [ ] I have completed at least one practical exercise
- [ ] I have documented the commands and configuration
- [ ] I have recorded common errors and solutions
- [ ] I can explain the topic without reading notes
- [ ] I can use the topic inside a larger project

---

# Final Goal

By completing this repository, I should be able to:

- Deploy applications on Linux servers
- Containerize applications using Docker
- Deploy and manage applications using Kubernetes
- Provision AWS infrastructure using Terraform
- Automate configuration using Ansible
- Build CI/CD pipelines
- Monitor applications and infrastructure
- Apply cloud and DevSecOps security practices
- Troubleshoot real deployment problems
- Present practical Cloud and DevOps projects to employers

---

## License

This repository is for personal learning and portfolio development.
