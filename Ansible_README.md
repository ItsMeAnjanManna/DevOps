# Ansible Interview Prep Guide (with Azure Examples)

## 1. What is Ansible?

**Ansible is an open-source automation tool** that lets you configure servers, deploy applications, and orchestrate IT workflows — all using simple, human-readable YAML files.

Think of it as a **"remote control for your infrastructure."** Instead of logging into 50 servers one by one to run commands, you describe *what you want the end state to be*, and Ansible makes it happen across all of them at once.

**Azure example:** You have 10 Azure VMs running Ubuntu that all need Nginx installed, the same config file, and the firewall opened on port 80. With Ansible, you write it once and run it against all 10.

---

## 2. Why is Ansible called an Agentless tool?

Most configuration tools (like Puppet or Chef) require you to **install a small piece of software (an "agent")** on every server you want to manage. That agent constantly talks back to a central server.

**Ansible doesn't need this.** It has no agent to install, no daemon to run, and no client-side software on the managed machines.

It works by:

- Connecting to the remote machine **on demand** using SSH (Linux) or WinRM (Windows)
- Pushing a temporary piece of Python code (the module) to run the task
- Cleaning up after itself when done

**Azure example:** When you provision a fresh Azure VM from the portal or CLI, it's a blank server. There is no Ansible agent pre-installed, and you don't install one — Ansible just SSHes in and works.

**Why it matters in an interview:** Agentless = less maintenance, less security surface area, and easier to get started. The tradeoff is that it's *push-based* rather than *pull-based*, which we'll cover later.

---

## 3. What problems does Ansible solve?

Ansible solves the **"snowflake server" problem** — the situation where every server is configured slightly differently because someone manually changed something on one of them, and nobody documented it.

Specifically, it solves:

| Problem | How Ansible solves it |
|---|---|
| **Manual, error-prone config** | You declare the desired state in code; Ansible enforces it |
| **Configuration drift** | Playbooks are **idempotent** — running them repeatedly produces the same result |
| **Scalability** | Configure hundreds of servers from one control node, in parallel |
| **Reproducibility** | Your whole environment is defined in code, so you can rebuild it anywhere |
| **Team collaboration** | Playbooks live in Git, get reviewed, versioned, and CI/CD'd |
| **Cross-platform inconsistency** | Same playbook works on Linux, Windows, network gear, cloud APIs |

**Azure example:** Your team has a staging environment in Azure that nobody can reproduce because it was built by hand over months. With Ansible, the entire staging setup — VMs, installed packages, config files, application deployment — is captured in playbooks. You can destroy it and rebuild it identically.

---

## 4. Difference between Ansible and Shell Scripting?

| | Shell Scripting | Ansible |
|---|---|---|
| **Type** | Imperative — you specify *how* to do it step by step | Declarative (mostly) — you specify *what* the end result should be |
| **Idempotency** | Not built-in; you must write checks yourself | Built-in; Ansible checks current state first |
| **Error handling** | Manual; script stops or continues based on your logic | Handles failures gracefully, with retries and handlers |
| **Parallelism** | You have to write your own loops/background jobs | Runs on many hosts in parallel out of the box |
| **Sharing/Reuse** | Hard to reuse logic across scripts | Modules, roles, and collections are reusable |
| **Security** | Secrets often hardcoded | Vault encryption, vaulted variables |
| **Portability** | Depends on shell, distro, command availability | Modules abstract OS differences (mostly) |

**Key interview point:** A shell script is like giving someone a recipe with exact steps ("chop the onion, heat the pan..."). Ansible is like a **contract:** "there must be a chopped onion and a hot pan." If it's already true, Ansible does nothing. This is the **idempotency** difference.

---

## 5. Difference between Ansible and Terraform?

This is one of the most common senior interview questions. The short answer:

> **Terraform provisions infrastructure (the "what hardware/cloud resources exist"). Ansible configures infrastructure (the "what software/runs on those resources").**

| | Terraform | Ansible |
|---|---|---|
| **Primary focus** | Infrastructure **provisioning** — create VMs, networks, storage | Configuration **management** — install software, configure files, deploy apps |
| **Domain** | Cloud APIs (Azure RM, AWS, GCP) | Servers, OS config, apps, plus some provisioning |
| **Language** | HCL (HashiCorp Configuration Language) | YAML |
| **State** | Maintains a **state file** tracking real-world resources | Stateless (no persistent state; checks live systems) |
| **Maturity of the resource** | Declarative; plans and applies | Declarative but executed as ordered tasks |
| **Operational model** | Creates/destroys cloud objects | Logs in and changes the machine |

**Real-world pairing (Azure):** You use Terraform to create an Azure resource group, a virtual network, and 3 VMs. Then you use Ansible to install Docker, deploy your application containers, create users, and set up monitoring on those VMs.

**In the interview, say:** "They're complementary, not competitors. Terraform is about *getting the infrastructure to exist*; Ansible is about *making it behave correctly*. Most mature setups use both — often chained in CI/CD: Terraform provisions, Ansible configures."

---

## 6. What are the advantages of Ansible?

- **Agentless** — nothing to install on managed nodes
- **Simple learning curve** — YAML is human-readable; no programming language required
- **Idempotent** — safe to run repeatedly; converges to desired state
- **Push-based** — you control when changes happen (no pull interval delays)
- **Large module library** — thousands of modules for cloud, OS, network, and apps
- **Parallel execution** — fast across many hosts
- **Secure by default** — uses SSH/WinRM; no open ports except the ones you already need
- **Free & open source** — with an enterprise option (Ansible Automation Platform / Red Hat)
- **Cross-platform** — Linux, Windows, macOS, network devices, cloud APIs

**Azure example:** You can use the `azure_rm_virtualmachine` module directly in a playbook to start/stop Azure VMs, or the `azure_rm_resourcegroup` module to manage resource groups — meaning Ansible isn't just for inside the VM; it can also *drive Azure itself*.

---

## 7. Explain Ansible architecture.

At a high level, the architecture is simple:

```
+-----------------------------------------+
|           CONTROL NODE                  |
|  (your laptop / CI runner / Linux box)  |
|                                         |
|  ansible.cfg -> inventory -> playbook   |
|          |                              |
|          | SSH / WinRM                  |
|          v                              |
|  Python + Modules (pushed temporarily)  |
+-----------------------------------------+
          |        |        |
          v        v        v
    [Managed Node] [Managed Node] [Managed Node]
    (Azure VM)     (Azure VM)     (Azure VM)
```

**Key components:**
- **Control node** — the machine where Ansible runs (any machine with Python; can't be Windows as control node, though you can use WSL)
- **Inventory** — the list of hosts and groups
- **Modules** — the units of work (small programs Ansible runs on the target)
- **Playbooks** — YAML files that orchestrate modules against the inventory
- **Plugins** — extend functionality (connection plugins, filter plugins, etc.)
- **Collections** — packaged bundles of modules, roles, and plugins
- **Facts** — data gathered about managed nodes

**Azure example:** Your control node could be an Azure VM running Ubuntu, or a GitHub Actions runner in Azure DevOps, or your local machine. It connects out to your managed Azure VMs via SSH.

---

## 8. What is the Control Node?

The **control node is the machine from which you run Ansible.** It's the only machine that needs Ansible installed. It holds your playbooks, inventory, and configuration.

Requirements:
- Any machine with Python 3.9+ (Linux/macOS/BSD; Windows works via WSL)
- It's the *source* of all connections — Ansible *pushes* out from here

**Azure example:** You spin up a small Azure Linux VM (say, a B2s) purely as your "jump box" control node, or use your Azure DevOps pipeline agent. From there you run `ansible-playbook deploy.yml` against your application servers.

---

## 9. What are Managed Nodes?

**Managed nodes (also called "hosts" or "targets") are the machines Ansible manages.** These are the servers where tasks actually execute.

- They need **no Ansible installed** (agentless)
- They need SSH (Linux) or WinRM (Windows) access
- They need Python (for most modules; some run without it via raw/script modules)

**Azure example:** Your managed nodes are the Azure VMs (app servers, database servers, web servers) that Ansible configures — like your `web-vm-01`, `db-vm-01`, etc.

---

## 10. How does Ansible communicate with remote servers?

Ansible uses **connection plugins**, the most common being:

- **SSH** — for Linux/Unix managed nodes (default). Uses OpenSSH.
- **WinRM** — for Windows managed nodes
- **local** — runs on the control node itself (no remote connection)
- **docker, kubernetes, aws, etc.** — specialized connection plugins

For SSH specifically:
- Ansible connects over SSH using your credentials (password, or preferred: **SSH keys**)
- It then copies a small Python script (the module) to the remote host
- The module executes, gathers results, and sends output back over the same connection
- Ansible removes the temporary files afterward

**Azure example (senior-level nuance):** In Azure you'd typically either:
- Use SSH key pairs you inject when creating VMs with `azure_rm_virtualmachine` (via `ssh_public_keys`), or
- Use Azure AD-based SSH login, or
- Use an SSH bastion host

You'd never store passwords in plaintext in inventory — you'd use `ansible-vault` or an SSH key.

---

## 11. What is SSH-based automation?

SSH-based automation means **using the SSH protocol as the transport to run commands and copy files on remote machines**, programmatically rather than interactively.

- You write logic (in Ansible's case, modules/playbooks) that connects over SSH
- Every SSH session authenticates securely (keys ideally)
- The remote machine executes the commands and returns output
- This is exactly what Ansible does under the hood for Linux hosts

**Why it matters for Ansible:** Because SSH is already universally available on Linux, Ansible doesn't need its own agent or daemon. Any server you can SSH into, you can automate with Ansible.

**Azure example:** You create Azure VMs with your public key in `~/.ssh/authorized_keys` (or via cloud-init). Ansible connects with the matching private key and configures those VMs — no agent, no extra port beyond 22.

---

## 12. What are Ansible modules?

**Modules are small, self-contained programs that Ansible runs on managed nodes** to perform a specific task. They're the *actual workers* — playbooks just orchestrate them.

Examples:
- `apt` / `yum` / `dnf` — install packages
- `copy` / `template` — manage files
- `service` / `systemd` — manage services
- `command` / `shell` — run arbitrary commands
- `user` — manage users
- `azure_rm_virtualmachine` — manage Azure VMs
- `uri` — make HTTP requests

Each module:
- Takes parameters (e.g., `name: nginx`, `state: started`)
- Is idempotent where possible (checks current state first)
- Returns structured JSON (`changed: true/false`, `rc`, stdout, etc.)

**Azure example:**

```yaml
- name: Ensure web server is running
  azure_rm_virtualmachine:
    resource_group: my-rg
    name: web-vm-01
    started: true
```

---

## 13. What are Ansible collections?

**Collections are the packaging format for distributing Ansible content** — modules, roles, plugins, playbooks, and inventory. They replace the older "roles in galaxy" model and let you share versioned, self-contained bundles.

- Distributed via **Ansible Galaxy** (or private automation hub)
- Typically namespaced: `<namespace>.<collection>` (e.g., `azure.azcollection`, `community.general`, `ansible.posix`)
- Install with `ansible-galaxy collection install azure.azcollection`

**Azure example:** The Azure collection (`azure.azcollection`) is the official collection for Azure modules. You install it once, and then all `azure_rm_*` modules are available to your playbooks.

---

## 14. What is an inventory file?

The **inventory (or "hosts" file) is a list of the managed nodes Ansible knows about**, grouped logically. It can be INI or YAML format.

**INI example:**

```ini
[web]
web-vm-01 ansible_host=20.10.1.5
web-vm-02 ansible_host=20.10.1.6

[db]
db-vm-01 ansible_host=20.10.2.10

[all:vars]
ansible_user=azureuser
ansible_ssh_private_key_file=~/.ssh/azure_key
```

Groups let you target subsets: `ansible -i inventory web -m ping` or run a playbook only on `[web]`.

**Azure example:** Your inventory lists your Azure VM IPs/hostnames, grouped by role (web, db, app). You can also define group vars like SSH user and key path.

---

## 15. Difference between Static and Dynamic Inventory?

| | Static Inventory | Dynamic Inventory |
|---|---|---|
| **What is it** | A hand-written file (INI/YAML) listing hosts | A script/plugin that queries a source (cloud, CMDB, etc.) for hosts |
| **When it's used** | Small, stable environments | Cloud environments where VMs come and go |
| **Updates** | You edit it manually | Auto-updates every time you run Ansible |
| **Maintenance** | Low tech, but manual | No manual editing; always current |
| **Examples** | A text file of 5 Azure VM IPs | A script that calls Azure REST API / `azure_rm` inventory plugin |

**Azure example:** A dynamic inventory plugin queries your Azure subscription and automatically discovers all VMs in a resource group, including their IPs, tags, and resource groups. When you scale out and add a VM, the next Ansible run automatically sees it — no file editing.

```ini
[azure]
plugin: azure.azcollection.azure_rm
auth_source: auto
include_vm_resource_groups:
  - my-rg
conditions:
  - tags.environment == "prod"
```

---

## 16. What is ansible.cfg?

`ansible.cfg` is the **configuration file for Ansible's control node** — it sets defaults for how Ansible behaves.

Common settings:
- `inventory` — default inventory file path
- `remote_user` — default SSH user
- `private_key_file` — default SSH key
- `host_key_checking` — enable/disable host key verification
- `forks` — number of parallel connections
- `roles_path` — where roles are located
- `timeout` — connection timeout
- `ansible_python_interpreter` — Python path on remote hosts

**Search order (senior point):** Ansible looks for config in this order, first match wins:
1. `ANSIBLE_CONFIG` environment variable
2. `ansible.cfg` in the current directory
3. `~/.ansible.cfg` (home)
4. `/etc/ansible/ansible.cfg` (system default)

**Azure example:**

```ini
[defaults]
inventory = ./inventory/azure_rm.yml
remote_user = azureuser
private_key_file = ~/.ssh/azure_key
host_key_checking = False
forks = 20
```

---

## 17. What are ad-hoc commands?

**Ad-hoc commands are one-off Ansible commands** run directly from the CLI, without writing a playbook. They're for quick tasks: checking connectivity, one-off config changes, copying a file.

Syntax: `ansible <pattern> -m <module> -a "<args>"`

**Examples:**

```bash
# Ping all hosts in inventory
ansible all -m ping

# Check disk space on web servers
ansible web -m shell -a "df -h"

# Install nginx on db servers
ansible db -m apt -a "name=nginx state=present" -b

# Restart a service
ansible web -m service -a "name=nginx state=restarted"
```

**Interview tip:** Mention that ad-hoc commands are great for *sanity checks and quick fixes*, but anything reusable or complex should be a playbook. Ad-hoc is not for production-grade repeated work.

---

## 18. What are Ansible Facts?

**Facts are pieces of information Ansible gathers about each managed node** — its OS, IP addresses, memory, CPU, disk, hostname, distribution, etc.

They're stored as variables, typically prefixed with `ansible_`:
- `ansible_hostname`
- `ansible_os_family` (Debian, RedHat, etc.)
- `ansible_distribution`
- `ansible_default_ipv4.address`
- `ansible_memtotal_mb`
- `ansible_fqdn`

**Azure example usage in a playbook:**

```yaml
- name: Show OS info
  debug:
    msg: "Host {{ ansible_hostname }} is running {{ ansible_distribution }} {{ ansible_distribution_version }}"
```

Facts are powerful for writing **portable playbooks** — e.g., "if `ansible_os_family == 'Debian'`, use apt; if RedHat, use yum." They also help in templates: `{{ ansible_default_ipv4.address }}` to configure apps with their own IP.

---

## 19. What is fact gathering?

**Fact gathering is the process Ansible runs at the start of each playbook** (by default) to collect facts from every host in the play's scope.

- Controlled by `gather_facts: yes/no` in the play (default: yes)
- Facts are collected and stored per-host, available to all tasks in the play
- You can see all facts with `ansible hostname -m setup`

**Performance/security nuance (senior point):**
- Fact gathering adds time to every run — disable it (`gather_facts: false`) when you don't need facts
- You can cache facts with a cache plugin (e.g., `jsonfile` or Redis) for faster runs
- On Windows, use `gather_subset` or `setup` module accordingly

**Azure example:** When you run a playbook against 50 Azure VMs, Ansible first SSHes into each to gather facts (OS, IPs, etc.). If you don't need them, you can skip to save 50 × ~1–2s of runtime.

---

## 20. What happens when you run an Ansible playbook?

Here's the step-by-step flow (a solid answer shows you understand the internals):

1. **Read config & inventory** — Ansible loads `ansible.cfg`, parses the inventory (static or dynamic), and builds the host list.

2. **Parse the playbook** — It reads the YAML playbook, resolves variables, and validates syntax.

3. **Connect to hosts** — For each host in the play's scope, Ansible opens an SSH/WinRM connection from the control node (respecting `forks` for parallelism).

4. **Gather facts** (if enabled) — It runs the `setup` module to collect host facts.

5. **Execute tasks in order** — For each task:
   - Ansible evaluates any conditions (`when:`, loops, etc.)
   - It "pushes" the relevant module + args to the host (as a small Python script)
   - The module runs on the remote host
   - The result (JSON: changed/ok/failed, stdout, rc) returns to the control node
   - Ansible records results; if a task fails, it stops (default) or runs `ignore_errors`/handlers as configured

6. **Trigger handlers** — Notifications from tasks trigger handlers (e.g., "restart nginx") at the end of the play, only if a change occurred.

7. **Report summary** — Ansible prints a recap: per-host counts of `ok`, `changed`, `unreachable`, `failed`, `skipped`, `rescued`, `ignored`.

**Azure example:**

```bash
ansible-playbook -i inventory deploy.yml
```

Output recap:

```
PLAY RECAP *************************************************************
web-vm-01 : ok=7 changed=2 unreachable=0 failed=0 skipped=0 rescued=0 ignored=0
web-vm-02 : ok=7 changed=2 unreachable=0 failed=0 skipped=0 rescued=0 ignored=0
```

---

## Quick "cheat sheet" table

| Concept | One-liner |
|---|---|
| Ansible | Agentless automation tool using YAML |
| Agentless | No software installed on managed nodes; uses SSH/WinRM |
| Problems solved | Drift, snowflakes, reproducibility, scalability |
| vs Shell | Declarative + idempotent vs imperative step-by-step |
| vs Terraform | Terraform provisions; Ansible configures |
| Control node | Machine where Ansible runs |
| Managed nodes | Targets Ansible configures |
| Communication | SSH (Linux) / WinRM (Windows), push model |
| Modules | Units of work Ansible pushes to hosts |
| Collections | Packaged bundles of modules/roles/plugins |
| Inventory | List of hosts, grouped |
| Static vs dynamic | Hand-written vs auto-discovered from cloud |
| ansible.cfg | Control node configuration file |
| Ad-hoc | One-off CLI commands without playbooks |
| Facts | Data collected about hosts (OS, IPs, etc.) |
| Fact gathering | Process of collecting facts at play start |
| Running a playbook | Connect → gather facts → run tasks → handlers → recap |

---

**A senior interviewer will probe deeper — be ready for follow-ups like:**
- "How do you handle secrets in Ansible?" → `ansible-vault`, or Azure Key Vault lookup plugins
- "How do you make playbooks idempotent?" → use state-aware modules (`state: present`), avoid raw `shell`/`command` where possible
- "How do you handle rollback?" → pre/post tasks, snapshots (Azure VM snapshots), or Blue-Green via Terraform + Ansible
- "How do you integrate with CI/CD?" → run Ansible from Azure DevOps pipelines or GitHub Actions

Want me to run a mock interview on any of these follow-up topics, or generate a sample playbook with Azure modules to study?
