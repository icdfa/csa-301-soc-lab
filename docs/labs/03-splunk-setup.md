# Lab 3: SIEM Installation (Splunk)

## Objective
Deploy Splunk Enterprise on an Ubuntu Server to act as the central brain for log analysis and security monitoring.

## Step 1: Prepare Ubuntu Server
1.  Download **Ubuntu Server 22.04 LTS** ISO.
2.  Create a VM: `Splunk-SIEM`, 4GB RAM (8GB recommended), 50GB Disk.
3.  **Network:** Attached to `Host-only Adapter`.
4.  Install Ubuntu Server with default settings. Use `socadmin` as the username.

## Step 2: Configure Static IP
Edit the netplan configuration:
```bash
sudo nano /etc/netplan/00-installer-config.yaml
```
Apply the following settings:
```yaml
network:
  version: 2
  ethernets:
    enp0s3:
      addresses: [192.168.56.10/24]
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]
      routes:
        - to: default
          via: 192.168.56.1
```
Apply changes: `sudo netplan apply`.

## Step 3: Install Splunk
1.  Update the system: `sudo apt update && sudo apt upgrade -y`.
2.  Download Splunk (you may need to use `wget` with a link from the Splunk website or transfer the `.deb` package).
3.  Install the package:
    ```bash
    sudo dpkg -i splunk-xxxx-linux-2.6-amd64.deb
    ```
4.  Start Splunk and accept the license:
    ```bash
    sudo /opt/splunk/bin/splunk start --accept-license
    ```
5.  Enable boot start: `sudo /opt/splunk/bin/splunk enable boot-start`.

## Step 4: Access Splunk Web
1.  From your host browser, go to `http://192.168.56.10:8000`.
2.  Login with the credentials you created during installation.

---
**Next Step:** [Lab 4: Endpoint Integration](./04-endpoint-setup.md)
