# DNS Sinkhole Deployment & Custom DHCP Infrastructure Routing

## Project Overview
This project documents the installation, deployment, and network orchestration of a network-wide Pi-hole utility. 
Because the host environment utilizes a locked-down ISP gateway router with zero native capabilities for modifying custom DNS parameters, 
a custom DHCP Isolation / Starvation architecture was engineered to force all local area network traffic through the server's ad-blocking and privacy filtering engine.

---

## Phase 1: Environment Preparation & Installation

Before deploying the blocking framework, the headless Debian environment package repositories were synchronized and core dependencies updated to establish a secure application baseline.

1. **System Hardening Update:**
    sudo apt update && sudo apt upgrade -y

2. **Automated Pipeline Deployment:**
   The automated, verified network installation script was retrieved and piped directly into the system terminal interpreter:
    git clone --depth 1 https://github.com/pi-hole/pi-hole.git Pi-hole
    cd "Pi-hole/automated install/"
    sudo bash basic-install.sh

---

## Phase 2: Bypassing ISP Firmware Constraints via DHCP Starvation

### The Engineering Challenge
The deployment network is managed by a primary consumer gateway router with restricted firmware. The device lacks settings to change the default DNS servers distributed to clients, and the built-in DHCP server cannot be disabled entirely.

### The Architectural Workaround
To circumvent these hardware restrictions without replacing the gateway, a DHCP Starvation strategy was implemented:
* The primary router's active DHCP pool range was tightly constrained down to a size of one single address slot (covering only *.1 and *.2).
* The Raspberry Pi was permanently assigned to the *.2 address slot, effectively starving the router of any remaining addresses to hand out.
* The Pi-hole application framework was then configured to act as the primary, authoritative DHCP server for the rest of the local network topology, distributing addresses from *.3 through *.254.

### Infrastructure Mapping Baseline
* Gateway Router IP: *.1 (e.g., x.x.x.1)
* Raspberry Pi IP: *.2 (e.g., x.x.x.2) [Static/Only Router Client]
* Active Pi-hole DHCP Pool Range: *.3 through *.254

---

## Phase 3: Activating the Pi-hole DHCP Engine

With the router's scope successfully locked down, the centralized infrastructure services were enabled via the administration control panel.

1. Authenticated into the administrative dashboard interface by navigating a browser to: http://x.x/admin
2. Traversed the sidebar menu to Settings, and selected the DHCP tab.
3. Enabled the checkbox labeled "DHCP server enabled".
4. Defined the From and To ip address boundary inputs matching the isolated topology range (*.3 to *.254).
5. Input the primary Gateway Router IP address (*.1) into the Router fields to maintain physical internet transit.
6. Committed the configuration settings by clicking Save.

---

## Phase 4: Network Client Migration & Verification

To complete the network migration, connected household clients must drop their legacy lease data profiles and authenticate against the Pi-hole's active DHCP coordinator.

### Workstation Lease Renewal (Windows Terminal)
    ipconfig /release
    ipconfig /renew

### IoT & Mobile Device Migration
To migrate smartphones, smart home utilities, and media devices, network interfaces were cycled via temporary Airplane Mode toggles or local hardware restarts.

### Active DNS Filtering Verification
To verify that local client queries are cleanly routing through the security layer, execute an internal infrastructure query:
    nslookup pi.hole

A successful deployment returns the local IP address of the Pi server (*.2), validating that network tracking and advertisement blocking are actively enforced at the packet level.
