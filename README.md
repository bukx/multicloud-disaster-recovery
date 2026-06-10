# Multi-Cloud Disaster Recovery Platform

Multi-cloud resilience project spanning AWS, Azure, and GCP with automated failover workflows, Kubernetes deployments, infrastructure as code, and centralized monitoring. The repo combines Terraform, Pulumi, Ansible, and Python automation to model how a platform team could run cross-cloud recovery drills from a single codebase.

![Architecture Diagram](docs/architecture.png)

## Why this repo matters

Most disaster recovery demos stop at one provider. This repo is stronger because it treats resilience as a cross-cloud systems problem: infrastructure parity, failover automation, operational hardening, and shared visibility all have to work together.

## What is included

- AWS, Azure, and GCP infrastructure definitions
- Kubernetes deployment manifests for each cloud environment
- Python DR scripts for failover and restoration workflows
- Ansible hardening playbooks
- Datadog monitoring configuration
- GitHub Actions workflow definitions under `.github/`

## Platform design

- **AWS** acts as the primary environment
- **Azure** and **GCP** act as standby targets for recovery scenarios
- **Terraform** provisions AWS and Azure infrastructure
- **Pulumi** provisions GCP infrastructure
- **Ansible** applies hardening and configuration consistency
- **Route 53** manages global traffic steering and failover
- **Datadog** provides centralized visibility across providers

## Quick start

```bash
# Provision AWS (primary)
cd terraform/aws/environments/prod && terraform init && terraform apply

# Provision Azure (standby)
cd terraform/azure/environments/prod && terraform init && terraform apply

# Provision GCP (standby)
cd pulumi/gcp && pulumi up

# Harden all hosts
ansible-playbook -i ansible/inventory ansible/roles/hardening/site.yml

# Run a DR drill
python dr-scripts/failover.py --target azure --reason "DR drill" --dry-run
python dr-scripts/failover.py --target azure --reason "DR drill"

# Restore primary
python dr-scripts/failover.py --target aws --reason "Restore primary"
```

## Repository layout

```text
.
|-- ansible/              # hardening and configuration automation
|-- app/                  # application source and container assets
|-- dr-scripts/           # failover and restore automation
|-- k8s/                  # Kubernetes manifests per cloud
|-- monitoring/           # Datadog configuration
|-- pulumi/               # GCP infrastructure
|-- terraform/            # AWS and Azure infrastructure
|-- docs/                 # diagrams and supporting documentation
`-- .github/              # automation workflows
```

## What this demonstrates

- multi-cloud DR planning beyond marketing-level architecture diagrams
- mixed IaC strategies across different providers
- operational automation for drills and recovery actions
- centralized observability and hardening across heterogeneous environments
