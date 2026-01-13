# Wazuh SOC Home Lab: Deployment and Threat Detection

## Project Overview
This project demonstrates the end-to-end deployment of a **Wazuh SIEM/XDR** ecosystem. It covers the infrastructure setup, remote management, agent enrollment, real-time threat detection, and forensic log analysis, simulating a professional Security Operations Center (SOC) environment.

---

## Phase 1: Operating System Deployment
To host the Wazuh SIEM, I deployed an **Ubuntu Server 24.04 LTS** instance. This environment was configured with 8GB of RAM and 50GB of storage to ensure high performance during log analysis. The network was set to **Bridge Mode** to allow seamless communication between the server and monitored endpoints.

![OS Deployment](img/phase1.png)

## Phase 2: Establishing Secure Remote Management (SSH)
To streamline the deployment and management of the Wazuh server, I established a remote connection from my Windows host to the Ubuntu VM using the **SSH protocol via PowerShell**. This setup confirms network reachability between the host and the guest and allows for more efficient command execution and system monitoring.
* **Tool:** Windows Terminal / PowerShell (SSH Client)
* **Target:** matheus-soc@192.168.0.22
* **Port:** 22 (Default SSH)

![SSH Connection](img/phase2.png)

## Phase 3: Automated Deployment & Service Validation
Following the successful validation of the Ubuntu Server environment, I initiated the deployment of the **Wazuh ecosystem (v4.9.2)**. The centralized installation assistant was utilized via a remote SSH connection to ensure precision and system integrity.

**Key technical milestones:**
* **Hardware Resource Validation:** The script verified that the VM resources met the requirements for real-time log indexing.
* **Security Architecture & Encryption:** Automated generation of a Root Certificate Authority (CA) and specific node certificates to ensure all internal traffic is fully encrypted.
* **Component Provisioning:** Successful initialization of the Wazuh Indexer, Manager (vulnerability engine), Filebeat, and Dashboard.

![Wazuh Installation](img/phase3.png)

## Phase 4: Web Interface Integration and Initial Telemetry
After successful provisioning, I accessed the **Wazuh Dashboard** via HTTPS using the server's local IP (192.168.0.22). This stage confirms the proper integration between the Indexer and the Dashboard UI. Upon initial login, the system already recorded **21 security events** related to internal server processes and integrity checks.

![Dashboard Access](img/phase4.png)

## Phase 5: Agent Enrollment and Endpoint Deployment
To begin active monitoring, I initiated the agent enrollment process. I selected the **Windows MSI** package for the local host and assigned the server address `192.168.0.22`. The agent was customized with the name **'My-Windows'** for clear identification within the security group.

![Agent Configuration](img/phase5.png)

## Phase 6: Successful Agent Synchronization and Visibility
This stage marks the establishment of active monitoring. The Wazuh Manager is now receiving real-time telemetry from the deployed endpoint. The system successfully retrieved detailed OS metadata, identifying the host as **Windows 11 Pro**, with a 100% connectivity rate.

![Active Agent Visibility](img/phase6.png)

## Phase 7: Threat Detection and Event Correlation Analysis
The SIEM triggered alerts for suspicious activity on the 'My-Windows' endpoint. The dashboard recorded **3 Authentication Failure** events, which were automatically correlated with the **MITRE ATT&CK Framework** (Tactic: Account Access), providing immediate context for incident response.

![Threat Detection Dashboard](img/phase7.png)

## Phase 8: Deep Log Analysis and Forensic Investigation
Moving into digital forensics, I analyzed the raw event data. The investigation revealed **Event ID 4625** (Failed Logon) with **Logon Type 3** (Network-based). The failure status **0xc000006d** specifically points to an invalid username ('usuario_falso') or authentication process failure.

![Forensic Analysis](img/phase8.png)

## Phase 9: Incident Response and Remediation
Following the detection, I implemented a structured **Incident Response** protocol:
* **IP Blocking:** Identified and simulated an IP block via Windows Firewall to prevent further attempts.
* **Account Hardening:** Reviewed the **Account Lockout Policy** to ensure accounts are disabled after 5 failed attempts.
* **Service Review:** Audited RDP/SMB settings to ensure remote access is restricted to authorized users via VPN or MFA.
* **Active Response:** Evaluated the feasibility of enabling Wazuh’s Active Response module for automated threat mitigation.

---

## Phase 10: Conclusion and Key Takeaways
The deployment of this Cybersecurity Home Lab provided a comprehensive view of the **Detection and Response lifecycle**. By integrating an Ubuntu-based Wazuh Manager with a Windows 11 endpoint, I established a robust environment for threat hunting.

**Professional Competencies Demonstrated:**
* **Infrastructure Management:** Deployment of Linux-based security servers and remote SSH management.
* **SIEM/XDR Proficiency:** Experience in log ingestion, rule correlation, and dashboard customization.
* **Analytic Mindset:** Ability to interpret raw Windows Event Logs (XML/JSON) and map them to the MITRE ATT&CK framework.
* **Technical Reporting:** Documenting complex security processes for technical and executive audiences.
