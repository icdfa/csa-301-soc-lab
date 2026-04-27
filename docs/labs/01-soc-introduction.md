# Lab 1: Introduction to SOC Operations

## Objective
This lab introduces fundamental Security Operations Center (SOC) concepts, including organizational structures, roles, and key frameworks used for threat analysis. You will gain an understanding of the threat landscape and learn to apply frameworks like the Cyber Kill Chain and MITRE ATT&CK to analyze cyber attacks.

## Topics Covered
*   SOC models & organizational structures
*   SOC roles (Tier 1, 2, 3)
*   SOC processes & workflows
*   Threat landscape & threat actors
*   Cyber Kill Chain framework
*   MITRE ATT&CK framework & tactics/techniques
*   Alert triage & escalation procedures

## Activities

### Activity 1: Research & Documentation - Analyzing a Recent Cyber Attack

Choose a recent, publicly documented cyber attack (e.g., a major ransomware incident, a supply chain attack, or a data breach). Research the attack details from credible cybersecurity news outlets, threat intelligence reports, and official advisories.

**Deliverable:** A short report (2-3 pages) documenting your findings, including:

1.  **Attack Overview:** Briefly describe the incident, including the target, attacker, and impact.
2.  **Threat Actor Profile:** If identifiable, describe the likely threat actor(s) and their motivations.
3.  **Cyber Kill Chain Analysis:** Map the attack stages to the Cyber Kill Chain phases (Reconnaissance, Weaponization, Delivery, Exploitation, Installation, Command & Control, Actions on Objectives).
4.  **MITRE ATT&CK Mapping:** Identify specific MITRE ATT&CK tactics and techniques used by the adversary during the attack. Provide a table mapping the observed techniques to their corresponding ATT&CK IDs.

    | Tactic | Technique ID | Technique Name | Description in Attack |
    | :--- | :--- | :--- | :--- |
    | Initial Access | Txxxx | Example Technique | Adversary gained access via... |
    | ... | ... | ... | ... |

5.  **SOC Response Considerations:** Based on the attack, suggest how a SOC might detect, analyze, and respond to similar incidents, considering alert triage and escalation procedures.

### Activity 2: Interactive Mapping of Attack Techniques

Using the MITRE ATT&CK Navigator (available at [https://attack.mitre.org/navigator/](https://attack.mitre.org/navigator/)), create a layer that highlights the techniques identified in your Activity 1 report. Export this layer as a JSON file.

**Deliverable:** The exported MITRE ATT&CK Navigator JSON file.

## Key Deliverables
*   Documented analysis of a real-world attack (report from Activity 1).
*   MITRE ATT&CK Navigator JSON file (from Activity 2).

## Reference Resources
*   **MITRE ATT&CK Framework:** [https://attack.mitre.org/](https://attack.mitre.org/)
*   **Cyber Kill Chain:** [Lockheed Martin Cyber Kill Chain](https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html)
*   **BleepingComputer (Cyber News):** [https://www.bleepingcomputer.com/](https://www.bleepingcomputer.com/)

## Submission Guidelines
Upon completion, compile your report and JSON file into a single documentation package. Include screenshots of your ATT&CK Navigator layer. Submit the final documentation via the portal at [https://icdfa.edu.ng](https://icdfa.edu.ng) for grading.

---
**Next Step:** [Lab 2: Building Your SOC Home Lab](./02-home-lab-setup.md)

Prepared by:
Mr. Aminu Idris
Bsc.Ed, CCNA, CompTIA Security+, CEH, OSCP, CISSP, MPCSEAN
