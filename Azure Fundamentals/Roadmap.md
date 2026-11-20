Here's the **complete AZ-900 roadmap** — every topic, every subtopic, laid out day-by-day for 6 weeks. It's designed for a beginner: each day is ~60 minutes, and everything builds on what came before.

> 💡 **Start any Monday.** I've written it as "Day 1, Day 2…" so it works no matter when you begin.

---

# 🗓️ COMPLETE AZ-900 STUDY SCHEDULE

## Week 1 — Cloud Concepts (Domain 1: 25–30% of exam)

| Day | Topic | Subtopics You Must Know |
|-----|-------|--------------------------|
| **Day 1** | **What is cloud computing?** | Cloud definition; the shared responsibility model (you vs. Microsoft); on-premises vs. cloud |
| **Day 2** | **The 3 service models** | **IaaS** (rent VMs, networking, storage), **PaaS** (rent a platform — App Services, DBs), **SaaS** (rent software — Office 365) |
| **Day 3** | **Deployment models** | **Public cloud**, **private cloud** (on-prem), **hybrid cloud** (mix), and *multi-cloud* briefly |
| **Day 4** | **Benefits of cloud — Part 1** | High availability, scalability (vertical = bigger machine, horizontal = more machines), elasticity (auto scale up/down) |
| **Day 5** | **Benefits of cloud — Part 2** | Agility (deploy fast), fault tolerance (keeps running after failure), disaster recovery (backup/restore), predictability (cost + performance) |
| **Day 6** | **Cost models** | **CapEx** (buy upfront — expensive) vs. **OpEx** (pay as you go — Azure's model); consumption-based pricing |
| **Day 7** | **Review & quiz** | Re-watch your Week 1 videos. Take a 10-question "cloud concepts" practice quiz. Write down 15 terms you now know |

---

## Week 2 — Core Architectural Components (start of Domain 2: 35–40% of exam)

| Day | Topic | Subtopics You Must Know |
|-----|-------|--------------------------|
| **Day 8** | **Azure account & subscription** | What an Azure account is; how **subscriptions** group your resources and billing; free account mechanics |
| **Day 9** | **Resource Groups** | What they are (containers/logical folders); why you group related resources; all resources must belong to exactly one |
| **Day 10** | **Regions & Region Pairs** | What a region is (geographic location of data centers); why region pairs exist (recovery + 99.99% uptime); Sovereign regions (like India Central/South) |
| **Day 11** | **Availability Zones** | Physically separate data centers within a region; how they protect against a whole data center failing; zone-redundant services |
| **Day 12** | **Management Groups** | Top-level containers that organize multiple subscriptions; apply policies at the management-group level |
| **Day 13** | **Azure Resource Manager (ARM)** | The "brain" that manages all resources; how the portal, CLI, PowerShell, and templates all use ARM |
| **Day 14** | **Review + go hands-on** | Create a resource group in the portal, then create a resource inside it. Delete both. Practice test on architecture components |

---

## Week 3 — Compute, Networking & Storage (Domain 2 continued)

| Day | Topic | Subtopics You Must Know |
|-----|-------|--------------------------|
| **Day 15** | **Azure Virtual Machines (VMs)** | What a VM is; VM scale sets (auto-run many VMs); availability sets; when to use VMs (full control, lift-and-shift) |
| **Day 16** | **App Services & Containers** | **App Service** (host web apps without managing servers); **Azure Functions** (serverless, event-driven); **Containers** (ACI, AKS) and when to use each |
| **Day 17** | **Virtual Networking (VNet)** | What a VNet is; subnets; **VNet peering** (connecting networks); private vs. public IP addresses |
| **Day 18** | **Load Balancing & Routing** | **Azure Load Balancer** (Layer 4, distributes traffic to VMs); **Application Gateway** (Layer 7, web traffic, has WAF); simple explanation of DNS |
| **Day 19** | **Connecting to on-premises** | **VPN Gateway** (secure connection over the internet); **ExpressRoute** (dedicated private fiber connection); when to choose which |
| **Day 20** | **Azure Storage** | Storage account basics; **Blob storage** (files for apps); **Disk storage** (VM hard drives); **File storage** (shared network drives); **Queues & Tables** (briefly) |
| **Day 21** | **Storage redundancy & tiers** | **LRS, ZRS, GRS, GZRS** (how many copies, where); storage tiers: **Hot, Cool, Cold, Archive** (price vs. speed) |
| **Day 22** | **Azure Databases** | **Azure SQL Database** (relational, managed); **Cosmos DB** (globally distributed NoSQL); **Database for MySQL/PostgreSQL**; when to use each |
| **Day 23** | **Review & practice test** | Full practice test on compute + networking + storage. Identify weak spots (e.g., redundancy levels) and re-watch those |

---

## Week 4 — Identity, Security & Compliance (Domain 2 final part)

| Day | Topic | Subtopics You Must Know |
|-----|-------|--------------------------|
| **Day 24** | **Microsoft Entra ID (Azure AD)** | What identity is; Entra ID = the cloud directory that stores users & groups; single sign-on (SSO) |
| **Day 25** | **Authentication vs. Authorization** | Who you are (auth) vs. what you can do (authz); **Multi-Factor Authentication (MFA)** basics; **Conditional Access** (rules that gate sign-in) |
| **Day 26** | **Role-Based Access Control (RBAC)** | Roles (Owner, Contributor, Reader); scopes (subscription, resource group, resource); who can do what |
| **Day 27** | **Security tools** | **Microsoft Defender for Cloud** (monitors/advises security); network security groups (NSGs); Azure Firewall; key vault (stores secrets) |
| **Day 28** | **Compliance & privacy** | Compliance offerings (GDPR, ISO, HIPAA etc.); the **Trust Center**; Microsoft Privacy Statement; data residency & sovereignty |
| **Day 29** | **Complete Domain 2 review** | Re-do the architecture + compute + storage + security practice tests. Aim for 70%+ |
| **Day 30** | **Rest / light day** | Watch one recap video. No new content. Let it sink in |

---

## Week 5 — Management & Governance (Domain 3: 30–35% of exam)

| Day | Topic | Subtopics You Must Know |
|-----|-------|--------------------------|
| **Day 31** | **Cost factors** | What drives price: resource type, size, region, bandwidth, reserved vs. pay-as-you-go |
| **Day 32** | **Cost management tools** | **Azure Pricing Calculator** (estimate costs); **TCO Calculator** (compare on-prem vs. cloud); **Cost Management + Billing** (track actual spend); **Azure Cost alerts** |
| **Day 33** | **Azure Policy & Blueprints** | **Azure Policy** (enforce rules — e.g., "only allow VMs in India"); **Blueprints** (pre-packaged policy + resource templates); **Resource Locks** (prevent deletion) |
| **Day 34** | **Tags & Resource Groups** | **Tags** (labels like `costcenter`, `environment:dev`); using tags for organization and cost reporting |
| **Day 35** | **Management tools** | **Azure Portal** (website); **Azure CLI** & **PowerShell** (command-line); **Cloud Shell** (browser terminal); **ARM templates / Bicep** (infrastructure-as-code, concept level) |
| **Day 36** | **Monitoring & health** | **Azure Monitor** (logs, metrics, alerts); **Service Health** (Azure service outages/notifications); **Azure Advisor** (personalized recommendations) |
| **Day 37** | **Azure Arc & migration tools** | **Azure Arc** (manage on-premises machines from Azure); **Azure Migrate** (helps move on-prem workloads) |
| **Day 38** | **Complete Domain 3 review** | Practice test on all governance topics. Note your weakest area |

---

## Week 6 — Full Review & Final Practice

| Day | Topic | What To Do |
|-----|-------|------------|
| **Day 39** | **Full mock exam #1** | Sit a full-length practice test (60 questions, timed, like the real thing). Score it |
| **Day 40** | **Review every wrong answer** | For each miss, re-read that topic. Write a one-line note on why you got it wrong |
| **Day 41** | **Weak-spot deep dive** | Spend today ONLY on your weakest domain (probably redundancy levels, RBAC, or cost tools) |
| **Day 42** | **Full mock exam #2** | Take another full practice test. Target 80%+ |
| **Day 43** | **Review + memory aids** | Memorize the quick tables: IaaS/PaaS/SaaS, LRS/ZRS/GRS, Hot/Cool/Cold, Owner/Contributor/Reader |
| **Day 44** | **Light review + rest** | Skim your notes, watch a 20-min "AZ-900 cram" video, relax. Don't cram hard |
| **Day 45** | **📝 EXAM DAY** | Get good sleep the night before, arrive early, and go pass it! 🎉 |

---

## 📊 Quick-Reference Cheat Sheet (memorize these)

| Concept | The 3 you must know |
|---------|---------------------|
| **Service models** | IaaS (VMs) → PaaS (App Service) → SaaS (Office 365) |
| **Deployment** | Public / Private / Hybrid |
| **Storage redundancy** | LRS (1 copy, 1 zone) · ZRS (3 zones) · GRS (2 regions) |
| **Storage tiers** | Hot (fast, costly) · Cool (medium) · Cold/Archive (cheap, slow) |
| **RBAC roles** | Owner (full) · Contributor (build, no access) · Reader (view only) |
| **Cloud benefits** | Availability, Scalability, Elasticity, Agility, Fault Tolerance, DR |
| **Cost model** | CapEx (buy) vs. OpEx (rent) — Azure is OpEx |
That's the entire course, Day 1 through Day 45. Follow it at your own pace — if a day's topic feels hard, spend an extra day on it and shift everything after by one day. The consistency matters more than the calendar.

Good luck — you've got this! 💪
