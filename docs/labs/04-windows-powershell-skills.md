# Lab 4: Essential Windows & PowerShell Skills

## Objective
Develop proficiency in Windows security tools and PowerShell scripting for security analysis, event log management, and threat hunting in a Windows environment.

## Topics Covered
*   Windows event logs & Event Viewer
*   Windows security event types
*   PowerShell fundamentals & scripting
*   PowerShell for security analysis
*   Sysmon installation & configuration
*   Windows Registry & security implications
*   Windows process & service management
*   PowerShell remoting & automation

## Prerequisites
*   A functional Windows 10 VM (`Windows10-Victim` from Lab 2).
*   Administrative access to the Windows VM.

## Activities

### Activity 1: Windows Event Log Analysis

On your Windows 10 VM:

1.  **Explore Event Viewer:** Open Event Viewer (`eventvwr.msc`) and navigate through `Windows Logs` (Application, Security, Setup, System, Forwarded Events).
2.  **Identify Key Security Events:** Focus on the `Security` log. Identify and understand common security event IDs, such as:
    *   `4624`: Successful Logon
    *   `4625`: Failed Logon
    *   `4634`: Logoff
    *   `4720`: A user account was created
    *   `4722`: A user account was enabled
    *   `4732`: A security-enabled local group was changed
3.  **Filter and Search:** Use Event Viewer's filtering capabilities to find specific events (e.g., all failed login attempts, events from a specific source).
4.  **Export Logs:** Export a filtered security log to a `.evtx` file and a `.csv` file.

### Activity 2: PowerShell Fundamentals for Security

Open PowerShell as Administrator on your Windows 10 VM and perform the following:

1.  **Basic Commands:** Use `Get-Help`, `Get-Command`, `Get-Service`, `Get-Process`, `Get-Item` to explore system information.
2.  **Object Pipelining:** Understand how to pipe objects (`|`) between cmdlets (e.g., `Get-Service | Where-Object {$_.Status -eq 'Running'}`).
3.  **Variables and Loops:** Create simple scripts using variables and loops (e.g., a script to list all services and their status).
4.  **Remote Execution (Optional):** If you have another Windows VM, explore `Invoke-Command` for basic remote execution (ensure WinRM is configured).

### Activity 3: Sysmon Installation & Configuration

Sysmon (System Monitor) is a Windows system service and device driver that, once installed on a system, remains resident across system reboots to monitor and log system activity to the Windows event log. It provides detailed information about process creations, network connections, and changes to file creation time.

1.  **Download Sysmon:** Download the latest Sysmon from Microsoft Sysinternals ([https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)).
2.  **Download a Configuration File:** Obtain a well-regarded Sysmon configuration file (e.g., SwiftOnSecurity's Sysmon config from GitHub: [https://github.com/SwiftOnSecurity/Sysmon-config](https://github.com/SwiftOnSecurity/Sysmon-config)). Save it as `sysmonconfig.xml`.
3.  **Install Sysmon with Configuration:** Open an elevated PowerShell prompt and run:
    ```powershell
    .\Sysmon64.exe -i sysmonconfig.xml
    ```
4.  **Verify Sysmon Events:** After installation, generate some activity (e.g., open a browser, run `notepad.exe`). Then, open Event Viewer and check `Applications and Services Logs > Microsoft > Windows > Sysmon > Operational` for new events.

### Activity 4: PowerShell Scripting for Threat Hunting

Write PowerShell scripts to automate the following security tasks:

1.  **Failed Logon Reporter:** A script that queries the Security Event Log for failed logon attempts (`Event ID 4625`), extracts the username and source IP, and outputs them to a CSV file.
2.  **Suspicious Process Detector:** A script that lists all running processes, checks their digital signatures, and flags any unsigned processes or processes running from unusual locations.
3.  **Sysmon Event Analyzer:** A script that filters Sysmon events (e.g., `Event ID 1: Process Creation`, `Event ID 3: Network Connection`) to identify suspicious activities based on your `sysmonconfig.xml`.
4.  **Registry Change Monitor (Basic):** A script that monitors a specific registry key for changes (e.g., `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run`) and logs any modifications.

**Deliverable:** Submit your PowerShell scripts with comments explaining their functionality.

## Key Deliverables
*   Proficiency with Windows security tools (Event Viewer, Sysmon).
*   PowerShell scripts for automation and threat hunting.
*   Understanding of Windows security events and their significance.

## Reference Resources
*   **Microsoft Sysmon Documentation:** [Sysmon Docs](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)
*   **PowerShell Scripting Guide:** [Microsoft PowerShell Docs](https://learn.microsoft.com/en-us/powershell/scripting/overview)
*   **Ultimate IT Professional’s Guide to Windows Event Forwarding:** [LogRhythm Guide](https://logrhythm.com/blog/windows-event-forwarding-guide/)

## Submission Guidelines
Submit your PowerShell scripts and screenshots of your Sysmon configuration and Event Viewer logs. Ensure all scripts are well-commented. Submit the full documentation via the portal at [https://icdfa.edu.ng](https://icdfa.edu.ng) for grading.

---
**End of Unit 1 Labs.**

Prepared by:
Mr. Aminu Idris
Bsc.Ed, CCNA, CompTIA Security+, CEH, OSCP, CISSP, MPCSEAN
