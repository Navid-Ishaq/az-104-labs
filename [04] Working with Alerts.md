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


