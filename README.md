# CSA-301: SOC Fundamentals & Home Lab Setup

Welcome to the **CSA-301: SOC Fundamentals & Home Lab Setup** course repository. This repository is designed to guide students through the process of building a professional Security Operations Center (SOC) home lab from scratch.

## Course Overview

In this course, you will learn the core concepts of Security Operations and gain hands-on experience by building your own virtualized SOC environment. This lab will serve as your primary platform for threat detection, incident response, and security monitoring exercises.

## Lab Components

The lab architecture consists of the following key components:

| Component | Technology | Role |
| :--- | :--- | :--- |
| **Hypervisor** | VirtualBox / VMware | Virtualization Platform |
| **Firewall** | pfSense | Network Gateway & Security |
| **SIEM** | Splunk Enterprise | Centralized Log Management & Analysis |
| **Attacker** | Kali Linux | Offensive Security Testing |
| **Victim** | Windows 10 / Ubuntu | Target Systems for Monitoring |

## Repository Structure

*   `docs/`: Detailed documentation and lab guides.
    *   `labs/`: Step-by-step instructions for each lab module.
*   `diagrams/`: Network architecture and flow diagrams.
*   `scripts/`: Automation scripts for lab setup and configuration.

## Getting Started

To begin your journey, follow the step-by-step guides in the `docs/labs/` directory:

1.  **[Lab 1: Environment Preparation](./docs/labs/01-environment-prep.md)** - Setting up your hypervisor and virtual networking.
2.  **[Lab 2: Firewall Deployment](./docs/labs/02-pfsense-setup.md)** - Installing and configuring pfSense.
3.  **[Lab 3: SIEM Installation](./docs/labs/03-splunk-setup.md)** - Deploying Splunk on Ubuntu Server.
4.  **[Lab 4: Endpoint Integration](./docs/labs/04-endpoint-setup.md)** - Setting up Kali and Windows victim machines.

## Safety Warning

> [!IMPORTANT]
> All lab activities must be conducted within the isolated virtual network. Never run malware or perform offensive actions on your host machine or any network you do not have explicit permission to test.

## Reference Resources & Support

If you encounter issues during the lab setup, please refer to the following official documentation and community resources:

*   **VirtualBox Documentation:** [https://www.virtualbox.org/wiki/Documentation](https://www.virtualbox.org/wiki/Documentation)
*   **pfSense Documentation:** [https://docs.netgate.com/pfsense/en/latest/](https://docs.netgate.com/pfsense/en/latest/)
*   **Splunk Documentation:** [https://docs.splunk.com/Documentation](https://docs.splunk.com/Documentation)
*   **Ubuntu Server Guide:** [https://ubuntu.com/server/docs](https://ubuntu.com/server/docs)
*   **MITRE ATT&CK Resources:** [https://attack.mitre.org/resources/](https://attack.mitre.org/resources/)
*   **ICDFA Support Portal:** [https://icdfa.edu.ng](https://icdfa.edu.ng)

## Submission Instructions

Once you have completed each lab, you must submit your documentation for grading:

1.  **Documentation:** Prepare a comprehensive PDF or Word document detailing the steps you took.
2.  **Screenshots:** Include clear screenshots of key milestones (e.g., successful installations, network pings, SIEM dashboards).
3.  **Submission:** Upload the full documentation package to the student portal at [https://icdfa.edu.ng](https://icdfa.edu.ng) for grading.

## License

Prepared by:
Mr. Aminu Idris
Bsc.Ed, CCNA, CompTIA Security+, CEH, OSCP, CISSP, MPCSEAN

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
