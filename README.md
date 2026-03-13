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
![Analytics Rules](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/analyticreview.png)
![Analytics Rules](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/analyticcreatereview.png)
![Analytics Rules](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/analyticnearrealtime.png)
![Analytics Rules](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/analyticwizardquerytest.png)



---

### 3. Incident Management

Simulated SOC incident workflow using alerts generated in Microsoft Sentinel.

**Severity Handling**

* **Low severity** – Investigate alerts and verify false positives
* **Medium severity** – Perform deeper log analysis and document findings
* **High severity** – Trigger automated response using Sentinel playbooks (e.g., disable account, notify SOC team)

#### Case Scenario: User Account Creation Alert

A custom detection rule was created to detect **new user account creation** in Microsoft Entra ID. When a new account is added, Microsoft Sentinel generates an alert and automatically creates an incident.

**SOC Investigation Process**

1. **Alert Received**
   An incident is generated in the Sentinel **Incidents dashboard**.

2. **Initial Triage**

   * Check the **incident severity level** (Low / Medium / High)
   * **Assign the incident owner** for investigation
   * Update the **incident status** ( New → Active)
   ![Incident Dashboard](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/incident0.png)

3. **Incident Review**

   * Read the **incident description and alert details**
   * Review **entities involved** (user)
   ![Incident Dashboard](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/incident1.png)
4. **Timeline Analysis**
   * Check the **time the incident was created**
   * Review related activities around the same timeframe

5. **Log Investigation**
   * Query **AuditLogs** using KQL to identify who created the account and whether the action succeeded.
   ![Incident Dashboard](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/incident2.png)

6. **Validation**
- To confirm the alert represented legitimate activity, the following was reviewed:
- **Who:** The newly created account (`TargetUser`) and the authorised administrator (`InitiatingUser`) who created it.
- **What:** Creation of a new user account in Entra ID.
- **When:** Timestamp of the account creation (can be seen in the screenshot below).
- **Where:** The account was created within the **Entra ID environment,
- **Why:** Part of normal administrative process / user onboarding.
- **How:** Administrator performed the action using standard Entra ID console or admin tools; operation succeeded with no anomalies.

![Incident Dashboard](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/incident3.png)
**Conclusion:**  
Based on this validation, the activity was determined to be **legitimate administrative behaviour** related to normal user account management. The incident was therefore **closed as Benign / Expected Activity**.
![Incident Dashboard](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/incident4.png)



This scenario demonstrates how a SOC analyst investigates **identity-related alerts**, correlates logs, and determines whether the activity is legitimate or a potential security incident.

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

