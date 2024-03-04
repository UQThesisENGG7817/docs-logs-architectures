# docs-logs-architectures
Documenting, diagrams, logs and architecture of the thesis - also acts as a Proof of Orginally Work by Hoang Phuc Pham
# Project journal - so far
1. Created an Organization for demo
2. Setup infrastructure directories
3. Exploring options for GitOps deploy -> Must have GitOps option first -> went with ArgoCD
---
1. Dex connector for ArgoCD SSO and Github OAuth app setup
---
1. Init IaC repository, using terragrunt as a wrapper
2. Terragrunt can be served as multi-env, multi-stage one
3. Exploring SOPS
4. Mixing terraform with terragrunt
5. Local backend, pretty weird that I'm doing IaC for niche / none Cloud Provider there - do't have such supports and dynamoDB, hash table, state locking
6. Root terraform setup
---
1. Terraform module added for argo-helm release
2. Terragrunt built-in functions: `get_parent_terragrunt_dir`, `fileexists` for Kubernetes host file referencing
---
1. Data block is not available for terragrunt -> mixed use with terraform and use as output
2. Kubernetes provider for terraform
---
1. A base helm-charts?
2. A github page for chart
3. Github actions - workflow for chart repository page
---
1. Terraform module sonarscan?
---
1. Currently using pgp for secrets right now -> might consider moving to Vault later
2. Added a thesis bot to Org -  [potter-uq-thesis-bot](https://github.com/potter-uq-thesis-bot)
3. Polishing helm chart for ArgoCD via context variable
4. Exploring notification via email
5. Trigger notifiaction field section
---
1. Exploring ingress and domain option