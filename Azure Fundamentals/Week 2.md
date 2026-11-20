# 📘 WEEK 2 — AZURE CORE ARCHITECTURE
### *(Covers the first half of Domain 2: 35–40% of the exam)*

---

# 📅 Day 8 — Azure Account & Subscriptions

## 🧠 First, the hierarchy (remember this whole week)
Azure organizes everything in a neat family tree:

```
Azure Account
 └── Subscription(s)          ← billing & limits
      └── Resource Group(s)    ← logical folders for resources
           └── Resources        ← actual things (VM, storage, DB)
```

**Real-life analogy:** Think of your bank account.
- **Azure account** = you (your identity).
- **Subscription** = a separate bank account. You can have multiple accounts.
- **Resource group** = a wallet/wallet-folder inside each account.
- **Resources** = the actual notes and coins in the wallet.

## 👤 1. What is an Azure Account?
- Your **identity** to get into Azure — you sign in with a Microsoft account (email/phone) or a work/school account.
- **Important:** The *account* is free to create. You only pay when you create *resources*.
- You can have **multiple subscriptions** under one account.

**Real-life analogy:** Your "account" is like your Aadhaar/identity card — it proves who you are. Having subscriptions is like having multiple bank accounts under that identity.

## 🎟️ 2. The Free Account (what a beginner should use)
When you create a free Azure account, you get:
- **₹7,000-ish (~$200) of credit** for the first 30 days (to experiment with paid services).
- **12 months of popular free services** (like a certain amount of VMs, storage, and databases).
- **25+ services that are permanently free** (some with usage limits).
- You will **NOT be charged** unless you manually upgrade to a paid subscription.

> ⚠️ **Beginner warning:** Always watch your usage. Even "free" services have limits. When you experiment, **delete what you create** (you'll practice this on Day 14).

## 💳 3. What is a Subscription?
A subscription is **a container for your resources that ties billing and limits together**. Everything you create lives inside a subscription.

**Think of it as a billing bucket** — you get one bill per subscription.

**Types of subscriptions:**
| Subscription type | What it's for |
|-------------------|---------------|
| **Free** | Beginners exploring (limited credits) |
| **Pay-As-You-Go** | Most common; you pay monthly for what you use |
| **Enterprise Agreement (EA)** | Large organizations with custom pricing |
| **Student** | For students — free credit via Azure for Students |
| **Visual Studio / Dev** | For developers with included monthly credit |

## 🎭 4. Why would anyone have MULTIPLE subscriptions?
| Reason | Example |
|--------|---------|
| **Billing separation** | Each department pays its own bill |
| **Environment separation** | Separate subscriptions for **dev**, **test**, and **production** (prod apps never get broken by experiments) |
| **Security boundary** | Different teams get different access, isolated from each other |
| **Limit management** | Subscriptions have limits (e.g., max VMs); splitting lets you raise effective capacity |

**Real-life analogy:** You might have one **personal bank account** and one **business bank account**. Same person (account), but separate money buckets (subscriptions) that are tracked, limited, and governed separately.

## 📦 5. What needs a subscription? Everything.
- Creating a resource **requires** a subscription.
- You can **move** subscriptions between management groups (Day 12).
- Subscriptions have **billing ownership**, **access control**, and **usage limits**.

## ✅ Day 8 Checklist
- [ ] I can explain the hierarchy: Account → Subscription → Resource Group → Resource
- [ ] I know a subscription = a billing container
- [ ] I can give 2 reasons to have multiple subscriptions

---

# 📅 Day 9 — Resource Groups

## 🧠 What is a Resource Group?
A **resource group (RG)** is a **logical container** that holds related Azure resources together.

**Real-life analogy:** It's like a **folder in your phone's gallery**:
- You collect related photos into one album (e.g., "Trip to Manali").
- You can add/remove photos anytime.
- Deleting the album deletes everything inside it.
- The photos themselves live in your phone's storage — the album is just a *way to organize*.

> 🔑 **Key point:** A resource group is **not** a physical thing. It doesn't store data. It's just **organization**.

## 📏 The golden rules of resource groups (exam favourite!)

1. **Every resource must belong to exactly ONE resource group.** No orphans, no double membership.
2. **A resource group can contain many resources** (dozens or hundreds).
3. **A resource group can contain resources from different regions.** (e.g., one RG can hold a VM in Mumbai *and* a storage account in Pune — they're still "related" logically.)
4. **Resource groups cannot be nested.** You can't put a resource group inside another resource group. (Think of a folder that can't contain folders — only files/resources.)
5. **You can move resources between resource groups.** (When you reorganize, resources can be moved.)
6. **Deleting a resource group deletes ALL the resources inside it.** ⚠️
7. **Actions on a resource group apply to everything inside it** — permissions (RBAC), policies, tags, and locks all flow down to resources.

## 👨👩👧 Why group resources logically? (the "why")
| Reason | Analogy |
|--------|---------|
| **Lifecycle management** | Need to build a project, use it, then delete it? Put all project resources in one RG — delete the RG, everything goes. **One click cleans up everything.** |
| **Management** | Apply permissions, policies, and tags to the whole group at once instead of one-by-one |
| **Billing / cost reporting** | Tag and group resources to see how much a project costs |
| **Access control** | Give a team access to the whole RG (and thus everything in it) in one action |

**Real-life analogy:** Think of a **house renovation project**: you hire electricians, plumbers, painters. If you bundle them under one contract (resource group), you manage them all together, and when the project ends you pay them all off together. 🏠

## 🛠️ Naming & organizing tips (best practice)
- Name RGs by **project or environment**: e.g., `rg-app-prod`, `rg-data-dev`.
- Use **tags** for extra labelling (week 5 covers tags deeply).
- Put resources that **share a lifecycle** in the same RG (e.g., a web app + its database + its storage = one RG). If they have different lives, separate them.

## ⚠️ Common beginner mistake
Thinking a resource group is like a *location* or *zone* — **it isn't**. It's just a folder. Resources inside can be scattered across regions.

## ✅ Day 9 Checklist
- [ ] I can explain what a resource group is in one sentence
- [ ] I know all 7 golden rules (especially "one RG per resource" and "no nesting")
- [ ] I can explain why grouping by lifecycle is smart

---

# 📅 Day 10 — Regions & Region Pairs

## 🧠 What is a Region?
A **region** is a **geographic location that contains one or more Azure data centers** (buildings full of servers).

**Real-life analogy (India):** Think of regions like **cities where "post offices" (data centers) exist**. Azure has regions in places like **Mumbai (Central India)**, **Pune (West India)** and **Chennai (South India)** — each is a separate physical location.

📍 **Current Azure regions in India (for context):**
- **Central India** — Pune
- **South India** — Chennai
- **West India** — Mumbai
*(As of this writing, these are India's three regions. There are 60+ regions worldwide, grouped into geographies.)*

## 🎯 Why do regions matter? (3 big reasons)

| Reason | Explanation |
|--------|-------------|
| **Latency** | Put your app **closer to your users** → less delay. An Indian user's app hosted in Mumbai responds much faster than one hosted in the US. |
| **Data residency / compliance** | Some laws require data to stay in a country (e.g., Indian banking data rules). Regions let you keep data **inside India**. |
| **Disaster recovery** | You can copy data to *another* region as backup (this is where **region pairs** come in — next). |

## 🔗 What are Region Pairs?
Azure pairs each region with **another region in the same geography** (usually within ~300 miles).

**Examples of pairs:**
- **Central India (Pune) ↔ South India (Chennai)** → an India pair
- **East US ↔ West US**
- **North Europe ↔ West Europe**

**Why pair regions? Three superpowers:**
1. **Disaster recovery:** If a whole region fails (earthquake, flood), Azure can fail over to the **paired region** automatically. Your data is safe.
2. **Rolling updates:** When Microsoft updates Azure, it updates **one region of a pair at a time** — so both never go down together. Users in one region keep working while the other updates.
3. **Better availability guarantee:** Paired regions help Azure offer services with **99.99% uptime** (only ~52 minutes of downtime per year). Solo regions can't hit that alone.

## 📊 Best practice for you as a beginner
- Deploy critical resources **across two paired regions** (e.g., app in Pune + backup in Chennai).
- This is the **redundancy** you learned in Week 1 — now you know *where* it goes.

## 🧭 Special region types (know these names)
| Type | What it is | Example |
|------|------------|---------|
| **Sovereign regions** | Isolated Azure instances for specific governments | Azure Government (US), Azure China (21Vianet) |
| **Geographies** | Bigger grouping of regions that obey data-residency rules | India geography = all Indian regions |

> Note: **Sovereign regions are physically and logically separate** from the main "global" Azure — data doesn't leave those boundaries. (Mainly a *know-they-exist* fact for the exam.)

## ✅ Day 10 Checklist
- [ ] I can define a region and name India's three
- [ ] I can explain why regions matter (latency, compliance, DR)
- [ ] I know what a region pair is and why it exists

---

# 📅 Day 11 — Availability Zones

## 🧠 What are Availability Zones?
Within **some regions**, Azure builds **physically separate data centers** called **Availability Zones**. Each zone has its own **power, cooling, and networking** — so if one zone has a fire or power cut, the others keep working.

**Real-life analogy:** Imagine a **city with 3 separate power plants**. If one plant fails, the other two keep lighting the city. Availability zones are like those separate plants — *independent* and *isolated*.

## 📏 The core facts (exam favourites)

| Fact | Explanation |
|------|-------------|
| **At least 3 zones per region** | Regions that support zones usually have 3 (sometimes more) |
| **Zones are close together** | ~a few kilometres apart within a region (low latency between them) |
| **But physically separate** | Each zone = separate buildings, power, cooling, network |
| **Zones are NOT available in every region** | Some regions don't offer zones (check service docs) |

## 🏗️ How services use zones (know these 2 patterns)

**1. Zonal services** — you pick *one specific zone* to run in.
- Example: You create a VM and pin it to Zone 1.
- Risk: If *that* zone fails, your VM fails (you chose a single basket).
- **Best practice:** deploy to *multiple* zones for safety.

**2. Zone-redundant services** — the *platform itself* automatically spreads your data/app across all zones.
- Example: A zone-redundant storage account (ZRS — you saw this in Week 1's table!) copies data across zones automatically.
- **Benefit:** Even if one zone dies, your service keeps running. You did nothing extra.

## ⚖️ Availability Zones vs. Region Pairs (super-important difference!)

| | Availability Zones | Region Pairs |
|---|---|---|
| **Distance** | Close — within one region | Far — two different regions |
| **Protects against** | A **data center / zone** failure | A **whole region** failure |
| **Latency** | Very low | Higher |
| **Typical use** | Run your app across zones for everyday resilience | Disaster-recovery backup in another region |
| **Analogy** | **Backup generators in the same building complex** | **A second branch office in another city** |

> 🧠 **Memory trick:** Zones = "same city, different buildings". Pairs = "different cities". Use zones for day-to-day resilience, pairs for disaster recovery.

## 🛡️ One more related concept: Availability Sets (know the name)
An **availability set** is an *older* way to keep VMs available during maintenance/failures by spreading VMs across **fault domains** (different racks) and **update domains** (machines updated at different times).
- **Fault domains** = physical racks. If one rack's power dies, VMs on other racks survive.
- **Update domains** = groups updated separately so maintenance never takes down everything at once.
- **Note for AZ-900:** Availability sets are an *older* mechanism; **availability zones are the modern way**. Just know what both mean.

## ✅ Day 11 Checklist
- [ ] I can explain what an availability zone is in one sentence
- [ ] I know zonal vs. zone-redundant services
- [ ] I can clearly explain zones vs. region pairs (with the "cities vs. buildings" analogy)

---

# 📅 Day 12 — Management Groups

## 🧠 Why do we need them?
As a company grows, it can have **dozens of subscriptions** (one per department, project, or environment). Managing them one-by-one is chaos.
**Management Groups** are **containers above subscriptions** that let you manage many subscriptions at once.

**Real-life analogy:** Think of a **company org chart**:
- The **CEO** is at the top.
- Then come departments (Marketing, Engineering, Finance) — these are like management groups.
- Under each department come teams — those would be subscriptions or resource groups.

## 🔺 The full hierarchy (now complete!)

```
Management Group(s)          ← top-level containers (like departments)
 └── Subscription(s)         ← billing containers (like projects)
      └── Resource Group(s)  ← logical folders (like folders)
           └── Resources      ← actual items (like files)
```

## 📏 Key facts about Management Groups (exam favourites)

| Fact | Explanation |
|------|-------------|
| **Can have multiple levels** | You can nest management groups (Management Group inside another Management Group) — up to 6 levels deeper than the root |
| **The root management group** | Automatically created for every tenant; sits at the very top of the tree |
| **Everything inherits** | **Policies, access (RBAC), and tags** applied to a management group **flow down** to all subscriptions, resource groups, and resources beneath it |
| **All subscriptions belong somewhere** | Every subscription must be attached to a management group (or the root) |
| **They help with governance** | Apply one rule at the top → it applies everywhere below |

## 💡 Great real-world example
A company has two departments: **Finance** and **Engineering**.
- They create a management group called **"Finance"** containing the finance team's subscriptions.
- They create another called **"Engineering"** for dev/test/prod subscriptions.
- Now, if they want a rule like *"Only allow resources in India regions"* for the whole company, they apply it at the **root management group** — and it applies to *every* subscription underneath.

## 🎯 Management Groups vs. Resource Groups (don't mix them)
| | Management Group | Resource Group |
|---|---|---|
| **Level** | Above subscriptions | Inside a subscription |
| **Contains** | Subscriptions (and other MGs) | Resources only |
| **Use** | Apply rules to the whole organization | Organize related resources for one project |
| **Analogy** | Company department | Project folder |

## ⚠️ Beginner gotcha
Don't confuse them: **Resource groups organize resources *within* one subscription. Management groups organize *subscriptions themselves*.**

## ✅ Day 12 Checklist
- [ ] I can draw the full hierarchy from memory
- [ ] I know management groups are ABOVE subscriptions
- [ ] I know policies applied at MG level flow down to everything below

---

# 📅 Day 13 — Azure Resource Manager (ARM)

## 🧠 What is ARM?
**Azure Resource Manager (ARM)** is the **management layer** — the "brain" of Azure. Every single request to create, modify, or delete a resource goes through ARM.

**Real-life analogy:** Think of **air traffic control at an airport**:
- Every plane (your request) must be cleared by the control tower (ARM).
- The tower verifies who you are (authentication), whether you're allowed (authorization), and directs the plane to the right gate.
- No plane takes off or lands without the tower.

## 🔄 How do you actually talk to ARM? (the 5 ways)
All of these are just different "remote controls" — they all end up calling the same ARM service:

| Tool | What it is | Real-life analogy |
|------|------------|-------------------|
| **Azure Portal** | The website you click around in | Using a bank's mobile app |
| **Azure CLI** | Commands typed in a terminal | Using a bank's ATM |
| **Azure PowerShell** | Commands using PowerShell | The ATM again, different interface |
| **REST API / SDKs** | Code that calls Azure programmatically | A bank's API for other apps |
| **ARM templates / Bicep** | Declarative JSON/text files that define your entire infrastructure | A **blueprint** of the building you want built |

> 🔑 **Key point:** Whatever way you use, **the outcome is the same** — it's all ARM underneath. The portal, CLI, and PowerShell are just different *ways* to send the same instructions.

## 🧱 What are ARM Templates? (a bigger deal than you'd think)
An **ARM template** is a **JSON file that describes your entire infrastructure** — "I want a VM with this name, this size, this storage, in this region, with this tag."

**Real-life analogy:** A **house blueprint**. Instead of telling a builder every detail verbally (portal, click-by-click), you hand over the blueprint (template) and the builder constructs exactly that — every time, perfectly, the same way.

**Why they're brilliant:**
| Benefit | Explanation |
|---------|-------------|
| **Repeatable** | Deploy the exact same environment 100 times (dev → test → prod) |
| **Declarative** | You say *what* you want; ARM figures out *how* and *in what order* |
| **Dependency-aware** | ARM builds resources in the right order (e.g., creates the database before the app that needs it) |
| **Idempotent** | Run the same template twice → same result, no duplication |
| **Version-controlled** | Your infrastructure lives in code (like app code) — reviewable, auditable |

*(Bicep is Microsoft's newer, simpler language for the same idea — just know it exists.)*

## 🎯 What else does ARM do? (the 4 superpowers)

1. **Consistent management layer** — every resource goes through the same security, validation, and auditing pipeline.
2. **Role-Based Access Control (RBAC)** — ARM checks *who* you are and *whether* you're allowed before doing anything. (We'll deep-dive RBAC in Week 4.)
3. **Tagging** — ARM lets you attach key-value labels (like `owner:raj`) to resources for cost and management. (Full tags lesson: Week 5.)
4. **Governance** — ARM enforces policies and locks at every level of the hierarchy.

## ✅ Day 13 Checklist
- [ ] I can explain ARM as "the brain of Azure"
- [ ] I can name the 5 ways to talk to ARM
- [ ] I can explain an ARM template with the blueprint analogy

---

# 📅 Day 14 — Review, Vocabulary & Hands-On Challenge

## 📋 Week 2 Summary Table (memorize this)

| Concept | One-line meaning | Example / analogy |
|---------|------------------|-------------------|
| **Azure account** | Your identity to access Azure | Your Aadhaar/ID |
| **Subscription** | Billing container for resources | A bank account |
| **Resource group** | Logical folder for related resources | Photo album/folder |
| **Region** | Geographic location of Azure data centers | A city with data centers |
| **Region pair** | Two paired regions for DR & rolling updates | Pune ↔ Chennai |
| **Availability zone** | Separately powered data centers *within* a region | Separate buildings |
| **Management group** | Container above subscriptions for org-wide governance | Company department |
| **ARM** | The management layer that processes every request | Air traffic control |
| **ARM template** | Declarative JSON "blueprint" of infrastructure | House blueprint |
| **Zonal service** | You choose one specific zone | Picking one building |
| **Zone-redundant** | Platform spreads you across all zones automatically | Backup in all buildings |

## 📖 Your Week 2 Vocabulary List
1. **Subscription** — a container that ties resources to billing and limits
2. **Resource group** — a logical container for related resources
3. **Region** — a geographic area containing Azure data centers
4. **Region pair** — two paired regions for recovery and updates
5. **Availability zone** — a physically separate data center in a region
6. **Zone-redundant** — data/service automatically duplicated across zones
7. **Zonal** — deployed in a single specific zone
8. **Management group** — a container above subscriptions for governance
9. **Root management group** — the top-level group for your tenant
10. **Azure Resource Manager (ARM)** — the management layer for all Azure requests
11. **ARM template** — a JSON file defining infrastructure (IaC)
12. **Bicep** — modern, simpler IaC language for Azure
13. **RBAC** — role-based access control (who can do what)
14. **Tag** — a key-value label on a resource (e.g., `env:dev`)
15. **Sovereign region** — isolated Azure instances (e.g., Azure Government)

## ✍️ Self-Test (10 questions — try before reading the key)

1. What is the correct hierarchy order? (Account, Subscription, Resource Group, Resource — put them in order)
2. A resource must belong to exactly ___ resource group(s).
3. True/False: You can nest resource groups inside other resource groups.
4. Which is closer together: availability zones or region pairs?
5. Which protects you if a WHOLE region fails: availability zones or region pairs?
6. What sits ABOVE subscriptions in the hierarchy?
7. What does ARM stand for, and what is it in one line?
8. Which tool would a developer use to deploy infrastructure as repeatable code? (Portal / CLI / ARM template)
9. Name India's three Azure regions.
10. If you apply a policy on a management group, where does it apply?

**Answer key:** 1. Account → Subscription → Resource Group → Resource · 2. one · 3. False · 4. availability zones · 5. region pairs · 6. Management groups · 7. Azure Resource Manager — the management layer that processes every request · 8. ARM template · 9. Central India (Pune), South India (Chennai), West India (Mumbai) · 10. Everything beneath it (all subscriptions, resource groups, resources)

## 🛠️ Hands-On Challenge (actually do this — it cements everything)

1. **Log into** the [Azure Portal](https://portal.azure.com) with your free account.
2. **Create a resource group** called `rg-myfirst-rg` (choose region: Central India).
3. **Create a storage account** inside it (name like `mystorage<yourname>`), region Central India.
4. **Create a Virtual Machine** inside the SAME resource group (use the cheapest size — e.g., `Standard_B1s`; before you finish, notice the "Tags" tab — add tag `owner=you` and `purpose=learning`).
5. **Open the resource group** — see how all 3 resources appear together.
6. **Test the hierarchy:** click the resource group → look at "Properties" → you'll see its subscription.
7. **Delete the resource group** (`rg-myfirst-rg`) — watch it delete all 3 resources at once. ✅ (This is why resource groups are great for cleanup!)

> ⚠️ Cleanup tip: Deleting the **resource group** (not each resource) is the lazy-cleanup superpower. Always do this after experiments so you aren't billed.

---

## 🏁 Week 2 Complete! What's next?
You've now finished the **architecture core** — subscriptions, groups, regions, zones, management groups, and ARM. Next up in **Week 3 (Day 15–23)**: the real working services — **Compute (VMs, App Services, Functions, Containers), Networking (VNet, load balancers, VPN/ExpressRoute), Storage (blobs, redundancy levels, tiers), and Databases**.

Want me to write the same complete, beginner-style notes for **Day 15–23 (Week 3)** next? 📚
