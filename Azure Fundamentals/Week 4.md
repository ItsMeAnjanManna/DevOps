# 📘 WEEK 4 — DATABASES, IDENTITY, SECURITY & COMPLIANCE
### *(Completes Domain 2 and covers Domain 3's security portion — ~35–40% of the exam)*

---

# 📅 Day 22 — Azure Databases (SQL, Cosmos DB, Open-Source)

## 🧠 First: what is a database? (quick refresher)
A **database** is an organized collection of data that a computer can store and query quickly — like a **giant, super-organized digital filing cabinet**.

**Real-life analogy:** A **library**:
- Books (data) are organized on shelves (tables).
- The librarian (database software) can instantly find any book by title, author, or topic.
- A database does this for your app's data.

## 📊 Two main database "families" (know the difference!)

**1. Relational (SQL) databases — "the grid/tables type"**
- Data goes in **tables** with **rows and columns** (like an Excel sheet).
- Rows are linked by **keys** (like IDs).
- Use **SQL (Structured Query Language)** to query.
- **Real-life analogy:** An **Excel workbook** with multiple sheets — each sheet (table) has neat rows/columns, and you join sheets by common values (like customer ID).
- **Best for:** structured data with clear relationships — orders, customers, inventory, bank records.

**2. Non-relational (NoSQL) databases — "the flexible type"**
- No strict tables/columns — data can be stored as **documents (JSON)**, key-value pairs, graphs, etc.
- Super flexible and scales massively.
- **Real-life analogy:** A **filing cabinet full of loose folders** — each folder can contain anything, in any format (a photo, a note, a form). No fixed template required.
- **Best for:** huge, fast-changing, unstructured data (user profiles, product catalogs, IoT data, social feeds).

| | Relational (SQL) | Non-relational (NoSQL) |
|---|---|---|
| Structure | Tables, rows, columns | Documents/key-value/graph |
| Query language | SQL | Varies (often APIs) |
| Best for | Structured, related data | Flexible, huge-scale data |
| Analogy | Excel workbook | Loose folder cabinet |

## 🗄️ The Azure database services you must know:

**1. Azure SQL Database** — the managed relational star
- A **fully managed relational database** built on Microsoft SQL Server.
- Azure handles backups, patching, monitoring, and scaling — you just point your app at it.
- **Real-life analogy:** A **serviced office** — you move in with your desk (schema/data); the building management handles electricity, cleaning, security.
- **When to use:** Existing SQL Server apps, e-commerce, ERP, line-of-business apps.
- **Exam note:** It's **PaaS** — you don't manage the server, just the database content.

**2. Azure Cosmos DB** — the global NoSQL superstar
- A **globally distributed NoSQL database** — your data is automatically replicated across regions so users anywhere read it with low latency.
- Supports multiple APIs: document (JSON), key-value, graph, Cassandra, MongoDB, etc.
- **Real-life analogy:** A **global franchise chain** — every city has a local branch so customers get instant service; the company syncs inventory everywhere.
- **When to use:** Global apps, IoT, gaming, real-time feeds where speed everywhere matters; massive scale.
- **Exam note:** It's the "globally distributed, multi-model database" — remember that phrase.

**3. Azure Database for MySQL / PostgreSQL** — open-source relatives
- Managed versions of the popular **open-source databases** (MySQL and PostgreSQL).
- Same benefits as SQL Database (managed, patched, scaled) but for the open-source engine your team already knows.
- **When to use:** Apps already built on MySQL/PostgreSQL (very common in startups, WordPress, etc.).

## 🆚 PaaS Database vs. Running a Database on a VM
| | Database on a VM (IaaS) | Managed Azure Database (PaaS) |
|---|---|---|
| You manage | OS, DB install, backups, patching | Just your data & schema |
| Effort | High | Low |
| Best when | Need exact custom DB config | Want to focus on the app |

> 💡 **Rule of thumb:** If you *can* use a managed database (PaaS), do it. Only use a VM database when you have a specific custom need.

## 📊 Quick memory table

| Service | Type | Key phrase for the exam |
|---------|------|-------------------------|
| Azure SQL Database | Relational (SQL) | Managed SQL Server |
| Cosmos DB | Non-relational (NoSQL) | Globally distributed, multi-model |
| Database for MySQL | Relational, open-source | Managed MySQL |
| Database for PostgreSQL | Relational, open-source | Managed PostgreSQL |

## ✅ Day 22 Checklist
- [ ] I can explain relational vs. non-relational with the Excel/folder analogy
- [ ] I can name all 4 database services and one key fact each
- [ ] I know the phrase "globally distributed" belongs to Cosmos DB

---

# 📅 Day 23 — Review & Practice (Compute + Networking + Storage + DB)

Today is a **consolidation day**. No new topics. You'll review Weeks 2–3 material with a practice test and a hands-on exercise.

## 📋 What to review today (quick checklist)

**Compute (Day 15–16):**
- VM = software computer; price depends on size/OS/region/uptime.
- Scale sets = auto-scaling groups; availability sets = fault/update domains.
- App Service = managed web hosting (PaaS); Functions = event-triggered serverless.
- Containers = packaged apps (ACI simple, AKS big).

**Networking (Day 17–19):**
- VNet = private network; subnets = partitions; peering = bridge between VNets.
- Load Balancer (L4) vs. Application Gateway (L7 + WAF).
- VPN Gateway (encrypted, on public internet) vs. ExpressRoute (private, dedicated).

**Storage (Day 20–21):**
- Blob (files), Disk (VM drives), Files (shares), Queue (messages), Table (key-value).
- Redundancy: LRS → ZRS → GRS → GZRS (increasing protection & cost).
- Tiers: Hot → Cool → Cold → Archive (decreasing cost, slower retrieval).

**Databases (Day 22):**
- SQL = relational/table-based; NoSQL = flexible/documents.
- SQL Database (managed SQL Server), Cosmos DB (globally distributed), MySQL/PostgreSQL (managed open-source).

## ✍️ Practice Test (10 mixed questions — answer before checking)

1. Which PaaS lets you host a web app without managing servers?
2. Which service runs code only when a trigger fires?
3. True/False: ExpressRoute uses the public internet.
4. Which storage redundancy copy data to a second region?
5. Which storage tier is cheapest to store but slowest to access?
6. Which database is "globally distributed and multi-model"?
7. Which load balancer understands URL paths and has a firewall?
8. Which storage service would you use for a shared network drive for many VMs?
9. VNet peering connects: (a) subnets, (b) two VNets, (c) regions only?
10. Which is cheaper: a VM or App Service hosting the same simple website? (Hint: what are you paying to manage?)

**Answer key:** 1. App Service · 2. Azure Functions · 3. False (it's private/dedicated) · 4. GRS (and GZRS) · 5. Archive · 6. Cosmos DB · 7. Application Gateway · 8. Azure Files · 9. (b) two VNets · 10. App Service (you're not paying to manage a VM you don't need)

## 🛠️ Hands-On Challenge (ties everything together)
1. Create a **resource group** `rg-learn-wk3` (Central India).
2. Create a **Storage Account** in it → upload a small file to a **blob container**.
3. Create an **App Service** (choose the free F1 tier if available, else the cheapest) and note how there's NO VM to manage.
4. Create a **Virtual Network** with a subnet (just observe its structure).
5. In the portal, open the **load balancer** section (just browse — don't create).
6. **Delete the entire resource group** — watch it clean up everything in one click. ✅

## ✅ Day 23 Checklist
- [ ] I scored 7+/10 on the mixed test (if not, re-read the flagged days)
- [ ] I did the hands-on challenge and deleted everything
- [ ] I can now explain the "big picture" of how a simple app is built (App Service + Storage + DB + VNet)

---

# 📅 Day 24 — Microsoft Entra ID (Azure Active Directory)

## 🧠 What is identity?
**Identity = who you are.** In the cloud, *identity* systems answer: *"How do we know you're you, and how do we let you into the right places?"*

**Real-life analogy:** Your **Aadhaar card / passport** proves who you are at airport security. Identity systems in IT do the same for people *and* machines.

## 🏢 What is Microsoft Entra ID (formerly Azure AD)?
**Microsoft Entra ID** is Microsoft's **cloud-based identity and access management service**. It's the **directory of users, groups, and devices** that Microsoft uses to let people sign in to Azure, Microsoft 365, and thousands of other apps.

**Real-life analogy:** Think of it as the **master guest list at a giant, secure office complex**:
- It stores who everyone is (users) and which team they belong to (groups).
- When you swipe your badge at a door, the system checks the list: *"Is this person allowed in?"* 
- Entra ID is that master list + the badge-checking system.

**Key things to know:**
| Feature | Explanation |
|---------|-------------|
| **Directory** | Stores users, groups, and their attributes |
| **Single Sign-On (SSO)** | Sign in once → access many apps without re-entering passwords (like one badge opening every door in the building) |
| **Supports cloud-only AND on-premises** | Can sync with your existing on-premises AD (called **Entra Connect** / AD Connect — just know it exists) |
| **Used by Microsoft 365 too** | Same identity powers Office apps, Teams, etc. |

> 🧠 **Memory trick:** Entra ID = "Azure Active Directory" renamed (March 2023). If old material says **Azure AD**, it's the same thing. The exam may use either name — treat them as identical.

**Who needs to know about Entra ID?** Everyone. It's the front door to Azure — when you sign into the Azure portal, Entra ID is checking who you are.

## Port Groups (know the concept)
- **Users** = individual people.
- **Groups** = collections of users (like "Finance Team"). You assign permissions to the *group*, and everyone in it inherits them — far easier than managing users one-by-one.
- **Real-life analogy:** Instead of giving each employee a separate key to a room, you give one key to the "Finance Team" group; anyone in that team uses it.

## ✅ Day 24 Checklist
- [ ] I can explain Entra ID as "the master guest list / front door"
- [ ] I know SSO = sign in once, access many
- [ ] I know Entra ID = old "Azure AD"

---

# 📅 Day 25 — Authentication vs. Authorization, MFA & Conditional Access

## 🔑 The two "A"s — don't confuse them (exam favourite!)

| | Authentication | Authorization |
|---|---|---|
| **What it is** | Verifying **WHO you are** | Deciding **WHAT you can do** |
| **Question it answers** | "Are you really you?" | "Are you allowed to do this?" |
| **Analogy** | Showing your **ID/passport** at the gate | The security guard checking whether you have a **ticket for that section** |
| **Simplified** | Proving identity → **Are you who you say you are?** | Assigning permissions → **What are you allowed to do?** |

**Real-life example:** At an airport:
- **Authentication:** You show your passport → the officer verifies it's really you. ✅
- **Authorization:** The officer checks your boarding pass → only passengers with a boarding pass may enter the gate area. 🎫

**In Azure:** Signing in = authentication. Being allowed to create/delete resources = authorization (that's RBAC tomorrow).

## 📱 Multi-Factor Authentication (MFA) — your digital bodyguard
**What it is:** Requires **two or more different pieces of evidence** to prove who you are.

**The 3 "factors" (remember these):**
| Factor | Type | Example |
|--------|------|---------|
| **Something you KNOW** | Knowledge | Password, PIN |
| **Something you HAVE** | Possession | Phone (SMS code), authenticator app, security key |
| **Something you ARE** | Inherence | Fingerprint, face scan, retina |

**Real-life analogy:** Withdrawing money from an ATM:
- Your **ATM card** = something you HAVE.
- Your **PIN** = something you KNOW.
- (Modern banks add your **fingerprint/face** = something you ARE.)

**Why MFA matters (the exam loves "why"):** If someone steals your password, they still can't get in without the second factor. **MFA blocks over 99% of account-compromise attacks** (Microsoft's own stat — you can quote it).

## 🚦 Conditional Access
**What it is:** **Rules** that decide *whether* to let someone in based on conditions — like a smart security guard with extra instructions.

**Real-life analogy:** A nightclub bouncer with a VIP list:
- *Normal hours:* anyone with a ticket enters.
- *After midnight:* only VIPs (condition: time) with two forms of ID (condition: MFA) enter.

**Conditions that can trigger extra checks:**
- User's **location/country** (e.g., block sign-ins from unknown countries).
- **Device** (must be a company-managed device).
- **Risk** (unusual sign-in behavior).
- **App sensitivity** (admin portal requires MFA, email doesn't).

**Result:** If a condition is met, Azure can **require MFA, block access, or limit access** — automatically.

## ✅ Day 25 Checklist
- [ ] I can explain auth vs. authz with the passport/ticket analogy
- [ ] I know the 3 MFA factors (know/have/are)
- [ ] I can explain Conditional Access as "smart conditional rules"

---

# 📅 Day 26 — Role-Based Access Control (RBAC)

## 🧠 What is RBAC?
**RBAC** is how Azure controls **authorization** — *who can do what* on which resources. It's Azure's permissions system.

**Real-life analogy:** An **office building with key cards**:
- You get a card that opens *certain doors only*.
- The cleaning staff can enter rooms to clean but can't open the safe.
- The manager can open everything.
- RBAC is the same for Azure resources: everyone gets exactly the access they need — no more, no less.

## 🧩 The 3 parts of RBAC (memorize this formula)
**RBAC = Security Principal + Role + Scope**

| Part | What it is | Example |
|------|------------|---------|
| **Security principal** | WHO gets permission | A user, group, service principal (app), or managed identity |
| **Role** | WHAT they can do | Owner, Contributor, Reader (see below) |
| **Scope** | WHERE they can do it | Management group, subscription, resource group, or a single resource |

## 📜 The 3 built-in roles you MUST know (exam favourite)

| Role | What it lets you do | Analogy |
|------|---------------------|---------|
| **Owner** | **Full control** — everything Contributor can do, PLUS manage access (give roles to others) | The building owner |
| **Contributor** | **Create and manage resources**, but cannot grant access to others | A facilities manager |
| **Reader** | **View everything**, but can't change anything | A security guard watching cameras / a guest with read-only access |

**Memory ladder:** Reader (👀 view only) → Contributor (🛠️ build/manage) → Owner (👑 everything + access control). More responsibility as you go up.

**Other roles to know exist (not in depth):**
- **User Access Administrator** — manages user access only.
- Custom roles can be created too, but the exam focuses on the big three.

## 🎯 Scopes: "WHERE does the permission apply?"
Permissions flow **downward** through the hierarchy:

```
Management Group → Subscription → Resource Group → Resource
```

**Key rule:** If you grant a role at a higher level, it applies to everything below it.
- Grant **Reader on a resource group** → you can read *all* resources inside it.
- Grant **Contributor on a subscription** → you can manage *all* resource groups and resources under that subscription.
- Grant **Owner on a single VM** → you control just that VM.

**Real-life analogy:** A **museum badge system**:
- "Visitor" badge at the entrance (whole museum) = everyone inside can view.
- "Staff" badge for the storage room only = only that room.

## 💡 Best practices (know these principles)
- **Least privilege:** Give people only the minimum access they need. Don't hand out Owner to everyone.
- **Use groups, not individuals:** Assign roles to groups, not single users (easier to manage).
- **Grant at the narrowest scope possible:** Prefer resource-group-level over subscription-level unless needed.

## ⚠️ Beginner gotcha
**RBAC ≠ Entra ID (that's identity) ≠ MFA (that's authentication).** RBAC is purely about *permissions* after someone is authenticated. (Many exam questions test that you know these three are different things.)

## ✅ Day 26 Checklist
- [ ] I know the 3 RBAC parts: principal + role + scope
- [ ] I can recite the 3 roles and what each can do
- [ ] I know permissions flow downward through the hierarchy
- [ ] I can explain "least privilege"

---

# 📅 Day 27 — Security Tools: Defender for Cloud, NSGs, Firewall, Key Vault

## 🛡️ 1. Microsoft Defender for Cloud
**What it is:** A **unified security monitoring tool** that watches your Azure resources and gives you **recommendations** and **alerts** if something looks risky.

**Real-life analogy:** A **24/7 security control room with CCTV plus a security consultant**:
- It watches everything (CCTV).
- It flags suspicious activity (alerts).
- It tells you how to fix weaknesses (recommendations) — like "your VM is missing a security update."

**Key facts:**
- Provides **security posture assessment** (a score) across your subscription.
- **Alerts** on threats (e.g., brute-force login attempts).
- **Recommendations** to harden resources.
- **Azure Secure Score** — a number (0–100%) showing how well-protected you are. (Know this term — exam loves it.)

## 🔒 2. Network Security Groups (NSGs)
**What it is:** A **firewall rule-set at the network level** — a filter attached to a subnet or a NIC (network interface card) that allows/denies traffic.

**Real-life analogy:** The **security guard at your building's entrance** who checks a list: *"Allowed in: employees with badges. Not allowed: anyone else."* He stands at the door (network boundary) and applies the rules.

**Key facts:**
- Contains **rules** with: source, destination, port, protocol, and action (Allow/Deny).
- Example rule: "Deny all internet traffic to port 3389 (RDP) on the database subnet."
- **Default NSG rules** allow internal traffic within a VNet by default and deny inbound internet traffic by default — you add rules to open specific things.

## 🔥 3. Azure Firewall
**What it is:** A **fully managed, stateful firewall service** — a bigger, smarter, cloud-native firewall for your *entire VNet* (whereas NSGs are per-subnet/per-NIC filters).

**Real-life analogy:** The **main security checkpoint at a city's border** (the whole city = your VNet). It checks all traffic entering/leaving and can block known bad destinations.

**Key facts:**
- **Stateful:** it remembers connections and tracks traffic direction.
- Can filter by IP, port, protocol, and FQDN (domain names).
- Centralized logging + integration with monitoring.
- **Exam note:** NSG = per-subnet network filter; **Azure Firewall = whole-VNet managed firewall**. That's the core difference.

## 🗝️ 4. Azure Key Vault
**What it is:** A secure, centralized **place to store secrets** — passwords, connection strings, API keys, and certificates — encrypted and protected.

**Real-life analogy:** A **bank safety deposit box**:
- Your app needs its password (like needing cash) but you don't leave cash lying around.
- You keep the cash in the vault; your app requests it from the vault when needed — securely, with logging.

**Key facts:**
- Stores **secrets** (passwords/keys), **keys** (encryption keys), **certificates**.
- Controls access via RBAC/policies.
- **Rotation** (changing secrets regularly) and audit logging.
- **Best practice:** Never store secrets in your app code; fetch them from Key Vault instead.

## 📊 Security tools quick table

| Tool | What it watches/controls | Analogy |
|------|--------------------------|---------|
| **Defender for Cloud** | Overall security posture + alerts | CCTV control room + consultant |
| **NSG** | Filters traffic at a subnet/NIC | Entrance guard with a checklist |
| **Azure Firewall** | Firewall for the whole VNet | City border checkpoint |
| **Key Vault** | Stores secrets safely | Bank safety deposit box |

## ✅ Day 27 Checklist
- [ ] I can explain Defender for Cloud and "Secure Score"
- [ ] I know NSG (per-subnet) vs. Azure Firewall (whole VNet)
- [ ] I know Key Vault stores secrets and why that matters

---

# 📅 Day 28 — Privacy, Compliance & Trust

## 🧠 What is compliance, in one line?
**Compliance = following laws, regulations, and standards** about how data must be handled, stored, and protected.

**Real-life analogy:** A **restaurant must pass health inspections**. If it handles customers' private data (not food), it must pass *data protection* inspections (like GDPR). Compliance is "passing the inspection."

## 🌍 Why does this matter for Azure?
Different countries/industries have rules:
- **GDPR** (Europe) — strict rules for personal data of EU citizens.
- **HIPAA** (US) — health data protection.
- **ISO 27001** — international information security standard.
- **PCI DSS** — payment card data standard.
- **IT Act / DPDP Act** (India) — India's data protection framework (the Digital Personal Data Protection Act, 2023).

**The key idea for the exam:** **Microsoft (Azure) offers compliance offerings** that help *your* organization meet these standards — Azure provides certifications, guarantees, and tools, but *you* are still responsible for configuring services correctly to stay compliant.

## 🤝 Shared responsibility for compliance (remember Week 1!)
- **Microsoft** is responsible for the *security of the cloud* (the infrastructure is compliant).
- **You** are responsible for the *security in the cloud* (how you configure and use services).

## 🛡️ Azure's compliance & trust toolkit (know these names)

| Tool/Offering | What it does | Analogy |
|---------------|--------------|---------|
| **Microsoft Trust Center** | The hub where you can see all compliance certifications & how Microsoft protects data | The "health inspection report" wall |
| **Service Trust Portal** | Deeper documents, audit reports, and compliance guides (often used by compliance officers) | The actual inspection files |
| **Compliance Manager** | A tool that helps you track your compliance obligations (like a compliance "score") | A self-check list before inspection |
| **Azure Policy** | Enforces rules on your resources (e.g., "only resources in India regions") | Automated rule enforcement |
| **Sovereign regions** | Isolated Azure clouds for governments (e.g., Azure Government) | A special, isolated campus |

*(Azure Policy gets full coverage in Week 5 — today just know it exists as a compliance enforcement tool.)*

## 🗄️ Data residency, sovereignty & privacy

**1. Data residency** — where data *physically lives*.
- Azure lets you store data in specific regions (e.g., India) to satisfy local laws.
- **Real-life analogy:** Your bank keeps your locker in a branch within your city because rules say it must.

**2. Data sovereignty** — *which country's laws apply*.
- If data is stored in India, Indian law governs it. Azure's **geographies** group regions so data stays within boundaries (e.g., the "India geography" keeps data in India).

**3. Microsoft Privacy Statement** — the document explaining *how Microsoft handles your data*.
- Key promises: Microsoft **does not use your customer data for advertising**, and you **own your data** — Microsoft only process it to provide the services.

**4. Azure provides Data Protection tools:**
- **Encryption at rest** — data is encrypted when stored (like a locked safe).
- **Encryption in transit** — data is encrypted while moving (TLS/HTTPS — like a sealed envelope).
- **Azure Information Protection / Purview** — helps classify and protect sensitive documents (just know they exist).

## 🔐 One more important concept: Zero Trust (know the phrase)
Modern security model: **"Never trust, always verify."**
- Assume every request could be a threat until verified.
- Always authenticate, authorize, encrypt, and monitor — regardless of whether the request is "inside" or "outside" the network.
- **Real-life analogy:** Instead of trusting anyone inside the building automatically, the bouncer checks *everyone's* badge — every time, at every door.

## ✅ Day 28 Checklist
- [ ] I can define compliance in one sentence
- [ ] I know the Trust Center / Service Trust Portal / Compliance Manager names
- [ ] I can explain data residency vs. data sovereignty
- [ ] I know the "security of the cloud vs. in the cloud" split
- [ ] I can explain Zero Trust in one line

---

# 🏁 Week 4 Review & Self-Test

## 📋 Week 4 Summary Table (memorize)

| Concept | One-line meaning | Analogy |
|---------|------------------|---------|
| Azure SQL Database | Managed relational SQL database | Serviced office |
| Cosmos DB | Globally distributed NoSQL | Global franchise chain |
| MySQL/PostgreSQL | Managed open-source databases | Managed versions of popular engines |
| Microsoft Entra ID | Cloud identity/access directory | Master guest list |
| SSO | Sign in once, access many apps | One badge, every door |
| Authentication | Proving WHO you are | Passport check |
| Authorization | Deciding WHAT you can do | Boarding-pass check |
| MFA | 2+ factors to prove identity | ATM card + PIN |
| Conditional Access | Smart sign-in rules | Bouncer with VIP rules |
| RBAC | Permissions = principal + role + scope | Office key-card system |
| Owner/Contributor/Reader | Full / manage / view-only | Building owner / manager / guard |
| Defender for Cloud | Security monitoring + recommendations | CCTV + security consultant |
| NSG | Per-subnet network filter | Entrance guard with checklist |
| Azure Firewall | Whole-VNet managed firewall | City border checkpoint |
| Key Vault | Secure storage for secrets | Bank safety deposit box |
| Compliance | Following laws & standards | Passing inspections |
| Trust Center | Where certifications are shown | Health-inspection reports |
| Data residency | Where data physically lives | City where your locker is |
| Data sovereignty | Which country's laws apply | Which city's rules govern |
| Zero Trust | Never trust, always verify | Check everyone's badge every time |

## 📖 Week 4 Vocabulary (learn these)
1. **Database** — organized collection of queryable data
2. **SQL** — language for relational databases
3. **NoSQL** — non-relational, flexible data
4. **Identity** — who a user/device is
5. **Directory** — the store of users/groups (Entra ID)
6. **SSO** — single sign-on
7. **Authentication** — verifying identity
8. **Authorization** — granting/denying permissions
9. **MFA** — multi-factor authentication (know/have/are)
10. **Conditional Access** — context-based sign-in rules
11. **RBAC** — role-based access control
12. **Principal** — who is receiving permission
13. **Role** — what they can do
14. **Scope** — where they can do it
15. **Least privilege** — minimum access needed
16. **Secure Score** — Defender for Cloud's security rating
17. **NSG** — network security group (per-subnet filter)
18. **Key Vault** — secret storage service
19. **Compliance** — meeting laws/standards
20. **Zero Trust** — "never trust, always verify"

## ✍️ Self-Test (12 questions — try before reading the key)

1. Which is "proving who you are": authentication or authorization?
2. Which is "deciding what you can do": authentication or authorization?
3. Name the three MFA factors.
4. Which MFA factor is a fingerprint? Know / Have / Are
5. Which RBAC role can grant access to others? Reader / Contributor / Owner
6. Which role can create resources but NOT grant access? Reader / Contributor / Owner
7. If you grant Reader on a resource group, where does it apply?
8. Which tool gives a "Secure Score" for your whole subscription?
9. Which filters traffic at the subnet level: NSG or Azure Firewall?
10. Where should you store your app's connection string? In code / In Key Vault
11. ____ = where data physically lives; ____ = which country's laws apply.
12. What does "Zero Trust" mean in one phrase?

**Answer key:** 1. Authentication · 2. Authorization · 3. Something you know / have / are · 4. Are (inherence) · 5. Owner · 6. Contributor · 7. All resources inside that resource group (and below) · 8. Defender for Cloud · 9. NSG · 10. Key Vault · 11. Residency / Sovereignty · 12. "Never trust, always verify"

---

## 🏁 Week 4 Complete! What's next?
You've now finished **all of Domain 2** and the **security/compliance half of Domain 3**. You know how Azure is built, how apps run, and how it's all protected. **Week 5 (Day 31–38)** covers the *management & governance* half of Domain 3: **cost factors, pricing/TCO calculators, Azure Policy, tags, resource locks, management tools, monitoring, Azure Arc, and Azure Migrate** — then Week 6 is full mock exams and final review.

Want me to write the same complete, beginner-style notes for **Day 31–38 (Week 5)** next? 📚
