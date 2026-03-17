# SOAR-EDR-Automation-Playbook-using-LimaCharlie-Tines-Slack

## Project Overview
This project demonstrates the implementation of an automated Security Orchestration, Automation, and Response (SOAR) playbook integrated with Endpoint Detection and Response (EDR).

The lab simulates real-world incident detection where an infected machine generates telemetry, which is analyzed using LimaCharlie EDR. Alerts are forwarded to Tines SOAR, where an automated workflow notifies the SOC team via Slack and email, and enables analyst-driven response actions.

The playbook allows analysts to decide whether to isolate a compromised machine, enabling a semi-automated incident response process.


# Lab Architecture
The environment consists of an endpoint generating malicious activity, an EDR platform for detection, and a SOAR platform for automation and response.

<img width="775" height="841" alt="soar Edr Project" src="https://github.com/user-attachments/assets/a0221dc5-e080-4cf9-ab53-3f55d5225b8d" />

<img width="882" height="415" alt="soar edr project list out" src="https://github.com/user-attachments/assets/09b83324-a6d3-42df-9c2e-3abe75295904" />

## Workflow:

Infected machine generates telemetry
LimaCharlie detects suspicious activity
Detection sent to Tines via Webhook

**Tines triggers:**
- Slack alert
- Email notification
- User prompt (Isolate machine?)
- Decision:
- Yes → Isolate machine via LimaCharlie
- No → Notify SOC to investigate

<img width="1058" height="822" alt="final playbook for soar edr project" src="https://github.com/user-attachments/assets/e991329d-8f51-451b-baa7-1a9bf2e1573a" />


# Component Used

<img width="913" height="302" alt="image" src="https://github.com/user-attachments/assets/3b54930d-dcf6-4a1b-96ca-2e8cfdbaf79b" />


# Implementation Steps

# Phase 1: Environment Setup

- Installed LimaCharlie agent on endpoint machine
- Verified agent connectivity in LimaCharlie dashboard
- Accessed Sensor Timeline for telemetry visibility

- <img width="1217" height="581" alt="lima charlie agent installation" src="https://github.com/user-attachments/assets/4ae4490e-4865-4bad-ad1b-6a884659093f" />

<img width="1857" height="703" alt="rule lazagne search" src="https://github.com/user-attachments/assets/45d20ed2-f385-420b-9b3e-c5df6125901d" />

<img width="1836" height="640" alt="sample output connect with limacharlie to  tine" src="https://github.com/user-attachments/assets/96ee8843-cebe-4d58-8a55-a5a88b4aec61" />


# Phase 2: Attack Simulation & Detection
To simulate malicious activity:
Installed and executed LaZagne:

.\LaZagne.exe all


This generated credential dumping activity detected by LimaCharlie

Detection Engineering:

Created custom detection rule in LimaCharlie

Triggered alerts based on suspicious process execution

<img width="1836" height="640" alt="sample output connect with limacharlie to  tine" src="https://github.com/user-attachments/assets/a113261e-8a6b-44ca-af67-22a0cc100eb9" />

<img width="1857" height="703" alt="rule lazagne search" src="https://github.com/user-attachments/assets/0dd97148-126a-4c76-989e-1a4894bad52b" />


# Phase 3: SOAR Integration with Tines

Created account in Tines
Generated Webhook URL
Integrated LimaCharlie output with Tines webhook

**Flow:**
Detection → Sent to Tines → Trigger automation

<img width="1438" height="727" alt="send alert messages from tine to slack" src="https://github.com/user-attachments/assets/6f5e9d4c-5bab-4580-870f-7b42d4f72ee4" />


# Phase 4: Playbook Automation

A complete SOAR playbook was developed in Tines. </br>
Playbook Logic </br>
Receive detection from LimaCharlie </br>

Send alert to: </br>
  Slack </br>
  Email </br>
  Include details: </br>
  Time </br>
  Computer Name </br>
  Source IP </br>
  Process </br>
  Command Line </br>
  File Path </br>
Generate User Prompt: </br>
“Do you want to isolate the machine?” </br>

Decision Workflow </br>
**If YES:** </br>
  Trigger isolation via LimaCharlie API </br>
  Confirm isolation status </br>
  Send Slack message: </br>
    “Machine has been isolated successfully” </br>
**If NO:** </br>
No isolation performed </br> 

Send Slack message: </br>
“Machine not isolated, investigation required” </br>

<img width="813" height="691" alt="user input" src="https://github.com/user-attachments/assets/29d6dae8-97bd-43b5-9879-4d3b3643aa7d" />

<img width="1761" height="473" alt="send all message from tnies to slack (user input" src="https://github.com/user-attachments/assets/063760d1-2a05-4bc4-84a2-e854de6ae6f6" />

<img width="1827" height="573" alt="receive emails from tines (user input" src="https://github.com/user-attachments/assets/699e8b22-d37d-477d-893a-fd290c3bae0a" />



# Phase 5: Alerting & Response
Slack Notifications </br>
Detection alert sent to SOC channel </br>
Isolation success message (if YES) </br>
Investigation alert (if NO) </br>

<img width="813" height="691" alt="user input" src="https://github.com/user-attachments/assets/d282661d-96b4-442e-88ad-63015e299caf" />

 </br>
<img width="1917" height="543" alt="if user click on yes and then user has been isolated" src="https://github.com/user-attachments/assets/b8d7b80c-c8c4-483e-8e9c-44891b4915f5" />

 </br>
<img width="1845" height="460" alt="if user input no then message will be go in slack that user is not isolated " src="https://github.com/user-attachments/assets/369461cd-c012-49b7-8009-d362c23fb2cb" />

# Email Notifications
Detailed alert sent to SOC analyst

<img width="1827" height="573" alt="receive emails from tines (user input" src="https://github.com/user-attachments/assets/25fc2a6b-9edb-40af-a69c-daff3907f54d" />

# Key Findings & Observations

- EDR tools like LimaCharlie effectively detect credential dumping activity
- SOAR platforms like Tines enable rapid automation of incident response
- Analyst-driven decision (Yes/No) balances automation with control
- Slack integration improves real-time visibility for SOC teams
- Automated isolation significantly reduces response time to threats

**Skills Demonstrated**
- Endpoint Detection & Response (EDR)
- Detection Engineering
- SOAR Playbook Development
- Incident Response Automation
- Threat Simulation (Credential Dumping)
- API Integration (Webhook, HTTP Requests)
- Security Monitoring & Alerting

**Project Takeaways**
- Built a custom detection and response workflow using LimaCharlie
- Designed a real-world SOC playbook using Tines
- Implemented automated + human-in-the-loop response model
- Gained hands-on experience with EDR + SOAR integration

# Conclusion
This project demonstrates how modern SOC teams combine EDR and SOAR technologies to detect, analyze, and respond to threats efficiently.

By integrating LimaCharlie with Tines, Slack, and email notifications, the project replicates a real-world automated incident response pipeline where threats are not only detected but also mitigated with minimal manual effort.
