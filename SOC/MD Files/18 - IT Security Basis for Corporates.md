# LECTURE18: IT Security Basis for Corporates

## 1) Introduction to IT Security Basis for Corporates
 
We will look at the basic questions to help you to evaluate your level of protection against cyber disasters on your infrastructure.

This course will include the subjects below:
* Inventory
* Backups
* Phishing Prevention
* Internet Browsing Protection
* Patching
* Access Control
* Risk Analysis
* Network
* Incident Response for IT Security

## 2) Inventory

Protecting an organization's infrastructure requires maintaining a **complete inventory** of all assets connected to the network. This helps security teams track devices, software usage, access permissions, and applied security controls.

### Inventory Information

The inventory should include at least the following information:

| Item | Description |
|-----|-------------|
| Hardware | Hardware details of each workstation and server |
| Installed Software | All installed software with **exact version numbers** |
| Last Report Date | Date when the asset information was last updated |

---

### End-of-Life Equipment

Equipment that has reached **End-of-Life (EOL)** no longer receives **security patches**, making it a security risk.

| Action | Description |
|------|-------------|
| Identification | Use the inventory to detect unsupported hardware and software |
| Mitigation | Remove unsupported systems from the network whenever possible |
| Exception | If removal is not possible, **CISO risk acceptance** must be documented |
| Review | Reassess risks regularly, especially when **new vulnerabilities** are discovered |

---

### Secure Boot

Secure Boot ensures that systems start only with **trusted manufacturer-approved software**.

| Requirement | Description |
|------------|-------------|
| Enablement | Must be enabled on all compatible devices |
| Security Benefit | Prevents unauthorized or malicious bootloaders during system startup |

---

### Software Management

To reduce the **attack surface**, organizations should maintain strict control over allowed and prohibited software.

#### Allowed Software

| Control | Description |
|-------|-------------|
| Deployment Tools | Use **GPO** or **Intune** to distribute approved software |
| User Access | Allows installation without granting administrative privileges |
| Security Benefit | Prevents users from downloading software from untrusted sources |

#### Forbidden Software

| Control | Description |
|-------|-------------|
| Blocking Tools | **Intune** or **AppLocker** can block unauthorized applications |
| Reason | Applications may be restricted due to security risks or known **CVE vulnerabilities** |
| Monitoring | Attempts to run prohibited software should be reported to the IT team |

---

### Security Hardening

Security hardening ensures that systems follow **secure configuration standards**.

| Area | Description |
|----|-------------|
| Configuration Audits | Regular checks to verify secure device configurations |
| Change Monitoring | Alerts triggered when configurations are modified |
| Implementation | Hardening policies can be applied using **Ansible, GPO, or Intune** |

---

### Antivirus / EDR

All organizational devices should be protected with **Antivirus or Endpoint Detection and Response (EDR)** solutions.

| Control | Description |
|--------|-------------|
| Deployment | Install on all endpoints, prioritizing critical systems |
| Monitoring | Security teams must track and investigate generated alerts |

---

#### Which of the following is not an issue to be considered while doing hardening work?
>**ANSWER: D) Mouse movements of devices**


## 3) Backups
Backups are not a mechanism for stopping ransomware attacks, but they represent the **last line of defense** for recovering data after an incident. If backups are not operational after an attack, the survival of the business may be at risk.

---

### Rule 3-2-1

The **3-2-1 rule** is the minimum recommended backup strategy for most infrastructures.

| Requirement | Description |
|-------------|-------------|
| **3 Copies** | Maintain at least three copies of your data (original + two backups). |
| **2 Media** | Store backups on two different storage systems or locations. |
| **1 Offsite Backup** | Keep one backup outside the primary location. |

---

#### Three Copies

Your data should exist in **three separate copies**:

- The **original data** on the production server  
- **Two backup copies**

This redundancy ensures that if one backup fails or becomes corrupted, another copy remains available.

---

#### Two Different Media

Two media do not necessarily mean two different physical formats (such as HDD and tape). Instead, the goal is to avoid **shared points of failure**.

Examples include:

- Backups stored in **different datacenters**
- Storage systems not connected to the same **RAID infrastructure**
- Separate storage environments that are **independent from each other**

---

#### One Offsite External Backup

At least one backup should be stored **outside the main infrastructure location**.

This protects critical data against disasters such as:

- Fire  
- Flooding  
- Physical damage to the primary datacenter  

---

### Rule 3-2-1-1-0

The **3-2-1-1-0 rule** extends the previous strategy and is recommended for **critical systems**.

| Requirement | Description |
|-------------|-------------|
| **1 Offline Copy** | Maintain one backup completely disconnected from the network. |
| **0 Errors** | Ensure backups can be restored successfully without errors. |

---

#### One Offline Copy

An **offline backup** is a backup that is not connected to any network or IT infrastructure.

The purpose is to prevent attackers who have compromised the network from:

- Deleting backups  
- Encrypting backups  
- Modifying backup data  

---

#### Zero Errors During Restoration

Backups must be **regularly tested** to ensure they can be restored successfully.

If backups are not tested, it is possible to discover **corrupted or incomplete files only during an incident**, which could make recovery impossible.

---

### Minimum Storage Time

Backup retention should allow restoration of **data that is at least 30 days old**.

This is important because the **average time between a network intrusion and its detection is often several weeks**.

---

### Backup Tests

Backup restoration tests should be performed regularly.

Best practices include:

- Tracking all **backup restoration tests**
- Ensuring that **each server is restored at least once per year**
- Verifying that **critical data remains intact after restoration**

---

## 4) Phishing Prevention
Phishing attacks represent one of the biggest initial attack vectors along with the exploitation of vulnerabilities on your online servers.


Antispam and Email Protection
Do all emails received by your employees pass through a spam filter? Does your Antivirus (AV) software analyze the attachment in the mail? Is this configuration reviewed and kept up to date with new threats?


Analysis Procedure
When one of your employees receives an email and has a doubt, she/he should have the possibility to contact someone to perform an analysis of the email.


Phishing Drill
It is often perceived as an attack by the staff. It may be worthwhile to conduct a test to ensure your staff is properly prepared.

#### What is the name of the simulation study performed to raise corporate employees' awareness of phishing attacks?
>**ANSWER: Phishing drill**

## 5) Internet Browsing Protection
Filter connections to unauthorized websites, suspicious domain names and known malicious domain names.


DNS Filtering
Block dangerous sites and filter unwanted content through your firewalls. In addition to "unprofessional" categories like +18 adult content, there is one category that is rarely blocked, URL shorteners. This service is massively used, especially for phishing. Once the blocking is configured, it is necessary to control the blocked sites that your employees have tried to visit.


Centralized Management of Browsers
Updating browser security settings can make it harder for malware to install. For example, to reduce the ability to install plug-ins or to disable the automatic execution of certain types of content.

#### What security technique is used to block unwanted addresses from being accessed within the institution?
>**ANSWER: DNS Filtering**

## 6) Patching

Deploy patches to your software and firmware as quickly as possible. Enable automatic updates whenever possible.


SLA for Patching According to CVE
What is SLA?
A service-level agreement (SLA) is a contract between a service provider and its customers that documents what services the provider will furnish and defines the service standards the provider is obligated to meet.


Have you set up a maximum update time for your workstations/servers/softwares? If yes, do you take into account criteria such as the CVSS (Common Vulnerability Scoring System) score, the fact that the server to be patched is on the Internet-facing or not, that the flaw is known to be exploited (0-day)?

## 7) Access Control
Implement policies, processes and technologies that ensure that only authorized users are granted the least privileges necessary. There is no magic bullet here that works for everyone, you need to adapt, take it step by step.


Password & MFA
The lowest level of protection is the implementation of a password policy within your environment. In the case of a Windows environment, this policy should be set in the "Default Domain Policy" to ensure that it applies to all computers. 

Whenever possible, use stronger mechanisms than password authentication, such as biometrics, one-time passwords and application tokens. Multi-factor authentication (MFA), via SMS or application authenticator, is highly recommended, starting with privileged users and extending to all users.


Zero Trust
Identify and disable unused accounts, eliminate shared accounts, remove unnecessary privileges and enforce strong password policies.


Audit of Account Usage
Monitor and analyze user activity for anomalous behavior such as access attempts outside of normal business hours or from unusual locations. Your fleet should not contain more than 15% of accounts with the "domain administrator" privilege.

## 8) Risk Analysis
Use risk assessments to prioritize the allocation of resources and investments.

Return to Service
Has your company conducted a study to define which resources should be recovered first? This analysis can also be used to estimate the impact of disruptions and identify allowable downtime.

Review of Risks on Connected Networks
Every connection to your company is a risk to it. Whether it's within an entity of your company or a partner. Keep in mind that each of these parties may not have the same security requirements as you do. 

## 9) Network

Monitor your organization's incoming and outgoing Internet traffic.

PCAP
Use the SPAN ports of your network equipment to capture your network activities. This capture will allow you to detect abnormal behavior (increased use of a protocol, abnormal destination addresses, etc.) as well as to perform a post-mortem in case of compromise.

Segmentation
Segmentation divides a computer network into smaller parts. Network segmentation improves network performance and security by reducing the attack surface and limiting the range of an attack. The use of VLAN, PVLAN allows you to separate your different networks. 

Are the administration interfaces of your network equipment available from Alice's (or whoever) accounting station? Is the remote office service only available on a dedicated network?

Review of Blocked Flows
Now that your corporate network is segmented, and flows are prohibited, the next step is to set up a review to identify the origin of the requests that get blocked with your new policy. It could be a compromised workstation, an application that went under your radar in the inventory, etc.

Alert Outside of Standard Use
Once all this is in place, you can generate alerts in case of abnormal network usage. Besides the security gain, these alerts could allow you to identify weak points in your organization, for example when your backup tools saturate the network.

## 10) Incident Response for IT Security
Make sure you have clear processes in place and known to your staff regarding escalation of major incidents. A major incident that is quickly escalated to the experts can allow you to mitigate the impact of a cyber attack.

## 11) Quiz
#### Which of the options should be in your IT inventory kept for security purposes?
>**ANSWER: The software installed with the exact version**
#### Why is it important to restrict various software?
>**ANSWER: To prevent known malware from running**
#### What is the main reason to keep an offline backup of backups?
>**ANSWER: To use in case of damage to online backups**
#### How many days should the Minimum Retention Time be?
>**ANSWER: 30**
#### What does Phishing Drill do?
>**ANSWER: The company provides awareness to employees about phishing**
#### Why is it important to use a password policy?
>**ANSWER: To standardize password security**
#### What should be done to detect abnormal activities in the network?
>**ANSWER: Monitoring**
#### Which of the following should be included in the scope of Hardening?
>**ANSWER: Audit of the secure configuration of the devices**
#### Why should endpoint devices have EDR or at least AV?
>**ANSWER: To track and secure devices**
#### Why is it important not to use end of life device?
>**ANSWER: Because they pose a security risk**

# END. 