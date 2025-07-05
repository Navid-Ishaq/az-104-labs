# Lab 8: Monitor and Troubleshoot Azure Storage with Log Analytics

**Duration:** 1h 0m
---
---
---
---

## ✅ Azure Lab Steps: **Monitor and Troubleshoot Azure Storage with Log Analytics**

**After logging in with your credentials:**

---

### 🔹 Step 1: Create a Storage Account

1. In the Azure Portal, search for **Storage accounts** and select it.
2. Click **+ Create**.
3. Under the **Basics** tab:

   * **Subscription**: Select your active subscription.
   * **Resource group**: Choose or create `rg-cloudlabx-naveed`.
   * **Storage account name**: Use a globally unique name such as `stcloudopsnaveed`.
   * **Region**: Select `East US`.
   * **Performance**: Choose `Standard`.
   * **Redundancy**: Select `Geo-redundant storage (GRS)`.
4. Go to the **Advanced** tab:

   * Ensure **Access tier** is set to `Hot`.
5. Click **Review + create**, then click **Create**.
6. After deployment, select **Go to resource**.

---

### 🔹 Step 2: Add a Blob Container

1. In the storage account pane, under **Data storage**, select **Containers**.
2. Click **+ Container**.
3. Name it `monitor-blobs-container`.
4. Leave all other settings as default and click **Create**.

---

### 🔹 Step 3: Upload Files to the Blob Container

1. On your local computer, create three `.txt` files:

   * **sample1.txt**:

     ```
     Sample File 1 - Blob Monitoring Test  
     This is a test file for upload.
     ```

   * **sample2.txt**:

     ```
     Sample File 2 - Blob Monitoring Test  
     This is another test file for upload.
     ```

   * **sample3.txt**:

     ```
     SampleFile3-BlobMonitoringTest  
     This is another test file for upload.
     ```

2. In the Azure Portal, open `monitor-blobs-container`.

3. Click **Upload** and upload `sample1.txt`.

4. Wait **1 minute**, then upload `sample2.txt`.

5. Wait another **minute**, then upload `sample3.txt`.

6. Wait a few more minutes to allow telemetry data to be captured.

---

### 🔹 Step 4: Create a Log Analytics Workspace

1. In the search bar, search for **Log Analytics workspaces**.
2. Click **+ Create**.
3. In the **Basics** tab:

   * **Subscription**: Use the same subscription.
   * **Resource group**: Select `rg-cloudlabx-naveed`.
   * **Name**: Enter `log-ncloudedge-naveed`.
   * **Region**: Use `East US`.
4. Click **Review + create**, then **Create**.

---

### 🔹 Step 5: Create a Diagnostic Setting

1. Go to the storage account `stcloudopsnaveed`.
2. Under **Monitoring**, click **Diagnostic settings**.
3. If prompted, select the **blob service**.
4. Click **+ Add diagnostic setting**.
5. Provide a name such as `diag-blob-naveed`.
6. Under **Category details**, check `StorageRead`.
7. Under **Destination details**, select `Send to Log Analytics workspace`, and then choose `log-ncloudedge-naveed`.
8. Click **Save**.

---

### 🔹 Step 6: Generate Log Activity by Downloading a Blob

1. Go back to **Containers**, and open `monitor-blobs-container`.
2. Locate one of the uploaded files (e.g., `sample2.txt`).
3. Click the ellipsis `...` next to the file and select **Download**.

---

### 🔹 Step 7: Query Logs in Log Analytics

1. In the storage account, under **Monitoring**, click **Logs**.
2. Close the **Queries hub**, if open.
3. Switch to **KQL mode**.
4. Paste the following query:

```kusto
StorageBlobLogs
| where TimeGenerated > ago(1h) and OperationName == "GetBlob"
| project TimeGenerated, AuthenticationType, RequesterObjectId, OperationName, Uri
```

5. Click **Run**.
6. You should see the results showing the blob read operations performed earlier.

---

### 🔚 Final Step

**Delete all the resources** (Storage account, Log Analytics workspace, and resource group) to avoid any charges.

---
---
---

## ✅ **Structured Summary: Monitor and Troubleshoot Azure Storage with Log Analytics**

### 🎯 **Purpose of the Lab**

The purpose of this lab is to help learners like **Naveed**, the **Curious Cloud Explorer**, understand how to **monitor** and **troubleshoot Azure Blob Storage** activity using **Log Analytics**. This lab simulates real-world scenarios where cloud administrators need visibility into storage operations such as uploads, reads, and access diagnostics. By integrating **Azure Storage** with **Log Analytics**, Naveed learns how to track, query, and analyze storage access events—crucial for auditing, security, and performance tuning in professional cloud environments.

---

### 🛠️ **Azure Tools and Services Used**

Here is a list of the **Azure tools** utilized in this lab, including their descriptions and specific relevance to the lab’s objective:

---

#### 1. **Azure Storage Account**

* **Description**: A storage container in Microsoft Azure that provides access to **Blobs**, **Files**, **Queues**, and **Tables**.
* **Role in Lab**: Used to create a **blob container** (`monitor-blobs-container`) that stores files whose access is tracked. This is the primary data source being monitored.

**Example**: `stcloudopsnaveed` — created in region `East US` for the fictional company **CloudLabX**.

---

#### 2. **Blob Container**

* **Description**: A sub-component of Azure Storage used to organize **unstructured data** like text and binary files.
* **Role in Lab**: **Three .txt files** are uploaded to this container to simulate real-world blob activity, such as file storage and retrieval.

**Example**: The container `monitor-blobs-container` is where Naveed stores the test files (`sample1.txt`, `sample2.txt`, etc.).

---

#### 3. **Log Analytics Workspace**

* **Description**: A centralized repository in **Azure Monitor** for collecting, storing, and analyzing log data from Azure resources.
* **Role in Lab**: Enables **querying and filtering** of the blob access logs using **KQL (Kusto Query Language)**.

**Example**: `log-ncloudedge-naveed` — where storage activity logs are collected and queried.

---

#### 4. **Diagnostic Settings**

* **Description**: Settings within an Azure resource (like Storage Account) that define how platform logs and metrics are collected and routed.
* **Role in Lab**: Configured to **send StorageRead logs** from the Blob service to the Log Analytics Workspace for visibility.

**Example**: `diag-blob-naveed` setting enables logging of blob **read operations** to `log-ncloudedge-naveed`.

---

#### 5. **KQL (Kusto Query Language)**

* **Description**: A query language designed for querying large datasets in Azure Monitor and Log Analytics.
* **Role in Lab**: Used to write custom queries to **extract details** such as timestamps, file URIs, operation types, and requester identities from blob logs.

**Example Query**:

```kusto
StorageBlobLogs
| where TimeGenerated > ago(1h) and OperationName == "GetBlob"
| project TimeGenerated, AuthenticationType, RequesterObjectId, OperationName, Uri
```

---

### ✅ **Outcome**

By the end of this lab, the **Curious Cloud Explorer**, Naveed, successfully:

* **Configured** Azure Storage to emit diagnostic logs.
* **Uploaded** test files to a blob container to simulate real-world usage.
* **Integrated** the storage account with a Log Analytics workspace.
* **Queried** blob access logs to validate logging and monitoring.
* **Understood** how to trace operational activity in storage environments, a critical skill in securing and auditing enterprise cloud workloads.

This lab provides foundational knowledge required for real-world roles in **cloud operations**, **DevOps**, and **cloud security monitoring**, aligned with the **AZ-104 certification**.

---
---
---

### **Structured Summary: Monitor and Troubleshoot Azure Storage with Log Analytics**

---

#### **Lab Purpose**

The primary objective of this lab is to demonstrate how to **monitor** and **troubleshoot Azure Storage account activities** using **Log Analytics**. By configuring diagnostic settings and uploading/downloading blobs, the lab enables learners to generate meaningful data and analyze storage operations such as **read access** using **Kusto Query Language (KQL)**. This practice is essential for maintaining visibility, enhancing security, and optimizing performance in enterprise-scale cloud storage environments.

---

#### **Azure Tools Utilized**

1. ### **Azure Storage Account**

   * **Description:** A service that allows users to store large amounts of unstructured data such as text or binary data.
   * **Role in Lab:** Used to store blob data and configure diagnostic logging to track activities such as uploads and downloads.

2. ### **Blob Container**

   * **Description:** A logical container within a storage account used to store blobs (files).
   * **Role in Lab:** Hosts the text files uploaded to simulate user activity and trigger logging mechanisms.

3. ### **Azure Log Analytics Workspace**

   * **Description:** A centralized data repository where monitoring data is collected, analyzed, and visualized using queries.
   * **Role in Lab:** Collects diagnostic logs from the storage account to support detailed monitoring and troubleshooting via queries.

4. ### **Diagnostic Settings**

   * **Description:** A feature that enables resource logs and metrics to be sent to various destinations such as **Log Analytics**, **Event Hubs**, or **Storage accounts**.
   * **Role in Lab:** Configured on the storage account to send **StorageRead** logs to the **Log Analytics workspace**, enabling visibility into blob read operations.

5. ### **Azure Monitor Logs (Log Analytics Query Editor)**

   * **Description:** A query interface used to run **Kusto Query Language (KQL)** queries over collected telemetry data.
   * **Role in Lab:** Used to run queries that return details about blob read events for analysis and troubleshooting.

6. ### **Kusto Query Language (KQL)**

   * **Description:** A powerful, read-only query language used for performing diagnostics and analytics on log data.
   * **Role in Lab:** Used to filter and retrieve `GetBlob` operations, showing who accessed what data, and when.

7. ### **Azure Portal**

   * **Description:** The web-based interface for managing Azure services.
   * **Role in Lab:** The primary platform through which all configurations, deployments, and monitoring tasks are performed.

---

This lab integrates these tools to simulate a realistic monitoring workflow for cloud storage systems, equipping learners with practical skills in visibility, auditing, and incident analysis.

---
---
---
## 🌐 Real-World Scenario: **“Keeping an Eye on the Cloud – Blob Monitoring with Confidence”**

At **CloudLabX**, the IT team was facing a rising concern: how to **track file access and read operations** in their growing **Azure Blob Storage** environment. Files containing financial reports, confidential project briefs, and customer contracts were being stored in blobs—but no one really knew **who accessed what, and when**.

Enter **Naveed**, the **Curious Cloud Explorer** and junior cloud administrator. Freshly onboarded at **CloudLabX**, Naveed was assigned the task of setting up a **monitoring system** to track blob activities and generate audit trails for compliance reviews. The CTO wanted **real-time visibility** without purchasing third-party tools.

Naveed rolled up his sleeves and got to work.

---

### 🔹 Step 1: Create a Centralized Storage Account

Naveed first logged into the **Azure portal** and created a new **Storage Account** named `stcloudlabx-naveed` inside the resource group `rg-learntech-naveed`. He chose the **Geo-redundant storage (GRS)** option to ensure data durability across regions and set the **Access tier to Hot** to prioritize quick access performance.

📌 **Why this matters**: Choosing the right redundancy and performance options is key to **balancing cost and availability** based on how often the files are accessed.

---

### 🔹 Step 2: Simulate Blob Activity

To replicate real-world behavior, Naveed created a **blob container** called `monitor-blobs-container`. On his local PC, he crafted three simple text files: `sample1.txt`, `sample2.txt`, and `sample3.txt`. These files were uploaded **one at a time** with intervals to help generate distinct timestamp logs.

📌 **Why this matters**: Uploading files in a staggered way gives **clear traceable events** for Azure to log and helps validate the accuracy of **log tracking**.

---

### 🔹 Step 3: Set Up a Log Analytics Workspace

To begin tracking activity, Naveed created a **Log Analytics workspace** named `log-ncloudedge-naveed`. This workspace would be the **central brain** where all diagnostics data is collected and queried using **Kusto Query Language (KQL)**.

📌 **Why this matters**: Instead of guessing or manually checking logs, using **Log Analytics** enables you to create **dashboards, alerts, and reports** based on actual usage data.

---

### 🔹 Step 4: Configure Diagnostic Settings

Inside the storage account, Naveed went to **Diagnostic settings** and created a rule named `diag-blob-naveed`. He enabled the **StorageRead** category to capture blob read operations and sent the logs to the **Log Analytics workspace** he just created.

📌 **Why this matters**: Without enabling diagnostic settings, no data would be sent to Log Analytics. This is like **turning on the camera before expecting any footage**.

---

### 🔹 Step 5: Test the Monitoring Setup

To trigger a real read operation, the Curious Cloud Explorer downloaded one of the uploaded blobs. This was a great way to simulate a **real user action**.

He waited a few minutes, then opened the **Logs** pane in Azure Monitor, switched to **KQL mode**, and entered the following query:

```kusto
StorageBlobLogs
| where TimeGenerated > ago(1h) and OperationName == "GetBlob"
| project TimeGenerated, AuthenticationType, RequesterObjectId, OperationName, Uri
```

The query ran—and boom! 🎉 There it was: every access event, complete with **timestamp**, **requester identity**, and **blob URI**.

📌 **Why this matters**: This validates that **Azure Monitor** and **Log Analytics** are working as intended. It's a powerful example of **observability** in action.

---

### 🟩 Business Value

By the end of the task, Naveed demonstrated a key concept in **cloud governance**: **observability and accountability**. Not only did he ensure the storage account was being used securely, but he also helped the organization meet internal audit requirements—**without needing any paid third-party tools**.

He even documented everything and shared the **KQL query templates** with the Security team at **CloudLabX**, helping others reuse the process.

---

### ✅ Real-World Alignment

This story reflects the kind of **practical, job-ready work** that an **AZ-104-certified** administrator should be able to perform. The lab mimics tasks in real-world operations—**troubleshooting, log monitoring, and configuring diagnostic pipelines**—to ensure storage security and transparency in modern enterprises.

Naveed, the **Curious Cloud Explorer**, not only completed his task successfully—he also made a lasting impact on his team's security posture.

---
---
---
## Comic-Style Summary: **“Watch Those Blobs Like a Hawk!”**

### 🧠 Meet Naveed – The Curious Cloud Explorer

Once again, our star learner **Naveed**, the **Curious Cloud Explorer**, was on a mission. His new assignment from **CloudLabX** was clear: **monitor and troubleshoot Azure Blob Storage activity** to make sure no file access goes unnoticed. The team wanted **visibility and auditability**, and he had to deliver—without using any external tools!

---

### 🗃️ Step 1 – Setting Up the Stage

Naveed started by creating a **Storage Account** named `stcloudlabx-naveed` in the **East US** region under the resource group `rg-learntech-naveed`. He enabled **Geo-redundant storage** to keep things safe and picked the **Hot access tier** for fast blob access. Like a skilled architect, he created a **container** called `monitor-blobs-container`.

**💡Why?** You need a solid storage base before you can monitor anything!

---

### 📁 Step 2 – Upload Some Noise

To simulate real file activity, our Azure admin created three small **.txt files** with sample data on his local computer. He uploaded them to the container **one by one**, with a minute break between each upload. This helped Azure generate **distinct metrics** and log each action clearly.

**💡Why?** Staggered uploads = better timestamps = easier tracking!

---

### 📊 Step 3 – Build the Brain: Log Analytics

Next, the TechWaveNaveed admin created a **Log Analytics Workspace** called `log-ncloudedge-naveed`. This workspace would collect all the juicy insights from the storage activity—like a **security camera** for blobs.

Then, he configured a **Diagnostic Setting** named `diag-blob-naveed` and enabled the **StorageRead** category, pointing it to the workspace. This meant any future read/download actions would be captured and stored.

**💡Why?** No logging = no proof. Diagnostic settings make sure every action is recorded!

---

### ⏬ Step 4 – Time to Download and Detect

To trigger a **read operation**, the CloudOps engineer downloaded one of the uploaded files from Azure Storage. A few minutes later, he went to the **Logs** section, opened **KQL mode**, and ran a precise query to filter out “**GetBlob**” operations.

🎉 Result: Boom! He could see who accessed the file, when, and how!

---

### ✅ Mission Complete – Did Naveed Succeed?

Absolutely, yes! 💪
**Naveed successfully completed** his assigned task. He built a complete **blob monitoring system** using **native Azure tools**—no third-party apps, no magic—just smart cloud engineering. His solution was lightweight, scalable, and **audit-friendly**, and impressed both his team and the compliance folks at **CloudLabX**.

---

### 🧩 Moral of the Story

Even the simplest file uploads can carry risk if left **unmonitored**. With the help of **Azure Storage**, **Log Analytics**, and **KQL queries**, our **Curious Cloud Explorer** showed how cloud-native tools can **unlock visibility and control**—and build confidence in your cloud environment.

Stay curious. Stay secure.
Because **watching your blobs is just as important as storing them!** 🕵️‍♂️✨

---
---
---

### **Real-World Scenario: Monitoring Azure Blob Storage with Log Analytics**

---

**Meet Sarah**, a **Cloud Operations Engineer** at **TechSolutions Inc.**, a software company that manages cloud-hosted applications and services for enterprise clients. One of their key applications stores sensitive customer documents and analytics logs in **Azure Blob Storage**. Recently, Sarah received a request from the **Security and Compliance Team** to implement a solution that tracks **read operations** on stored documents to improve audit visibility and detect any suspicious access patterns.

To meet this request, Sarah decides to implement a solution using **Azure Storage Account diagnostics** and **Log Analytics**. Here’s how she goes about it:

---

### **Step 1: Create a New Storage Account for Monitoring**

Sarah logs into the **Azure Portal** and creates a new **Storage Account** using **Standard performance** and **Geo-redundant storage (GRS)** to ensure high availability. She selects **Hot** as the **Access Tier** to optimize performance for frequently accessed data. This account will host the blob data she wants to monitor.

> **Why this matters:** This ensures reliable, highly available blob storage while supporting future auditing through diagnostics.

---

### **Step 2: Create a Blob Container**

She adds a **Blob Container** named **monitor-blobs-container** within the storage account. This container will hold sample text files that simulate production data.

> **Why this matters:** The container provides a secure, logical space to organize and manage blob files.

---

### **Step 3: Upload Sample Blobs**

To simulate typical file usage, Sarah creates and uploads three text files—**sample1.txt**, **sample2.txt**, and **sample3.txt**—into the container, spacing each upload by a minute to generate time-stamped logs.

> **Why this matters:** These uploads help generate activity logs that will later be analyzed using **Log Analytics**.

---

### **Step 4: Set Up a Log Analytics Workspace**

Next, Sarah creates a **Log Analytics Workspace** named **MonitorLAWorkspace**. This workspace will collect and store logs related to the **Storage Account's blob activities**.

> **Why this matters:** Without a workspace, diagnostic data would not have a destination for collection and analysis.

---

### **Step 5: Configure Diagnostic Settings**

She then creates a **Diagnostic Setting** on the storage account. She names it **BlobStorageDiagnostics**, selects **StorageRead** under categories, and configures it to **send logs to the Log Analytics workspace** she just created.

> **Why this matters:** This setup enables tracking of read operations (like blob downloads), essential for compliance auditing and troubleshooting.

---

### **Step 6: Generate Read Activity**

Sarah navigates back to the container and **downloads one of the uploaded blobs** (e.g., **sample2.txt**) to simulate a user performing a **read operation**.

> **Why this matters:** This action triggers the generation of log data related to blob access, which can be queried and analyzed.

---

### **Step 7: Run a Log Analytics Query**

Finally, Sarah goes to the **Logs** section under **Monitoring** in the storage account. She writes a **Kusto Query Language (KQL)** query to fetch all **GetBlob** operations within the last hour:

```kusto
StorageBlobLogs
| where TimeGenerated > ago(1h) and OperationName == "GetBlob"
| project TimeGenerated, AuthenticationType, RequesterObjectId, OperationName, Uri
```

She runs the query and successfully sees the log entry for the blob download.

> **Why this matters:** This query provides insight into who accessed what data, when, and how—delivering full visibility into storage access patterns.

---

### **Outcome**

Sarah presents the solution to the Security Team, who are impressed by the ability to trace every read operation through **Log Analytics**. They now plan to apply this setup across other production storage accounts to improve monitoring and auditing standards.

---

### **Business Value**

By using **Azure Storage**, **Blob Containers**, **Diagnostic Settings**, and **Log Analytics**, Sarah built a scalable and secure monitoring solution that:

* Enhances **audit transparency**
* Detects **unauthorized access**
* Supports **compliance requirements**
* Provides **centralized visibility** using a single query interface

---

This scenario showcases how real-world engineers can use Azure’s built-in tools to solve business-critical challenges with confidence, visibility, and control.

---
---
---
## Lab-Based Conceptual MCQs

### 1. What is the primary benefit of using **Log Analytics Workspace** in the context of Azure Storage monitoring?

**(a)** Increases blob storage capacity  
**(b)** Enables querying and analyzing operational logs  
**(c)** Automatically encrypts all blob data  
**(d)** Reduces the cost of storage

**✅ Correct answer: (b)**  
**Explanation**: **Log Analytics Workspace** is used to collect and analyze log data from Azure resources, making it essential for monitoring and troubleshooting.

---

### 2. Why is it necessary to configure a **Diagnostic Setting** for the **Storage Account**?

**(a)** To increase storage redundancy  
**(b)** To enable logging of read/write operations  
**(c)** To assign permissions to users  
**(d)** To connect the storage account to a virtual network

**✅ Correct answer: (b)**  
**Explanation**: **Diagnostic Settings** allow logs and metrics to be collected and sent to a destination like a **Log Analytics Workspace** for analysis.

---

### 3. What does the **GetBlob** operation represent in **Log Analytics** queries?

**(a)** A failed storage operation  
**(b)** An upload operation  
**(c)** A blob read or download request  
**(d)** A blob deletion

**✅ Correct answer: (c)**  
**Explanation**: **GetBlob** corresponds to read or download requests made on blob data, which is important for audit and monitoring.

---

### 4. Which Azure service is required to execute **KQL (Kusto Query Language)** queries?

**(a)** Azure Synapse Analytics  
**(b)** Log Analytics  
**(c)** Azure Virtual Machines  
**(d)** Azure DevOps

**✅ Correct answer: (b)**  
**Explanation**: **Log Analytics** uses **KQL** to query collected logs from connected Azure resources.

---

### 5. Why is the **Hot Access Tier** selected when creating a **Storage Account** for monitoring purposes?

**(a)** It supports encryption  
**(b)** It is required for private endpoint connections  
**(c)** It provides low latency for frequent data access  
**(d)** It enables zone-redundant storage

**✅ Correct answer: (c)**  
**Explanation**: The **Hot Access Tier** is optimized for data that is accessed frequently, which is suitable for monitoring and testing scenarios.

---

### 6. What happens when you upload blobs in intervals during the lab?

**(a)** It triggers billing alerts  
**(b)** It prevents overwriting data  
**(c)** It generates time-stamped activity logs  
**(d)** It disables diagnostic logging

**✅ Correct answer: (c)**  
**Explanation**: Uploading files at intervals creates distinct **log entries** for each event, which can then be analyzed for patterns.

---

### 7. What is the role of the **Diagnostic Setting name** like "BlobStorageDiagnostics"?

**(a)** It encrypts data at rest  
**(b)** It defines the storage SKU  
**(c)** It labels and manages diagnostic configurations  
**(d)** It creates firewall rules

**✅ Correct answer: (c)**  
**Explanation**: Naming a **Diagnostic Setting** helps identify and manage specific logging configurations for resources.

---

### 8. Why should you wait a few minutes after uploading blobs before querying logs?

**(a)** To reduce latency  
**(b)** To allow logs to propagate to **Log Analytics**  
**(c)** To avoid data loss  
**(d)** To enable data encryption

**✅ Correct answer: (b)**  
**Explanation**: There's typically a short delay before logs become available in **Log Analytics**, so waiting ensures accurate results.

---

### 9. In the query `StorageBlobLogs | where OperationName == "GetBlob"`, what is the expected output?

**(a)** List of deleted blobs  
**(b)** Blob access requests  
**(c)** Blob uploads  
**(d)** Blob access tiers

**✅ Correct answer: (b)**  
**Explanation**: The query filters for **GetBlob** operations, which indicate read/download access events on blob containers.

---

### 10. What is a practical use case for sending storage diagnostics to **Log Analytics**?

**(a)** Real-time collaboration  
**(b)** Creating blob snapshots  
**(c)** Monitoring unauthorized access attempts  
**(d)** Accelerating CDN performance

**✅ Correct answer: (c)**  
**Explanation**: Analyzing logs in **Log Analytics** helps detect unusual access patterns and support security auditing for storage.

---
---
---
## Professional Job Interview Questions – Monitor and Troubleshoot Azure Storage with Log Analytics

1. **Naveed**, the Curious Cloud Explorer, is tasked with ensuring that all read operations on a specific blob container are being monitored. Which Azure feature allows him to collect and analyze these logs in near real-time?

(a) **Azure Activity Logs**  
(b) **Log Analytics Workspace**  
(c) **Application Insights**  
(d) **Azure Security Center**

**Correct answer: (b)**  
**Explanation:** **Log Analytics Workspace** allows telemetry data from services like **Azure Storage** to be queried and visualized. It's designed for detailed monitoring and operational insights.

---

2. While configuring diagnostics for blob storage, Naveed must ensure download operations are logged. What **category** must he enable in the diagnostic settings?

(a) **StorageDelete**  
(b) **StorageWrite**  
(c) **StorageRead**  
(d) **BlobServiceMetrics**

**Correct answer: (c)**  
**Explanation:** The **StorageRead** category captures operations like **GetBlob**, which are necessary to monitor file download activities.

---

3. Naveed has just created a **Log Analytics Workspace** and needs to route diagnostic data to it. What destination setting must he choose within the diagnostic settings?

(a) **Send to Storage Account**  
(b) **Send to Event Hub**  
(c) **Send to Log Analytics workspace**  
(d) **Archive to Blob**

**Correct answer: (c)**  
**Explanation:** To view and query diagnostic data, it must be sent to a **Log Analytics Workspace**, where it can be queried using **Kusto Query Language (KQL)**.

---

4. After uploading several blobs, Naveed wants to confirm that file access was logged. Which of the following **KQL queries** should he use?

(a) `AzureActivity | where OperationName == "GetBlob"`  
(b) `BlobDiagnostics | where OperationName == "UploadBlob"`  
(c) `StorageBlobLogs | where OperationName == "GetBlob"`  
(d) `StorageRead | filter Operation == "ReadBlob"`

**Correct answer: (c)**  
**Explanation:** **StorageBlobLogs** is the table that captures storage-level logging; filtering by `"GetBlob"` shows read operations like downloads.

---

5. The CloudOps engineer added a diagnostic setting but isn’t seeing data in the workspace. What is the most **likely cause**?

(a) Diagnostic category was set to StorageDelete  
(b) Files weren’t uploaded before diagnostic settings were created  
(c) Blob container is using Cool access tier  
(d) Log Analytics region is mismatched

**Correct answer: (b)**  
**Explanation:** Diagnostic settings do not capture historical data. If files were uploaded before the diagnostic was configured, those actions won't appear in logs.

---

6. Naveed is asked to configure monitoring for multiple storage accounts. What is the most **scalable** solution for managing diagnostics across these resources?

(a) Configure individual alerts  
(b) Use policy to enforce diagnostic settings  
(c) Use Azure Monitor templates manually  
(d) Rely on Activity Logs only

**Correct answer: (b)**  
**Explanation:** Using **Azure Policy**, Naveed can enforce consistent diagnostic settings across multiple storage accounts automatically and at scale.

---

7. A stakeholder wants to ensure that downloaded blobs are logged for **security auditing**. Why is the **StorageRead** metric category sufficient?

(a) It tracks authentication events only  
(b) It logs all container metadata changes  
(c) It includes operations like **GetBlob** and **ListBlobs**  
(d) It logs key vault access policies

**Correct answer: (c)**  
**Explanation:** The **StorageRead** category includes blob-level read operations, which are essential for auditing data access.

---

8. What is a potential reason Naveed would set the **access tier** of his storage account to **Hot** when preparing this monitoring lab?

(a) Reduces cost of infrequent access  
(b) Optimizes for archival purposes  
(c) Ensures quicker file availability for upload/download testing  
(d) Encrypts all blobs at rest

**Correct answer: (c)**  
**Explanation:** The **Hot access tier** is best for frequently accessed data, making it ideal for quick testing and read/write scenarios in this lab.

---

9. Why did Naveed choose to **download** a blob after configuring diagnostics and Log Analytics?

(a) To trigger StorageWrite metrics  
(b) To test access control policies  
(c) To generate a **GetBlob** operation that can be logged  
(d) To back up the container to a different region

**Correct answer: (c)**  
**Explanation:** Downloading a blob triggers a **GetBlob** request, which can be logged and later queried in **Log Analytics**.

---

10. In a real-world scenario, what is a key benefit of using **Log Analytics with Azure Storage**?

(a) It provides backup capabilities  
(b) It performs real-time replication  
(c) It supports advanced querying and operational monitoring  
(d) It encrypts data automatically

**Correct answer: (c)**  
**Explanation:** **Log Analytics** enables **deep insight and querying** into operations like reads and writes, which is critical for performance tuning and security auditing.

---
---
---
## Comic-Style Summary: **“Blob Drama and Log Magic with Naveed!”**

### 🌩️ Mission Accepted: Storage Set-Up by the Curious Cloud Explorer

**Naveed**, known in the tech realm as the **Curious Cloud Explorer**, began his day with a cup of chai and a clear task: "Monitor blob activities using logs!" With a twinkle in his eye, he launched into the **Azure Portal**, spun up a new **Storage Account** named `stcloudlabxlogs`, and made sure it had **Geo-Redundant Storage (GRS)** and the **Hot Access Tier**. Smooth start for a cloudy mission!

---

### 📦 Operation Blob Drop: Let the Upload Begin

Next, our TechWaveNaveed admin created a new container: **monitor-blobs-container**. He whipped up three test files—**sample1.txt**, **sample2.txt**, and **sample3.txt**—on his laptop. One by one, he uploaded them to the blob container, pacing himself like a suspense novelist dropping cliffhangers. A minute between uploads, because... well, metrics take their time to appear.

---

### 🕵️‍♂️ Enter Log Analytics: The Detective Desk

Naveed then built a **Log Analytics Workspace** named `MonitorLAWorkspace`, which he linked to his storage account via **Diagnostic Settings**. He selected **StorageRead** logs and sent them off to his shiny new workspace. “Now let’s see who’s been peeking at my blobs,” he joked, channeling his inner data detective.

---

### 🧙 Blob Activity Revealed with KQL Magic

To test the monitoring, our CloudOps engineer downloaded a blob file to trigger activity. Then he opened the **Logs** blade and ran a sleek **KQL query** on `StorageBlobLogs` to catch that sneaky download. Boom! It worked—logs showed when, who, and what file was touched. The **operation name**, **timestamp**, and **requester's ID**—all neatly logged like magic.

---

### ✅ Mission Complete: Data Watched, Logs Caught

With the monitoring setup verified and the logs in hand, Naveed wrapped up his work. “No sneaky downloads will go unnoticed again!” he smiled proudly. He deleted all resources like a responsible admin and logged off, ready to conquer the next cloud adventure with even sharper **Azure Storage** and **Log Analytics** skills.

---

### 🧠 What Did We Learn?

From blob uploads to **log diagnostics**, Naveed built an end-to-end **monitoring solution** that can help any organization gain visibility into **storage operations**. With tools like **Log Analytics**, **KQL**, and **diagnostic settings**, any admin—seasoned or new—can be a real cloud detective.

---

💡 **Key Concepts Highlighted**: **Storage Account**, **Blob Container**, **Log Analytics Workspace**, **Diagnostic Settings**, **KQL**, **StorageBlobLogs**, **Monitoring**, **Geo-redundant storage**, **Access Tier**, **Hot**, **StorageRead**, **GetBlob Operation**.

---
---
---
## Text-Based Diagram for the Lab: **"Monitor and Troubleshoot Azure Storage with Log Analytics"**

```plaintext
+-------------------------+
| 1. Naveed Logs In to   |
|    Azure Portal        |
+-------------------------+
            |
            v
+-------------------------+
| 2. Create Storage       |
|    Account              |
| - Name: stcloudlabxlogs |
| - Region: East US       |
| - GRS & Hot Tier        |
+-------------------------+
            |
            v
+-------------------------+
| 3. Create Container     |
| - Name: monitor-blobs-  |
|   container             |
+-------------------------+
            |
            v
+-------------------------+
| 4. Upload 3 Files       |
| - sample1.txt           |
| - sample2.txt           |
| - sample3.txt           |
| (With time intervals)   |
+-------------------------+
            |
            v
+-------------------------+
| 5. Create Log Analytics |
|    Workspace            |
| - Name: MonitorLAWorkspace |
+-------------------------+
            |
            v
+-----------------------------+
| 6. Create Diagnostic Setting|
| - Category: StorageRead     |
| - Send to: Log Analytics WS |
+-----------------------------+
            |
            v
+-------------------------+
| 7. Download a Blob File |
| - Triggers a log entry  |
+-------------------------+
            |
            v
+------------------------------+
| 8. Query Logs Using KQL      |
| - Table: StorageBlobLogs     |
| - Filter: GetBlob operations |
| - View: Time, URI, etc.      |
+------------------------------+
            |
            v
+---------------------------+
| 9. Confirm Logs Captured  |
+---------------------------+
            |
            v
+-------------------------+
| 10. Delete All Resources |
+-------------------------+
```

---

### 📘 **Diagram Summary**

This diagram shows how **Naveed**, the **Curious Cloud Explorer**, configured **Azure Storage monitoring** using **Log Analytics**. It walks through creating a **storage account**, uploading test blobs, setting up **diagnostic settings**, querying **StorageBlobLogs** with **KQL**, and validating monitoring outcomes. The flow illustrates how cloud admins can track blob access activities efficiently using **Azure-native tools**.

---
---
---
