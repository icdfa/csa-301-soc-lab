# Lab 3: Essential Linux & Command Line Skills

## Objective
Develop proficiency in essential Linux command-line tools and Bash scripting for security analysis, log parsing, and automation within a SOC environment.

## Topics Covered
*   Linux file system hierarchy
*   File permissions & ownership
*   User & group management
*   Command-line tools for security analysis (`grep`, `awk`, `sed`, `cut`, `sort`, `uniq`)
*   Bash scripting fundamentals
*   Regular expressions for log analysis
*   Log file parsing & analysis
*   System administration commands

## Prerequisites
*   A functional Linux VM (e.g., the `Splunk-SIEM` Ubuntu Server or `Kali-Attacker` VM from Lab 2).
*   Basic familiarity with Linux concepts.

## Activities

### Activity 1: Linux Command-Line Fundamentals

Perform the following tasks on your Linux VM:

1.  **File System Navigation:** Use `ls`, `cd`, `pwd`, `find` to navigate and locate files.
2.  **File Operations:** Use `cat`, `less`, `head`, `tail`, `cp`, `mv`, `rm`, `mkdir`, `rmdir` to view and manipulate files and directories.
3.  **Permissions:** Use `chmod`, `chown` to modify file permissions and ownership. Explain the meaning of `rwx` and octal permissions.
4.  **User & Group Management:** Use `useradd`, `usermod`, `userdel`, `groupadd`, `groupdel` to create, modify, and delete users and groups. (Perform these carefully in a lab environment).
5.  **Process Management:** Use `ps`, `top`, `kill` to monitor and manage running processes.

### Activity 2: Log Analysis with Command-Line Tools

Using sample log files (you can generate some or use existing system logs like `/var/log/auth.log` or `/var/log/syslog`), perform the following:

1.  **`grep` for Keywords:** Search for specific keywords (e.g., "failed password", "error", "authentication") in log files.
2.  **`awk` for Field Extraction:** Extract specific fields from structured log entries (e.g., IP addresses, usernames, timestamps).
3.  **`sed` for Text Manipulation:** Replace or delete specific patterns in log files.
4.  **`cut` for Column Selection:** Extract specific columns from delimited log data.
5.  **`sort` and `uniq` for Aggregation:** Sort log entries and count unique occurrences of events.
6.  **Combine Tools:** Chain multiple commands using pipes (`|`) to perform complex log analysis tasks (e.g., `cat syslog | grep 
 'failed' | awk '{print $11}' | sort | uniq -c | sort -nr`).

### Activity 3: Bash Scripting for SOC Tasks

Write Bash scripts to automate the following:

1.  **Log Archiver:** A script that compresses and archives log files older than 7 days to a specified directory.
2.  **Failed Login Detector:** A script that monitors `/var/log/auth.log` for failed login attempts and reports the source IP and username.
3.  **Process Monitor:** A script that lists all running processes, filters for suspicious ones (e.g., unknown users, high CPU usage), and outputs to a file.

**Deliverable:** Submit your Bash scripts with comments explaining their functionality.

## Key Deliverables
*   Proficiency with Linux command-line tools for security analysis.
*   Bash scripts for log parsing and automation.
*   Understanding of Linux security concepts.

## Reference Resources
*   **Linux Command Library:** [https://linuxcommandlibrary.com/](https://linuxcommandlibrary.com/)
*   **Bash Scripting Guide:** [TLDP Advanced Bash-Scripting Guide](https://tldp.org/LDP/abs/html/)
*   **Regex101 (Regex Testing):** [https://regex101.com/](https://regex101.com/)

## Submission Guidelines
Submit your Bash scripts as separate files or within your documentation. Include screenshots of your scripts in action and the results of your log analysis exercises. Submit the full documentation via the portal at [https://icdfa.edu.ng](https://icdfa.edu.ng) for grading.

---
**Next Step:** [Lab 4: Essential Windows & PowerShell Skills](./04-windows-powershell-skills.md)

Prepared by:
Mr. Aminu Idris
Bsc.Ed, CCNA, CompTIA Security+, CEH, OSCP, CISSP, MPCSEAN
