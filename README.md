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
*(Insert architecture diagram here – e.g., draw.io or Lucidchart export)*

![Architecture Diagram](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/SentinelArchitecture.png)

---

## Key Implementations

### 1. Data Connectors
Connected various sources to Sentinel for comprehensive monitoring:
- **Azure AD** – monitor user sign-ins, risky accounts, and privileged activity.  
- **Office 365** – track email-based threats and suspicious activity.  
- **Windows Security Events** – detect failed logins, account lockouts, and process anomalies.  
- **Syslog/Linux Logs** – track critical system events.

**Screenshot:**  
![Data Connectors](./screenshots/connectors.png)

---

### 2. Analytics & Detection Rules
Configured **custom analytics rules** to detect potential threats:
- Failed login attempts (**Low severity**)  
- Multiple admin account logins from unusual locations (**Medium severity**)  
- Malware or suspicious process execution (**High severity**)  

**Screenshot:**  
![Analytics Rules](./screenshots/analytics_rules.png)

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

