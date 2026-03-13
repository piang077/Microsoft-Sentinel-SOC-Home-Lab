# Microsoft Sentinel Home Lab – SOC & Threat Detection 

## Project Overview
This project demonstrates a hands-on cybersecurity lab using **Microsoft Sentinel** to simulate a Security Operations Center (SOC) environment. The lab focuses on **threat detection, alerting, incident investigation, and automated response** in a cloud-based SIEM environment.  

The objective of this lab is to showcase practical skills in **security monitoring, alert triage, and incident response**, reflecting real-world cybersecurity workflows.

---

## Lab Architecture

**Components:**
- **Virtual Machines (Windows/Linux)** – generate security logs and simulate endpoint activity.  
- **Azure Sentinel Workspace** – central SIEM for collecting and analyzing security data.  
- **Connectors** – integrate Microsoft 365, Azure AD, Syslog, and custom logs.  
- **Playbooks** – automate responses for detected threats.  
- **Workbooks & Dashboards** – visualize alerts and incidents for SOC monitoring.

**Diagram:**  
![Architecture Diagram](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/SentinelArchitecture.png)

---

## Key Implementations

### 1. Data Connectors
Connected various sources to Sentinel for comprehensive monitoring:
- **Microsoft Entra ID** – monitor user sign-ins, risky accounts, and privileged activity.  
- **Office 365** – track email-based threats and suspicious activity.  
- **Windows Security Events** – detect failed logins, account lockouts, and process anomalies.  
- **Syslog/Linux Logs** – track critical system events.

**Screenshot:**  
![Data Connectors](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/connectorinstalled.png)

---

### 2. Analytics & Detection Rules
Configured custom analytics rules in Microsoft Sentinel to detect suspicious activities and potential security threats.

- **Failed Login Attempts (Low Severity)**  
  Detects repeated authentication failures from the same user or IP address. This rule helps identify potential brute-force attempts or incorrect credential usage.

- **New User Account Creation (Low Severity)**  
  Monitors Entra ID audit logs for newly created user accounts. This detection helps identify unauthorised account provisioning or potential persistence mechanisms used by attackers.

- **Multiple Admin Logins from Different Locations (Medium Severity)**  
  Detects administrative accounts signing in from different geographic locations within a short period. This may indicate credential compromise or suspicious administrator activity.

- **Suspicious Process Execution on Endpoint (High Severity)**  
  Identifies potentially malicious processes such as PowerShell abuse, encoded commands, or unusual parent-child process relationships that may indicate malware execution or attacker activity.
  
**Screenshot:**  
Finds all newly created users in Entra ID and shows who created them and when.
![Analytics Rules](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/howicreatethequery.png)
![Analytics Rules](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/analyticwizardquerytest.png)
![Analytics Rules](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/analyticreview.png)
![Analytics Rules](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/analyticcreatereview.png)
![Analytics Rules](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/analyticnearrealtime.png)



---

### 3. Incident Management
Simulated SOC incident workflow:
- **Low severity**: investigate alerts for context, verify false positives.  
- **Medium severity**: escalate incidents, perform deeper investigation, document findings.  
- **High severity**: execute automated response via Sentinel playbooks (e.g., disable account, notify SOC team).

**Screenshot:**  
![Incident Dashboard](./screenshots/incidents.png)

---

### 4. Automation with Playbooks
Implemented **playbooks** to improve SOC efficiency:
- Trigger email notifications for medium/high severity alerts.  
- Automatically disable accounts flagged as compromised.  
- Send alerts to Microsoft Teams for SOC collaboration.

**Screenshot:**  
![Playbook Example](./screenshots/playbook.png)

---

### 5. Workbooks & Dashboards
Created dashboards to visualize security posture and trends:
- Alert overview by severity and source  
- User activity reports  
- Incident summary for SOC monitoring

**Screenshot:**  
![Dashboard Example](./screenshots/dashboard.png)

---

## Skills Demonstrated
- Cloud-based SIEM deployment and configuration  
- Threat detection and alert triage  
- Incident response and SOC workflow simulation  
- Security automation with playbooks  
- Data visualization and reporting for cybersecurity monitoring  

---

## Summary
This lab reflects a real-world SOC environment and demonstrates practical skills in **monitoring, detection, investigation, and automated response**. It highlights the ability to manage and interpret security events while maintaining structured incident workflows, preparing for roles like **SOC Analyst, Security Engineer, or Cybersecurity Consultant**.

---

