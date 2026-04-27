# Lab 1: Environment Preparation

## Objective
The goal of this lab is to prepare your host machine for virtualization and configure the virtual networking required for your SOC lab.

## Prerequisites
*   **Hardware:** Minimum 16GB RAM, 4-core CPU, 200GB SSD space.
*   **BIOS/UEFI:** Virtualization (VT-x/AMD-V) must be enabled.

## Step 1: Install VirtualBox
1.  Download **VirtualBox** from [virtualbox.org](https://www.virtualbox.org/).
2.  Download the **VirtualBox Extension Pack**.
3.  Install VirtualBox following the default prompts.
4.  Open VirtualBox, go to `File > Tools > Extension Pack Manager`, and install the downloaded Extension Pack.

## Step 2: Configure Host-Only Networking
This network will allow your VMs to communicate with each other and your host, but remain isolated from your physical home network.

1.  Go to `File > Tools > Network Manager`.
2.  Click **Create** to add a new Host-only Network (usually named `vboxnet0` or `VirtualBox Host-Only Ethernet Adapter`).
3.  **Configure Adapter:**
    *   IPv4 Address: `192.168.56.1`
    *   IPv4 Network Mask: `255.255.255.0`
4.  **Configure DHCP Server:**
    *   **Uncheck** "Enable Server". We will use static IPs for all lab components to ensure consistency.

## Step 3: Verify Virtualization
If you encounter errors when starting a 64-bit VM, ensure virtualization is enabled in your BIOS:
*   **Intel:** Enable "Intel Virtualization Technology" or "VT-x".
*   **AMD:** Enable "SVM Mode".

---
**Next Step:** [Lab 2: Firewall Deployment](./02-pfsense-setup.md)
