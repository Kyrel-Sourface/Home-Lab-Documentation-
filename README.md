# Enterprise Homelab: Headless Debian Provisioning & DNS Sinkhole Deployment

## Project Overview
This repository documents the architecture and engineering lifecycle of a headless Debian Linux server deployed on local infrastructure. The node is configured to operate as a high-availability network-wide DNS sinkhole (Pi-hole) and core DHCP coordinator, mitigating tracking and advertising vectors at the packet layer.

### Core Engineering Milestones
* **Headless Remote Administration Framework:** Engineered an isolated terminal pipeline via SSH alongside an independent TightVNC visual desktop environment executing on an X11 graphics manager fallback layer to mitigate default display manager connection loops.
* **DHCP Starvation & Traffic Redirection:** Designed a custom network migration strategy to bypass locked ISP gateway firmware constraints. By executing a DHCP starvation model (restricting the primary router to a pool size of 1), all local network traffic was safely routed through the server's ad-blocking DNS engine.

## Technical Documentation Index
For full technical deployment logs, step-by-step terminal execution, and networking maps, see the dedicated engineering files:

1. [Phase 1: Headless OS Provisioning & Secure Remote Access](docs/headless-setup.md)
2. [Phase 2: Pi-hole Deployment & Advanced DHCP Infrastructure Routing](docs/pihole.md)
3. [OptiPlex 7060 Proxmox VE Bare-Metal Setup](docs/optiplex-7060-server-setup.md)

Post-Deployment Maintenance
​Immediately after establishing the stable headless connection, system packages were updated to ensure security and stability: sudo apt update && sudo apt upgrade -y
