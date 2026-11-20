# 📘 WEEK 3 — COMPUTE, NETWORKING & STORAGE
### *(Second half of Domain 2 — the biggest part of the exam)*

---

# 📅 Day 15 — Virtual Machines (VMs), Scale Sets & Availability

## 🧠 What is a Virtual Machine (VM)?
A **VM** is a **computer that exists only in software** — running on Azure's physical servers.

**Real-life analogy:** It's like a **video-game character** — it looks and acts like a real person, but it lives inside the game world (the cloud). Azure's physical servers are the "game console"; your VM is the character you created.

## 🛠️ How does it work (simplified)?
- One giant physical server (a "host") can run **many virtual machines** at once.
- A special program (the **hypervisor**) divides the physical machine into multiple isolated VMs.
- Each VM has its own virtual CPU, RAM, storage (disk), and operating system.
- To you, it feels exactly like owning a real computer — you can install software, run apps, log in, shut it down.

## 💰 What determines a VM's price?
| Factor | Explanation |
|--------|-------------|
| **Size (vCPU + RAM)** | Bigger = pricier. You pick from preset sizes (e.g., `Standard_A1`, `Standard_B1s`, `Standard_D2s_v3`) |
| **Operating system** | Windows VMs cost slightly more than Linux (Windows licensing) |
| **Disk type & size** | Standard HDD (cheap) vs. Premium SSD (fast, pricier) |
| **Region** | Different regions have different prices |
| **Uptime** | You pay while a VM is **running** (stopped = usually no compute charge, but disk storage still costs) |
| **Reserved vs. pay-as-you-go** | Prepay 1–3 years for big discounts |

## 🎯 When SHOULD you use a VM? (exam favourite)
Use a VM when you need **full control** over the environment:
- You need a **specific OS version** or custom configuration.
- You're doing **lift-and-shift** — moving an existing on-premises app "as-is" to Azure.
- You need to run **custom software** or install things freely.
- You need a **test environment** that mimics real hardware.

**Don't use a VM if** a PaaS service (App Service — Day 16) can do the job — you'd be paying to manage what Azure could manage for you.

## 👯 Two things often confused with VMs — get them clear now:

**1. VM Scale Sets**
- A **VM Scale Set** is a **group of identical VMs** that can **automatically grow/shrink** based on demand.
- Real-life analogy: A call center with a manager who adds agents during peak hours and sends them home when it's quiet.
- Use them for apps that need many identical machines and auto-scaling (e.g., a website that gets a Diwali traffic spike).

**2. Availability Sets**
- (You met these in Week 2 — quick recap.)
- An **availability set** spreads your VMs across **fault domains** (physical racks) and **update domains** (maintenance groups).
- Real-life analogy: Instead of storing all your servers on one rack (one plug point), you spread them across different racks with separate power — if one breaks, others survive.
- Limitations: availability sets live *within a single data center*; for cross-building protection, use **Availability Zones** (Week 2) — the modern approach.

## ⚠️ Beginner gotcha
A VM is **not a website** — it's a computer. If you want to *host a website easily*, you'd usually use **App Service** (tomorrow) not a VM. A VM is for when you need the whole machine.

## ✅ Day 15 Checklist
- [ ] I can explain a VM with the video-game analogy
- [ ] I can list 3 things that change VM price
- [ ] I know scale sets (auto-scaling group) vs. availability sets (rack protection) vs. availability zones (building protection)

---

# 📅 Day 16 — App Service, Azure Functions & Containers

Today is about the **PaaS** options — ways to run apps *without* managing servers.

## 🌐 1. Azure App Service (the everyday website host)

**What it is:** A fully managed **PaaS service to host web apps, REST APIs, and mobile backends**. You upload your code; Azure handles the servers, OS, patching, scaling, and load balancing.

**Real-life analogy:** It's like a **restaurant kitchen that's fully staffed** — you just bring your recipe (your code), and the kitchen (Azure) does the cooking, cleaning, and hires extra chefs automatically when it gets busy.

**Key features to know:**
| Feature | Meaning |
|---------|---------|
| **Automatic scaling** | It can add instances when traffic grows (no manual work) |
| **Built-in load balancing** | Traffic is spread automatically across instances |
| **Deployment slots** | Test a new version (staging) before swapping it into production |
| **Continuous deployment** | Auto-deploy from GitHub, Azure DevOps, etc. |
| **Managed certificates** | Free SSL/TLS certificates (HTTPS) |
| **Multiple languages** | .NET, Java, Node.js, Python, PHP, etc. |

**When to use App Service:** You have a **web app/API** and want zero server maintenance. This is *the* go-to PaaS for websites.

## ⚡ 2. Azure Functions (serverless compute)

**What it is:** Run **small pieces of code (functions)** that execute **only when triggered** — you pay only for the milliseconds they run. No server to manage, no VM to keep running.

**Real-life analogy:** A **vending machine** — it only "works" when someone presses a button (trigger). You don't pay for it standing idle; you pay per snack dispensed.

**Common triggers (what "wakes up" a function):**
- An HTTP request (someone visits a URL).
- A new file uploaded to storage.
- A message arrives in a queue.
- A timer (e.g., run every hour).
- A change in a database.

**When to use Functions:** Short, event-driven tasks — resizing images on upload, sending emails, processing orders, scheduled cleanup jobs.

> 🧠 **Memory trick:** **App Service** = a restaurant that runs continuously. **Functions** = a vending machine that only works on demand. ("Continuously running" vs. "event-triggered.")

## 📦 3. Containers (the modern way to package apps)

**What they are:** A **container** bundles your app + all its dependencies (libraries, settings, runtime) into one neat, portable package that runs the same anywhere.

**Real-life analogy:** A **shipping container**. A container of goods can be loaded on a ship, truck, or train and handled identically everywhere. The goods (your app) travel safely with everything they need inside.

**Key concepts (just the basics for AZ-900):**
| Term | Meaning |
|------|---------|
| **Container** | A packaged, isolated app + its environment |
| **Image** | The "blueprint" template a container is created from |
| **Docker** | The most popular tool for building/running containers |
| **Container registry** | A library of images (like Azure Container Registry) |
| **Orchestration** | Automating many containers (like Kubernetes) |

**Azure container services to know the names of:**
- **Azure Container Instances (ACI)** — simplest way to run a single container (no management).
- **Azure Kubernetes Service (AKS)** — runs many containers across many machines with auto-scaling and self-healing (the big enterprise option).
- **Azure Container Apps** — a middle ground (serverless containers).

**When to use containers vs. VMs:**
- **Containers:** You want portability, fast startup (seconds), and to run many copies of your app on one machine efficiently.
- **VMs:** You want a full isolated machine with a custom OS — containers share the host OS, VMs don't.

## 📊 Compare the 4 ways to run apps (memorize this table)

| Option | Model | You manage | Serverless? |
|--------|-------|------------|:---:|
| **Virtual Machine** | IaaS | OS + everything above | ❌ |
| **App Service** | PaaS | Just your app code | ❌ (always running) |
| **Azure Functions** | PaaS/serverless | Just your function code | ✅ |
| **Containers (ACI/AKS)** | PaaS-ish | The container itself | ACI = yes, AKS = partly |

## ✅ Day 16 Checklist
- [ ] I can explain App Service vs. Functions (restaurant vs. vending machine)
- [ ] I know what a container is (shipping container analogy)
- [ ] I know when to choose VM vs. App Service vs. Functions

---

# 📅 Day 17 — Virtual Networks (VNet) & Subnets

## 🧠 What is a Virtual Network (VNet)?
A **VNet** is Azure's version of **your own private network in the cloud** — a secure, isolated boundary where your resources communicate with each other.

**Real-life analogy:** Think of your **home Wi-Fi network**:
- Your phone, laptop, and TV are all connected to the same router.
- They can talk to each other and share the internet.
- A VNet is exactly this — but for your cloud resources (VMs, databases, apps) instead of gadgets.

## 🔑 Why do we need a VNet?
- **Isolation:** Your resources are separated from everyone else's by default.
- **Secure communication:** VMs can talk to each other privately, without going over the public internet.
- **Control:** You define IP ranges, subnets, and rules.

## 📏 Key terms & facts

**1. Private IP ranges (the basics)**
VNet addresses come from private ranges, like `10.0.0.0/16` or `192.168.0.0/16`. (Don't stress about CIDR notation for AZ-900 — just know you *define an address space*.)

**2. Subnets**
A **subnet** is a **sub-division of your VNet** — like splitting your home network into "kids' devices" and "parents' devices" or "guest Wi-Fi".
- You put resources that share rules into the same subnet.
- Example: A subnet for web servers and a separate subnet for databases (so databases are harder to reach from outside).

**3. VNet Peering**
**VNet peering** securely connects **two VNets** so their resources can talk to each other — like putting a **bridge between two separate Wi-Fi networks**.
- Works across regions and subscriptions.
- Traffic stays on Microsoft's private backbone (not public internet) → fast and secure.

**4. Public vs. Private IP addresses**
| Type | Meaning | Example |
|------|---------|---------|
| **Private IP** | Only reachable inside your VNet | Your home devices' internal addresses |
| **Public IP** | Reachable from the internet | Your home's public address, visible to the world |

## 🏠 Real-world example to tie it together
Imagine you build a website:
- Your web VMs sit in a **"web subnet"** (reachable from the internet via a public IP).
- Your database sits in a **"db subnet"** (only reachable from the web subnet — never directly from the internet).
- The web VM and database talk to each other **privately inside the VNet**. 🔒

## ⚠️ Beginner gotcha
**A VNet is not a region or a resource group** — it's a network. It lives inside a resource group, within a region, and it's one of the resources in your subscription. Also: **you can't create a VNet in the free "permanently free" tier** — but you *can* create one if you have active credit; just delete it after experimenting (we'll do it on Day 23).

## ✅ Day 17 Checklist
- [ ] I can explain a VNet using the home Wi-Fi analogy
- [ ] I know what a subnet and VNet peering are
- [ ] I can explain public vs. private IP in simple terms

---

# 📅 Day 18 — Load Balancer, Application Gateway & DNS

## ⚖️ 1. Azure Load Balancer (Layer 4)
**What it does:** Spreads incoming traffic across multiple VMs **so no single VM gets overloaded** — and it automatically stops sending traffic to a VM that fails.

**Real-life analogy:** A **restaurant hostess** at the door who sends customers to whichever waiter is least busy. If one waiter is sick, she stops sending customers to him.

**Key facts:**
- Works at **Layer 4** (network level — it looks at IP addresses and ports).
- Best for **internal traffic** between VMs and for basic internet traffic splitting.
- It **doesn't look at the content** of the traffic — it just balances the connections.

## 🌐 2. Application Gateway (Layer 7)
**What it does:** A smarter load balancer that **understands web traffic** and routes based on URL, path, or host — plus it includes a **Web Application Firewall (WAF)** to block attacks.

**Real-life analogy:** A **smart traffic controller that can read delivery packages** — he sees that food deliveries should go to the kitchen door, parcels to the loading bay, and visitors to the front desk. The simple hostess (Load Balancer) can't read the packages.

**Key facts:**
- Works at **Layer 7** (application level — it understands HTTP/HTTPS).
- Can route: `/images/*` → image servers, `/api/*` → API servers.
- **WAF** protects your app from common web attacks (SQL injection, XSS).
- Best for **web applications** where intelligent routing is needed.

## 📊 Load Balancer vs. Application Gateway (memorize)

| | Load Balancer | Application Gateway |
|---|---|---|
| Layer | 4 (network) | 7 (web/application) |
| Smart routing by URL/path? | ❌ No | ✅ Yes |
| WAF (firewall for web)? | ❌ No | ✅ Yes |
| Best for | General traffic to VMs | Web apps needing routing + protection |
| Analogy | Restaurant hostess | Controller who reads the packages |

## 🌍 3. DNS (Domain Name System)
**What it is:** The internet's **phonebook** — it translates human-friendly names like `www.example.com` into machine-friendly IP addresses like `20.123.45.6`.

**Real-life analogy:** You don't dial your friend's number from memory; you search their name in your phone's contacts. DNS is that contacts list for the internet.

**Azure DNS (know it exists):**
- **Azure DNS** lets you host your domain names (like `mysite.com`) and manage DNS records in Azure.
- It's fast, secure, and works with Azure services.

## ✅ Day 18 Checklist
- [ ] I can explain Load Balancer vs. Application Gateway with the two analogies
- [ ] I know WAF belongs to Application Gateway
- [ ] I can explain DNS as "the internet's phonebook"

---

# 📅 Day 19 — Connecting Azure to the Outside World: VPN Gateway & ExpressRoute

These two are about **connecting your on-premises network to Azure** securely.

## 🔐 1. VPN Gateway (site-to-site VPN)
**What it does:** Connects your **on-premises (office) network to Azure** over the **public internet, but through an encrypted tunnel** — like a secure private "pipe" inside a public road.

**Real-life analogy:** It's like **sending your valuables in a locked, armored truck through a busy public highway**. The road is public (internet), but your cargo is locked and unreadable (encrypted).

**Key facts:**
- Uses **encryption** so no one can read the data in transit.
- The connection travels over the **public internet** — so it's cheaper but speed depends on internet quality.
- Good for: connecting a branch office to Azure, hybrid scenarios, testing.
- Types: **Site-to-Site** (office to Azure, the main one), **Point-to-Site** (a single user, e.g., working from home, connects via VPN client).

**VPN Gateway analogy recap:** Locked armored truck on public highway 🚚🔒

## 🔌 2. ExpressRoute
**What it does:** A **dedicated, private, physical connection** between your on-premises data center and Azure — entirely **bypassing the public internet**.

**Real-life analogy:** A **private railway line built just for you** — no public highway, no traffic, no other vehicles. It's faster, more reliable, and more secure — but you must build and pay for the line.

**Key facts:**
- Provided with help from **connectivity partners** (telecom providers like Tata Communications, Airtel, etc.).
- Traffic never touches the public internet.
- Higher bandwidth and **lower latency** (faster).
- More expensive and takes longer to set up.
- Good for: large enterprises moving massive data, latency-sensitive workloads, compliance requirements (private connection, no third parties).

## 📊 VPN Gateway vs. ExpressRoute (memorize)

| | VPN Gateway | ExpressRoute |
|---|---|---|
| Path | Over public internet | Private, dedicated connection |
| Encrypted? | ✅ Yes | ✅ Yes (and physically private) |
| Speed | Depends on internet | Higher, consistent |
| Cost | Lower | Higher |
| Setup time | Quick | Weeks (needs provider) |
| Analogy | Locked armored truck on public highway | Private railway line |

## 💡 When to choose which (quick rule)
- **Small/medium, budget-sensitive, quick setup** → VPN Gateway.
- **Big enterprise, huge data, strict performance/compliance** → ExpressRoute.

## ✅ Day 19 Checklist
- [ ] I can explain VPN Gateway (encrypted tunnel over public internet)
- [ ] I can explain ExpressRoute (private dedicated link)
- [ ] I know when to pick each

---

# 📅 Day 20 — Azure Storage: The 5 Types

## 🧠 What is Azure Storage?
**Azure Storage** is Microsoft's cloud storage service — secure, massively scalable storage for files, data, backups, and messages. It's like a **giant, secure warehouse** in the cloud.

**Real-life analogy:** A **fully-managed self-storage facility** — you rent space, move things in/out, and the facility handles security, climate control, and building maintenance.

## 📦 The 5 main storage services (you must know these)

**1. Azure Blob Storage** — for unstructured files
- "Blob" = Binary Large Object — basically any file (images, videos, documents, backups, logs).
- Designed for **massive amounts of unstructured data**.
- **Real-life analogy:** A **giant digital storage room** where you can throw any box (file) — you don't need to organize it in folders.
- Common uses: serving images/videos to websites, backups, storing data for big-data analytics.
- **Exam link:** Blob storage has **hot/cool/cold/archive tiers** — exactly what tomorrow's lesson (Day 21) covers.

**2. Azure Disk Storage** — VM hard drives
- **Disks are used by VMs** — they're the "hard drives" attached to your virtual machines (their C:/ or /dev/sda drive).
- **Real-life analogy:** The **hard drive inside your computer** — it's tied to that machine (your VM).
- Types: **Standard HDD** (cheap, slow), **Premium SSD** (fast, for VMs with heavy I/O), and managed/unmanaged disks (for AZ-900, just know disks = VM drives).

**3. Azure Files** — shared file shares
- Managed **file shares** accessible via the standard SMB protocol (like a network drive).
- Multiple machines can mount the same file share simultaneously (Windows, Linux, macOS).
- **Real-life analogy:** A **shared office network drive** (like a school's shared folder) where many computers access the same files.
- Examples: lift-and-shift of on-premises file servers, shared app settings.

**4. Azure Queue Storage** — message queue
- A **message queue** for decoupling app components: one part of your app puts messages in a queue; another part picks them up and processes them.
- **Real-life analogy:** A **restaurant order ticket rail** — the kitchen puts tickets on the rail, and the waiter picks them up for delivery. The kitchen and the waiter don't have to be in sync.
- Example: processing orders — a web app drops an "order placed" message in a queue; a background worker processes payments.

**5. Azure Table Storage** — NoSQL key-value store
- Stores **structured, non-relational data** (huge amounts of key-value pairs).
- **Real-life analogy:** A **telephone directory** — you look up by a key (name) to get values (number, address). Very fast lookups.
- Example: storing user profiles, IoT device telemetry, metadata.

## 📊 Summary table (memorize)

| Service | What it stores | Analogy |
|---------|----------------|---------|
| **Blob** | Unstructured files (images, videos, backups) | Giant storage room |
| **Disk** | VM hard drives | Drive inside your computer |
| **Files** | Shared file shares (SMB) | Shared office network drive |
| **Queue** | Messages between app parts | Ticket rail at a restaurant |
| **Table** | NoSQL key-value data | Telephone directory |

## ⚠️ Beginner gotcha
**Disk storage ≠ Blob storage.** Disks are attached to VMs like local drives; blobs are standalone files you access over the internet. If a VM dies, its disks are gone with it — but blobs persist independently. (That's why backups go to blob storage!)

## ✅ Day 20 Checklist
- [ ] I can name all 5 storage services and what each stores
- [ ] I can give the analogy for each
- [ ] I can explain the difference between disk and blob storage

---

# 📅 Day 21 — Storage Redundancy & Access Tiers

Today is one of the most exam-heavy topics in the whole AZ-900: **how Azure keeps your data safe (redundancy)** and **how pricing/performance tiers work**.

## 🛡️ Part 1: Redundancy — "How many copies, and where?"

Azure never stores your data once — it always keeps **multiple copies** to protect against failure. The difference is **how many copies and where they live**.

**Real-life analogy:** Compare **saving your important documents**:
- One copy on your laptop → disaster if the laptop dies.
- Copies on your laptop + USB + cloud → safe.

**The 4 redundancy options (memorize this table):**

| Name | Full name | Copies | Where | Protects against |
|------|-----------|:---:|------|------------------|
| **LRS** | Locally Redundant Storage | 3 | Same data center (same zone) | Disk/server failure in that one room |
| **ZRS** | Zone-Redundant Storage | 3 | 3 availability zones in one region | A whole data center/zone failing |
| **GRS** | Geo-Redundant Storage | 6 | 3 in primary region + 3 in a **paired secondary region** | A whole region failing |
| **GZRS** | Geo-Zone-Redundant Storage | 6 | 3 zones in primary + 3 in secondary region | Both zone AND region failures |

**How to read the table:**
- **LRS = cheapest, least protection** (only within one building).
- **ZRS = protects against zone failure** (LRS + zonal spread).
- **GRS = protects against whole-region failure** (LRS + another region).
- **GZRS = maximum protection** (ZRS + another region).
- **Price:** Higher protection = higher cost. GZRS is the most expensive.

> 🧠 **Memory trick:** The letters literally tell the story:
> - **L**RS = **L**ocal (same building)
> - **Z**RS = **Z**one (3 zones)
> - **GR**S = **G**eo-**R**egion (second region)
> - **GZ**RS = **G**eo-**Z**one (zones + second region)
> More magic letters = more copies = more money = more safety.

**Which to choose?**
- **Dev/test, non-critical data** → LRS (cheapest).
- **Production apps needing zone resilience** → ZRS.
- **Critical data needing disaster recovery across regions** → GRS or GZRS.

## 🌡️ Part 2: Access Tiers — "How hot is your data?"

Tiers balance **price vs. speed** based on how often you access data.

**Real-life analogy:** Your **wardrobe**:
- Favourite clothes (worn daily) → hang at arm's reach = **Hot**.
- Seasonal clothes (worn occasionally) → higher shelves = **Cool**.
- Old clothes (rarely used) → attic storage = **Cold/Archive**.

**Azure's tiers (memorize):**

| Tier | Best for | Access speed | Cost |
|------|----------|:---:|------|
| **Hot** | Frequently accessed data (active app data) | Fastest | Highest storage cost (but no retrieval fee) |
| **Cool** | Infrequently accessed (1×/month), stored 30+ days | Fast | Cheaper storage, small retrieval fee |
| **Cold** | Rarely accessed (1×/quarter), stored 90+ days | Slower | Cheaper still |
| **Archive** | Rarely accessed (1×/year), stored 180+ days | Slowest (hours to retrieve) | Cheapest storage; biggest retrieval fee |

**Key understanding:**
- **Hot = expensive to store, cheap/free to read.**
- **Archive = cheap to store, expensive and slow to read.**
- You **pay less to store cold data, but pay when you retrieve it.** That trade-off is the whole point.

> 🧠 **Memory trick:** **Hot = everyday clothes (near you, pricier). Archive = attic boxes (cheapest, but a hassle to fetch).**

**Blob storage + tiers together:**
You can set a **default tier** for your blob storage account (e.g., "Cool") and even **move blobs between tiers** automatically over time as data ages (a feature called *lifecycle management* — just know it exists).

## 📊 Quick recap of today's two big ideas
1. **Redundancy** answers: *"If hardware fails, how many copies of my data survive, and where?"* → LRS → ZRS → GRS → GZRS (increasing protection & cost).
2. **Tiers** answer: *"How quickly do I need my data, and how much am I willing to pay to store it?"* → Hot → Cool → Cold → Archive (decreasing cost & speed).

## ✅ Day 21 Checklist
- [ ] I can write out all 4 redundancy options and what each protects against
- [ ] I can explain the wardrobe/tier analogy
- [ ] I know Archive = cheapest storage but slowest/expensive retrieval

---

# 🏁 Week 3 Review & Self-Test

## 📋 Week 3 Summary Table (memorize)

| Concept | One-line meaning | Analogy |
|---------|------------------|---------|
| Virtual Machine | A computer running in software | Video-game character |
| VM Scale Set | Auto-scaling group of identical VMs | Call center with flexible agents |
| App Service | Managed hosting for web apps/APIs | Fully staffed restaurant kitchen |
| Azure Functions | Event-triggered, pay-per-run code | Vending machine |
| Containers | App + dependencies packaged together | Shipping container |
| VNet | Your private network in Azure | Home Wi-Fi |
| Subnet | Sub-division of a VNet | Separate Wi-Fi for guests |
| VNet peering | Bridge between two VNets | Bridge between two networks |
| Load Balancer | Layer-4 traffic spreader | Restaurant hostess |
| Application Gateway | Layer-7 smart router + WAF | Controller who reads packages |
| DNS | Translates names → IPs | Internet's phonebook |
| VPN Gateway | Encrypted tunnel over public internet | Locked armored truck |
| ExpressRoute | Private dedicated connection to Azure | Private railway line |
| Blob storage | Unstructured files | Giant storage room |
| Disk storage | VM hard drives | Drive inside your PC |
| File storage | Shared network file shares | Shared office drive |
| Queue storage | Messages between app parts | Restaurant ticket rail |
| Table storage | NoSQL key-value data | Telephone directory |
| LRS/ZRS/GRS/GZRS | Redundancy levels (copies & locations) | More backups = safer |
| Hot/Cool/Cold/Archive | Storage tiers (price vs. speed) | Wardrobe shelves |

## 📖 Week 3 Vocabulary (learn these)
1. **VM (Virtual Machine)** — a software-based computer
2. **Hypervisor** — software that creates and runs VMs
3. **Scale set** — auto-scaling group of identical VMs
4. **PaaS** — platform as a service (App Service, Functions)
5. **Serverless** — you don't manage servers; pay per execution
6. **Trigger** — event that starts a function
7. **Container** — packaged app + dependencies
8. **Docker** — tool for building containers
9. **Orchestration** — managing many containers (Kubernetes)
10. **VNet** — virtual private network in Azure
11. **Subnet** — a partition of a VNet
12. **Peering** — connecting two VNets
13. **Load balancer** — spreads traffic across resources
14. **WAF** — web application firewall
15. **VPN** — encrypted tunnel over the internet
16. **ExpressRoute** — private dedicated connection
17. **Blob** — binary large object (unstructured file)
18. **Redundancy** — keeping multiple copies of data
19. **LRS/ZRS/GRS/GZRS** — redundancy levels
20. **Tier** — storage pricing/performance class (hot/cool/cold/archive)

## ✍️ Self-Test (12 questions — try before reading the key)

1. Which would you use to host a website with zero server management: VM or App Service?
2. Which service runs code ONLY when triggered and bills per run?
3. A ___ is to a shipping container what an app is to its dependencies.
4. Name the two ways to connect an on-premises network to Azure.
5. Which is private and dedicated: VPN Gateway or ExpressRoute?
6. Which load balancer can route based on URL path and has WAF?
7. Which storage service stores "hard drives" for VMs?
8. Which storage type is a giant file dump for images/videos/backups?
9. Which redundancy option has copies in a *second region*? LRS / ZRS / GRS / GZRS
10. Which redundancy is cheapest? LRS / ZRS / GRS / GZRS
11. Which storage tier is cheapest to *store* and slowest to retrieve?
12. Which tier is fastest but most expensive to store?

**Answer key:** 1. App Service · 2. Azure Functions · 3. Container · 4. VPN Gateway & ExpressRoute · 5. ExpressRoute · 6. Application Gateway · 7. Disk storage · 8. Blob storage · 9. GRS (and GZRS) · 10. LRS · 11. Archive · 12. Hot

## 🛠️ Hands-On Challenge (Day 23's practice, but you can try now)
1. Create a **Storage Account** (region: Central India).
2. Inside it, create a **Blob container** and upload any small file (even a text file).
3. Click your blob → notice the **"Access tier"** setting (Hot/Cool/Cold/Archive) — set it to Cool, then back to Hot. See how easy it is to change.
4. In the storage account's **"Redundancy"** setting, *see* the options (LRS, GRS, etc.) — don't change it, just observe.
5. **Delete the storage account** when done (or the whole resource group). ✅

---

## 🏁 Week 3 Complete! What's next?
You've now covered the three biggest service families — **Compute, Networking, and Storage**. Remaining big topics: **Databases (Day 22)**, then **Identity, Security & Compliance (Week 4)**, then **Cost & Governance (Week 5)**, then final review (Week 6).

Want me to write the same complete, beginner-style notes for **Day 22–30 (rest of Week 3 + Week 4: databases, identity, security, compliance)** next? 📚
