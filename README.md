# Microsoft Sentinel Home Lab – SOC & Threat Detection 

## Project Overview
This project demonstrates a hands-on cybersecurity lab using **Microsoft Sentinel** to simulate a Security Operations Center (SOC) environment. The lab focuses on **threat detection, alerting, incident investigation, user and entity behavior analysis, and automated response** in a cloud-based SIEM environment.  

The objective of this lab is to showcase practical skills in **security monitoring, alert triage, and incident response**, reflecting real-world cybersecurity workflows.

---

## Lab Architecture

**Components:**
- **Azure Sentinel Workspace** – central SIEM for collecting and analysing security data.  
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

- **New User Account Creation (Medium Severity)**  
  Monitors Entra ID audit logs for newly created user accounts. This detection helps identify unauthorised account provisioning or potential persistence mechanisms used by attackers.

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

* **Low severity** – Investigate alerts, verify false positives or Benign, and monitor.  
* **Medium severity** – Perform deeper log analysis, document findings, and escalate if needed.  
* **High severity** – Trigger predefined automated response using Sentinel playbooks (e.g., disable account, notify senior analyst or SOC team)

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

### 4. User and Entity Behavior Analytics (UEBA)

Enabled **User and Entity Behavior Analytics (UEBA)** in Microsoft Sentinel to enhance threat detection by analysing user and entity activity patterns.

UEBA helps identify **anomalous behaviour** by creating behavioural baselines for users, devices, and other entities. Sentinel then applies machine learning to detect activities that deviate from normal patterns.
![UEBA Turn On](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/turnonueba.png)
![UEBA Rule](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/prebuiltuebarule.png)



### 5. Automation & Playbooks
- Created an automation rule in Microsoft Sentinel to streamline incident handling.
**Rule Name:** New User Automation  
**Trigger:**  
- Activated when an incident is generated for **new user creation in Entra ID**.
**Automated Actions:**
- **Change Incident Status** → Set to *Active*
- **Update Severity** → Set to *High*
- **Assign Owner** → Assigned to the SOC analyst (myself) for investigation

![createautorule](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/createautorule.png)
![succeedautorule](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/Succeedautorule.png)

### Playbook Automation – VirusTotal Threat Intelligence

Installed the **VirusTotal connector** from the Microsoft Sentinel **Content Hub** to enrich incident investigations with external threat intelligence.

**Playbook Name:** `Get-VirusTotalIPReport-IncidentTriggered`

**Functionality:**
- Extracts **IP address entities** associated with the incident.
- Queries **VirusTotal** for threat intelligence information related to the IP address.
- Retrieves details such as reputation, malicious detections, and analysis results.

**Automated Actions:**
- Writes the VirusTotal analysis results to **Log Analytics**.
- Adds a **comment to the incident** with the enriched threat intelligence data.
This playbook helps SOC analysts quickly determine whether an IP address involved in an incident is **malicious or suspicious**, enabling faster and more informed investigations.
![Playbook Example](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/createplaybook.png)
![Playbook Example](https://github.com/piang077/Microsoft-Sentinel-SOC-Home-Lab/blob/main/ScreenShots/logicapp.png)

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
This lab reflects a real-world SOC environment and demonstrates practical skills in **monitoring, detection, investigation, and automated response**. It highlights the ability to manage and interpret security events while maintaining structured incident workflows, preparing for roles like **SOC Analyst, Security Engineer**.

---

