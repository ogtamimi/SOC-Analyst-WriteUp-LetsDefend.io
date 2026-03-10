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

In **Splunk**, data can be added in several ways.  
In this lab, we will explore two common methods:

- Adding data using a **Forwarder installed on a Windows 10 machine**
- **Uploading a log file manually**

---

### 1️⃣ Add Data from a Forwarder

#### Step 1 — Open Add Data
Navigate to:

`Settings → Add Data`

![Add Data](../Assets/lab15/5.1.png)

---

#### Step 2 — Select Forward

Click **Forward** at the bottom of the page.

![Forward Option](../Assets/lab15/5.2.png)

---

#### Step 3 — Add the Host

Add the computer to the **Selected Hosts** list and assign a **Server Class Name**.

Then click **Next**.

![Add Host](../Assets/lab15/5.3.png)

---

#### Step 4 — Select Data Source

Choose what you want Splunk to monitor.

In this case we collect **Local Windows Event Logs**.

Select the logs you want and click **Next**.

![Select Logs](../Assets/lab15/5.4.png)

---

#### Step 5 — Choose an Index

Select the index where logs will be stored.

In this lab we create a new index:
`WinLog_clients`

To do this:

- Click **Create New Index**
- Name it **WinLog_clients**
- Click **Review**
- Then click **Submit**

After submitting, click **Start Searching** to check the client's logs.

---

### 2️⃣ Check Your Indexes

Navigate to:

`Settings → Indexes`

![Indexes](../Assets/lab15/5.5.png)

Search for the index created earlier.

![Search Index](../Assets/lab15/5.6.png)

If no events appear yet, the receiver must be configured.

---

### 3️⃣ Add a Receiver

Navigate to:

`Settings → Forwarding and Receiving`

Click **Add New Receiving Port**

![Add Receiver](../Assets/lab15/5.7.png)

Add port:

`9997` (default Splunk forwarder port)

Wait a few minutes and check the index again.  
You should start seeing incoming events.

![Events Received](../Assets/lab15/5.8.png)

Run a quick search to verify the logs.

![Search Logs](../Assets/lab15/5.9.png)

---

### 4️⃣ Add Data by Uploading Logs

Another way to add data is by **uploading log files manually**.

Navigate to:

`Settings → Add Data`

![Add Data Upload](../Assets/lab15/5.10.png)

---

#### Step 1 — Select Upload

Choose **Upload** from the bottom-left corner.

![Upload Option](../Assets/lab15/5.11.png)

---

#### Step 2 — Upload the File

Select the file you want to upload and click **Next**.

![Upload File](../Assets/lab15/5.12.png)

---

#### Step 3 — Review File Parsing

Splunk will show how the file will be parsed.

- Review the preview
- If everything looks correct, click **Next**

Select:

- **Host value** (if required)
- **Index** where the logs should be stored

Complete the process and start searching.

![Search Uploaded Logs](../Assets/lab15/5.13.png)

---

✅ we have now learned how to add data to Splunk using:
- **Forwarders**
- **Manual log uploads**

## 🔎 6) Searching in Splunk

Splunk provides powerful search capabilities to analyze logs and investigate security events. Below are the key features you should understand.

---

### ⚠️ Traps & Tips

Keep these important points in mind when writing searches:

- 🔠 **Field names are case-sensitive**
- 🔡 **Field values are NOT case-sensitive**
- ⭐ **Wildcard is supported** → use `*`
- 🔗 **Logical operators are supported**
  - `AND`
  - `OR`
  - `NOT`

---

### 📅 Date Selection

Splunk allows multiple ways to select time ranges for searches.

![Date Selection](../Assets/lab15/6.1.png)

From here you can choose:
#### 🕒 Presets
Quick predefined time ranges such as:
- Today
- Last 24 hours
- Last week
- Last month
- Last year

![Presets](../Assets/lab15/6.2.png)

---

#### ⏱ Relative Time
Search relative to the current time:
- Beginning of the hour
- `X` minutes ago
- `X` hours ago
- `X` days or weeks ago

![Relative Time](../Assets/lab15/6.3.png)

---

#### 🔴 Real-Time Search
Allows monitoring events **as they happen** in real time.

---

#### 📆 Date Range
Specify a fixed date range:
00:00 DD/MM/YYYY → 24:00 DD/MM/YYYY


![Date Range](../Assets/lab15/6.4.png)

---

#### 🕓 Date & Time Range

Similar to date range but allows **precise time selection**.

---

### 📊 Timeline

When you run a search, Splunk automatically generates a **Timeline** showing event distribution over time.

![Timeline](../Assets/lab15/6.5.png)

This helps you:

- Identify **event spikes**
- Detect **unusual activity**
- Focus on **specific time windows**

---

### ⚙️ Search Mode

Splunk offers **three search modes**:

1️⃣ **Fast Mode** – Quick searches with minimal processing  
2️⃣ **Smart Mode** – Balanced performance (recommended)  
3️⃣ **Verbose Mode** – Full event details

Most analysts use **Smart Mode**.

![Search Mode](../Assets/lab15/6.6.png)

![Search Mode](../Assets/lab15/6.7.png)

---

### 🔍 Search Bar

This is where you write your **Splunk queries**.

![Search Bar](../Assets/lab15/6.8.png)

You can combine:

- Wildcards `*`
- Fields
- Logical operators
---
![Search Bar](../Assets/lab15/6.9.png)
![Search Bar](../Assets/lab15/6.10.png)

#### How many different client IPs are there requesting the "/productscreen.html" path?
>**ANSWER: 65**

![alt text](../Assets/lab15/6.11.png)

#### What is the path where the client IP address "128.241.220.82" sends the most web requests?
>**ANSWER: /cart.do**

![alt text](../Assets/lab15/6.12.png)


## 7) Creating and Managing Splunk Reports

Reports in **Splunk** are **saved search results** that allow analysts to quickly access important queries without rewriting them every time.

Reports can be:

* 🕒 **Scheduled** to run automatically
* ▶️ **Executed manually** whenever needed

---

### 🧪 Exercise: Creating a Report

In this exercise, we will create a report that detects **failed login attempts** using accounts that contain **"admin"**.

---

#### 🔎 Search Query

Enter the following query in the Splunk search bar:

```spl
source="WinEventLog:*" index="winlog_clients" EventCode=4625 AND Nom_du_compte=Admin
```

⚠️ **Note:**
Depending on your dataset, the field `Nom_du_compte` may instead be called:

```
accountname
```

In that case, your query should be:

```spl
source="WinEventLog:*" index="winlog_clients" EventCode=4625 AND accountname=Admin
```

---

#### 1️⃣ Run the Search

Type the query in the **Splunk Search Bar** and execute it.

![Run Search](../Assets/lab15/7.1.png)

---

#### 2️⃣ Save the Search as a Report

Click **Save As** and select **Report**.

![Save As Report](../Assets/lab15/7.2.png)

---

#### 3️⃣ Add Report Information

Provide the following details:

* **Title** → Name of the report
* **Description** → Brief explanation of what the report does

![Report Details](../Assets/lab15/7.3.png)

---

#### 4️⃣ Save and View the Report

After saving the report, click **View** to open it.

![View Report](../Assets/lab15/7.4.png)

---

### 🛠 Editing or Deleting an Existing Report

Splunk allows you to manage your reports anytime.

---

#### 1️⃣ Go to the Reports Section

From the **Search & Reporting App**, navigate to the **Reports** section.

![Reports Section](../Assets/lab15/7.5.png)

![Reports List](../Assets/lab15/7.6.png)

Here you will see **all available reports**.

---

#### 2️⃣ Select Your Report

Click the report you created earlier.

![Select Report](../Assets/lab15/7.7.png)

You will see the report's details and settings.

---

#### 3️⃣ Edit the Report

Click the **Edit** button to modify the report.

![Edit Report](../Assets/lab15/7.8.png)

From here you can:

* ✏️ Modify the **search query**
* 🕒 Change the **schedule**
* 📝 Update the **title or description**
* 🗑 Delete the report if necessary

---

#### 💡 SOC Analyst Tip

Reports are extremely useful for monitoring **recurring security events**, such as:

* Failed login attempts
* Brute-force attacks
* Suspicious IP activity
* Malware alerts
* Unauthorized access attempts

Saving frequently used queries as reports helps **SOC analysts investigate incidents faster and maintain consistent monitoring workflows**.

#### Can you send an email when a report is generated?
>**ANSWER: Y**



## 8) Alerts on Splunk
Alerts are saved searches that trigger when certain conditions are met. They can be scheduled or in real-time. In that case, be careful not to overload your Splunk server.

>**ANSWER: CHECK**



## 9) Dashboards

A dashboard is nothing more than a dashboard. Here you can find a lot of information you need. You can make one for analysts, and one for your customers, with different types of information. If you use always the same requests and always need the same information, then making a Dashboard is a good idea.

![alt text](../Assets/lab15/9.1.png)

Here we have only one panel, but you can add other panels to this dashboard

>**ANSWER: CHECK**

## 10) Splunk Health Status Check
When you're connected to Splunk, click near the Administrator menu.

![alt text](../Assets/lab15/10.1.png)

On the left control panel, you have the status of each part of Splunk Server. On the right control panel, you have the description of each signal.

>**ANSWER: CHECK**

## 11) User Management on Splunk

Roles
By default Splunk give you some roles, to find or create a new role, go to Settings > Roles

![alt text](../Assets/lab15/11.1.png)

![alt text](../Assets/lab15/11.2.png)

From here you can edit or add a new role. A role can give you permission on the Splunk server, Splunk request, on which events you can see or which events you can not see, etc.


Users
When you install it, Splunk gives you only one user, which is admin. A good practice is to create another administrator account and use admin only in emergency cases. Thus, if you see an admin connection you can see there is a problem.

To find the users list and create a new one, go to Settings > Users.

![alt text](../Assets/lab15/11.3.png)

Password Management
When you install Splunk, they only ask for an 8 character password, no matter the complexity. You can modify it on Settings > Password Management

#### How many users do we have on our Splunk?
>**ANSWER: 1**
#### How many roles do we have on our Splunk?
>**ANSWER: 5**

# END.