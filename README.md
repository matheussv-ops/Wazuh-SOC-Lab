# Wazuh SOC Home Lab: Deployment and Threat Detection

## Project Overview
This project demonstrates the end-to-end deployment of a **Wazuh SIEM/XDR** ecosystem. It covers the infrastructure setup, remote management, agent enrollment, real-time threat detection, and forensic log analysis, simulating a professional Security Operations Center (SOC) environment.

---

## Phase 1: Operating System Deployment
To host the Wazuh SIEM, I deployed an **Ubuntu Server 24.04 LTS** instance. This environment was configured with 8GB of RAM and 50GB of storage to ensure high performance during log analysis. The network was set to **Bridge Mode** to allow seamless communication between the server and monitored endpoints.

![OS Deployment](img/phase1.png)

## Phase 2: Establishing Secure Remote Management (SSH)
To streamline the deployment and management of the Wazuh server, I established a remote connection from my Windows host to the Ubuntu VM using the **SSH protocol via PowerShell**. This setup confirms network reachability and allows for more efficient command execution and system monitoring.
* **Tool:** Windows Terminal / PowerShell (SSH Client)
* **Target:** matheus-soc@192.168.0.22
* **Port:** 22 (Default SSH)

![SSH Connection](img/phase2.png)

## Phase 3: Automated Deployment of Wazuh SIEM/XDR
Following the successful validation of the Ubuntu Server environment, I initiated the deployment of the **Wazuh ecosystem (v4.9.2)**. To ensure precision and system integrity, the centralized installation assistant was utilized via a remote SSH connection. 

Key technical milestones:
* **Hardware Resource Validation:** Verified that VM resources met the requirements for real-time log indexing.
* **Security Architecture:** Automated generation of a Root Certificate Authority (CA) and specific node certificates for full encryption.

![Automated Installation](img/phase3.png)

## Phase 4: Successful Provisioning and Service Validation
The automated installation script concluded successfully, marking the completion of the SIEM server infrastructure. All core components (Indexer, Manager, and Dashboard) were provisioned and initialized without errors.

![Service Validation](img/phase4.png)

## Phase 5: Web Interface Integration and Initial Telemetry
I accessed the **Wazuh Dashboard** via HTTPS using the server's local IP (192.168.0.22). This stage confirms the proper integration between the Indexer and the Dashboard UI. Upon initial login, the system already recorded **21 security events** related to internal server processes.

![Dashboard Overview](img/phase5.png)

## Phase 6: Agent Enrollment Configuration
To begin active monitoring, I initiated the agent enrollment process through the Wazuh Dashboard. I configured a **Windows MSI** package for the local host, assigning the server address and naming the agent **'My-Windows'**.

![Agent Enrollment](img/phase6.png)

## Phase 7: Successful Agent Synchronization and Visibility
This stage marks the establishment of active monitoring. The Wazuh Manager is now receiving real-time telemetry from the Windows 11 Pro endpoint, confirming that the communication channel is secure and operational.

![Active Agent Status](img/phase7.png)

## Phase 8: Threat Detection and Event Correlation Analysis
The SIEM triggered alerts for suspicious activity on the 'My-Windows' endpoint. The dashboard recorded **3 Authentication Failure** events, which were automatically mapped to the **MITRE ATT&CK Framework** (Tactic: Account Access).

![Threat Detection Dashboard](img/phase9.png)

## Phase 9: Deep Log Analysis and Forensic Investigation
Moving from general detection to digital forensics, I analyzed the raw event data to understand the nature of the security breach. This granular view allows for a precise identification of the threat actor's tactics.

**Technical Forensic Evidence:**
* **Targeted Identity:** The log identifies a logon attempt using the username **'usuario_falso'**, confirming an unauthorized credential testing activity.
* **Windows Event Correlation:** The system successfully captured **Event ID 4625**, the standard Windows telemetry for failed logon attempts.
* **Logon Type Analysis:** The record shows **Logon Type 3**, indicating a remote network-based attempt rather than a local physical access, which is consistent with external scanning or brute-force patterns.
* **Error Code Diagnostics:** The failure status **0xc000006d** specifically points to an invalid username or authentication process failure, providing the necessary evidence to initiate an incident response protocol.

![Forensic Log Details](img/phase10.png)

## Phase 10: Incident Response and Remediation
Following the detection of the brute-force attempt (Event ID 4625), I implemented a structured **Incident Response** protocol to mitigate the risk and harden the endpoint:
* **IP Blocking:** Identified the source of the unauthorized attempts and simulated an IP block via the host-based firewall (Windows Firewall) to prevent further connection attempts.
* **Account Hardening:** Verified that the targeted username ('usuario_falso') did not exist. As a preventive measure, I reviewed the **Account Lockout Policy** to ensure accounts are automatically disabled after 5 failed attempts.
* **Service Review:** Audited RDP/SMB settings to ensure remote access is restricted to authorized users only.
* **Active Response:** Evaluated the feasibility of enabling Wazuh’s Active Response module for automated threat mitigation.

## Phase 11: Conclusion and Key Takeaways
The deployment of this Cybersecurity Home Lab provided a comprehensive view of the **Detection and Response** lifecycle. This project solidifies my foundation as a **Junior SOC Analyst**, demonstrating the technical maturity required to monitor, detect, and respond to modern cyber threats in an enterprise environment.
