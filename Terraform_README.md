# Terraform-for-Azure

Here's a senior-level breakdown of all 20 questions — each one explained simply, with an Azure angle so it clicks. I've grouped them logically and added "interview tip" callouts where interviewers dig deeper.

---

## 1. What is Terraform?

Terraform is an **open-source Infrastructure as Code (IaC) tool** created by HashiCorp. You describe your infrastructure (VMs, networks, databases, etc.) in **configuration files** using a human-readable language called **HCL** (HashiCorp Configuration Language), and Terraform turns that description into real resources on Azure (or AWS, GCP, etc.).

Key mental model: **You declare the end state — not the steps.** You say "I want a resource group and a Linux VM," not "create a resource group, then wait, then create a VM."

```hcl
# main.tf
provider "azurerm" {
  features {}
}

resource "azurerm_resource_group" "rg" {
  name     = "rg-interview-prep"
  location = "East US"
}
```

**Interview tip:** Be ready to say Terraform is *declarative* (you state the desired state) as opposed to *imperative* tools like Ansible or shell scripts (you state the steps). Also mention it's provider-agnostic — the same workflow works across Azure, AWS, GCP, Kubernetes, and even on-prem.

---

## 2. What problem does Terraform solve?

Before Terraform, provisioning infrastructure was **manual, slow, and inconsistent**:

- Engineers clicked around the Azure portal to create resources.
- Environments drifted — dev looked nothing like prod (the "snowflake" problem).
- Nobody could easily review or audit what was created.
- Rebuilding an environment took days and required tribal knowledge.
- Terraforming (tearing down and rebuilding) was terrifying, so nobody did it.

Terraform solves this by making infrastructure **repeatable, versionable, reviewable, and automatable**. The same code can create dev, staging, and prod environments, and it's all tracked in Git.

**Interview tip:** Connect this to real pain: *configuration drift*, *snowflake servers*, *change review*, and *automation* (CI/CD pipelines can run `terraform apply`).

---

## 3. What is Infrastructure as Code (IaC)?

IaC is the practice of **managing and provisioning infrastructure through machine-readable definition files** instead of manual UI clicks or ad-hoc commands. Key characteristics:

- Files live in version control → changes are reviewable and auditable.
- Environments are reproducible → same code, same result.
- Enables automation → CI/CD pipelines, self-service platforms.

There are two main styles:

| Style | Example | Meaning |
|---|---|---|
| **Declarative** | Terraform, CloudFormation, Bicep | You declare the *result*; tool figures out the steps |
| **Imperative** | Ansible, shell scripts, Azure CLI | You specify the *steps* to reach the result |

**Interview tip:** Mention that Terraform is declarative *and* that it computes the steps automatically by comparing desired state vs. current state.

---

## 4. What are the benefits of Terraform?

1. **Declarative & readable** — HCL is easy for humans and machines to understand.
2. **Execution plans** — `terraform plan` shows exactly what will change *before* touching anything.
3. **Multi-cloud** — one tool for Azure, AWS, GCP, Kubernetes, VMware, etc.
4. **State-based drift detection** — Terraform knows what's deployed and can detect manual changes.
5. **Automation-friendly** — runs headlessly in CI/CD pipelines with no UI.
6. **Modularity** — reusable modules let teams standardize (e.g., one "networking" module used everywhere).
7. **Version-controlled** — infrastructure changes go through pull requests and reviews like code.
8. **Fast teardown** — `terraform destroy` removes everything cleanly.
9. **Huge ecosystem** — thousands of providers and community modules.
10. **Idempotent** — running apply multiple times converges to the same end state.

**Interview tip:** For a senior role, emphasize **drift detection** and **predictable change management** — those are the operational wins, not just "it's faster."

---

## 5. How does Terraform differ from CloudFormation?

| | Terraform | CloudFormation |
|---|---|---|
| **Scope** | Multi-cloud (Azure, AWS, GCP, K8s…) | AWS only |
| **Language** | HCL (also JSON) | YAML/JSON |
| **State** | Explicit state file (local or remote backend) | Managed internally by AWS; you don't handle a state file |
| **Failure behavior** | Partial apply — keeps what succeeded, reports errors | Automatic rollback of the whole stack by default |
| **Cost** | Open-source core free; paid enterprise features | Free (part of AWS) |
| **Ecosystem** | Providers + module registry, third-party tools | AWS-native only; integrates deeply with IAM, CloudWatch |
| **Maturity** | Broad community, more third-party integrations | Deepest AWS-specific integration (e.g., custom resources, drift via CloudFormation APIs) |

**Interview tip:** A classic senior nuance: **CloudFormation rolls back on failure; Terraform doesn't.** In Terraform you must design for idempotency and use remote state locking to handle concurrent applies. Also note you can use **Azure Bicep** as Azure's native IaC alternative — a common comparison in Azure-focused interviews.

---

## 6. What is the Terraform workflow?

The core workflow is **Write → Plan → Apply**:

1. **Write** — author `.tf` configuration files (resources, variables, outputs, modules).
2. **Init** — `terraform init` downloads providers/modules and sets up the backend.
3. **Plan** — `terraform plan` shows a preview of changes.
4. **Review** — (team practice) review the plan in a PR or CI.
5. **Apply** — `terraform apply` executes the plan and updates state.
6. **(Optional) Destroy** — `terraform destroy` tears infrastructure down.

In a team setting you add: code review, CI runs of `fmt`/`validate`/`plan`, and applying via pipeline with approvals for production.

**Interview tip:** Mention the **"plan with approval" pattern**: CI runs `terraform plan`, posts the diff, a human approves, then a pipeline runs `terraform apply -auto-approve`. This is the enterprise-grade workflow.

---

## 7. What is a Terraform provider?

A **provider** is a plugin that lets Terraform talk to a specific platform's API. It translates Terraform config into API calls. For Azure, the provider is **`azurerm`** (and `azuread` for Entra ID / AAD).

```hcl
# providers.tf
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~> 3.0"
    }
  }
}

provider "azurerm" {
  features {}
  subscription_id = var.subscription_id
}
```

Providers are downloaded from the **Terraform Registry** during `terraform init`, and it's best practice to **pin versions** so behavior doesn't change unexpectedly.

**Interview tip:** Distinguish *provider* (e.g., `azurerm`) from *resource* (e.g., `azurerm_virtual_network`). Interviewers like hearing that the provider also handles **authentication** (Azure CLI, service principal, managed identity) and **API versioning**.

---

## 8. What is Terraform Core?

**Terraform Core** is the engine of Terraform — the binary that:

- Reads and parses HCL configuration.
- Builds a **dependency graph** of resources (what depends on what).
- Determines the order of operations (create VNet before VM, etc.).
- Produces the execution plan.
- Orchestrates providers via a plugin interface (RPC).
- Manages **state**.

Think of it as the brain; providers are the hands that actually touch Azure.

**Interview tip:** A senior answer: "Core is *platform-agnostic*; all cloud-specific behavior lives in providers. Core computes the graph and the plan; providers execute the API calls." Also mention **graph parallelism** — Terraform applies independent resources in parallel.

---

## 9. What are Terraform resources?

**Resources** are the fundamental building blocks of Terraform — the things it creates, updates, and deletes: VMs, resource groups, subnets, storage accounts, etc. A resource block has a type, a name, and arguments.

```hcl
resource "azurerm_resource_group" "rg" {
  name     = "rg-prod"
  location = "Central India"
}

resource "azurerm_virtual_network" "vnet" {
  name                = "vnet-prod"
  resource_group_name = azurerm_resource_group.rg.name
  location            = azurerm_resource_group.rg.location
  address_space       = ["10.0.0.0/16"]
}
```

Resources expose **attributes** (e.g., `azurerm_resource_group.rg.name`) that other resources can reference — this creates dependencies. They also support **meta-arguments**: `count`, `for_each`, `depends_on`, `provider`, `lifecycle` (e.g., `prevent_destroy`, `ignore_changes`).

**Interview tip:** Be fluent in `for_each` vs `count`, and `lifecycle` blocks — those are classic senior-level questions.

---

## 10. What are Terraform data sources?

**Data sources** are **read-only queries** — they fetch existing information from the cloud without creating or changing anything. Useful when infrastructure already exists and you want to reference it.

```hcl
# Fetch an existing resource group instead of creating one
data "azurerm_resource_group" "existing" {
  name = "rg-existing"
}

resource "azurerm_virtual_network" "vnet" {
  name                = "vnet-new"
  resource_group_name = data.azurerm_resource_group.existing.name
  location            = data.azurerm_resource_group.existing.location
  address_space       = ["10.1.0.0/16"]
}
```

Common use cases: looking up the current subscription (`data "azurerm_client_config"`), existing VNets, key vaults, images, or reading secrets to pass to resources.

**Interview tip:** Emphasize the contrast: **resources manage infrastructure; data sources read it.** Also mention data sources can have `depends_on` and are refreshed during plan/apply.

---

## 11. What is `terraform init`?

`terraform init` **initializes the working directory**. It:

- Downloads and installs the required providers (e.g., `azurerm`).
- Downloads modules referenced in the config.
- Configures the **backend** (where state is stored — e.g., Azure Storage Account).
- Creates `.terraform` directory and `.terraform.lock.hcl` (dependency lock file).

It's the **first command** you run in any Terraform project, and it's **safe to run repeatedly** — the lock file ensures consistent provider versions.

**Interview tip:** Mention the lock file and that `init` is also needed after changing providers, modules, or backend configuration.

---

## 12. What is `terraform plan`?

`terraform plan` is a **dry run** — it compares your configuration against the current state and shows the **execution plan**: what will be created, changed, or destroyed. It makes **no actual changes**.

Output symbols:

- `+` create
- `~` update/change
- `-` destroy
- `-/+` replace (destroy then recreate)

You can save the plan to a file with `-out=plan.tfplan` and apply that exact plan later — this guarantees what you reviewed is exactly what gets applied.

**Interview tip:** Say "plan is the change-management review artifact. In CI, we run `plan` and post the output for review before any apply." Also mention `-refresh-only` plans (see #17).

---

## 13. What is `terraform apply`?

`terraform apply` **executes the plan** — it creates, updates, or deletes real infrastructure to match your config. By default it runs a plan first and asks for confirmation; `-auto-approve` skips the prompt. After a successful apply, Terraform updates the state file.

```bash
terraform apply                 # preview + confirm
terraform apply -auto-approve   # no prompt (CI)
terraform apply plan.tfplan      # apply a saved plan
```

**Interview tip:** Mention that apply is **not all-or-nothing** — it applies resources in dependency order and, if something fails partway, the successful resources remain (unlike CloudFormation's rollback). That's why idempotent code and remote state locking matter.

---

## 14. What is `terraform destroy`?

`terraform destroy` **removes all resources tracked in state** for the current configuration. It's essentially an apply of an "empty" plan. You can also target specific resources with `-target`.

```bash
terraform destroy
terraform destroy -target=azurerm_virtual_network.vnet
```

**Interview tip:** Emphasize safety: in production, use `lifecycle { prevent_destroy = true }` on critical resources (like databases) and require approval via pipelines. Also note `destroy` is a big superpower — it enables ephemeral environments, which is a huge DevOps win.

---

## 15. What is `terraform validate`?

`terraform validate` performs a **static check** of your configuration — it validates:

- HCL syntax correctness.
- Valid attribute names and types.
- References (e.g., referencing a resource that doesn't exist).
- Required arguments present.

It runs **offline** (no cloud credentials needed) and is perfect for CI gates.

**Interview tip:** Contrast with `plan`: `validate` is fast and requires no cloud connection; `plan` is deeper and talks to the cloud/state. Run both in CI.

---

## 16. What is `terraform fmt`?

`terraform fmt` **auto-formats** HCL code to the canonical style — fixes indentation, alignment, spacing. It's idempotent and safe. Use `terraform fmt` (folder-wide) or `terraform fmt -check` in CI to fail on unformatted code.

```bash
terraform fmt
terraform fmt -check -recursive
```

**Interview tip:** Mention the `-recursive` and `-check` flags and that it belongs in pre-commit hooks / CI, like `gofmt` or `prettier`.

---

## 17. What is `terraform refresh`?

`terraform refresh` **updates the state file** to match the real-world infrastructure — it detects manual changes (drift) and syncs them into state, without modifying infrastructure.

Modern nuance: since Terraform 1.5, `plan` and `apply` auto-refresh by default, so `terraform refresh` is rarely run directly. You can now do `terraform plan -refresh-only` (and `apply -refresh-only`) to sync state without changing anything else.

**Interview tip:** This is a favorite senior question. Say: "Refresh reconciles state with reality. With auto-refresh in plan/apply, standalone refresh is mostly obsolete, but `-refresh-only` plans give you a safe, reviewable drift-sync." Also note refresh does **not** fix drift in the cloud — it just records it.

---

## 18. What is a Terraform configuration file?

A **configuration file** is a `.tf` file that defines the desired infrastructure. A typical project splits concerns across files:

| File | Contents |
|---|---|
| `providers.tf` | Provider requirements & configuration |
| `main.tf` | Core resources |
| `variables.tf` | Input variable declarations |
| `outputs.tf` | Output values |
| `terraform.tfvars` | Variable values (filled in) |
| `versions.tf` | Required Terraform version constraints |

All `.tf` files in a directory are **merged** into one configuration. The directory is called the **root module**.

**Interview tip:** Mention that everything in a folder is a module, and that modules are the unit of reuse — e.g., an internal "azure-vnet" module shared by many projects.

---

## 19. What file extensions are used by Terraform?

| Extension | Purpose |
|---|---|
| `.tf` | HCL configuration files |
| `.tf.json` | JSON-format configuration (machine-generated) |
| `.tfvars` | Variable definitions (HCL format) |
| `.tfvars.json` | Variable definitions (JSON format) |
| `.hcl` | Generic HCL (e.g., `.terraformrc` CLI config) |
| `.terraform.lock.hcl` | Dependency lock file (created by `init`) |
| `.terraform` | Directory (internal cache; not committed) |
| `.terraformignore` | Files to exclude when packaging modules |

**Interview tip:** Know that `.tfvars` files override defaults and that sensitive variable files (like `.auto.tfvars`) should be gitignored or stored in a secret store.

---

## 20. Explain Terraform architecture.

The architecture has these layers:

```
┌─────────────────────────────────────────────┐
│  CLI (user commands: init, plan, apply...)  │
├─────────────────────────────────────────────┤
│  TERRAFORM CORE                             │
│  • Parses HCL config                        │
│  • Builds dependency graph                  │
│  • Computes plan (desired vs current state) │
│  • Manages state & locking                  │
│  • Orchestrates providers (plugin RPC)      │
├─────────────────────────────────────────────┤
│  PROVIDERS (plugins)                        │
│  • hashicorp/azurerm                        │
│  • hashicorp/azuread                        │
│  • Others...                                │
├─────────────────────────────────────────────┤
│  CLOUD APIs                                 │
│  • Azure Resource Manager (ARM)             │
│  • Microsoft Graph / Entra ID               │
└─────────────────────────────────────────────┘
```

Key architecture elements to mention:

1. **Core** — the engine (graph, plan, state).
2. **Providers** — plugins translating config → API calls.
3. **Backend** — where state lives. Local by default; remote for teams (e.g., Azure Storage Account with blob-based **state locking** via leases).
4. **State** — the source of truth for what exists.
5. **Module registry** — reusable, published configurations.
6. **Variables/Outputs** — inputs and outputs that make configs reusable.

For Azure specifically: the backend is an **Azure Storage Account** (container + blob), with `azurerm` backend config:

```hcl
terraform {
  backend "azurerm" {
    resource_group_name  = "rg-tfstate"
    storage_account_name = "tfstateprod"
    container_name       = "tfstate"
    key                 = "terraform.tfstate"
  }
}
```

**Interview tip:** Explain the full loop: *Config → Core builds graph → Providers call Azure APIs → State records results*. And note that **remote state + locking** is a hard requirement for any team — you don't want two engineers applying simultaneously.

---

## Senior-level golden notes

- **State is sensitive** — secrets live in state; use remote backends + encryption, and never commit local state.
- **Drift is real** — manual Azure portal changes show up in the next `plan`; auto-refresh surfaces them.
- **Provider versioning** — pin versions, use the lock file, upgrade deliberately.
- **Module hygiene** — design small, composable modules; version them.
- **CI/CD integration** — `fmt -check` → `validate` → `plan` → approval → `apply -auto-approve` is the enterprise pattern.
- **Destructive change safety** — `prevent_destroy`, `-target` with caution, and destroy approval gates.

Good luck with the interview — master the workflow (init → plan → apply → destroy), the Core-vs-Provider split, and remote state with locking, and you'll handle 90% of what a senior DevOps panel throws at you.
