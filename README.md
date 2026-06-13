# Home-Lab-Documentation-
A journey of my home lab projects. 


# Raspberry Pi Configuration: Transitioning to a Headless System

## 📋 Project Overview
This project documents the process of taking a Raspberry Pi running a standard Linux OS desktop setup and configuring it to run entirely **headless** (without a monitor, keyboard, or mouse). All ongoing management is now handled via remote network access.

* **Operating System:** Debian Linux / Raspberry Pi OS
* **Remote Management:** SSH (Terminal) & VNC (Remote Desktop)

---

## 🛠️ Configuration Workflow

### Step 1: Initial Setup with Peripherals
Before making the system headless, the Pi was initially hooked up like a traditional desktop computer to verify the OS and configure core settings:
* Connected a monitor, keyboard, and mouse.
* Flashed and booted into the Linux OS desktop environment.
* Successfully connected to the local Wi-Fi network.

### Step 2: Enabling Remote Access Settings
While still using the monitor and peripherals, the necessary background services were enabled to allow for future remote management:
1. Opened the terminal and launched the system configuration tool:
   ```bash
   sudo raspi-config

​Navigated to Interface Options.
​Enabled SSH for secure command-line access.
​Enabled VNC Server for remote graphical desktop access.
​Rebooted the system to ensure the services started automatically on boot.

​Step 3: Identifying the Network IP
​Before disconnecting the hardware, the Pi's local IP address was retrieved so it could be targeted from another computer on the network: hostname -I

Step 4: Going Headless
​With all remote services active and the IP address noted, the peripherals were completely disconnected: 
Unplugged the monitor, keyboard, and mouse.
Relocated the Pi to its permanent headless spot on the network.
Verified remote command-line access from a main workstation via SSH: ssh username@your-pi-ip-address
Verified remote desktop access by connecting a VNC Viewer client to the same IP address.

Post-Deployment Maintenance
​Immediately after establishing the stable headless connection, system packages were updated to ensure security and stability: sudo apt update && sudo apt upgrade -y
