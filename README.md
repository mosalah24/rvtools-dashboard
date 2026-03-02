# 🖥️ RVTools VMware Infrastructure Dashboard

A fully client-side, single-file HTML dashboard that transforms raw **RVTools CSV exports** into a rich, interactive VMware infrastructure analysis tool. No server, no backend, no installation — just open the file in a browser and drop your CSVs in.

**Live demo:** [mosalah24.github.io/rvtools-dashboard](https://mosalah24.github.io/rvtools-dashboard)

---

## ✨ What It Does

RVTools exports data across dozens of CSV files that are difficult to analyse manually. This dashboard loads all of them at once, cross-references the data, and surfaces actionable intelligence across 28 tabs organised into 6 sections.

---

## 🚀 Quick Start

1. Go to the [live dashboard](https://mosalah24.github.io/rvtools-dashboard) **or** download `index.html` and open it locally in any modern browser
2. In RVTools, go to **File → Export All to CSV** and save the folder
3. Click **📂 Load CSV Files** in the dashboard and select all the CSV files at once
4. Everything populates instantly — no page reload required

> **Tip:** Load all files together in one go for full cross-tab analysis. The more files you load, the richer the insights.

---

## 📁 Supported RVTools Files

| File | Used For |
|------|----------|
| `tabvInfo.csv` | VM inventory, CBT, hardware version, creation dates |
| `tabvHost.csv` | ESXi host specs, CPU/RAM, uptime, certificates |
| `tabvDatastore.csv` | Capacity, free space, provisioned space |
| `tabvDisk.csv` | Thin/thick provisioning, disk controllers, VM→DS mapping |
| `tabvNetwork.csv` | NIC adapters, VLANs, IP addresses |
| `tabvSnapshot.csv` | Snapshot age and size |
| `tabvTools.csv` | VMware Tools status and version |
| `tabvHealth.csv` | vHealth alerts, zombie VMDKs |
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
| 🗄️ **Datastores** | Capacity, fill rates, accessibility status |
| 🌐 **VM Networks** | NIC types, VLAN distribution, adapter inventory |
| 🏥 **vHealth Alerts** | All vHealth warnings grouped by type and severity |
| 📊 **Host Performance** | Per-host CPU%, memory%, VM density |
| 🔧 **VMware Tools** | Tools status, version currency, upgrade candidates |

### Intelligence
| Tab | Description |
|-----|-------------|
| 📑 **Executive Summary** | KPI cards, top risk findings, VLAN distribution — ready for management |
| 🛡️ **Backup Readiness** | Per-VM backup score based on CBT, Tools, snapshots, NIC type |
| 🗑️ **VM Sprawl** | Orphan/zombie VM candidates scored by inactivity signals |
| 📆 **VM Age Analysis** | Creation timeline, hardware version distribution, oldest VMs |

### Compliance
| Tab | Description |
|-----|-------------|
| 🛡️ **ESXi Compliance** | ESXi version (6.x/7.x/8.x), uptime, certificate expiry, NTP status per host |
| ✅ **VM Compliance Audit** | Per-VM compliance score across 6 rules with filter buttons |
| ⚖️ **Datastore Balance** | Specific storage vMotion recommendations to rebalance critical datastores |

### Planning
| Tab | Description |
|-----|-------------|
| 🗺️ **VM → Datastore Map** | Which VMs are on which datastores, flagging VMs on critical ones |
| 💿 **Disk Audit** | LSI Logic vs Paravirtual SCSI, thin vs thick provisioning breakdown |
| 📈 **Capacity Planning** | CPU/RAM runway per cluster, datastore fill projections, VM growth timeline |
| 🎛️ **What-If Simulator** | Drag sliders to add VMs and see real-time impact on CPU, RAM and storage |
| 💥 **Host Failure Impact** | N-1 / N-2 HA analysis — what happens to each cluster if hosts fail |
| ♻️ **Reclamation ROI** | Quantified CPU, RAM and storage recoverable from remediation actions |
| 🌊 **Thin Overcommit Risk** | Overcommit ratio per datastore, phantom space, write-storm risk |
| 🎯 **VM Placement Advisor** | Enter new VM specs → get ranked host recommendations with scoring breakdown |

---

## 🎯 VM Placement Advisor

The most interactive feature. Enter your new VM's requirements and the advisor:

- **Scores every ESXi host** out of 100 using weighted criteria (RAM headroom, CPU ratio, current load, VM density, ESXi version)
- **Filters out ineligible hosts** automatically (insufficient RAM, CPU ratio would exceed 8:1, host >97% memory, maintenance mode) with reasons shown
- **Displays top 3 hosts** as ranked cards with live after-placement RAM and CPU bars
- **Recommends the best datastore** for each top candidate
- **Adjusts weights by workload type** — CPU Intensive, Memory Intensive, Storage Intensive, or Balanced

---

## ✅ VM Compliance Rules

Each powered-on VM is scored 0–100 across 6 rules:

| Rule | Weight | What It Checks |
|------|--------|----------------|
| VMware Tools OK | 20 | Tools installed, running, and current |
| CBT Enabled | 20 | Changed Block Tracking active for backup |
| No Legacy NIC | 15 | No E1000 / E1000e / PCNet32 adapters |
| No Old Snapshots | 15 | No snapshots older than 30 days |
| HW Version ≥ 14 | 15 | Hardware version supports modern features |
| Thin Provisioned | 15 | All disks using thin provisioning |

---

## 💡 Key Findings From Real Data

When connected to a real environment this dashboard surfaces issues like:

- Hosts with **>2 years uptime** without a reboot
- Datastores at **<10% free** with projected fill dates
- VMs with **snapshots aged 400+ days** degrading disk I/O daily
- Clusters that **cannot survive a single host failure** (N-1 RAM ratio >1:1)
- **Phantom storage** — space promised to VMs that doesn't physically exist
- Powered-off VMs holding **hundreds of TiB** of provisioned storage

---

## 🛠️ Technical Details

| Property | Value |
|----------|-------|
| Architecture | Single HTML file, fully client-side |
| Dependencies | Chart.js (CDN), no build step required |
| Browser support | Chrome, Firefox, Edge, Safari (modern versions) |
| Data privacy | All processing happens in your browser — no data leaves your machine |
| File size | ~200 KB |
| Network required | Only to load Chart.js from CDN on first use |

---

## 📂 Repository Structure

```
/
├── index.html          # The entire dashboard — one file
└── README.md           # This file
```

---

## 🔄 Updating With New Data

Just reload the page and drop in fresh CSV exports. The dashboard has no persistent state — every load is a clean analysis of your current environment.

---

## 🤝 Contributing

Issues and pull requests welcome. The entire application is self-contained in `index.html` — search for the JavaScript section starting at `<script>` to find the rendering functions for each tab.

---

## 📄 License

MIT — free to use, modify, and distribute.

---

*Built to make VMware infrastructure analysis fast, visual, and actionable without requiring vCenter access or additional tooling.*
