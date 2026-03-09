# LECTURE15: Splunk
## 1) Introduction to Splunk

**What is Splunk?**

Splunk is a **data platform** designed to provide **enterprise observability, unified security, and customizable applications** across hybrid IT environments.  
It is widely used in the **cybersecurity industry** for monitoring, searching, analyzing, and visualizing machine-generated data from applications, systems, and infrastructure.  

Splunk enables organizations to:  
- Detect security incidents in real-time  
- Monitor operational performance  
- Build custom dashboards and alerts  
- Integrate with multiple data sources across hybrid environments  

Because of its popularity in cybersecurity and IT operations, understanding how Splunk works is essential for SOC analysts and IT professionals.

---

**Requirements for Installing Splunk**

**1. Sizing**  
To determine the appropriate server sizing for your Splunk deployment, you can use the **[Splunk Sizing Tool](https://www.splunk.com/en_us/resources/sizing.html)**. Sizing depends on the volume of data ingested, number of users, and types of searches or dashboards you plan to run.

**2. System Requirements**  
Splunk Enterprise on-premises requires specific system configurations. You can check the official requirements here: **[Splunk Enterprise System Requirements](https://docs.splunk.com/Documentation/Splunk/latest/Installation/Systemrequirements)**

**3. Network Ports**  
Ensure the necessary ports are open on your firewall for proper communication:  
- **9997** – For forwarders to send data to the Splunk indexer  
- **8000** – For accessing the Splunk Search & Reporting web interface  
- **8089** – For splunkd communication (also used by the deployment server)  

For a complete list of common ports used by Splunk, see: **[Splunk Common Network Ports v2.0.3](https://docs.splunk.com/Documentation/Splunk/latest/Admin/Ports)**

**4. License**  
Splunk offers a **60-day free trial**. After the trial expires, you can convert to a **perpetual free license** with limited functionality.

#### How many days do you have for the free trial?  
>**ANSWER: 60**

## 2) Splunk Installation on Windows

#### What's the service display name for Splunk on Windows?  
>**ANSWER: Splunkd Service**

## 3) Splunk Installation on Linux

#### Which command to check the Splunk status on Linux?
>**ANSWER: /opt/splunk/bin/splunk status**
#### Does Splunk start on Linux startup by default?
>**ANSWER: N**

## 4) Splunk Universal Forwarders

*For the training, we are going to install the universal forwarder in the default configuration. Our goal is to send Windows logs to Splunk.*
>**ANSWER: CHECK**

## 5) Add Data to Splunk

#### 
>**ANSWER: **