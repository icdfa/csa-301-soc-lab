# Lab 2: Building Your SOC Home Lab

## Objective
To build a fully functional virtualized Security Operations Center (SOC) home lab environment for hands-on practice. This lab will cover virtualization concepts, network design, OS installation, and initial configuration of key SOC components.

## Topics Covered
*   Virtualization concepts & software (VirtualBox, VMware)
*   Network design for lab environments
*   Virtual machine setup & configuration
*   OS installation (Windows, Linux)
*   Firewall configuration (pfSense)
*   SIEM deployment in lab environment (Splunk Free)
*   Network segmentation in the lab

## Prerequisites
*   A host computer with:
    *   **CPU:** Intel Core i5/AMD Ryzen 5 or better (with virtualization support)
    *   **RAM:** Minimum 16GB (32GB recommended)
    *   **Storage:** 200GB free space (SSD recommended)
    *   **OS:** Windows 10/11, macOS, or Linux
*   Virtualization enabled in BIOS/UEFI (refer to [Lab 1: Environment Preparation](./01-soc-introduction.md) for details).
*   Administrative access to your computer.

## Lab Duration
Approximately 3-4 hours (plus download time).

## Part 1: Hypervisor Installation and Network Configuration

This part ensures your host machine is ready and your virtual network is properly segmented. Refer to [Lab 1: Environment Preparation](./01-soc-introduction.md) for detailed steps on installing VirtualBox and configuring the Host-Only Network (`192.168.56.0/24`).

## Part 2: pfSense Firewall Setup

### Step 1: Download pfSense
1.  Go to [https://www.pfsense.org/download/](https://www.pfsense.org/download/).
2.  Select **Architecture:** `AMD64 (64-bit)`, **Installer:** `DVD Image (ISO) Installer`.
3.  Download the ISO file.

### Step 2: Create pfSense VM
1.  In VirtualBox, click "New".
2.  Configure VM Settings:
    *   **Name:** `pfSense-Firewall`
    *   **Type:** `BSD`, **Version:** `FreeBSD (64-bit)`
    *   **Memory:** `1024 MB (1GB)` RAM
    *   **Hard Disk:** Create a virtual hard disk now, `VDI (VirtualBox Disk Image)`, `Dynamically allocated`, `8 GB`.

### Step 3: Configure pfSense VM Network
1.  Select the `pfSense-Firewall` VM and click **Settings**.
2.  Go to **Network**:
    *   **Adapter 1 (WAN - Internet):**
        *   Enable Network Adapter: ✓
        *   Attached to: `NAT`
    *   **Adapter 2 (LAN - Internal):**
        *   Enable Network Adapter: ✓
        *   Attached to: `Host-only Adapter`
        *   Name: Select your host-only network (e.g., `vboxnet0`).

### Step 4: Install pfSense
1.  Start the `pfSense-Firewall` VM.
2.  Mount the pfSense ISO file (Devices → Optical Drives → Choose disk image).
3.  Follow the on-screen installation steps:
    *   `Accept Copyright` (Press Enter).
    *   `Install pfSense` (Select and Press Enter).
    *   `Keymap Selection` (Select your keyboard layout, e.g., `US`).
    *   `Partitioning`: Select `Auto (UFS)`.
    *   Wait for installation to complete.
    *   `Manual Configuration`: Select `No`.
    *   `Reboot`.
4.  **Important:** Before rebooting, unmount the ISO: `Devices → Optical Drives → Remove disk from virtual drive`.

### Step 5: Configure pfSense Interfaces
After reboot, you'll see the pfSense console menu:
1.  If prompted "Should VLANs be set up now?", type `n` and press Enter.
2.  **Assign Interfaces:**
    *   WAN Interface: Enter `em0` (or the first interface shown).
    *   LAN Interface: Enter `em1` (or the second interface shown).
    *   Additional Interfaces: Press Enter (none).
    *   Confirm: Type `y` and press Enter.
3.  **Set LAN IP Address:**
    *   From the menu, select `2` (Set interface(s) IP address).
    *   Select `2` (LAN).
    *   Enter LAN IP: `192.168.56.1`.
    *   Enter subnet mask: `24`.
    *   Press Enter for no upstream gateway.
    *   Press Enter for no IPv6.
    *   Enable DHCP? Type `n` (we'll use static IPs).
    *   Revert to HTTP as webConfigurator protocol? Type `n`.

### Step 6: Access pfSense Web Interface
1.  From your host computer, open a web browser.
2.  Navigate to: `https://192.168.56.1`.
3.  Accept the security warning (self-signed certificate).
4.  **Login:**
    *   Username: `admin`
    *   Password: `pfsense`
5.  Complete the Setup Wizard:
    *   Change the admin password (crucial for security!).
    *   Ensure "Block RFC1918 Private Networks" is **unchecked** for the WAN interface.

## Part 3: SIEM Deployment (Splunk Free)

### Step 7: Download Ubuntu Server
1.  Go to [https://ubuntu.com/download/server](https://ubuntu.com/download/server).
2.  Download **Ubuntu Server 22.04 LTS ISO**.

### Step 8: Create Splunk VM
1.  In VirtualBox, click "New".
2.  Configure VM:
    *   **Name:** `Splunk-SIEM`
    *   **Type:** `Linux`, **Version:** `Ubuntu (64-bit)`
    *   **Memory:** `4096 MB (4GB)` minimum, `8192 MB (8GB)` recommended.
    *   **Hard Disk:** Create virtual hard disk, `VDI`, `Dynamically allocated`, `50 GB`.
3.  **Network Configuration:**
    *   Settings → Network → Adapter 1
    *   Attached to: `Host-only Adapter`
    *   Name: Select your host-only network.

### Step 9: Install Ubuntu Server
1.  Start the `Splunk-SIEM` VM and mount the Ubuntu ISO.
2.  Follow the installation wizard:
    *   Select language: `English`.
    *   Select `Install Ubuntu Server`.
    *   Keyboard: Select your layout.
    *   Network: Accept DHCP (we'll set static later).
    *   Storage: Use entire disk.
    *   Profile Setup: Your name: `socadmin`, Server name: `splunk-siem`, Username: `socadmin`, Password: `[Choose a strong password]`.
    *   SSH: Install `OpenSSH server` (check the box).
    *   Wait for installation to complete and reboot.

### Step 10: Configure Static IP for Splunk VM
1.  Login to your Ubuntu Server VM with `socadmin` credentials.
2.  Check current IP: `ip addr show`.
3.  Edit netplan configuration:
    ```bash
    sudo nano /etc/netplan/00-installer-config.yaml
    ```
4.  Replace contents with:
    ```yaml
    network:
      version: 2
      ethernets:
        enp0s3:
          addresses:
            - 192.168.56.10/24
          nameservers:
            addresses:
              - 8.8.8.8
              - 1.1.1.1
          routes:
            - to: default
              via: 192.168.56.1
    ```
5.  Apply configuration: `sudo netplan apply`.
6.  Verify: `ip addr show enp0s3` and `ping -c 3 8.8.8.8`.

### Step 11: Install Splunk Enterprise (Free License)
1.  Update system: `sudo apt update && sudo apt upgrade -y`.
2.  Download Splunk Enterprise for Linux (`.deb` package) from [splunk.com/download](https://www.splunk.com/en_us/download/splunk-enterprise.html). You will need to create a free account.
3.  Transfer the `.deb` file to your Ubuntu VM (e.g., using `scp` or shared folders).
4.  Install Splunk:
    ```bash
    sudo dpkg -i splunk-*-linux-2.6-amd64.deb
    ```
5.  Start Splunk and accept the license:
    ```bash
    sudo /opt/splunk/bin/splunk start --accept-license
    ```
6.  Create admin credentials when prompted.
7.  Enable boot start: `sudo /opt/splunk/bin/splunk enable boot-start -user socadmin`.

### Step 12: Access Splunk Web Interface
1.  From your host browser, navigate to: `http://192.168.56.10:8000`.
2.  Login with the `admin` credentials you created.

## Part 4: Setting Up Target Machines for Testing

### Step 13: Create Kali Linux (Attacker) VM
1.  Download the **Kali Linux VirtualBox Image** (pre-built `.ova` file) from [https://www.kali.org/get-kali/](https://www.kali.org/get-kali/).
2.  Import the `.ova` file into VirtualBox.
3.  **VM Settings:**
    *   **Name:** `Kali-Attacker`
    *   **Memory:** `2048 MB`
    *   **Hard Disk:** `40 GB`
4.  **Network:** Change Adapter 1 to `Host-only Adapter` (select your host-only network).
5.  **Static IP:** Once Kali is running, configure its network settings to use a static IP: `192.168.56.20`, Subnet: `255.255.255.0`, Gateway: `192.168.56.1`, DNS: `8.8.8.8`.

### Step 14: Create Windows 10 (Victim) VM
1.  Download a **Windows 10 ISO** from Microsoft's official website (you might need to use the Media Creation Tool on a Windows host, or find a direct ISO download link).
2.  In VirtualBox, click "New".
3.  Configure VM:
    *   **Name:** `Windows10-Victim`
    *   **Type:** `Microsoft Windows`, **Version:** `Windows 10 (64-bit)`
    *   **Memory:** `4096 MB`
    *   **Hard Disk:** `50 GB`.
4.  **Network:** Change Adapter 1 to `Host-only Adapter` (select your host-only network).
5.  **Install Windows 10:** Start the VM, mount the Windows 10 ISO, and follow the installation wizard. You can skip the product key for evaluation purposes.
6.  **Static IP:** After installation, configure network settings for a static IP:
    *   IP: `192.168.56.30`
    *   Subnet: `255.255.255.0`
    *   Gateway: `192.168.56.1`
    *   DNS: `8.8.8.8`

## Part 5: Lab Verification and Documentation

### Step 15: Test Connectivity
From each VM (pfSense, Splunk, Kali, Windows), open a terminal/command prompt and ping the other machines and the internet:
*   `ping 192.168.56.1` (pfSense)
*   `ping 192.168.56.10` (Splunk)
*   `ping 192.168.56.20` (Kali)
*   `ping 192.168.56.30` (Windows)
*   `ping 8.8.8.8` (Internet - should work from pfSense, Splunk, Kali, and Windows if pfSense is configured correctly).

### Step 16: Document Lab Architecture
Create a network diagram (using tools like draw.io or Lucidchart) illustrating your lab setup. Include:
*   All VMs with their assigned IP addresses.
*   Network connections and segmentation.
*   VM specifications (CPU, RAM, Disk).
*   Software versions used.

### Step 17: Take VM Snapshots (CRITICAL)
Once all VMs are installed, configured, and can communicate, shut them down and take a snapshot of each. This allows you to revert to a clean state at any time.

*   For each VM: Right-click → `Snapshots` → `Take`.
*   **Name:** `"Clean Install - [Current Date]"`
*   **Description:** `"Fresh installation, ready for labs"`

## Key Deliverables
*   Fully functional virtual lab environment.
*   Documented lab architecture (network diagram).
*   Operational Splunk SIEM instance.

## Reference Resources
*   **VirtualBox Troubleshooting:** [VirtualBox Forums](https://forums.virtualbox.org/)
*   **pfSense Installation Guide:** [Netgate Docs](https://docs.netgate.com/pfsense/en/latest/install/index.html)
*   **Splunk Installation for Linux:** [Splunk Docs](https://docs.splunk.com/Documentation/Splunk/latest/Installation/InstallonLinux)

## Submission Guidelines
Document your entire setup process. Include screenshots of the pfSense dashboard, Splunk login page, and successful pings between all VMs. Attach your network diagram and submit the full documentation via the portal at [https://icdfa.edu.ng](https://icdfa.edu.ng) for grading.

---
**Next Step:** [Lab 3: Essential Linux & Command Line Skills](./03-linux-cli-skills.md)

Prepared by:
Mr. Aminu Idris
Bsc.Ed, CCNA, CompTIA Security+, CEH, OSCP, CISSP, MPCSEAN
