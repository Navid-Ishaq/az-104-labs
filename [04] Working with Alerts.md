# Lab 4: Working with Alerts

**Duration:** 1h 0m

**After logging in with your credentials:**

### Step 1: Create a Virtual Machine

1. Navigate to **Virtual Machines** in the Azure portal.
2. Click **+ Create > Azure virtual machine**.
3. On the **Basics** tab, configure:

   * **Resource group**: Select or create one (e.g., `rg_eastus_xyz`)
   * **Virtual Machine name**: `resizeVM`
   * **Region**: `East US`
   * **Availability options**: No infrastructure redundancy required
   * **Security type**: Standard
   * **Image**: Windows Server 2022 Datacenter: Azure Edition - x64 Gen2
   * **Size**: Select **B2s**
   * **Username**: `myfirstvm`
   * **Password**: `123_MyBirthDate`
   * **Inbound public ports**: None
4. Navigate to the **Disks** tab:

   * Set **OS disk type** to **Standard SSD**
5. Click **Review + create**, then click **Create** to deploy the virtual machine.

---

### Step 2: Create an Alert for the Virtual Machine

1. Go to the **resizeVM** virtual machine resource.
2. Under **Monitoring**, select **Alerts**.
3. Click **+ Create > Alert rule**.
4. Under **Scope**, click **+ Select scope**, then:

   * Search for **Virtual Machines**
   * Select your VM (`resizeVM`) and click **Apply**
5. Under the **Condition** section:

   * Click **See all signals**
   * Search for and select **All Administrative operations** under **Activity log**
   * Click **Apply**
6. Move to the **Action** tab:

   * Click **+ Create action group**
7. In the **Create action group** form, fill in:

   * **Resource group**: Select the same as used earlier
   * **Action group name**: `alertactiongrp`
   * **Display name**: `alertaction`
8. Under the **Notifications** tab:

   * Choose **Email/SMS message/Push/Voice**
   * Set **Name**: `Email action`
   * Tick **Email**, enter your email address, and confirm
9. Click **Review + create** and then **Create**
10. In the **Details** tab of the alert rule:

    * Set **Alert rule name**: `User Alert`
    * Add a short description if desired
    * Click **Review + create** and then **Create**

---

### Step 3: Trigger and Verify the Alert

1. Go back to **Virtual Machines** and open `resizeVM`.
2. Click **Restart** to initiate a restart operation.
3. Wait a few minutes.
4. Check the email inbox for an alert notification regarding the administrative action.

---

**Delete all the resources.**

---
---
---
## **Lab Summary: Working with Alerts**

### **🎯 Purpose of the Lab**

The purpose of this lab is to teach how to configure **monitoring alerts** for Azure resources—specifically, a **virtual machine (VM)**—to proactively track operational changes and activities. By the end of the lab, learners understand how to create alert rules that detect administrative operations and send email notifications using **action groups**, enabling real-time incident awareness and automation of response efforts.

This is critical in enterprise environments for ensuring **operational visibility**, **security compliance**, and **resource health monitoring**.

---

## **🛠️ Azure Tools and Services Used**

### 1. **Azure Virtual Machines**

* **Description**: Infrastructure-as-a-Service (IaaS) that allows users to deploy scalable compute resources in the cloud.
* **Role in the Lab**: A Windows Server VM is created as the monitored resource. It is used to demonstrate how alerts can be triggered based on administrative actions.

---

### 2. **Azure Alerts**

* **Description**: A monitoring feature in Azure that proactively notifies users when specified conditions on resources are met.
* **Role in the Lab**: The alert rule is configured to trigger when any **administrative action** (e.g., restarting a VM) occurs. It ensures operational awareness and rapid response.

---

### 3. **Azure Monitor**

* **Description**: A comprehensive service for collecting, analyzing, and acting on telemetry data from Azure resources.
* **Role in the Lab**: The alerting feature is part of Azure Monitor. It connects telemetry signals to defined conditions to generate alerts.

---

### 4. **Activity Log (Signal Source)**

* **Description**: A platform log in Azure that provides insight into operations performed on resources in a subscription.
* **Role in the Lab**: The alert rule listens for the **"All Administrative operations"** signal from the Activity Log to detect actions like VM restarts.

---

### 5. **Action Groups**

* **Description**: A collection of notification preferences and actions used by alert rules in Azure Monitor.
* **Role in the Lab**: An action group is configured to send an **email notification** when an alert condition is met. This simulates real-world alerting mechanisms in IT operations.

---

### 6. **Azure Portal**

* **Description**: A web-based interface for managing and configuring Azure services.
* **Role in the Lab**: The entire process—from VM creation to alert configuration and verification—is executed through the Azure Portal for ease of access and demonstration.

---

## ✅ Key Outcome

By configuring alert rules and linking them to an action group, users learn to **monitor Azure resources for specific events** and ensure that **critical changes or issues trigger timely notifications**, supporting better **governance**, **compliance**, and **operational efficiency**.

---
---
---
## **Scenario: Enabling Proactive Monitoring for a Cloud-Hosted Server**

**Context:**
*Naveed*, a cloud administrator at a mid-sized IT services firm, is responsible for managing a production environment hosted in **Microsoft Azure**. His team recently migrated several key workloads—including a financial reporting system—to **Windows Server virtual machines**. These systems must maintain high availability and security compliance, especially during working hours.

Recently, Naveed’s manager asked for **proactive monitoring** to track unauthorized or unexpected administrative activities—like restarts, shutdowns, or configuration changes—on the production VMs. In response, Naveed decides to implement an **alerting system** that notifies the team whenever a significant operation is performed.

---

## **Step-by-Step Story with Purpose**

### 🔹 **Step 1: Creating the Monitored Resource (Virtual Machine)**

To begin, **Naveed navigates to the Azure Portal** and creates a **new Windows Server 2022 virtual machine** named `resizeVM` in the `East US` region.

* He selects **B2s size** for cost-efficiency.
* He chooses **Standard SSD** for the OS disk to balance performance and budget.
* He disables public inbound ports to reduce the attack surface.

➡️ **Why?**
This VM serves as the monitored test system where Naveed can simulate administrative actions (like a restart) to trigger alerts.

---

### 🔹 **Step 2: Setting Up Alert Rules with Azure Monitor**

After the VM is provisioned, Naveed opens the **Monitoring > Alerts** section of the VM and begins creating a new **alert rule**.

* He defines the **scope** as the newly created `resizeVM`.
* Under **condition**, he selects the **"All Administrative operations"** signal from **Activity Log**.
* This ensures any action—like restarting, stopping, or modifying the VM—will trigger the alert.

➡️ **Why?**
Using **Activity Log signals** helps Naveed monitor operational changes across his Azure environment in real-time without deploying any additional agents.

---

### 🔹 **Step 3: Creating an Action Group**

To notify the right people, Naveed sets up an **action group**:

* He names it `alertactiongrp` and adds his email as a recipient under **Email/SMS/Push/Voice**.
* This group will handle alert **notifications** and could later include automation responses (e.g., invoking a runbook or webhook).

➡️ **Why?**
**Action groups** allow Naveed to route alerts to specific channels (email, SMS, automation) for fast and efficient responses from the ops team.

---

### 🔹 **Step 4: Testing the Alert Mechanism**

To verify the alert works, Naveed restarts the VM using the Azure portal.

* Within 2–5 minutes, he checks his email and sees a notification: “Administrative action detected on resizeVM.”
* Success! The alert has been triggered as expected.

➡️ **Why?**
Testing ensures the alert is functioning correctly and will respond to real incidents—helping the team stay informed and reactive.

---

## **Business Impact**

This setup gives Naveed’s team **proactive visibility** into changes happening across their cloud infrastructure. It helps:

* **Increase security** by monitoring potentially unauthorized admin activity.
* **Ensure compliance** by keeping an audit trail and enforcing accountability.
* **Reduce downtime** by quickly responding to unexpected changes.

---

## 🔚 Conclusion

Through this lab, Naveed implemented a foundational **alerting strategy using Azure Monitor, Alerts, Activity Log signals, and Action Groups**—all through the Azure Portal. These tools empower cloud teams to **stay ahead of issues**, reinforce operational standards, and drive business continuity in dynamic cloud environments.

---
---
---
## Comic-Style Summary: **“Alerts That Never Sleep!”**

Meet **Naveed**, a cloud admin who’s always on guard. His job? Keep critical servers safe and sound for a finance system that never sleeps. But lately, his manager has been worried about **unauthorized changes** on Azure virtual machines — like someone accidentally **restarting** or **stopping** a VM during work hours. That’s a big deal!

So, Naveed rolls up his sleeves and opens the **Azure Portal**. He first creates a test **Windows Server VM** named `resizeVM`, choosing a size that fits the budget and turning off **public access** — because safety comes first! This will be the test subject for his alerting setup.

Now comes the **superpower** part: **Azure Monitor Alerts**. Naveed navigates to the **Alerts** section inside the VM, selects **Activity Log**, and sets a condition for **“All Administrative operations.”** This means any **restart**, **shutdown**, or **change** will trigger a warning!

But alerts are no good without a receiver! So, Naveed creates an **Action Group** named `alertactiongrp`, and hooks up his **email** to it. Now, whenever something shady or sudden happens, **boom!** — he gets a message right in his inbox.

To test it, Naveed restarts the VM himself. A few minutes later — *ding!* — an email lands in his inbox: **“Administrative action detected.”** Success! The alert system is alive and working.

By the end of the day, Naveed has built a **watchdog system** that guards the cloud 24/7. Now the team gets **instant updates**, stays **compliant**, and handles problems **before they become disasters**.

**Lesson?** With **Azure Monitor**, **alerts**, and **action groups**, you don’t just watch your servers — you **protect them like a pro.** 🛡️💻📬

---
---
---

Lab-Based Conceptual MCQs
---

### 1. What is the main purpose of configuring alert rules on a virtual machine in Azure?

**(a)** Improve performance  
**(b)** Enable auto-scaling  
**(c)** Notify stakeholders about specific events  
**(d)** Encrypt VM data  

**✅ Correct answer: (c)**  
**Explanation**: Alert rules are used to detect and respond to specific actions or thresholds, such as administrative operations, by sending notifications to relevant users or teams.

---

### 2. Which Azure feature defines where and how alert notifications are delivered?

**(a)** Azure Log Analytics  
**(b)** Action Groups  
**(c)** Resource Locks  
**(d)** Diagnostic Settings  

**✅ Correct answer: (b)**  
**Explanation**: Action Groups allow you to specify the notification channels (email, SMS, webhook) that should be triggered when an alert condition is met.

---

### 3. What type of signal should you use to track actions like restarting a VM?

**(a)** Metric  
**(b)** Diagnostic  
**(c)** Activity Log  
**(d)** Network Trace  

**✅ Correct answer: (c)**  
**Explanation**: Activity log signals capture control-plane operations like start, stop, and restart, making them ideal for auditing administrative activity.

---

### 4. Why is it recommended to block public inbound ports during VM creation?

**(a)** To increase performance  
**(b)** To reduce billing  
**(c)** To minimize security risks  
**(d)** To support backup policies  

**✅ Correct answer: (c)**  
**Explanation**: Blocking public inbound ports limits external exposure, reducing the risk of unauthorized access and enhancing security.

---

### 5. What is the purpose of selecting “All Administrative operations” as a condition in an alert?

**(a)** To monitor disk usage  
**(b)** To notify when a VM is resized or restarted  
**(c)** To collect cost metrics  
**(d)** To manage storage tiers  

**✅ Correct answer: (b)**  
**Explanation**: This condition captures all user-initiated operations such as VM start, stop, and restart for audit and monitoring purposes.

---

### 6. How can email alerts benefit system administrators?

**(a)** They reduce VM boot time  
**(b)** They block failed logins  
**(c)** They provide immediate notification of important actions  
**(d)** They auto-correct VM issues  

**✅ Correct answer: (c)**  
**Explanation**: Email notifications ensure that administrators are promptly informed about critical operations or changes that require attention.

---

### 7. What defines the resource that an alert rule applies to?

**(a)** Action Group  
**(b)** Condition  
**(c)** Scope  
**(d)** Subscription tier  

**✅ Correct answer: (c)**  
**Explanation**: The scope identifies the specific Azure resource (e.g., a virtual machine) that the alert is monitoring.

---

### 8. Why might Activity Log alerts be preferred over Metric alerts in governance scenarios?

**(a)** They’re easier to configure  
**(b)** They track system-level performance  
**(c)** They capture control-plane operations  
**(d)** They don’t require action groups  

**✅ Correct answer: (c)**  
**Explanation**: Activity Log alerts monitor who did what and when — making them ideal for governance and compliance tracking.

---

### 9. Which Azure service integrates alert rules, metrics, and diagnostic settings?

**(a)** Azure Monitor  
**(b)** Azure DevOps  
**(c)** Azure Firewall  
**(d)** Azure Cost Management  

**✅ Correct answer: (a)**  
**Explanation**: Azure Monitor provides a centralized platform for managing metrics, logs, and alerts across all Azure resources.

---

### 10. After restarting a virtual machine with an alert rule in place, what confirms that the alert is functioning?

**(a)** A new VM is created  
**(b)** Email notification is received  
**(c)** The VM auto-scales  
**(d)** The alert is deleted  

**✅ Correct answer: (b)**  
**Explanation**: Receiving the alert email after performing the configured action (e.g., a restart) confirms that the alert rule and action group are working as intended.

---
---
---

## Lab-Based Conceptual MCQs

---

### 1.

Naveed is setting up a **Windows Server 2022** virtual machine in Azure for a financial system. To improve security, he chooses to **disable public inbound ports** during deployment. Why is this considered a best practice?

(a) It improves performance for internal network traffic
(b) It reduces billing costs related to public IPs
(c) It limits external attack exposure by blocking unsolicited access
(d) It simplifies Azure region selection during setup

**Correct answer: (c)**
Disabling public inbound ports helps minimize exposure to the internet and reduces the attack surface, which enhances the VM’s security posture.

---

### 2.

After creating a virtual machine named **resizeVM**, Naveed wants to be notified if any user performs **administrative operations** such as restarting or stopping the VM. Which Azure feature should he use to detect such actions?

(a) **Azure Resource Manager** templates
(b) **Azure Activity Log** alert signal
(c) **Azure Advisor** recommendations
(d) **Azure Key Vault** logging

**Correct answer: (b)**
The **Activity Log** provides a record of all control-plane operations, such as restarts or deletions. Naveed can configure an alert based on the **All Administrative operations** signal from this log.

---

### 3.

When defining the **scope** of an alert rule in Azure Monitor, Naveed selects a specific virtual machine. What is the role of the scope in an alert rule configuration?

(a) It defines the pricing tier for alerts
(b) It determines the region where alerts will be applied
(c) It limits the monitoring to a specific Azure resource
(d) It specifies how long the alert will be active

**Correct answer: (c)**
The **scope** determines which Azure resource the alert rule monitors. In this case, Naveed applies it to the **resizeVM** to receive alerts related to its activity.

---

### 4.

Naveed wants to notify both himself and another administrator by **email** when a critical VM change is detected. What Azure feature enables him to configure recipients and communication channels?

(a) **Role-Based Access Control (RBAC)**
(b) **Virtual Network Peering**
(c) **Action Group**
(d) **Azure Blueprints**

**Correct answer: (c)**
An **Action Group** defines who gets notified and how—via email, SMS, push notification, or webhook—when an alert is triggered.

---

### 5.

Why does Naveed choose the signal **All Administrative operations** instead of selecting individual events like "Restart VM" or "Stop VM" when creating the alert condition?

(a) It provides finer control over billing alerts
(b) It allows bulk scheduling of routine restarts
(c) It simplifies monitoring by covering all admin-level changes
(d) It avoids using custom scripts for alerts

**Correct answer: (c)**
Choosing **All Administrative operations** ensures a wide net is cast for detecting any significant operational changes without needing multiple alerts for each type.

---

### 6.

After setting up an alert, Naveed restarts the virtual machine to test whether his alert setup works. Why is this step important in cloud monitoring practice?

(a) It ensures the alert group has correct billing tags
(b) It validates that the alert logic and notification work as expected
(c) It clears out any hidden IP configuration issues
(d) It adds diagnostic logs to the VM image

**Correct answer: (b)**
Testing the alert by triggering a relevant event (like a restart) confirms that both the **alert rule** and **action group** function properly.

---

### 7.

While creating an **action group**, Naveed configures only email notifications. Later, he wants to automate a script execution whenever the alert is triggered. What should he add to the action group?

(a) Add a **metric alert**
(b) Add a **manual trigger**
(c) Add a **webhook or automation runbook**
(d) Add a **resource lock**

**Correct answer: (c)**
Action groups can be expanded with additional actions, including **webhooks** or **runbooks**, to automate responses to incidents.

---

### 8.

Which of the following Azure tools allows Naveed to monitor the operational and configuration changes made across Azure resources, including virtual machines?

(a) **Azure Policy**
(b) **Azure Monitor - Activity Log**
(c) **Azure Security Center**
(d) **Azure Site Recovery**

**Correct answer: (b)**
The **Activity Log** is the go-to source for tracking control-plane operations such as VM creation, restart, or deletion across Azure resources.

---

### 9.

Naveed configures the **alert rule** but forgets to **assign an action group**. What will be the consequence of this omission?

(a) The alert will auto-restart the VM
(b) The alert rule will fail to deploy
(c) The alert will trigger silently without notifying anyone
(d) Azure will prompt to assign a backup policy

**Correct answer: (c)**
Without an **action group**, the alert may be triggered, but there will be **no notifications** or automated responses — defeating the purpose of proactive monitoring.

---

### 10.

After the alert setup, Naveed receives an email saying, “Administrative action detected on resizeVM.” What does this confirm?

(a) The VM auto-scaled based on traffic
(b) The Azure Backup job completed successfully
(c) The alert rule and notification system are functioning as intended
(d) The VM diagnostic logs were reset

**Correct answer: (c)**
Receiving a timely notification indicates that the **alert rule**, **activity log condition**, and **action group** are properly configured and operating correctly.

---
---
---
## Professional Job Interview Questions – AZ-104 Labs

### 1. Naveed wants to ensure his team is notified whenever someone restarts a critical production VM. Which Azure feature should he use to detect such operational changes?

(a) Azure Role-Based Access Control  
(b) Azure Monitor Activity Log Alerts  
(c) Azure Service Health  
(d) Azure Log Analytics Workspace  

**Correct answer: (b)**  
Azure Monitor’s Activity Log alerts can detect administrative actions such as restarting or stopping a VM, making it the right tool for proactive monitoring.

---

### 2. To avoid delays in alerting, Naveed needs to define how notifications are delivered. Which component should he configure?

(a) Log Analytics Query  
(b) Azure Runbook  
(c) Action Group  
(d) Resource Lock  

**Correct answer: (c)**  
An **Action Group** specifies how and where to send alert notifications—via email, SMS, or webhook—once the alert rule is triggered.

---

### 3. After assigning an alert rule, Naveed wants to test it. What’s the best way to validate whether the alert works?

(a) Wait for a real incident  
(b) Restart the virtual machine manually  
(c) Check the metrics blade  
(d) Remove and recreate the alert  

**Correct answer: (b)**  
Restarting the VM triggers the alert defined on administrative operations, confirming the alert system works as expected.

---

### 4. Why did Naveed disable public inbound ports on the virtual machine?

(a) To prevent the VM from accessing the internet  
(b) To improve disk performance  
(c) To reduce the attack surface  
(d) To enforce a tagging policy  

**Correct answer: (c)**  
Disabling public inbound ports minimizes exposure to the internet and enhances **security** by limiting attack vectors.

---

### 5. What type of signal did Naveed use when creating the alert rule for administrative activity?

(a) Metric signal  
(b) Log signal  
(c) Activity Log signal  
(d) Diagnostic setting  

**Correct answer: (c)**  
**Activity Log signals** are ideal for detecting control plane operations like restart, delete, or modify events.

---

### 6. Naveed is concerned about alerting delays. Which action improves real-time responsiveness?

(a) Enable autoscale  
(b) Use activity log-based alerts with action groups  
(c) Enable diagnostic logs  
(d) Add a storage account to the VM  

**Correct answer: (b)**  
Using **activity log alerts** combined with **action groups** provides near real-time notifications to designated recipients.

---

### 7. Naveed needs alerts for multiple VMs with the same condition. What should he do to minimize effort?

(a) Create individual alerts for each VM  
(b) Use Azure Automation  
(c) Assign the alert at the resource group level  
(d) Use a VM extension  

**Correct answer: (c)**  
Assigning the alert at the **resource group level** applies the rule to all included VMs, making management more efficient.

---

### 8. Which feature allows Naveed to send alerts to email, SMS, or even automation tools?

(a) Alert Dashboard  
(b) Resource Health  
(c) Action Group  
(d) Role Assignment  

**Correct answer: (c)**  
**Action Groups** are built to route alerts to different channels and can trigger automated responses as well.

---

### 9. What would happen if Naveed configured an alert without assigning an action group?

(a) Azure will create a default notification  
(b) The alert will still function but not notify anyone  
(c) The alert cannot be saved  
(d) Azure will disable the alert automatically  

**Correct answer: (b)**  
Alerts can still run without an **action group**, but **no one will be notified**, defeating the alert's purpose.

---

### 10. Why is using Azure Monitor alerts a better practice than writing custom scripts for event detection?

(a) It is more expensive  
(b) It avoids using built-in Azure tools  
(c) It enables proactive, code-free monitoring  
(d) It requires advanced PowerShell skills  

**Correct answer: (c)**  
**Azure Monitor** enables scalable, proactive alerting through a GUI or templates—no custom scripting needed.

---
---
---
## Comic-Style Summary: **“Ping Me If Something Breaks!”**

---

### 🧑‍💻 The Setup Begins: Naveed vs The Quiet Cloud

**Naveed**, the always-alert Azure admin, was sipping chai when his boss stormed in:

> “We need to know if anyone restarts or messes with the production VM — *before* chaos breaks loose!”
> Naveed smiled and cracked his fingers. “Time to give this cloud some ears!” he declared, opening the **Azure Portal** to spin up a **Windows Server VM** named **resizeVM** — secure, lean, and ready to be watched like a hawk.

---

### 🚨 The Secret Weapon: Azure Alerts

Once the VM was up, Naveed headed straight to the **Monitoring > Alerts** blade.
“I need to catch every admin move — like a CCTV camera, but for the cloud,” he muttered.
He set up an **alert rule** using the **Activity Log signal** for **All Administrative Operations**. Any **restart**, **shutdown**, or **config change** would now send an alert.
“Good luck sneaking past *this* firewall, buddy,” he grinned.

---

### 📬 The Messenger Squad: Action Group Activated

Now that alerts were set, Naveed created an **Action Group** named **alertactiongrp**.
“I need these alerts to hit my inbox like a text from mom,” he joked, adding his email for notifications.
He imagined a team of digital pigeons flying alerts to his office, just in case someone touched that VM.

---

### 🔁 The Great Test: Restart and Wait

To make sure his setup worked, Naveed gave **resizeVM** a gentle reboot — just like poking a sleeping dragon.
“Let’s see if the cloud tattles,” he said, peeking at his inbox.
Boom! Within minutes, an email alert arrived:
**“Administrative action detected on resizeVM.”**
Naveed high-fived himself. “The cloud *listens* now.”

---

### 🎯 Mission Accomplished: Alerts That Work

Naveed reported back to his boss, “We now get notified before the damage is done. Like digital Spidey-sense.”
Thanks to **Azure Monitor**, **Activity Log alerts**, and **Action Groups**, the team could now **monitor**, **act fast**, and **stay compliant** without breaking a sweat.
The production environment was now **secure, transparent**, and **proactively protected** — all thanks to Naveed’s alert-fu!

---

✅ And so, the day was saved… by **smart monitoring**, **a few clicks**, and one very alert **Naveed**.

---
---
---
## Text-Based Diagram for the Lab: "Working with Alerts"

```plaintext
+----------------------------+
| 1. Create Virtual Machine |
+----------------------------+
            |
            v
+------------------------------------+
| Configure Windows Server 2022 VM  |
| - Region: East US                 |
| - Size: B2s                       |
| - OS Disk: Standard SSD           |
| - Disable Public Inbound Ports    |
+------------------------------------+
            |
            v
+-------------------------------+
| 2. Go to VM > Monitoring Tab |
+-------------------------------+
            |
            v
+---------------------------------------------+
| 3. Create Alert Rule                        |
| - Scope: resizeVM (the new VM)              |
| - Condition: "All Administrative Operations"|
+---------------------------------------------+
            |
            v
+--------------------------------------+
| 4. Create Action Group               |
| - Name: alertactiongrp               |
| - Action: Send Email to Naveed       |
+--------------------------------------+
            |
            v
+-------------------------------+
| 5. Restart the Virtual Machine|
+-------------------------------+
            |
            v
+----------------------------------+
| 6. Validate Email Notification   |
| - Check for alert in email inbox |
| - Confirm it mentions restart    |
+----------------------------------+
            |
            v
+----------------------------------------------+
| 7. Monitor for Real-World Admin Activities   |
| - Ensure alerts catch future changes         |
+----------------------------------------------+
```

### 📝 What This Diagram Shows:

This diagram outlines the **step-by-step process** Naveed followed to configure **alert-based monitoring** for a cloud-hosted **Windows VM** using **Azure Monitor**. It highlights the creation of an **alert rule**, setting up an **action group**, and validating real-time **email alerts** based on **administrative actions**. This flow empowers proactive monitoring and **incident response** using **native Azure tools**.

---
---
---
