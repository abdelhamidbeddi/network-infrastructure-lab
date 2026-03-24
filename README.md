[README.md](https://github.com/user-attachments/files/26179508/README.md)
# 🖧 Network Infrastructure Lab — Full IT Infrastructure Home Lab

> **Abdelhamid Beddi** — IT Systems & Networks Technician (TSSR)
> 📍 Lille, France | 🌍 Open to new opportunities
> 📧 abhbd59@gmail.com | 🔗 www.linkedin.com/in/abdelhamid-beddi



---

## 📌 Project Overview

This project is a **complete simulation of a professional IT infrastructure**, built entirely as a **personal home lab** to develop and demonstrate hands-on skills in systems administration, network engineering, virtualisation, and security.

The goal was to replicate the kind of infrastructure found in real organisations — covering user management, network security, monitoring, helpdesk tooling, and automated workstation deployment — all running on a single machine using virtualisation.

All components were deployed on **VMware Workstation** using virtual machines, covering both Windows Server and Linux environments.

**Duration:** October 2025 → November 2025  
**Context:** Personal home lab | Solo project

---

## 🏗️ Infrastructure Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                      VMware Workstation                      │
│                                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │
│  │  Windows     │  │  Windows     │  │  Windows Server  │  │
│  │  Server 2019 │  │  Server 2019 │  │  2019 (Storage)  │  │
│  │  (Primary DC)│  │ (Secondary   │  │  SMB / Backup    │  │
│  │  AD, DHCP,   │  │  DC Replica) │  │  NTFS Shares     │  │
│  │  DNS         │  │              │  │                  │  │
│  └──────────────┘  └──────────────┘  └──────────────────┘  │
│                                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │
│  │  Debian 12   │  │Ubuntu 22.04  │  │  Ubuntu 22.04    │  │
│  │  FOG Server  │  │  GLPI        │  │  Zabbix          │  │
│  │  PXE / Image │  │  ITSM / CMDB │  │  Monitoring      │  │
│  │  Deployment  │  │  Ticketing   │  │  & Alerting      │  │
│  └──────────────┘  └──────────────┘  └──────────────────┘  │
│                                                             │
│  ┌──────────────┐  ┌──────────────────────────────────────┐ │
│  │  pfSense     │  │       3x Client VMs (Windows 10)     │ │
│  │  Firewall    │  │       Domain-joined after FOG deploy  │ │
│  │  Squid, VPN  │  │                                      │ │
│  └──────────────┘  └──────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘

Network segmentation simulated in Cisco Packet Tracer (VLANs)
```

---

## ✅ Skills & Technologies Covered

| Domain | Technologies |
|---|---|
| **Virtualisation** | VMware Workstation, Snapshots, VM lifecycle |
| **Windows Server** | Active Directory, DHCP, DNS, GPO, AD DS replication |
| **Storage & Backup** | Windows Server Backup, NTFS permissions, SMB shares |
| **Linux Administration** | Debian 12, Ubuntu Server 22.04, CLI, service management |
| **Monitoring** | Zabbix (agents, dashboards, alerting) |
| **ITSM / Asset Management** | GLPI (inventory, ticketing, Apache + PHP + MariaDB stack) |
| **Image Deployment** | FOG Project, PXE boot, DHCP options 66/67, iPXE |
| **Network & Security** | pfSense, Squid proxy, WireGuard VPN, IP addressing plan |
| **Network Simulation** | Cisco Packet Tracer, VLAN segmentation |
| **Scripting** | PowerShell (automated AD user creation) |

---

## 📂 Project Modules

### 🪟 Module 1 — Active Directory Domain (Windows Server 2019)

**Goal:** Centralise user, group, and computer management across the infrastructure.

**What was done:**
- Installed and promoted Windows Server 2019 as a **Primary Domain Controller** (AD DS)
- Configured **DNS** and **DHCP** on the same server
- Deployed a **secondary DC** for replication and fault tolerance
- Structured **Organisational Units (OUs)** by department
- Deployed **Group Policy Objects (GPOs)** to enforce access rights and desktop policies
- Configured **centralised authentication** for all client workstations
- Wrote a **PowerShell script** to automate bulk user account creation

**Resources allocated:**
- Primary DC: 4 vCPU / 8 GB RAM
- Secondary DC: 2 vCPU / 4 GB RAM

---

### 🐧 Module 2 — Linux Services Administration

**Goal:** Deploy and manage three specialised Linux servers, each with a dedicated role.

#### FOG Project Server (Debian 12)
- 4 vCPU / 8 GB RAM / **500 GB storage**
- Configured as PXE boot server (DHCP options 66 & 67 with `ipxe.efi`)
- Captured a reference Windows 10 image and deployed it to multiple client VMs

#### GLPI Server (Ubuntu Server 22.04 LTS)
- 2 vCPU / 4 GB RAM / 50 GB storage
- Stack: **Apache + PHP 8.2 + MariaDB**
- Used for IT asset inventory, hardware tracking, and incident ticketing

#### Zabbix Server (Ubuntu Server 22.04 LTS)
- 4 vCPU / 8 GB RAM / 100+ GB storage
- Monitored all servers, services, and network consumption
- Configured alerts triggered on threshold breaches

---

### 🔒 Module 3 — Secure Network Architecture

**Goal:** Build a structured, secure IP network with firewall, proxy, and VPN.

**IP Addressing Plan:**
- All servers (Windows, Linux, pfSense): **static IP addresses**
- Client workstations: **dynamic IPs via Windows Server DHCP**

**pfSense Firewall VM:**
- 2 vCPU / 2 GB RAM / 32 GB SSD
- WAN + LAN interfaces
- **Squid** installed for web proxy and content filtering
- **WireGuard** configured for secure remote VPN access

**VLAN Segmentation (Cisco Packet Tracer):**
- Simulated logical network separation across multiple departments
- Topology designed to mirror a real enterprise network layout

---

### 💾 Module 4 — Centralised Storage & Backup

**Goal:** Ensure data protection and business continuity across the infrastructure.

- Deployed a dedicated **Windows Server 2019 storage server** (4 vCPU / 8 GB RAM / 500 GB)
- Created **secured SMB network shares** with NTFS permissions tied to AD groups
- Configured **automated scheduled backups** using Windows Server Backup + Task Scheduler
- Performed **manual restore tests** to validate recovery procedures

---

### 🖥️ Module 5 — Automated Workstation Deployment (FOG + PXE)

**Goal:** Standardise and automate OS deployment across all client machines.

- Captured a master Windows 10 image including pre-installed standard software
- Deployed the image to multiple VMs via PXE boot over the network
- Client VMs automatically **joined the Active Directory domain** post-deployment
- Integrated with existing IP infrastructure and simulated VLANs

---

### ☁️ Module 6 — Virtualisation Management (VMware)

**Summary of the full virtual environment:**

| VM | OS | Role | vCPU | RAM | Disk |
|---|---|---|---|---|---|
| win-dc01 | Windows Server 2019 | Primary DC / DHCP / DNS | 4 | 8 GB | 100 GB |
| win-dc02 | Windows Server 2019 | Secondary DC (replica) | 2 | 4 GB | 60 GB |
| win-storage | Windows Server 2019 | File server / Backup | 4 | 8 GB | 500 GB |
| fog-server | Debian 12 | FOG / PXE deployment | 4 | 8 GB | 500 GB |
| glpi-server | Ubuntu 22.04 LTS | GLPI ITSM | 2 | 4 GB | 50 GB |
| zabbix-server | Ubuntu 22.04 LTS | Zabbix monitoring | 4 | 8 GB | 100 GB |
| pfsense | pfSense | Firewall / Proxy / VPN | 2 | 2 GB | 32 GB |
| client-01/02/03 | Windows 10 | Domain workstations | 2 | 4 GB | 60 GB |

**Practices applied:**
- Snapshots taken before every critical change
- Manual backup and restore validation
- Resource allocation optimised per service role

---

## 🎯 Key Takeaways

This personal project gave me hands-on experience across the full stack of a real IT department:

- Designing and deploying a **multi-server Windows domain** from scratch
- Administering **Linux servers** via CLI and web interfaces
- Implementing **network security** with a real firewall, proxy, and VPN
- Setting up **monitoring** and **ITSM** tools used in production environments
- Automating repetitive tasks (user creation, OS deployment, backups)
- Understanding **virtualisation** as the backbone of modern infrastructure

---

## 📬 Contact

Feel free to reach out if you'd like to discuss this project or my profile:

- 📧 abhbd59@gmail.com
- 🔗 www.linkedin.com/in/abdelhamid-beddi
- 📍 Based in Lille, France — Available for opportunities in **Ireland** 🇮🇪
