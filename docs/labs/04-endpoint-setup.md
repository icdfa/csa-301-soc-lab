# Lab 4: Endpoint Integration

## Objective
Set up the offensive (Kali Linux) and defensive (Windows 10) endpoints to complete your SOC lab environment.

## Step 1: Kali Linux (Attacker)
1.  Download the **Kali Linux VirtualBox Image** from [kali.org](https://www.kali.org/get-kali/).
2.  Import the `.ova` file into VirtualBox.
3.  **Network:** Change the adapter to `Host-only Adapter`.
4.  **Static IP:** Set the IP to `192.168.56.20` in the Kali network settings.

## Step 2: Windows 10 (Victim)
1.  Download a **Windows 10 ISO** or a **Windows 10 Development VM** from Microsoft.
2.  Create/Import the VM.
3.  **Network:** Set to `Host-only Adapter`.
4.  **Static IP:**
    *   IP: `192.168.56.30`
    *   Subnet: `255.255.255.0`
    *   Gateway: `192.168.56.1`
    *   DNS: `8.8.8.8`

## Step 3: Connectivity Test
From each machine, try to ping the others:
*   `ping 192.168.56.1` (Firewall)
*   `ping 192.168.56.10` (Splunk)
*   `ping 192.168.56.20` (Kali)
*   `ping 192.168.56.30` (Windows)

## Step 4: Snapshot (CRITICAL)
Once everything is working, shut down all VMs and take a **Snapshot** named "Baseline - Lab Complete". This allows you to revert to a clean state if you break something during future exercises.

---
**Congratulations!** You have successfully built your CSA-301 SOC Home Lab.
