Absolutely, Rui — here’s a clean, modular `README.md` template tailored for your **VCF-LAB** GitHub repository. It documents your ESXi 8.0.3 USB install workflow, IP schema, and Kickstart automation.

---

## 📘 VCF-LAB: Automated ESXi 8.0.3 Deployment

This repository contains tools, scripts, and configuration files to automate the deployment of VMware ESXi 8.0.3 in a modular lab environment using a USB install stick powered by rEFInd and Kickstart.

---

### 🧭 Lab Overview

- **Hosts**: MN-A2-1, MN-A2-2, MN-A2-3
- **Management VLAN**: 10
- **IP Schema**:
  | Host     | IP Address       | Hostname     |
  |----------|------------------|--------------|
  | MN-A2-1  | 192.168.10.101   | mn-a2-1.lab  |
  | MN-A2-2  | 192.168.10.102   | mn-a2-2.lab  |
  | MN-A2-3  | 192.168.10.103   | mn-a2-3.lab  |

---

### 🛠 USB Install Stick Structure

```
USB/
├── efi/
│   └── boot/
│       └── bootx64.efi       ← rEFInd bootloader
├── ks/
│   ├── host1.cfg             ← Kickstart for MN-A2-1
│   ├── host2.cfg             ← Kickstart for MN-A2-2
│   └── host3.cfg             ← Kickstart for MN-A2-3
└── esxi/
    ├── boot.cfg              ← ESXi installer config
    └── mboot.c32             ← ESXi bootloader
```

---

### ⚙️ Kickstart Features

- Static IP assignment per host
- VLAN tagging for management
- Automated install to 1 TB NVMe
- VMFS datastore creation (`Tier0-DS`)
- Optional partition reserved for memory tiering

---

### 📦 Folder Guide

- `kickstart/` → Host-specific Kickstart files
- `refind/` → Boot menu configuration
- `esxi/` → ESXi installer files and bootloader

---

### 🧯 Disaster Recovery

- Backup Kickstart and rEFInd configs to `./lab-backups/`
- Register CRS309 and MN-A2 serials with supplier
- Export ESXi host configs post-deploy:
  ```bash
  vim-cmd hostsvc/firmware/backup_config
  ```
