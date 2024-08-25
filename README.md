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
---

In order to access the server UI you have the following options:

1. kubectl port-forward service/argo-cd-server -n argo 8080:443

and then open the browser on http://localhost:8080 and accept the certificate

2. enable ingress in the values file `server.ingress.enabled` and either
- Add the annotation for ssl passthrough: https://argo-cd.readthedocs.io/en/stable/operator-manual/ingress/#option-1-ssl-passthrough
- Set the `configs.params."server.insecure"` in the values file and terminate SSL at your ingress: https://argo-cd.readthedocs.io/en/stable/operator-manual/ingress/#option-2-multiple-ingress-objects-and-hosts


After reaching the UI the first time you can login with username: admin and the random password generated during the installation. You can find the password by running:

kubectl -n argo get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

(You should delete the initial secret afterwards as suggested by the Getting Started Guide: https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli)


---
[11/4/2024]

Remote Helm chart repo setup added

remote: Permission to UQThesisENGG7817/helm-charts.git denied to github-actions[bot].
fatal: unable to access 'https://github.com/UQThesisENGG7817/helm-charts/': The requested URL returned error: 403
Refers --> https://github.com/ad-m/github-push-action/issues/96#issuecomment-1647904286
Helm charts page: https://github.com/UQThesisENGG7817/helm-charts/tree/gh-pages

[13/4/2024]

Base Overlay folder structure for multi-env demo -> will only use prod
Setup argocd helpers for rbac demo
Setup argo-rollouts
Bootstrap services added

-> Demo pushing vault - self-hosted sercrets manager and metrics-server first

Argo RBAC CM
```   p, role:org-admin, applications, *, */*, allow
      p, role:org-admin, clusters, get, *, allow
      p, role:org-admin, repositories, get, *, allow
      p, role:org-admin, repositories, create, *, allow
      p, role:org-admin, repositories, update, *, allow
      p, role:org-admin, repositories, delete, *, allow
      p, role:org-admin, projects, get, *, allow
      p, role:org-admin, projects, create, *, allow
      p, role:org-admin, projects, update, *, allow
      p, role:org-admin, projects, delete, *, allow
      p, role:org-admin, logs, get, *, allow
      p, role:org-admin, exec, create, */*, allow

      g, UQThesisENGG7817:devops-team, role:org-admin
```

Vault init and unseal must be done manually - exec into


[4/5/2024]
Migrated to second cluster
Documented it
"When troubleshooting or testing the deployment of your applications we encourage you to configure your ACME client to use our staging environment. Rate limits for our staging environment are significantly higher."
SecretStore with Vault kv engine deployed
ExternalSecret deploy

[5/5/2024]
Prometheus deployed: logging.pinnamon.com
Robusta deployed - alert manager and notification sinking
Alert manager deployed: alertmanager.pinnamon.com
ACME 429 rate-limit problem
Alert manager silent
Nginx perhaps cannot be gitops (now) because we need to use UI to bootstrap App of Apps


...

[16/08/2024]
Deploy LGTMA Observability Stack

[19/08/2024]
kubectl apply -f https://github.com/open-telemetry/opentelemetry-operator/releases/latest/download/opentelemetry-operator.yaml

[24/08/2024]
Added trivy operator, trivy policy reporter, kyverno, kyverno reporter helm charts

[25/08/2024]
Grafana Dashboard Terraform Module

[26/08/2024]
Expose ArgoCD metrics service monitor
IaC JSON dashboard