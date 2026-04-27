# Lab 2: Firewall Deployment (pfSense)

## Objective
Install and configure pfSense to act as the gateway and firewall for your SOC lab.

## Step 1: Download pfSense
1.  Visit [pfsense.org/download](https://www.pfsense.org/download/).
2.  Select **Architecture:** `AMD64`, **Installer:** `DVD Image (ISO)`.
3.  Download and extract the GZ file to get the `.iso` image.

## Step 2: Create the pfSense VM
1.  **Name:** `pfSense-Firewall`
2.  **Type:** `BSD`, **Version:** `FreeBSD (64-bit)`
3.  **RAM:** `1024 MB`
4.  **Disk:** `8 GB (VDI, Dynamically Allocated)`
5.  **Network Configuration (CRITICAL):**
    *   **Adapter 1:** Attached to `NAT` (This provides internet access to the lab).
    *   **Adapter 2:** Attached to `Host-only Adapter` (Select the network created in Lab 1).

## Step 3: Installation
1.  Start the VM and select the pfSense ISO.
2.  Follow the prompts: `Accept > Install > Auto (UFS)`.
3.  Once finished, **remove the ISO** and reboot.

## Step 4: Interface Configuration
In the pfSense console:
1.  **Assign Interfaces:**
    *   WAN -> `em0` (NAT)
    *   LAN -> `em1` (Host-only)
2.  **Set LAN IP:**
    *   Select Option `2`.
    *   Set LAN IP to `192.168.56.1`.
    *   Subnet Mask: `24`.
    *   DHCP: `No`.

## Step 5: Web GUI Setup
1.  From your host machine, browse to `https://192.168.56.1`.
2.  Default login: `admin` / `pfsense`.
3.  Follow the wizard, change the admin password, and ensure "Block RFC1918 Private Networks" is **unchecked** for the WAN interface (since our WAN is technically a private NAT network).

---
**Next Step:** [Lab 3: SIEM Installation](./03-splunk-setup.md)
