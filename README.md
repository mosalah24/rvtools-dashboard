# 🖥️ RVTools VMware Infrastructure Dashboard

A fully client-side, single-file HTML dashboard that transforms raw **RVTools CSV exports** into a rich, interactive VMware infrastructure analysis and planning tool. No server, no backend, no installation — open the file in any browser and drop your CSVs in.

**Live demo:** [mosalah24.github.io/rvtools-dashboard](https://mosalah24.github.io/rvtools-dashboard)

---

## ✨ What It Does

RVTools exports data across dozens of CSV files that are hard to analyse manually. This dashboard loads all of them at once, cross-references the data, and surfaces actionable intelligence across **27 tabs in 6 sections** — from basic inventory to capacity planning, compliance auditing, and VM placement recommendations.

---

## 🚀 Quick Start

1. Go to the [live dashboard](https://mosalah24.github.io/rvtools-dashboard) **or** download `index.html` and open it locally in any modern browser
2. In RVTools, go to **File → Export All to CSV** and save the folder
3. Click **＋ Load Files** in the top bar and select all CSV files at once
4. Everything populates instantly — no page reload required

> **Tip:** Load all files together in one go for full cross-tab analysis. The more files you load, the richer the insights.

---

## 🔍 Global Search

Press **`⌘K`** (Mac) or **`Ctrl+K`** (Windows) from anywhere to focus the search bar instantly.

Search across **all data simultaneously** — VMs, ESXi hosts, datastores, snapshots, vHealth alerts, and network adapters. Results are grouped by category with match highlighting, contextual sub-text (CPU%, free space, power state), and full keyboard navigation:

- `↑` / `↓` — move through results
- `Enter` — jump to that entity's tab
- `Esc` — close and clear

---

## 📁 Supported RVTools Files

| File | Used For |
|------|----------|
| `tabvInfo.csv` | VM inventory, CBT, hardware version, power state |
| `tabvHost.csv` | ESXi host specs, CPU/RAM, uptime, certificates, NTP |
| `tabvDatastore.csv` | Capacity, free space, provisioned space, overcommit |
| `tabvDisk.csv` | Thin/thick provisioning, disk paths, VM→DS mapping |
| `tabvNetwork.csv` | NIC adapter types, VLANs, IP addresses |
| `tabvSnapshot.csv` | Snapshot age and size |
| `tabvTools.csv` | VMware Tools status and version |
| `tabvHealth.csv` | vHealth alerts, zombie VMDKs and VMX files |
| `tabvMemory.csv` | Memory balloon/swap data |
| `tabvCPU.csv` | CPU topology |

---

## 📊 Dashboard Tabs

### Overview
| Tab | Description |
|-----|-------------|
| ⬛ **Dashboard** | Environment summary — VM count, host count, resource ratios, top alerts |
| 🔲 **Clusters** | Per-cluster breakdown with overcommit ratios and host counts |
| 🖥️ **ESXi Hosts** | Full host inventory with CPU, RAM, version, and VM load |
| 📋 **VM Inventory** | Searchable, filterable VM table with all key attributes |

### Recommendations
| Tab | Description |
|-----|-------------|
| 💡 **CPU & Memory** | VMs with high vCPU counts or memory pressure warnings |
| 📸 **Snapshots** | Snapshot age, size, and deletion priority |
| 💾 **Storage** | Provisioned vs used, zombie VMDKs, storage waste |
| 📅 **End of Support** | OS and VMware product EOL tracking |

### Infrastructure
| Tab | Description |
|-----|-------------|
| 🗄️ **Datastores** | Capacity, fill rates, accessibility, thin overcommit |
| 🌐 **VM Networks** | NIC adapter types, VLAN distribution, legacy adapter detection |
| 🏥 **vHealth Alerts** | Zombie files grouped by datastore with DS free space context; all other vHealth alerts |
| 📊 **Host Performance** | Per-host CPU%, memory%, VM density, ESXi version status |
| 🔧 **VMware Tools** | Tools status, version currency, CBT state, upgrade candidates |

### Intelligence
| Tab | Description |
|-----|-------------|
| 📑 **Executive Summary** | KPI cards, top risk findings, VLAN distribution — ready for management |
| 🛡️ **Backup Readiness** | Per-VM backup score based on CBT, Tools, snapshots, and NIC type |
| ⚡ **Performance Advisor** | Per-VM performance analysis across 6 rules with fix guides and effort estimates |

### Compliance
| Tab | Description |
|-----|-------------|
| 🛡️ **ESXi Compliance** | ESXi version (6.x/7.x/8.x), host uptime, certificate expiry countdown, NTP status |
| ✅ **VM Compliance Audit** | Per-VM compliance score across 6 rules with one-click filters |
| ⚖️ **Datastore Balance** | Specific storage vMotion recommendations to rebalance critical datastores |

### Planning
| Tab | Description |
|-----|-------------|
| 🗺️ **VM → Datastore Map** | Which VMs live on which datastores, with critical DS flagging |
| 💿 **Disk Audit** | Thin vs thick provisioning, disk modes, controller types |
| 📈 **Capacity Planning** | CPU/RAM runway per cluster, datastore fill projections, VM growth rate |
| 🎛️ **What-If Simulator** | Sliders to model adding VMs — see real-time CPU, RAM and storage impact |
| 💥 **Host Failure Impact** | N-1 / N-2 HA survivability analysis per cluster with verdict badges |
| ♻️ **Reclamation ROI** | Quantified CPU, RAM and storage recoverable from specific remediation actions |
| 🌊 **Thin Overcommit Risk** | Overcommit ratio per datastore, phantom space totals, write-storm risk scoring |
| 🎯 **VM Placement Advisor** | Enter new VM specs → ranked host recommendations with scoring breakdown |

---

## ⚡ VM Performance Advisor

Every powered-on VM is analysed across 6 performance rules. Click any rule card to instantly filter the VM table. A fix guide at the bottom explains *why each issue hurts performance* and *exactly how to resolve it* with effort estimates.

| Rule | Severity | What It Checks |
|------|----------|----------------|
| High vCPU > 8 | 🔴 HIGH | Causes CPU ready time — scheduler waits for simultaneous free cores |
| Legacy NIC (E1000/E1000e) | 🔴 HIGH | Software-emulated NICs burn host vCPU per packet; VMXNET3 is paravirtualised |
| Old HW Version < 14 | 🔴 HIGH | Missing CPU hot-remove, higher memory limits, and performance bug fixes |
| VMware Tools issue | 🟡 MEDIUM | Balloon driver unavailable, guest metrics broken, timekeeping drift |
| Thick Disk | 🟡 MEDIUM | Pre-allocates storage on creation; convert to thin via storage vMotion |
| Active Snapshot | 🟡 MEDIUM | Delta chain grows over time, adding read latency — delete if not needed |

---

## ✅ VM Compliance Audit

Each powered-on VM is scored 0–100 across 6 rules. An overall compliance percentage tracks environment health over time. Six filter buttons isolate failing VMs per rule instantly.

| Rule | Weight | What It Checks |
|------|--------|----------------|
| VMware Tools OK | 20 | Tools installed, running, and current |
| CBT Enabled | 20 | Changed Block Tracking active for backup consistency |
| No Legacy NIC | 15 | No E1000 / E1000e / PCNet32 adapters |
| No Old Snapshots | 15 | No snapshots older than 30 days |
| HW Version ≥ 14 | 15 | Hardware version supports modern features |
| Thin Provisioned | 15 | All disks using thin provisioning |

---

## 🎯 VM Placement Advisor

Enter your new VM's requirements and the advisor:

- **Scores every ESXi host** out of 100 using weighted criteria — RAM headroom, CPU ratio after placement, current load, VM density, and ESXi version
- **Filters out ineligible hosts** automatically — insufficient RAM, CPU ratio would exceed 8:1, host >97% memory, or in maintenance mode — with the specific reason shown for each
- **Displays top 3 hosts** as ranked medal cards (🥇🥈🥉) with live after-placement RAM and CPU progress bars and a score breakdown by factor
- **Recommends the best datastore** for each top candidate based on free space
- **Adjusts scoring weights by workload type** — Balanced, CPU Intensive, Memory Intensive, or Storage Intensive

---

## 🛡️ ESXi Compliance Tracker

Tracks every ESXi host across version currency, uptime, certificate expiry, and NTP status:

- **ESXi 6.x** — flagged 🔴 End of Life (no security patches)
- **ESXi 7.x** — flagged ⚠️ approaching end of general support
- **ESXi 8.x** — ✅ current generation
- Hosts with **uptime > 365 days** flagged for maintenance reboot scheduling
- Certificate expiry countdown — warns at < 90 days and < 365 days

---

## ⚖️ Datastore Balance Advisor

Analyses free space across all datastores and generates a prioritised list of specific **storage vMotion operations** — exactly which VM to move from which critical datastore to which target, showing free space before and after each move. Moves are simulated in sequence so targets don't get overfilled by the recommendations themselves.

---

## 🏥 vHealth Zombie File Analysis

Zombie VMDKs and VM config files are grouped by datastore with:

- Count of VMDKs vs other file types (VMX, VMTX) per datastore
- Datastore capacity, free space, and fill percentage
- **Urgency to Clean** rating — cross-references zombie count with datastore criticality
- Full individual file list with file type badges and datastore free % inline

> **Note:** RVTools cannot report individual zombie file sizes because orphaned files are not attached to any VM and therefore not captured in tabvDisk. Use the vCenter Datastore Browser or `du` from an ESXi shell to find actual sizes.

---

## 🛠️ Technical Details

| Property | Value |
|----------|-------|
| Architecture | Single HTML file, fully client-side |
| Dependencies | Chart.js (CDN) — no build step, no npm, no server |
| Browser support | Chrome, Firefox, Edge, Safari (modern versions) |
| Data privacy | All processing happens in your browser — no data sent anywhere |
| File size | ~230 KB |
| Network required | Only to load Chart.js from CDN on first use |

---

## 📂 Repository Structure

```
/
├── index.html      # The entire dashboard — one self-contained file
└── README.md       # This file
```

---

## 🔄 Updating With New Data

Reload the page and drop in fresh CSV exports. The dashboard has no persistent state — every load is a clean analysis of your current environment snapshot.

---

## 🤝 Contributing

Issues and pull requests welcome. The entire application lives in `index.html`. Search for `// ──` comment banners in the JavaScript section to find the rendering function for each tab.

---

## 📄 License

MIT — free to use, modify, and distribute.

---

*Built to make VMware infrastructure analysis fast, visual, and actionable — without requiring vCenter access, additional tooling, or a backend.*
