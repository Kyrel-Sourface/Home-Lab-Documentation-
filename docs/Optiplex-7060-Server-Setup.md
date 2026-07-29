# Dell OptiPlex 7060 Proxmox VE Server Setup

Documentation covering hardware deployment, hypervisor installation, display bug resolution, and host-level optimizations.

---

### Core IT Skills Demonstrated
* **Hypervisor Management:** Proxmox VE installation, node configuration, and LXC container lifecycle.
* **Networking:** IPv4 static allocation, DHCP pool management, and subnet isolation.
* **Linux Systems Administration:** Package management, headless terminal operation, and hardware troubleshooting.

---

## Hardware & Hypervisor Overview

* **Host Machine:** Refurbished Dell OptiPlex 7060 SFF
* **Operating System:** Proxmox VE (Bare-Metal)
* **Primary Role:** Home Lab Virtualization & Container Host

---

## Step-by-Step Server Installation

### 1. Bare-Metal Proxmox VE Install
* Installed Proxmox VE directly onto the OptiPlex 7060 hardware.
* **Display Output Troubleshooting:** Resolved a DisplayPort hardware signaling issue during initial setup to complete the bare-metal installation.
* **Static IP Assignment:** Configured a dedicated static IP for the host strictly outside the active DHCP pool (and isolated from the Pi-hole host machine) to ensure uninterrupted management access.

### 2. Post-Install Hypervisor Optimizations
* Executed the Proxmox VE Helper-Scripts (Community Post-Install Script) to streamline host maintenance:
  * Disabled non-subscription GUI prompts.
  * Configured the `pve-no-subscription` repository streams.
  * Updated system packages and CPU microcode across the host.

---

## Host Status & Verification
- [x] Host Web UI reachable via static IP
- [x] Enterprise repository notices disabled
- [x] System updates applied via `pve-no-subscription`
