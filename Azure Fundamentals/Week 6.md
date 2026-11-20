# 📘 WEEK 6 — THE EXAM HOMESTRETCH
### *(2 full mock exams + review + memory toolkit + exam-day playbook)*

---

# 📅 Day 36 — Full Mock Exam #1

## 🧠 Today's mission
Sit down, set a timer for **60 minutes**, and attempt **25 realistic AZ-900-style questions** — with NO notes, NO phone, NO peeking. This simulates the real exam's pressure.

**Exam-style rules:**
- Answer every question (no penalty for wrong answers).
- Flag questions you're unsure about and move on.
- If you don't know, eliminate obviously wrong options, then guess.

## 📝 MOCK EXAM #1 (25 questions)

**Q1.** You need to migrate an on-premises server "as-is" to Azure with full control over the OS. Which service model should you use?
- A) SaaS
- B) PaaS
- C) IaaS
- D) Serverless

**Q2.** In the SaaS model, which item is the CUSTOMER responsible for?
- A) The operating system
- B) The physical servers
- C) The data and who has access to it
- D) Network security

**Q3.** A web app automatically adds server capacity during traffic spikes and removes it afterwards, with no manual action. This is called:
- A) High availability
- B) Elasticity
- C) Fault tolerance
- D) Agility

**Q4.** Which is an example of VERTICAL scaling?
- A) Adding 10 more identical servers to a farm
- B) Upgrading a VM from 2 vCPUs to 8 vCPUs
- C) Deploying to a new region
- D) Enabling autoscale rules

**Q5.** Which statement is TRUE about CapEx vs. OpEx?
- A) Azure uses a CapEx model — you buy hardware upfront
- B) CapEx means paying as you go for services
- C) Azure primarily uses OpEx with consumption-based pricing
- D) OpEx requires purchasing physical servers

**Q6.** Under the shared responsibility model, in a PaaS deployment (like App Service), WHO manages the operating system?
- A) The customer
- B) Microsoft
- C) The customer's IT team
- D) A third-party vendor

**Q7.** Which statement about resource groups is TRUE?
- A) A resource can belong to multiple resource groups
- B) Resource groups can be nested inside other resource groups
- C) A resource must belong to exactly one resource group
- D) A resource group can only contain resources from the same region

**Q8.** Why does Azure pair regions (e.g., Central India ↔ South India)?
- A) To reduce the price of VMs
- B) To provide disaster recovery and rolling updates
- C) To allow users to choose cheaper regions
- D) To store data closer to users only

**Q9.** What is an Availability Zone?
- A) A second region in another country
- B) A physically separate data center within a region, with independent power/cooling/network
- C) A logical folder inside a subscription
- D) A billing boundary for resources

**Q10.** Which of these is a valid reason to use MULTIPLE subscriptions?
- A) To nest resources inside other resources
- B) To separate dev, test, and production environments with separate billing
- C) To increase VM speed
- D) To avoid using resource groups

**Q11.** What sits directly ABOVE subscriptions in the Azure hierarchy?
- A) Resource groups
- B) Management groups
- C) Availability zones
- D) Administrative units only

**Q12.** A developer creates a JSON file describing an entire environment and deploys it repeatedly to dev, test, and prod with identical results. This is a benefit of:
- A) The Azure Portal
- B) Azure CLI
- C) ARM templates / Infrastructure as Code
- D) Cloud Shell

**Q13.** You need to host a website with zero server management and automatic scaling. Which service should you choose?
- A) Virtual Machine
- B) App Service
- C) ExpressRoute
- D) Blob storage

**Q14.** Which service runs code ONLY when triggered (e.g., a new file upload) and charges per execution?
- A) Kubernetes Service (AKS)
- B) Azure Functions
- C) App Service
- D) Azure SQL Database

**Q15.** You need a secure, dedicated private connection between your office and Azure that does NOT use the public internet. Which do you use?
- A) VPN Gateway
- B) ExpressRoute
- C) Load Balancer
- D) Azure DNS

**Q16.** Which Azure storage service would you use to provide a shared network drive that multiple VMs can mount simultaneously?
- A) Blob storage
- B) Disk storage
- C) Azure Files
- D) Queue storage

**Q17.** Which redundancy option copies your data to a SECOND region (a region pair)?
- A) LRS
- B) ZRS
- C) GRS
- D) LRS only

**Q18.** Which storage access tier is cheapest to STORE but slowest to access (hours to retrieve)?
- A) Hot
- B) Cool
- C) Cold
- D) Archive

**Q19.** Which database service is "globally distributed and multi-model" (NoSQL)?
- A) Azure SQL Database
- B) Cosmos DB
- C) Database for MySQL
- D) Database for PostgreSQL

**Q20.** What is Microsoft Entra ID (formerly Azure Active Directory)?
- A) A firewall service
- B) A cloud identity and access management directory
- C) A database service
- D) A cost management tool

**Q21.** A user proves identity with a password (something they know) AND a code from an authenticator app (something they have). This is:
- A) Authorization
- B) Conditional Access
- C) Multi-Factor Authentication
- D) Single Sign-On

**Q22.** Which RBAC role can create and manage resources but CANNOT grant access to others?
- A) Reader
- B) Contributor
- C) Owner
- D) User Access Administrator

**Q23.** You want to prevent accidental DELETION of a critical database but still allow changes. Which lock should you apply?
- A) ReadOnly
- B) CanNotDelete
- C) Azure Policy
- D) Tag lock

**Q24.** Which Azure Policy effect BLOCKS a non-compliant resource from being created?
- A) Audit
- B) Deny
- C) Append
- D) Disabled

**Q25.** Which tool provides personalized recommendations like "this VM is idle — downsize it"?
- A) Service Health
- B) Azure Monitor
- C) Azure Advisor
- D) TCO Calculator

---

## ✅ ANSWER KEY (no peeking until you've finished!)

| Q | Answer | Why (one line) |
|---|--------|-----------------|
| 1 | **C** | IaaS = you control OS and above, VMs |
| 2 | **C** | In SaaS you manage your data and access; Microsoft manages the rest |
| 3 | **B** | Elasticity = automatic scale up AND down with demand |
| 4 | **B** | Vertical = make one machine bigger; horizontal = add machines |
| 5 | **C** | Azure is consumption-based OpEx — pay for what you use |
| 6 | **B** | In PaaS, Microsoft manages the OS; you manage the app |
| 7 | **C** | Every resource must belong to exactly one resource group; no nesting; can span regions |
| 8 | **B** | Region pairs provide DR and sequential rolling updates |
| 9 | **B** | Zone = separate data center within the SAME region |
| 10 | **B** | Subscriptions separate billing, environments, limits, security |
| 11 | **B** | Management groups sit above subscriptions |
| 12 | **C** | IaC = repeatable, declarative, idempotent |
| 13 | **B** | App Service = managed PaaS web hosting |
| 14 | **B** | Functions = serverless, trigger-based, pay-per-run |
| 15 | **B** | ExpressRoute = private line, bypasses the internet |
| 16 | **C** | Azure Files = SMB shared file shares |
| 17 | **C** | GRS copies to a second region (GZRS also does, but of the listed options GRS is the classic) |
| 18 | **D** | Archive = cheapest storage, hours-long retrieval |
| 19 | **B** | Cosmos DB = global multi-model NoSQL |
| 20 | **B** | Entra ID = identity directory (old Azure AD) |
| 21 | **C** | Know + Have = MFA (two factors) |
| 22 | **B** | Contributor manages resources but can't grant access |
| 23 | **B** | CanNotDelete blocks deletion but allows changes |
| 24 | **B** | Deny effect blocks creation |
| 25 | **C** | Advisor = cost/security/reliability recommendations |

## 📊 Score yourself
- **21–25 correct (85%+)** → Excellent! You're exam-ready; Day 37 is light.
- **17–20 (70–85%)** → Good; target the specific traps in Day 37–38.
- **Below 17 (<70%)** → Normal for first try! Don't panic. Day 37–38 is exactly how you'll climb.

## ✅ Day 36 Checklist
- [ ] I took the mock under timed conditions, no notes
- [ ] I scored myself honestly
- [ ] I wrote down which questions I got wrong (topic names)

---

# 📅 Day 37 — Analyze & Create Your Personal "Hit List"

## 🧠 Today's mission
Turn your wrong answers into a **custom study plan**. The only way to waste a mock exam is to not learn from it.

## 📋 Step 1: Categorize each mistake
Put every wrong answer into ONE of three buckets:

| Bucket | Meaning | Fix |
|--------|---------|-----|
| **Memory miss** | I knew the concept but blanked on the fact | Rewrite it in the memory toolkit (Day 41) |
| **Confusion** | I mixed two similar things (e.g., LRS vs. GRS) | Do the Day 38 deep-dive comparisons |
| **Reading error** | I misread (e.g., "NOT" questions) | Slow down; underline keywords in questions |

## 🔍 Step 2: Find your weakest exam
Count errors by domain:
- Cloud Concepts (Day 1–7)
- Architecture (Day 8–14)
- Compute/Networking/Storage (Day 15–21)
- Databases (Day 22)
- Identity/Security (Day 24–28)
- Cost/Governance (Day 30–35)

**Rule:** Spend 80% of the next two days on your weakest 2 domains. Don't re-review what you already know.

## ⚠️ Step 3: Master the classic EXAM TRAPS
These are the questions Microsoft loves — the places where beginners stumble:

| Trap | The confusion | The truth |
|------|---------------|-----------|
| Availability zones vs. region pairs | "Both are backup" | Zones = same region, different buildings. Pairs = two regions |
| LRS vs. GRS | "LRS has 3 copies, so it's enough" | LRS copies are all in ONE building; GRS goes to a second region |
| NSG vs. Azure Firewall | "Both are firewalls" | NSG = per-subnet/NIC filter; Firewall = whole-VNet managed firewall |
| Authentication vs. authorization | "They're the same" | Authentication = who you are; authorization = what you can do |
| Reader vs. Contributor vs. Owner | "Contributor is highest" | Owner is highest (includes granting access); Contributor can't grant access |
| Pricing Calculator vs. Cost Management | "Both show my bill" | Calculator = estimate BEFORE; Cost Management = actual spend AFTER |
| App Service vs. Functions | "Both host websites" | App Service = always-running host; Functions = event-triggered, pay-per-run |
| Scalability vs. elasticity | "Same thing" | Scalability = ability to grow; elasticity = AUTOMATIC grow/shrink |
| Fault tolerance vs. disaster recovery | "Both survive failures" | Fault tolerance = never stops; DR = plan to recover after a stop |
| Azure Policy vs. RBAC | "Both control access" | Policy = rules on resources; RBAC = permissions for people |
| IaaS vs. SaaS responsibility | "Microsoft does everything" | In IaaS you manage OS+; in SaaS you manage only data/access |
| Blob vs. Disk storage | "Both store files" | Blob = standalone files for apps; Disk = attached VM hard drives |
| Hot vs. Archive tier | "Archive is faster because it's newer" | Archive = cheapest to store, SLOWEST to retrieve |
| CapEx vs. OpEx | "Azure charges upfront" | Azure = OpEx consumption-based; CapEx = buying physical hardware |
| Security vs. privacy compliance | "Microsoft handles compliance for me" | Microsoft secures the cloud; YOU configure services to stay compliant |

## 🛠️ Step 4: Re-test the missed questions
Tomorrow, after your deep dive, re-answer your exact wrong questions — from memory. If you get them right, your hit list is cleared.

## ✅ Day 37 Checklist
- [ ] I classified every mistake (memory / confusion / reading)
- [ ] I identified my 2 weakest domains
- [ ] I read the 15 most table carefully
- [ ] I planned what to study deeply tomorrow

---

# 📅 Day 38 — Weak-Spot Deep Dive

## 🧠 Today's mission
Spend today ONLY on your two weakest domains. Use the focused dives below as your guide — read the one(s) relevant to you, plus do the 5 targeted questions at the end.

## 🎯 Deep Dive A: Storage Redundancy (if this was weak)

**The mental model:** redundancy = "How many copies of my data exist, and where do they live?"

| Level | Copies | Where | Protects against |
|-------|:---:|-------|------------------|
| LRS | 3 | Same data center | One rack/server failing |
| ZRS | 3 | 3 zones, same region | One entire data center failing |
| GRS | 6 | 3 primary region + 3 in a PAIRED SECOND region | A whole region failing |
| GZRS | 6 | 3 zones in primary + 3 in second region | Zone AND region failures |

**Memory trick:** read the letters as a story:
- **L**RS = **L**ocal (one building)
- **Z**RS = **Z**one (3 buildings)
- **GR**S = **G**eo-**R**egion (two cities)
- **GZ**RS = **G**eo-**Z**one (3 buildings + two cities)

**Price ladder:** LRS < ZRS < GRS < GZRS (more protection = more cost).

**Exam question style:** "You need to survive a REGION-wide outage with minimal cost. Which redundancy?" → **GRS** (ZRS won't help across regions; GZRS is overkill for "minimal cost").

## 🎯 Deep Dive B: RBAC & Access (if this was weak)

**The formula:** RBAC = **Security Principal + Role + Scope**

**The roles ladder:**
| Role | Can do | Can grant access? |
|------|--------|:---:|
| Reader | View only | ❌ |
| Contributor | Create/manage resources | ❌ |
| Owner | Everything + manage access | ✅ |
| User Access Administrator | Manage access only | ✅ |

**Scope rule:** Permissions flow DOWN the hierarchy: Management Group → Subscription → Resource Group → Resource. Grant at a high scope → it applies to everything below.

**Exam question style:** "Who can create a VM but cannot give another user access?" → **Contributor**. "Who can give others access but not create VMs?" → **User Access Administrator**.

## 🎯 Deep Dive C: Service Models & Shared Responsibility (if weak)

**The responsibility shift:** as you move IaaS → PaaS → SaaS, YOUR management shrinks.

| What | IaaS (VM) | PaaS (App Service) | SaaS (365) |
|------|-----------|---------------------|------------|
| You manage | OS, runtime, app, data | App, data | Data & access only |
| Microsoft manages | Hardware, storage, network | OS, patching, platform | Everything else |

**Exam question style:** "In SaaS, who is responsible for the application?" → **Microsoft**. "In IaaS, who is responsible for OS patches?" → **The customer**.

## 🎯 Deep Dive D: Cost Tools (if weak)

| Tool | Question it answers |
|------|---------------------|
| Pricing Calculator | "What will this COST before I build?" |
| TCO Calculator | "Is cloud cheaper than on-prem over 3 years?" |
| Cost Management | "What am I ACTUALLY spending, and how do I cap it?" |
| Advisor (Cost category) | "How can I SAVE money?" |

**Exam question style:** "You want to compare on-premises vs. cloud total cost over 3 years" → **TCO Calculator**. "You want to set a spending alert" → **Cost Management**.

## ✍️ 5 Targeted Deep-Dive Questions

1. A UK bank must survive a region-wide Azure outage with data still accessible in another region. Which redundancy? (LRS / ZRS / GRS / GZRS)
2. A user must be able to view all resources in a resource group but not change anything. Which role? (Reader / Contributor / Owner)
3. In a VM (IaaS) deployment, who installs security patches on the OS? (Customer / Microsoft / Shared 50/50)
4. You want to SET a budget and receive an email when you hit 80% of it. Which tool? (Pricing Calculator / Cost Management / TCO)
5. Which redundancy level protects against a single ZONE failure but stays within one region? (LRS / ZRS / GRS / GZRS)

**Answers:** 1. GRS · 2. Reader · 3. Customer · 4. Cost Management · 5. ZRS

## ✅ Day 38 Checklist
- [ ] I deeply re-read my 2 weakest areas
- [ ] I attempted the 5 targeted questions
- [ ] I can explain the trap that caught me, in my own words

---

# 📅 Day 39 — Rapid-Fire All-Domain Recap

## 🧠 Today's mission
Refresh EVERY domain fast. Read each line and say it aloud — if any line feels unfamiliar, make a note and re-read that day's notes.

## ⚡ Domain 1: Cloud Concepts (Day 1–7)

- **IaaS** = rent VMs/networking (you manage OS+); **PaaS** = rent platform (you manage app only); **SaaS** = ready software (you manage data/access).
- **Public** = shared Microsoft cloud. **Private** = dedicated to one org. **Hybrid** = both connected.
- **Availability** = keeps working despite failures. **Scalability** = ability to grow (vertical = bigger, horizontal = more).
- **Elasticity** = automatic scale up AND down.
- **Fault tolerance** = never stops; **Disaster recovery** = plan to recover.
- **CapEx** = buy upfront; **OpEx** = pay as you go (Azure).
- **Shared responsibility:** customer manages less going IaaS → SaaS.

## ⚡ Domain 2: Architecture (Day 8–14)

- Hierarchy: **Account → Subscription → Resource Group → Resource**; **Management Groups** above subscriptions.
- Subscription = billing container (separate envs). Resource group = logical folder (one RG per resource, no nesting, deletion cascades).
- **Region** = geographic DC location (India: Pune, Chennai, Mumbai). **Region pair** = DR + rolling updates. **Availability zone** = separate building within region.
- **ARM** = management layer; **ARM templates/Bicep** = infrastructure as code.

## ⚡ Domain 2 continued: Compute/Networking/Storage (Day 15–21)

- **VM** = full control; **Scale Set** = auto-scaling group; **App Service** = managed web host; **Functions** = event-triggered; **Containers** = packaged apps (ACI, AKS).
- **VNet** = private network; **subnet** = partition; **peering** = connect VNets.
- **Load Balancer** (L4) vs. **Application Gateway** (L7 + WAF).
- **VPN Gateway** = encrypted over internet; **ExpressRoute** = private line.
- Storage: **Blob** (files), **Disk** (VM drives), **Files** (shares), **Queue** (messages), **Table** (key-value).
- Redundancy: **LRS → ZRS → GRS → GZRS**. Tiers: **Hot → Cool → Cold → Archive**.

## ⚡ Domain 2 final: Databases & Security (Day 22–28)

- **SQL** = relational tables; **NoSQL** = flexible. **SQL Database** = managed SQL; **Cosmos DB** = global multi-model; **MySQL/PostgreSQL** = managed open-source.
- **Entra ID** = identity directory; **SSO** = one sign-in, many apps.
- **Authentication** = who you are; **Authorization** = what you can do.
- **MFA factors:** know / have / are. **Conditional Access** = smart rules.
- **RBAC = principal + role + scope.** Reader/Contributor/Owner.
- **Defender for Cloud** = monitoring + Secure Score; **NSG** = subnet firewall; **Azure Firewall** = VNet firewall; **Key Vault** = secrets.
- **Compliance** = laws/standards; Trust Center = certifications; residency = where data lives; sovereignty = whose laws.

## ⚡ Domain 3: Cost & Governance (Day 30–35)

- Cost factors: type, size, region, bandwidth (egress costs), support/licenses.
- Pay-as-you-go vs. **Reserved** (1–3 yrs, up to ~72% off) vs. **Spot** (interruptible).
- **Pricing Calculator** = estimate; **TCO** = on-prem vs. cloud; **Cost Management** = actual + budgets/alerts.
- **Policy** = rules (Deny/Audit/Append); **Blueprints** = starter kits; **Locks** = CanNotDelete vs. ReadOnly; **Tags** = labels.
- Tools: **Portal**, **CLI**, **PowerShell**, **Cloud Shell**, **ARM/Bicep**.
- **Azure Monitor** = your resources; **Service Health** = Azure's own status; **Advisor** = recommendations.
- **Azure Migrate** = migration service; **Data Box** = physical offline transfer; **4 R's** = Rehost/Refactor/Rearchitect/Rebuild.

## 📌 Rule for today
If you stumble on 3+ lines in one domain, block 30 minutes tonight to re-read that domain's week.

## ✅ Day 39 Checklist
- [ ] I recited every domain out loud
- [ ] I noted and repaired any gaps
- [ ] I'm ready for Mock Exam #2 tomorrow

---

# 📅 Day 40 — Full Mock Exam #2

## 🧠 Today's mission
Same rules as Day 36: 60 minutes, no notes, no distractions. This time aim for **85%+**. These are NEW questions — no repeats from Mock #1.

## 📝 MOCK EXAM #2 (25 questions)

**Q1.** Which describes a PRIVATE cloud?
- A) A cloud shared by many organizations
- B) A cloud environment dedicated to a single organization
- C) A combination of public and on-premises
- D) Any cloud with pay-as-you-go pricing

**Q2.** Which characteristic means the system continues operating when a component fails?
- A) Agility
- B) Fault tolerance
- C) Scalability
- D) CapEx

**Q3.** Which is a benefit of consumption-based pricing?
- A) You pay a fixed fee regardless of usage
- B) You pay only for what you use
- C) You must buy hardware upfront
- D) You always get 72% off

**Q4.** Under the shared responsibility model in IaaS, who manages the VIRTUALIZATION layer?
- A) The customer
- B) Microsoft
- C) Both equally
- D) A third party

**Q5.** Which statement is TRUE about resource groups?
- A) A resource group can contain resources from multiple regions
- B) Resource groups can contain other resource groups
- C) A resource can be in several resource groups
- D) Resource groups are billed separately from subscriptions

**Q6.** What is the PRIMARY purpose of an Azure subscription?
- A) To define network boundaries
- B) To provide a billing boundary and access boundary for resources
- C) To store virtual machines
- D) To replace resource groups

**Q7.** Availability Zones are designed primarily to protect against:
- A) A whole-region failure
- B) A single data-center (zone) failure
- C) Internet outages
- D) Billing errors

**Q8.** Which statement about management groups is TRUE?
- A) They can only contain one subscription each
- B) Policies applied to them flow down to subscriptions below
- C) They sit below resource groups
- D) They are the same as resource groups

**Q9.** When would you choose a Virtual Machine over App Service?
- A) When you want zero server management
- B) When you need full control over the OS and custom software
- C) When you only need a static website
- D) When you need serverless code

**Q10.** Which Azure service is best for short, event-driven tasks that only run when triggered?
- A) App Service
- B) Container Instances
- C) Azure Functions
- D) Virtual Machine Scale Sets

**Q11.** Which is the difference between VPN Gateway and ExpressRoute?
- A) VPN is private; ExpressRoute uses the public internet
- B) VPN uses encrypted tunnels over the public internet; ExpressRoute is a dedicated private connection
- C) They are identical services
- D) ExpressRoute only works within one region

**Q12.** Which Azure storage service would you use to serve images and videos to a public website?
- A) Azure Files
- B) Blob storage
- C) Queue storage
- D) Disk storage

**Q13.** Which storage redundancy is the MOST expensive and offers maximum protection?
- A) LRS
- B) ZRS
- C) GRS
- D) GZRS

**Q14.** A user accesses data once a year and wants to pay the least for storage. Which tier?
- A) Hot
- B) Cool
- C) Cold
- D) Archive

**Q15.** Which Azure database is best for an app needing worldwide distribution with low latency everywhere?
- A) Azure SQL Database
- B) Cosmos DB
- C) Database for PostgreSQL
- D) Azure Cache

**Q16.** Which describes Single Sign-On (SSO)?
- A) Signing in once to access multiple applications
- B) Using two factors to authenticate
- C) A policy that blocks access
- D) A firewall rule

**Q17.** Which MFA factor is "something you ARE"?
- A) Password
- B) PIN
- C) Fingerprint
- D) Security token

**Q18.** A user is assigned the Reader role on a subscription. What can they do?
- A) Create resources in that subscription
- B) View all resources but change nothing
- C) Grant access to others
- D) Delete resources

**Q19.** Which service stores connection strings and API keys securely?
- A) Key Vault
- B) Blob storage
- C) Azure DNS
- D) Service Health

**Q20.** Which Azure Policy effect ALLOWS a resource but records a compliance warning?
- A) Deny
- B) Audit
- C) Append
- D) Notify

**Q21.** Which lock allows you to modify a resource but prevents deleting it?
- A) ReadOnly
- B) CanNotDelete
- C) Policy lock
- D) Tag lock

**Q22.** What is the purpose of tags on Azure resources?
- A) To increase security
- B) To organize resources and analyze costs
- C) To change the resource's performance
- D) To create backups

**Q23.** Which tool should you use to ESTIMATE the monthly cost of a planned solution before building it?
- A) Cost Management
- B) Azure Pricing Calculator
- C) TCO Calculator
- D) Advisor

**Q24.** Which service sends alerts and shows the health of AZURE ITSELF (e.g., an outage affecting a region)?
- A) Azure Monitor
- B) Service Health
- C) Advisor
- D) Defender for Cloud

**Q25.** Moving an on-premises app to Azure with NO code changes is called:
- A) Refactor
- B) Rehost
- C) Rebuild
- D) Rearchitect

---

## ✅ ANSWER KEY

| Q | Answer | Why |
|---|--------|-----|
| 1 | **B** | Private cloud = dedicated to one organization |
| 2 | **B** | Fault tolerance = keeps working through component failure |
| 3 | **B** | Consumption-based = pay only for what you use |
| 4 | **B** | Microsoft manages virtualization in IaaS; customer manages OS+ |
| 5 | **A** | RGs can span regions; no nesting; one RG per resource |
| 6 | **B** | Subscription = billing + access boundary |
| 7 | **B** | Zones protect against single data-center failure within a region |
| 8 | **B** | Policies at management groups flow down to subscriptions |
| 9 | **B** | VM = full control over OS/custom software |
| 10 | **C** | Functions = event-triggered serverless |
| 11 | **B** | VPN = encrypted over internet; ExpressRoute = private dedicated |
| 12 | **B** | Blob = unstructured files for websites |
| 13 | **D** | GZRS = max protection, most expensive |
| 14 | **D** | Archive = cheapest to store, rare access |
| 15 | **B** | Cosmos DB = global distribution |
| 16 | **A** | SSO = one sign-in, many apps |
| 17 | **C** | Fingerprint = biometrics = "something you are" |
| 18 | **B** | Reader = view only |
| 19 | **A** | Key Vault = secrets |
| 20 | **B** | Audit records warnings without blocking |
| 21 | **B** | CanNotDelete prevents deletion, allows changes |
| 22 | **B** | Tags = organization + cost analysis |
| 23 | **B** | Pricing Calculator = pre-build estimate |
| 24 | **B** | Service Health = Azure's own status |
| 25 | **B** | Rehost = lift-and-shift, no changes |

## 📊 Score yourself
- **23–25 (92%+)** → You are absolutely ready. Book the exam now. 🎉
- **20–22 (80–92%)** → Excellent. Review your 2–3 misses tonight and you're set.
- **Below 20 (<80%)** → Re-visit your weak spots with Day 38 dives tomorrow, then re-attempt this week's missed questions.

## ✅ Day 40 Checklist
- [ ] I took Mock #2 timed, without notes
- [ ] I scored and compared with Mock #1 (improvement?)
- [ ] I made a short list of remaining misses

---

# 📅 Day 41 — The Ultimate Memory Toolkit (Final Cheat Sheets)

## 🧠 Today's mission
**Memorize** the compact tables below. They compress the ENTIRE exam into the facts most worth remembering. Recite them 3× today (morning, noon, night), and again tomorrow before the exam.

## 🃏 Cheat Sheet 1: The "3s" of Azure

| Topic | The 3 |
|-------|-------|
| Service models | IaaS, PaaS, SaaS |
| Deployment models | Public, Private, Hybrid |
| Cloud benefits | Availability, Scalability, Elasticity |
| MFA factors | Know, Have, Are |
| RBAC big roles | Reader, Contributor, Owner |
| Redundancy levels | LRS, ZRS, GRS, GZRS |
| Storage tiers | Hot, Cool, Cold, Archive |
| Advisor categories | Cost, Security, Reliability, Performance, Operational Excellence |

## 🃏 Cheat Sheet 2: Responsibilities at a glance

| Level | You manage | Microsoft manages |
|-------|------------|-------------------|
| On-prem | Everything | Nothing |
| IaaS | OS, runtime, app, data | Hardware, storage, network, virtualization |
| PaaS | App, data | Everything below OS |
| SaaS | Data, access | Everything else |

## 🃏 Cheat Sheet 3: "Is it X or Y?" (final trap-buster)

| Confusion | Answer |
|-----------|--------|
| Zones vs. pairs | Zones = same region/separate buildings; pairs = two regions |
| LRS vs. GRS | LRS = one building; GRS = second region |
| NSG vs. Firewall | NSG = per-subnet; Firewall = whole VNet |
| Auth vs. Authz | Auth = who; Authz = what |
| VM vs. App Service | VM = full control; App Service = managed |
| App Service vs. Functions | App Service = always on; Functions = on-demand triggers |
| Scalability vs. elasticity | Scalability = ability; elasticity = automatic |
| Fault tolerance vs. DR | FT = never stops; DR = recover after |
| Policy vs. RBAC | Policy = resource rules; RBAC = people permissions |
| Calculator vs. Cost Mgmt | Calculator = estimate before; Cost Mgmt = actual after |
| Residency vs. sovereignty | Residency = where data lives; sovereignty = whose laws |
| Blob vs. Disk | Blob = standalone files; Disk = VM drives |

## 🃏 Cheat Sheet 4: The numbers to remember

| Fact | Number |
|------|--------|
| SLA 99.9% | ~8.76 hours downtime/year |
| SLA 99.99% | ~52.6 minutes downtime/year |
| Reserved instance discount | up to ~72% |
| MFA blocks account compromise | over 99% |
| Data Box usable size | ~80 TB |
| Availability zones per supported region | at least 3 |
| India regions | Pune (Central), Chennai (South), Mumbai (West) |
| Azure free account | ~₹7,000/$200 credit for 30 days |
| Pass score | 700 / 1000 |

## 🃏 Cheat Sheet 5: Mnemonics that stick

- **"I Put Stuff"** → IaaS = you manage more; PaaS = platform; SaaS = software. You manage *less* as you go right.
- **"P.H. Hybrid"** → Public, Hybrid, Private deployments.
- **"L Z G G" = "Little, Zone, Geo, Geo-Zone"** → LRS (little/one building), ZRS (zone), GRS (geo/second region), GZRS (both).
- **"Hot = Handle often; Archive = Attic"** → tier speed/cost ladder.
- **"R-C-O"** → Reader (view) < Contributor (manage) < Owner (everything + access).
- **"Know, Have, Are"** → MFA factors.
- **"4 R's = Rehost → Refactor → Rearchitect → Rebuild"** → moving from "same" to "new."

## 🎯 Final strategy for tricky questions
1. **Read the question fully** — look for "NOT," "EXCEPT," "LEAST," "MOST."
2. **Eliminate obviously wrong answers first** — two wrong options almost always exist.
3. **Watch for absolute words** — "always," "never," "only," "all" are usually wrong in Azure.
4. **Match the scenario word** — "managed," "serverless," "global," "private," "estimate," "actual" each point to a specific service.
5. **If stuck between two, pick the safer/Azure-best-practice one.**

## ✅ Day 41 Checklist
- [ ] I recited all 5 cheat sheets aloud
- [ ] I re-answered all my previously missed questions (from Mock 1 & 2) without notes
- [ ] I made flashcards OR a handwritten mini-cheat-sheet for tomorrow

---

# 📅 Day 42 — Exam Day Playbook (Booking, Format & Game Plan)

## 🧠 Today's mission
Make the **logistics** of the real exam stress-free. You'll learn exactly what to expect, how to book, and how to perform your best.

## 🗓️ Step 1: Book your exam

**Where:**
- Go to **learn.microsoft.com/certifications** → search **AZ-900** → click **"Schedule exam."**
- Exams are delivered by **Pearson VUE** — either **online (proctored)** from home or at a **test center** (choose whichever you prefer; online is convenient, test center avoids internet/tech worries).

**Cost:**
- ~**$55 USD** (about **₹4,500–5,000** in India).
- **Free vouchers exist** — watch for "Microsoft Training Days" (free sessions that include a free AZ-900 exam voucher), Microsoft Ignite events, and student/community offers. If you can wait, hunt these down — they come around regularly.
- Your retake (if ever needed) is ~$30.

**Validity:**
- AZ-900 is a **Fundamentals cert — it never expires** (no renewal needed). ✅

## 📋 Step 2: Know the exam format

| Fact | Details |
|------|---------|
| Questions | ~45–60 (typically ~50) |
| Time | 85 minutes |
| Question types | Multiple choice, multiple select, true/false, drag-and-drop, best-answer |
| Pass mark | **700 out of 1000** |
| Retake policy | Wait 24 hours before retaking |
| Difficulty | Beginner level — no hands-on tasks, purely conceptual |

**What the screen looks like:** You'll get a **Case Study/Scenario** style question at times (a short description, then 2–4 questions about it), plus standalone questions. You can **flag questions and review them** before submitting — use this!

## 🎯 Step 3: Your in-exam game plan (the "3-Pass Method")

1. **Pass 1 (fast):** Answer every question you know instantly. Flag the unsure ones. Don't linger.
2. **Pass 2 (medium):** Go back to flagged questions. Use elimination. Spend max ~1 minute each.
3. **Pass 3 (safe):** Review flags once more, then submit. Don't change answers unless you're SURE — your first instinct is usually right.

**Time math:** 50 questions / 85 minutes ≈ **1.7 minutes per question**. If you're stuck after 2 minutes, guess and flag — come back later.

## 🧘 Step 4: The night before + exam day

**Night before:**
- Review cheat sheets once (30 min max). **Do NOT cram new content.**
- Prepare ID (aadhaar/passport), headphones (if testing online), quiet room.
- Sleep 7–8 hours. This is the single biggest score boost. 😴

**Exam day (online proctored):**
- Sit in a **quiet, well-lit room**, clean desk, no extra monitors/devices.
- **Close all other tabs/apps** — the proctor checks your screen.
- Keep water outside the test area (usually not allowed inside).

**Exam day (test center):**
- Arrive **30 minutes early** with photo ID.
- Lockers for belongings; nothing but ID on your desk.

**During the exam:**
- Read the first screen carefully (some people miss that they can flag & review).
- Breathe. If your mind blanks, skip and return — the answer often resurfaces.

## 📈 Step 5: What happens after you pass
- Instant **pass/fail** on screen.
- Your **badge + certificate PDF** appear in your Microsoft Learn certification profile within ~24–48 hours.
- You can share the badge on LinkedIn — a great "beginner cloud certified" credential. 🎉

## ⚠️ Step 6: What if you fail?
- It happens — no shame. You'll see your **score by domain**, so you know exactly what to study.
- Wait 24 hours, re-focus on the weak domains (your hit list), and retake.

## ✅ Day 42 Checklist
- [ ] I know how to book (learn.microsoft.com → Pearson VUE)
- [ ] I know the format: ~50 Q / 85 min / pass 700
- [ ] I've planned my 3-pass strategy
- [ ] I've prepared my quiet space + ID for test day
- [ ] I've reviewed cheat sheets one last time

---

## 🏁 Week 6 Complete — and so is the entire course! 🎉

You've now studied **every single AZ-900 topic**, taken **50 practice questions**, mastered every trap, and built your memory toolkit. This is genuinely everything you need.

**If I could leave you with one message:** You've already done the hard part — showing up for 42 days. The exam tests exactly what you've just learned. Go in calm, use your 3-pass method, and trust your prep.

---

Want me to write your final **"Day 43–45: Cram Sheet + Exam-Day Checklist"** (the last mini-pack with a printable one-page revision sheet and final tips)? I can also give you a **bonus "last 10 hardest questions" quiz** to run the morning before your exam. Just say the word — and good luck, future Azure-certified! 🚀
