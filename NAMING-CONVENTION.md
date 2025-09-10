# 📚 Repository Naming & Subject Convention

This document defines the recommended naming and categorization plan for repositories in this organization.

## 🏷️ Naming Convention

Repositories should use a **prefix-subject** scheme:

| Prefix                | Description                                        | Example Subject(s)                |
|-----------------------|----------------------------------------------------|-----------------------------------|
| `template-bicep-`     | Bicep IaC templates                                | webapi, functionapp, appinsights  |
| `template-arm-`       | ARM template repositories                          | storage, sql, networking          |
| `template-tf-`        | Terraform templates                                | aks, appservice                   |
| `template-powershell-`| PowerShell deployment scripts/templates            | webapp, logicapp                  |
| `module-`             | Reusable modules (Bicep, ARM, Terraform)           | storage, vnet, sql                |
| `ops-`                | Operational tools, scripts, automation             | lab-cleanup, monitor, cost-analyze|
| `tool-`               | CLI or utility scripts                             | azure-cost-analyzer, tag-manager  |
| `showcase-`           | Portfolio & demo projects                          | fullstack-todo, ml-api            |
| `lab-`                | Hands-on labs, tutorials, exercises                | ai, ci-cd, openid, monitor        |
| `workshop-`           | Step-by-step guided workshops                      | devops-fundamentals, api-design   |
| `demo-`               | Small demo apps or scenarios                       | appinsights, cosmosdb             |
| `ref-`                | Reference implementations                          | openid-auth-flow, rbac            |
| `sample-`             | Example code/projects                              | bicep-basics, arm-intro           |
| `infra-`              | Infrastructure blueprints/guides                   | prod-network, multi-region        |
| `doc-`                | Documentation-only repos                           | azure-guides, bicep-notes         |
| `test-`               | Test harnesses or environments                     | integration, load                 |

## 🗂️ Example Subjects

- **Technologies/Resources:** webapi, functionapp, sql, appinsights, cosmosdb, storage, vnet, aks, appservice, logicapp
- **Scenarios:** ci-cd, ai, ml, openid, rbac, monitor, security, devops, eventgrid, staticwebapp, apim

## 📝 Usage Guidelines

- Use **prefixes** to indicate the repo’s category/purpose.
- Use **subjects** for technology, resource, or scenario focus.
- Keep names concise and lowercase, separated by hyphens.
- Add meaningful topics (tags) to each repository for discoverability.
- Document the repo clearly in its README.md.
- Update this file as new categories or subjects are adopted.

---

**Example Repo Names:**
- `template-bicep-webapi`
- `ops-lab-cleanup`
- `showcase-fullstack-todo`
- `lab-ci-cd-pipeline`
- `module-bicep-storage`
- `tool-azure-cost-analyzer`
- `demo-appinsights-monitoring`
- `ref-openid-auth-flow`
- `workshop-devops-fundamentals`

---

_Last updated: 2025-09-10_
