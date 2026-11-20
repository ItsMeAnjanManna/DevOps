# 📘 WEEK 5 — MANAGEMENT, GOVERNANCE & COST
### *(Covers the rest of Domain 3: 30–35% of the exam)*

---

# 📅 Day 29 — Week 4 Wrap-Up + The Final Roadmap

## 🧠 First, a quick win
You've already finished **all of Domain 1 (Cloud Concepts)** and **all of Domain 2 (Architecture, Compute, Networking, Storage, Databases, Security)**. That's roughly **60–65% of the exam** already in your pocket — no need to learn it again today, just *recall* it.

## 📋 Week 4 quick fire-review (say this out loud before reading further)
1. **SQL vs. NoSQL:** structured tables vs. flexible documents.
2. **Cosmos DB:** globally distributed, multi-model.
3. **Entra ID:** the master guest list (was "Azure AD").
4. **Authentication ≠ Authorization:** passport vs. boarding pass.
5. **MFA factors:** something you know / have / are.
6. **Conditional Access:** smart rules (time, device, risk).
7. **RBAC = principal + role + scope.** Roles: Reader → Contributor → Owner.
8. **Defender for Cloud:** CCTV + security consultant (Secure Score).
9. **NSG vs. Azure Firewall:** entrance guard vs. city checkpoint.
10. **Key Vault:** safety deposit box for secrets.
11. **Compliance:** passing inspections; Trust Center = report wall.
12. **Data residency vs. sovereignty:** where vs. whose laws.
13. **Zero Trust:** never trust, always verify.

## 🗺️ What's left (your final roadmap)
Only **one domain** remains — the "business/governance" side of Azure:

| Topic | What it really is | Where in this week |
|-------|-------------------|--------------------|
| Cost factors | What makes your bill go up/down | Day 30 |
| Cost tools | Pricing Calculator, TCO, Cost Management | Day 31 |
| Policy, locks, tags | Rules & labels to keep things tidy/safe | Day 32 |
| Management tools | Portal, CLI, PowerShell, templates | Day 33 |
| Monitoring | Azure Monitor, Service Health, Advisor | Day 34 |
| Migration | Moving existing systems to Azure | Day 35 |

After Week 5, **Week 6 = full mock exams + final review + exam-day tips.**

## 📌 Today's only task (keep it light)
- Do the quick fire-review above.
- Then set aside **20 minutes** to browse the **Azure Pricing Calculator** (`azure.microsoft.com/pricing/calculator`) — just click around, don't buy anything. You'll use it properly on Day 31.

## ✅ Day 29 Checklist
- [ ] I can say all 13 Week-4 points without peeking
- [ ] I know exactly what's left: only the governance domain
- [ ] I've clicked around the Pricing Calculator once

---

# 📅 Day 30 — What Actually Drives Azure Costs?

## 🧠 The core question
**"Why is my Azure bill what it is?"** Understanding cost factors is a favourite exam topic. The good news: it's mostly common sense — like understanding a restaurant bill.

## 💸 The 5 main cost factors (memorize)

**1. Resource type (what you use)**
- Different services cost different amounts: a large VM costs far more than a tiny storage account.
- **Real-life analogy:** A steak dinner costs more than a cup of chai — the *item* determines the base price.

**2. Size / performance tier (how big or fast)**
- Bigger VM = more vCPU + RAM = higher price.
- Premium SSD (fast) costs more than Standard HDD (slow).
- **Real-life analogy:** A bigger car (7-seater) costs more than a hatchback; a sports car costs more than a family sedan.

**3. Region (where it runs)**
- The same service costs differently in different regions (due to power costs, taxes, local pricing).
- **Real-life example:** Running a VM in Central India (Pune) vs. East US may have different prices. Data transfer out of a region also costs money.
- **Real-life analogy:** The same coffee costs more in a posh mall than at a local stall.

**4. Bandwidth / data transfer (how much moves)**
- **Ingress (data entering Azure) is usually free.**
- **Egress (data leaving Azure) costs money** — especially across regions or to the internet.
- **Real-life analogy:** Like an ISP plan — downloading may be unlimited, but sending huge files out costs data.

**5. Support & licensing extras**
- Support plans (free basic vs. paid professional/direct).
- Windows VMs cost more than Linux (license included).
- **Azure Hybrid Benefit:** If you already own Windows Server/SQL Server licenses, you can reuse them on Azure to save money.

## 🎛️ The pricing "models" (how you pay)

| Model | How it works | Best for | Example |
|-------|--------------|----------|---------|
| **Pay-as-you-go** | Pay per second/minute of use, no commitment | Variable/unknown workloads | Test environments, spikes |
| **Reserved Instances** | Commit 1 or 3 years, get big discount (up to ~72%) | Predictable, always-on workloads | A production VM that runs 24/7 |
| **Spot VMs** | Use Azure's unused capacity at a big discount; Azure can reclaim them anytime | Fault-tolerant, interruptible jobs | Batch processing, rendering, testing |
| **Azure Hybrid Benefit** | Bring your own Windows/SQL licenses to reduce cost | Companies with existing Microsoft licenses | Enterprises already paying for SQL |

> 🧠 **Memory trick:** Pay-as-you-go = pay per cup of chai. Reserved = buy a yearly chai pass (discount, but you pay even on days you skip). Spot = last-minute unsold restaurant table (cheap, but you may be asked to leave).

## 📉 What makes costs go UP (quick list)
- Adding more resources (more VMs, more storage).
- Choosing bigger sizes / faster disks.
- Leaving resources running when you don't need them (e.g., a dev VM left on overnight!). ⚠️
- High data egress (moving data out of Azure).
- Choosing premium tiers (e.g., Hot storage tier, Premium SSD).
- Not deleting test resources (the #1 beginner cost trap).

## ✅ Day 30 Checklist
- [ ] I can list the 5 cost factors
- [ ] I know ingress is usually free; egress costs
- [ ] I can explain pay-as-you-go vs. reserved vs. spot with the chai/table analogies
- [ ] I know "leaving dev VMs running" is a common money-waster

---

# 📅 Day 31 — Cost Management & Planning Tools

Today you learn the **tools that help you predict and control costs**. These are exam favourites — know each name and what it does.

## 🧮 1. Azure Pricing Calculator
**What it is:** An interactive web tool to **estimate the cost** of Azure services *before* you build anything.

**Real-life analogy:** A **proforma invoice** from a contractor — "if you build this, it will cost roughly this much."

**How to use it (concept):**
- Pick services (VM, storage, DB), configure size/region/uptime.
- It gives a monthly estimate in your currency.
- You can save/share configurations and export estimates.

**Exam fact:** It's for **estimating** (planning). It does NOT show your actual bill.

## ⚖️ 2. TCO Calculator (Total Cost of Ownership)
**What it is:** A tool that **compares the cost of running your workload on-premises vs. on Azure** over time (typically 3 years).

**Real-life analogy:** Comparing **owning a car vs. using Uber for 3 years** — the TCO calculator adds up car price + fuel + insurance + maintenance (on-prem) vs. per-ride costs (cloud).

**Exam fact:** It considers hardware, software, electricity, IT staff, and downtime. Great for building a business case to move to the cloud.

## 💳 3. Cost Management + Billing
**What it is:** The service where you **see your actual spending**, set budgets, and get alerts.

**Real-life analogy:** Your **bank's spending tracker** — it shows where money went, lets you set a monthly budget, and alerts you when you're close to the limit.

**Key features:**
| Feature | What it does |
|---------|--------------|
| **Cost analysis** | See where money is spent (by service, resource group, tag) |
| **Budgets** | Set a spending limit (e.g., ₹2,000/month) |
| **Alerts** | Get notified when you hit 80%, 90%, 100% of budget |
| **Recommendations** | Azure suggests ways to save (e.g., "resize this idle VM") |

## 🏷️ 4. Tags (cost connection)
Tags (key-value labels like `environment:dev` or `costcenter:marketing`) let you **group spending** in Cost Management. (Full tag lesson tomorrow — just know they power cost reporting.)

## ⚠️ 5. Free-account reality check (important for you!)
Your free account gives you **₹7,000-ish (~$200) credit for 30 days**, plus 12 months of popular free services and 25+ always-free services.
- **The catch:** When credit runs out or the free period ends, you can be charged if you still have paid resources running.
- **Beginner rule:** Always **delete experiments** (or the whole resource group) after playing. Free tiers exist, but they have limits — exceeding them costs money.

## ✅ Day 31 Checklist
- [ ] I can explain Pricing Calculator (estimate before building) vs. Cost Management (see actual spend)
- [ ] I know TCO Calculator compares on-prem vs. cloud
- [ ] I know budgets + alerts exist in Cost Management
- [ ] I remember to delete everything after experimenting!

---

# 📅 Day 32 — Governance: Policy, Blueprints, Locks & Tags

This is the "rules and discipline" day — how organizations keep thousands of resources safe, tidy, and compliant.

## 📜 1. Azure Policy
**What it is:** A service that **creates and enforces rules** on your resources. If a resource violates a rule, Azure can **deny, audit, or fix** it automatically.

**Real-life analogy:** **Building codes** in a city:
- The city says: "No building taller than 10 floors in this zone."
- When someone submits a plan, the inspector checks it against the code and rejects what doesn't comply.
- Azure Policy is that inspector — but automated and always on.

**How it works (keep simple):**
- You define a **policy definition** (the rule): e.g., "Only allow resources in India regions."
- You **assign** it to a scope (management group, subscription, resource group).
- The **effect** decides what happens:
  - **Deny** — block the resource creation outright.
  - **Audit** — allow it but record a warning.
  - **Append/Modify** — automatically add something (e.g., force a tag).

**Real-world examples:**
- "Deny VMs bigger than Standard_D4s_v3" (cost control).
- "Audit if disks are not encrypted" (security).
- "Require a tag named `owner` on every resource" (organization).

> **Exam note:** Azure Policy is about **rules on resources**. Don't confuse it with RBAC (permissions for people) — Policy is about *what resources may look like*, RBAC is about *who can touch them*.

## 📦 2. Azure Blueprints (know the concept)
**What it is:** A **pre-packaged bundle** of policy assignments, role assignments, resource groups, and ARM templates that you deploy as one unit — "a compliant starter kit" for a project.

**Real-life analogy:** A **"new restaurant opening" checklist kit**: the owner gets the same approved layout, licenses, safety rules, and equipment list every time — so every new branch is consistent and compliant.

**Exam note:** Blueprints standardize environments (e.g., every new subscription gets the same security policies and default resource group). *(Fun fact: Microsoft is slowly shifting away from Blueprints toward "Template Specs" + Policy Initiatives — but the exam still tests the Blueprints concept.)*

## 🔒 3. Resource Locks
**What it is:** A protection to **prevent accidental deletion or modification** of critical resources.

**Real-life analogy:** A **"do not remove" seal** on important office equipment — or a locked drawer for the cash box. Nobody can take it by accident.

**Two lock types (memorize):**

| Lock | What it prevents |
|------|------------------|
| **CanNotDelete** | Prevents deletion, but allows changes |
| **ReadOnly** | Prevents BOTH deletion and modification (read-only) |

**Exam notes:**
- Locks apply at **resource, resource group, or subscription** scope.
- Locks affect **everyone**, including Owners! (Only removing the lock lets you change the resource.)
- **Real-world use:** Lock your production database so no one deletes it during a late-night mistake. 🛡️

## 🏷️ 4. Tags
**What it is:** **Key-value labels** attached to resources (e.g., `environment=production`, `costcenter=sales`, `owner=raj`).

**Real-life analogy:** **Sticky notes on folders** — they don't change what's inside, but they make it easy to find, organize, and bill things.

**What tags do for you:**
- **Cost reporting:** group spending by tag in Cost Management.
- **Organization:** filter resources by project/department.
- **Automation:** perform actions on all tagged resources.
- **Compliance:** policies can *require* tags (via Append effect).

**Important gotcha:**
- Tags are **not inherited automatically** from a resource group (a policy can be used to copy/append them, but by default a tag on the RG doesn't flow to resources).
- Tags are **metadata only** — they don't affect how the resource works.
- Tags don't apply to all resource types equally (some legacy resources don't support tags).

## 📊 Governance tools quick table

| Tool | What it does | Analogy |
|------|--------------|---------|
| Azure Policy | Rules on what resources can be | Building codes/inspector |
| Blueprints | Pre-packaged compliant starter kit | New-branch checklist kit |
| Resource Locks | Prevent deletion/modification | "Do not remove" seal |
| Tags | Labels for cost & organization | Sticky notes on folders |
| Management Groups (recap) | Organize subscriptions, inherit rules | Company departments |

## ✅ Day 32 Checklist
- [ ] I can explain Policy (rules) vs. RBAC (permissions) vs. Locks (protection)
- [ ] I know the 3 effects: Deny / Audit / Append
- [ ] I know CanNotDelete vs. ReadOnly
- [ ] I know tags = metadata for cost/organization (and aren't auto-inherited)

---

# 📅 Day 33 — Management Tools: Portal, CLI, PowerShell, Cloud Shell & IaC

Today: the **different "remotes" you use to drive Azure.** They all do the same things — you just pick what feels comfortable.

## 🖥️ 1. Azure Portal (the website)
- The clickable web interface: `portal.azure.com`.
- **Best for:** beginners, visual exploration, one-off tasks.
- **Real-life analogy:** The bank's **mobile app** — friendly, visual, easy.

## ⌨️ 2. Azure CLI (command line)
- Text commands you type in a terminal, e.g.: `az vm create --name myvm ...`
- **Best for:** automation, scripting, repeatable tasks.
- **Real-life analogy:** The bank's **ATM** — faster once you know it, but you must know the buttons.

## 💻 3. Azure PowerShell
- Uses PowerShell cmdlets instead of CLI commands, e.g.: `Get-AzVM`
- **Best for:** Windows administrators who already script in PowerShell.
- **Real-life analogy:** Same ATM, but with a different button layout you already know.

## ☁️ 4. Azure Cloud Shell
- A **browser-based terminal** built into the portal — you get Bash or PowerShell **without installing anything**.
- **Real-life analogy:** A **bank kiosk inside the branch** — quick access without downloading an app.
- **Bonus:** It comes with storage (a small file share) so your scripts persist between sessions.

## 🧱 5. Infrastructure as Code (IaC) — ARM Templates & Bicep
**What it is:** Defining your entire infrastructure in **code/text files** instead of clicking.

**Real-life analogy:** A **house blueprint** vs. telling the builder verbally, brick by brick. With a blueprint, every house comes out identical; with verbal instructions, the builder might forget a window.

**Key facts:**
| Tool | What it is |
|------|------------|
| **ARM template** | JSON file describing resources (the classic way) |
| **Bicep** | Newer, simpler, cleaner language (compiles to ARM templates) |

**Why it matters (exam-loved):**
- **Repeatable** — deploy the same environment to dev, test, prod.
- **Declarative** — you say *what* you want; ARM figures out the order.
- **Idempotent** — running the same file twice gives the same result, no duplicates.
- **Version-controlled** — infrastructure lives in Git like code (auditable).

## 📊 Management tools compared

| Tool | Interface | Best for | Analogy |
|------|-----------|----------|---------|
| Portal | Clickable web UI | Beginners, exploring | Mobile banking app |
| CLI | Text commands | Scripting/automation | ATM |
| PowerShell | Cmdlets | Windows admins | ATM, familiar layout |
| Cloud Shell | In-browser terminal | Quick access, no install | Branch kiosk |
| ARM/Bicep | Code files | Repeatable deployments | House blueprint |

> 🔑 **Key exam fact:** The Portal, CLI, PowerShell, and templates all talk to the **same backend — Azure Resource Manager (ARM)** (Week 2, Day 13). They're just different front doors to the same building.

## ✅ Day 33 Checklist
- [ ] I can name 4 ways to manage Azure and when to use each
- [ ] I know Cloud Shell = browser terminal, no install
- [ ] I can explain IaC (blueprint analogy) and name ARM templates + Bicep
- [ ] I remember they all use ARM underneath

---

# 📅 Day 34 — Monitoring & Health: Azure Monitor, Service Health, Advisor

Today covers how you **keep an eye on** Azure — the "dashboards and early warnings" of the cloud.

## 📊 1. Azure Monitor (the big one)
**What it is:** The central service that **collects data** from your Azure resources — metrics, logs, and activity — so you can see health, performance, and problems.

**Real-life analogy:** The **control room of a building**:
- Sensors (metrics) report temperature, power, water.
- Cameras (logs) record events.
- Alarms (alerts) go off when something's wrong.
- You watch everything on one dashboard.

**Key parts (know the names):**

| Feature | What it does | Analogy |
|---------|--------------|---------|
| **Metrics** | Number-based data (CPU %, memory, requests) | Sensor readings |
| **Logs (Log Analytics)** | Detailed event records, queryable (KQL language) | Camera footage you can search |
| **Alerts** | Notify you when a threshold is crossed (e.g., CPU > 90%) | Alarm bells |
| **Application Insights** | Monitors your *application* performance (exceptions, page views, response times) | A specialist watching your app |
| **Workbooks** | Custom dashboards combining data | Your personal wall of screens |

**Example:** You set an alert: "Email me if VM CPU exceeds 90% for 10 minutes." When that happens, you get notified before users complain.

## 🏥 2. Azure Service Health
**What it is:** A dashboard showing the **health of Azure services themselves** (not your resources) — outages, planned maintenance, and advisories.

**Real-life analogy:** The **metro rail's official status board**:
- "Red line: signal fault, 20-min delay" (service issue).
- "Green line: planned maintenance Sunday 2–4 AM" (planned maintenance).
- You can't fix the metro, but you know what's happening and can plan around it.

**Key parts:**
| Part | What it covers |
|------|----------------|
| **Service issues** | Ongoing problems affecting Azure services |
| **Planned maintenance** | Upcoming changes that may affect you |
| **Health advisories** | Things to be aware of (e.g., service changes) |
| **Health history** | Past incidents and how they were resolved |

## 💡 3. Azure Advisor
**What it is:** A **personalized recommendation engine** that analyzes your resources and suggests best practices.

**Real-life analogy:** A **financial advisor for your Azure environment**:
- "You're paying for a VM that's been idle for 30 days — downsize it." (Cost)
- "This VM lacks backup — enable it." (Reliability)
- "Your database is exposed to the internet — restrict it." (Security)

**The 5 Advisor categories (memorize):**
1. **Cost** — save money.
2. **Security** — fix vulnerabilities.
3. **Reliability** — avoid outages.
4. **Performance** — speed things up.
5. **Operational Excellence** — process & monitoring improvements.

**Exam note:** Advisor is *proactive advice*; Defender for Cloud (Week 4) is *security-specific monitoring*. Don't mix them.

## 📊 Monitoring quick table

| Tool | What it watches | Analogy |
|------|-----------------|---------|
| Azure Monitor | Your resources (metrics/logs/alerts) | Building control room |
| Application Insights | Your *app's* behavior | App specialist |
| Service Health | Azure's own services | Metro status board |
| Advisor | Best-practice recommendations | Financial advisor |

## ✅ Day 34 Checklist
- [ ] I can explain Azure Monitor (your resources) vs. Service Health (Azure itself) vs. Advisor (advice)
- [ ] I know the 5 Advisor categories
- [ ] I know Log Analytics is where logs are queried

---

# 📅 Day 35 — Migration: Azure Migrate, Data Box + Week 5 Review

Today: how companies **move existing systems into Azure**, then a full Week-5 self-test.

## 🚚 1. Azure Migrate
**What it is:** The unified service for **discovering, assessing, and migrating** on-premises workloads to Azure (servers, databases, web apps).

**Real-life analogy:** A **professional moving company**:
- **Discovery:** They walk through your house and inventory everything (what servers/apps exist, what they need).
- **Assessment:** They estimate cost/size on Azure ("this server needs a Standard_D2s_v3").
- **Migration:** They pack, move, and unpack — minimizing disruption.

**Key steps (know the flow):**
1. **Discover** — scan on-prem servers/virtualization.
2. **Assess** — right-size and estimate Azure costs.
3. **Migrate** — move workloads (lift-and-shift VMs, or modernize apps).

**Related tools to know exist:**
- **Azure Database Migration Service** — for moving databases (e.g., SQL Server → Azure SQL).
- **Azure App Service Migration Assistant** — for moving web apps.

## 📦 2. Azure Data Box
**What it is:** A **physical storage device** Microsoft ships to you so you can upload massive amounts of data and ship it back (for when internet transfer is too slow/costly — e.g., terabytes/petabytes).

**Real-life analogy:** Moving a **whole house's furniture** — you don't carry each chair through traffic (internet); you load a moving truck (Data Box) and drive it to the destination.

**Exam facts:**
- For **large offline data transfers** (data too big to upload practically).
- Sizes: Data Box (~80 TB usable), plus smaller/larger siblings (Data Box Disk, Data Box Heavy).
- Microsoft handles the logistics; you copy data on, ship back, they upload it to your storage.

## 🛤️ Migration strategies (know the "4 R's" — exam favourite)

| Strategy | What it means | Analogy |
|----------|---------------|---------|
| **Rehost (lift-and-shift)** | Move as-is, no changes | Moving your furniture as-is |
| **Refactor (re-architect)** | Change the app to use cloud features (e.g., move to PaaS) | Renovating while moving |
| **Rearchitect** | Big redesign for cloud-native | Demolish & rebuild |
| **Rebuild** | Start from scratch with new code | Build a new house |

> 🧠 **Memory trick:** Rehost = pack & move. Refactor = tweak & move. Rearchitect = redesign. Rebuild = start over. **(The exam mainly wants you to know Rehost vs. Refactor.)**

## ⏰ Also know: Azure Update Management / maintenance
Not strictly required in depth, but know **Azure Update Manager** exists for patching VMs (just a mention — don't dive deep).

---

# 🏁 Week 5 Review & Self-Test

## 📋 Week 5 Summary Table (memorize)

| Tool/Concept | One-line meaning | Analogy |
|--------------|------------------|---------|
| Cost factors | Resource type, size, region, bandwidth, support | Restaurant bill items |
| Pay-as-you-go | Pay per use, no commitment | Per-cup chai |
| Reserved Instances | 1–3 yr commitment, up to ~72% off | Yearly chai pass |
| Spot VMs | Cheap unused capacity, can be reclaimed | Last-minute unsold table |
| Azure Hybrid Benefit | Reuse existing Windows/SQL licenses | Using your own spices |
| Pricing Calculator | *Estimate* costs before building | Contractor proforma invoice |
| TCO Calculator | Compare on-prem vs. cloud over time | Own vs. Uber for 3 years |
| Cost Management | See actual spend, budgets, alerts | Bank spending tracker |
| Azure Policy | Rules on what resources can be | Building codes |
| Blueprints | Pre-packaged compliant kit | New-branch checklist |
| Resource Locks | Prevent delete/modify | "Do not remove" seal |
| Tags | Key-value labels for cost/organization | Sticky notes |
| Portal | Visual web UI | Mobile banking app |
| CLI / PowerShell | Command-line control | ATM |
| Cloud Shell | Browser terminal, no install | Branch kiosk |
| ARM templates / Bicep | Infrastructure as code | House blueprint |
| Azure Monitor | Metrics/logs/alerts for your resources | Building control room |
| Service Health | Azure's own service status | Metro status board |
| Azure Advisor | Best-practice recommendations | Financial advisor |
| Azure Migrate | Discover/assess/migrate to Azure | Professional movers |
| Data Box | Physical device for huge offline transfers | Moving truck |
| 4 R's | Rehost / Refactor / Rearchitect / Rebuild | Move / tweak / redesign / rebuild |

## 📖 Week 5 Vocabulary (learn these)
1. **Egress** — data leaving Azure (costs money)
2. **Ingress** — data entering Azure (usually free)
3. **Reserved Instance** — prepaid compute discount (1–3 yrs)
4. **Spot VM** — interruptible cheap compute
5. **Azure Hybrid Benefit** — reuse existing Microsoft licenses
6. **Pricing Calculator** — pre-build cost estimator
7. **TCO Calculator** — on-prem vs. cloud cost comparison
8. **Budget** — a spending limit in Cost Management
9. **Azure Policy** — automated rules on resources
10. **Policy effect** — Deny / Audit / Append/Modify
11. **Resource Lock** — prevents deletion/modification
12. **CanNotDelete** — prevents deletion only
13. **ReadOnly** — prevents deletion + modification
14. **Tag** — key-value metadata label
15. **Azure CLI** — command-line tool for Azure
16. **Cloud Shell** — browser-based terminal
17. **IaC** — infrastructure as code
18. **ARM template** — JSON infrastructure definition
19. **Bicep** — newer, simpler IaC language
20. **Azure Monitor** — central monitoring service
21. **Log Analytics** — where logs are stored/queried
22. **Application Insights** — app-performance monitoring
23. **Service Health** — Azure's own status dashboard
24. **Azure Advisor** — personalized recommendations
25. **Azure Migrate** — migration service
26. **Data Box** — physical offline transfer device
27. **Rehost** — move as-is (lift-and-shift)
28. **Refactor** — modify to use cloud features

## ✍️ Self-Test (12 questions — try before reading the key)

1. Name the 5 cost factors.
2. Which is usually free: data entering or leaving Azure?
3. Which pricing model gives the biggest discount but requires a 1–3 year commitment?
4. Which tool estimates costs BEFORE you build?
5. Which tool compares on-premises vs. cloud over 3 years?
6. Where do you set a budget and see your actual spend?
7. Which service automatically denies non-compliant resources? RBAC / Azure Policy / Locks
8. Which lock prevents deletion but allows changes?
9. Which lock prevents everything, even changes?
10. Which tool gives you a terminal inside your browser?
11. Which service monitors Azure's *own* health?
12. Which Advisor category helps you save money?

**Answer key:** 1. Resource type, size/tier, region, bandwidth, support/licenses · 2. Ingress (entering) · 3. Reserved Instances · 4. Pricing Calculator · 5. TCO Calculator · 6. Cost Management + Billing · 7. Azure Policy · 8. CanNotDelete · 9. ReadOnly · 10. Cloud Shell · 11. Service Health · 12. Cost

## 🛠️ Hands-On Challenge (if you want to practice)
1. Open the **Pricing Calculator** and build a rough estimate: 1 VM (Standard_B1s, Central India, pay-as-you-go) + 1 storage account (LRS, Hot). Note the monthly total.
2. Compare: same VM but choose a 1-year **Reserved** option — see the discount %.
3. In the portal, go to **Cost Management + Billing** → “Budgets” and create a test budget of ₹100 with an alert (nothing will be billed — it's just a limit).
4. Optional: In your resource group, add a **CanNotDelete lock** to a test resource, try to delete it, see the error, then remove the lock. (Great hands-on understanding!)

---

## 🏁 Week 5 Complete! What's next?
You've now finished **the entire syllabus**: Cloud Concepts (Domain 1), Architecture/Compute/Networking/Storage/Databases/Security (Domain 2), and Cost/Governance/Monitoring/Migration (Domain 3). 🎉

**What remains is Week 6 — the "exam homestretch":**
- Day 36–38: full mock exams with strategy
- Day 39–41: weak-spot deep dives + memory tables
- Day 42–44: second round of mocks + cram sheets
- Day 45: exam day playbook (what to expect, how to book, tips)

Want me to write the complete **Week 6 notes (Day 36–45)** — including a full 60-question mock exam with answers and an exam-day checklist? That would make your prep 100% self-contained. 📚
