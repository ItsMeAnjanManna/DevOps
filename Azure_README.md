### 1. What is Microsoft Azure?
Azure is Microsoft's public cloud platform. It lets you rent Microsoft's compute, storage, networking, and databases on-demand instead of buying your own hardware. Think of it as "renting a computer in someone else's building, but the building is enormous and global."

### 2. What is cloud computing?
Cloud computing is delivering computing resources (servers, storage, databases, networking, software) over the internet, on-demand, with pay-as-you-go pricing. Key characteristics: **on-demand self-service, broad network access, resource pooling, rapid elasticity (scale up/down fast), and measured service** (you pay for what you use). In Azure, this means spinning up a VM in 2 minutes that would take weeks to procure physically.

### 3. What are the different cloud models?
Three deployment models:
- **Public cloud** — Azure, AWS, GCP. Shared infrastructure owned by the provider.
- **Private cloud** — Infrastructure dedicated to a single organization (on-premises or hosted), like Azure Stack or VMware private clouds.
- **Hybrid cloud** — Connecting public and private clouds (e.g., Azure Arc extending Azure management to on-premises servers).

There are also **multi-cloud** (using multiple public providers) and **community cloud** (shared by several organizations with common needs), though the big three are public, private, hybrid.

### 4. Difference between IaaS, PaaS, and SaaS?
This is about **how much you manage vs. the provider**:

- **IaaS (Infrastructure as a Service)** — You rent raw infrastructure: VMs, storage, networking. You manage OS, runtime, app; Azure manages physical hardware. *Example:* Azure Virtual Machines.
- **PaaS (Platform as a Service)** — The platform is managed for you. You just deploy your code; Azure handles OS patching, runtime, scaling, load balancing. *Example:* Azure App Service, Azure Functions.
- **SaaS (Software as a Service)** — Fully managed software you just use via a browser/API. *Example:* Microsoft 365, Dynamics 365.

**Interview tip:** Frame it as the "management responsibility spectrum" — IaaS = you manage most, PaaS = provider manages platform, SaaS = provider manages everything.

### 5. What are Azure Regions?
A region is a geographic area containing one or more datacenters (e.g., East US, West Europe, Southeast Asia). You choose a region for your resources to control latency (put resources near users) and meet data residency/compliance laws (e.g., India data must stay in India for some workloads).

### 6. What are Availability Zones?
Within a region, there are physically separate **datacenters** (typically 3) called Availability Zones. Each zone has independent power, cooling, and networking. If one zone fails, others keep running. You deploy your app across multiple zones for **high availability**. *Example:* Put two VMs in the same region but different zones behind a load balancer — if one datacenter burns down, the other zone still serves traffic.

### 7. What are Region Pairs?
Each region is paired with another region in the same geography (e.g., East US ↔ West US, Southeast Asia ↔ East Asia). Pairs are at least 300 miles apart, so a regional disaster rarely takes out both. Azure uses pairs for **planned maintenance** (only one side updated at a time) and **disaster recovery** (you replicate to the pair). *Example:* For DR, replicate your SQL database to the paired region.

### 8. What are Azure Datacenters?
Physical buildings housing servers, storage, networking, and power/cooling. They're the physical reality behind regions/zones. Azure has 300+ datacenters globally. Not much more to it at interview level — you'd mention physical security, redundancy (power, cooling), and that zones group datacenters.

### 9. What is Azure Resource Manager (ARM)?
ARM is Azure's **management/control plane** — the service that handles creating, updating, and deleting resources. Every resource is defined declaratively via ARM. When you click "create" in the portal, run a CLI command, or deploy a template, ARM processes it, validates it, and applies it. It handles auth (RBAC), tagging, and orchestration.

### 10. What is a Resource Group?
A resource group is a **logical container** that holds related resources for an Azure solution. Example: your web app's RG contains the App Service, SQL database, and VNet. You manage them as a unit — you can apply permissions, tags, and policies at the RG level, and delete the whole RG to clean up everything at once.

### 11. Can a resource belong to multiple Resource Groups?
**No.** Every resource belongs to exactly one resource group. That's a hard rule — a VM can't be in two RGs. (You *can* have a resource reference resources in other RGs, e.g., a VM using a VNet from another RG, but membership is one-to-one.)

### 12. Can a Resource Group span regions?
**Yes.** An RG is just a logical container in a specific subscription — it's not tied to a physical location. Its resources can live in different regions. The RG itself has a location (that's just where its metadata is stored), but that location doesn't constrain where its resources go.

### 13. What is an Azure Subscription?
A subscription is the **billing and access boundary** in Azure. It's a logical container for resource groups (which contain resources). Your organization's Azure account can have multiple subscriptions to separate billing, isolate environments (Dev/Test/Prod), and manage access/costs independently.

### 14. Difference between Subscription and Resource Group?

| | Subscription | Resource Group |
|---|---|---|
| **Scope** | Highest-level container in an account | Container *inside* a subscription |
| **Contains** | Resource groups | Resources |
| **Purpose** | Billing, access boundary, limits | Logical grouping of related resources |
| **Example** | "Production" subscription | "prod-web-app" RG holding the app + DB |

Subscriptions are for **cost + governance isolation**; RGs are for **logical organization** of resources.

### 15. What is Azure Management Group?
Management groups sit **above subscriptions** in the hierarchy. They let you organize multiple subscriptions and apply **policies, RBAC, and budgets** across all of them. *Example:* A "Dev" management group containing all dev subscriptions, where you enforce a policy that bans certain VM sizes and apply a shared cost budget. They support up to 6 levels of nesting.

### 16. Explain Azure Hierarchy.
Top-down:
```
Tenant (Azure AD / Entra ID)
 └── Management Groups
      └── Subscriptions
           └── Resource Groups
                └── Resources
```
- **Tenant** = your organization's identity boundary (Entra ID).
- **Management Groups** = organize subscriptions, apply policy/access across them.
- **Subscriptions** = billing + access boundary.
- **Resource Groups** = logical grouping of resources.
- **Resources** = actual services (VMs, storage, etc.).

Governance flows down: policies and RBAC assigned at higher levels inherit down to resources.

### 17. What is Azure Marketplace?
A catalog of pre-built solutions you can deploy into Azure — from Microsoft and third-party vendors. Includes VMs with pre-installed software, containers, SaaS apps, and templates. *Example:* Deploy a pre-configured NGINX VM or a Kubernetes cluster from the marketplace instead of building from scratch. Useful for quick starts and certified images.

### 18. What is Azure Portal?
The **web-based GUI** (portal.azure.com) for managing Azure resources. It's a UI front-end to ARM. You can browse resources, create/delete them, monitor, and use built-in tools like Cloud Shell. Good for exploration and manual ops, but not ideal for automation (that's CLI/templates/scripts).

### 19. What is Azure CLI?
A **cross-platform command-line tool** (works on Windows, macOS, Linux; also in-browser via Cloud Shell) for managing Azure. Commands follow a pattern like `az group create --name rg-web --location eastus`. It's scriptable, automation-friendly, and returns JSON output. Essential for DevOps — you can put CLI commands in CI/CD pipelines.

### 20. What is Azure PowerShell?
The same management capability as the CLI, but as **PowerShell cmdlets** (e.g., `New-AzResourceGroup -Name rg-web -Location eastus`). Use it when you're in a PowerShell ecosystem or need PowerShell-specific scripting (e.g., mixing Azure management with other PowerShell automation). Same ARM control plane underneath — just a different syntax.

### 21. What is Azure Cloud Shell?
An **in-browser terminal** in the Azure Portal that gives you a ready-to-use Bash (with Azure CLI) or PowerShell environment. It's authenticated automatically with your Azure credentials, persists files (home directory backed by an Azure File Share), and requires no local setup. Great for quick admin commands without installing anything.

### 22. What is ARM Template?
A **JSON (or Bicep) declarative file** that defines your infrastructure — all resources, their properties, and dependencies. You deploy it to Azure and ARM creates/updates everything in the correct order. It's **idempotent** (deploying the same template twice yields the same result) and supports parameters, variables, and loops. This is Azure's native Infrastructure-as-Code (IaC).

### 23. Difference between ARM and Terraform?

| | ARM (Bicep) | Terraform |
|---|---|---|
| **Scope** | Azure-only | Multi-cloud (Azure, AWS, GCP…) |
| **Language** | JSON / Bicep | HCL (Hashicorp Configuration Language) |
| **State** | Stored/managed by Azure (ARM handles it) | Local/remote state file you manage |
| **Best for** | Pure Azure shops, deep Azure integration | Multi-cloud or consistent IaC across providers |
| **Execution** | ARM control plane | Terraform binary executes against provider APIs |

**Interview tip:** Mention that Bicep is a newer, cleaner alternative to JSON ARM templates, and that Terraform is preferred when you want one tool across clouds. Both are valid; choose based on ecosystem.

### 24. What are Azure Tags?
Tags are **key-value pairs of metadata** you attach to resources, resource groups, or subscriptions — e.g., `Environment: Production`, `CostCenter: 1234`, `Owner: platform-team`. They're purely organizational — they don't affect how a resource functions.

### 25. Why are tags important?
Tags are your primary tool for **governance, cost management, and operations**:
- **Cost tracking** — group costs by tag (e.g., per-team, per-environment budgets in Cost Analysis).
- **Filtering & organization** — find resources quickly; list "all production VMs."
- **Automation** — trigger policies/scripts based on tags (e.g., auto-shutdown VMs tagged `Environment: Dev`).
- **RBAC & policy** — apply policies that *require* certain tags (e.g., deny resource creation without a cost-center tag).
- **Ownership** — document who owns what, critical at enterprise scale.

**Senior-level gotcha:** Tagging discipline must be enforced with **Azure Policy**, or it decays fast. Also, not all resources support all tags, and tags don't inherit automatically (though policy can enforce inheritance).

---

Want me to turn any of these into deeper drill-downs — e.g., ARM vs. Terraform in detail, governance with policy/RBAC, or typical senior DevOps interview follow-up questions on these topics?
