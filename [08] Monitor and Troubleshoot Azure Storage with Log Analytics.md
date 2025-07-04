# Lab 8: Monitor and Troubleshoot Azure Storage with Log Analytics

**Duration:** 1h 0m
---
**After logging in with your credentials:**

### 1. Create a Storage Account

1. In the portal search bar, enter **Storage accounts** and select it.
2. Click **Create**.
3. In the **Basics** tab:

   * Choose the available **Subscription**.
   * Select the available **Resource group**.
   * Enter a unique **Storage account name** (lowercase letters and numbers only).
   * Choose the default **Region**.
   * Set **Performance** to **Standard**.
   * Set **Redundancy** to **Geo-redundant storage (GRS)**.
4. Go to the **Advanced** tab and ensure the **Access tier** is set to **Hot**.
5. Click **Review + create**, then **Create**.
6. Once deployment completes, select **Go to resource**.

---

### 2. Add a Blob Container

1. In the storage account, under **Data storage**, select **Containers**.
2. Click **+ Container**.
3. Name the container **monitor-blobs-container**.
4. Leave other settings at default and click **Create**.

---

### 3. Upload Files to the Blob Container

1. On your local computer, create three text files:

   * `sample1.txt`:

     ```
     Sample File 1 - Blob Monitoring Test  
     This is a test file for upload.
     ```
   * `sample2.txt`:

     ```
     Sample File 2 - Blob Monitoring Test  
     This is another test file for upload.
     ```
   * `sample3.txt`:

     ```
     SampleFile3-BlobMonitoringTest  
     This is another test file for upload.
     ```
2. In the Azure portal, return to **monitor-blobs-container**.
3. Click **Upload** and upload `sample1.txt`.
4. Wait 1 minute, then upload `sample2.txt`.
5. Wait another minute, then upload `sample3.txt`.
6. Wait a few additional minutes to ensure metrics are recorded.

---

### 4. Create a Log Analytics Workspace

1. Search for and select **Log Analytics workspaces**.
2. Click **+ Create**.
3. In the **Basics** tab:

   * Choose the same **Subscription** and **Resource group**.
   * Enter a name like **MonitorLAWorkspace**.
   * Use the default **Region**.
4. Click **Review + create**, then **Create**.

---

### 5. Create a Diagnostic Setting for the Storage Account

1. Open your **Storage account**.
2. Under **Monitoring**, click **Diagnostic settings**.
3. Select the **blob** service if prompted.
4. Click **+ Add diagnostic setting**.
5. Provide a name (e.g., `BlobStorageDiagnostics`).
6. Under **Categories**, select **StorageRead**.
7. Under **Destination**, select **Send to Log Analytics workspace** and choose **MonitorLAWorkspace**.
8. Click **Save**.

---

### 6. Download a Blob to Generate Activity

1. Open **Containers** in the storage account.
2. Select **monitor-blobs-container**.
3. Locate one of the uploaded files.
4. Click the **ellipsis (...)** next to the file and choose **Download**.

---

### 7. View Logged Activity with Log Analytics

1. In the storage account, under **Monitoring**, click **Logs**.
2. Close the **Queries hub**.
3. Switch to **KQL mode**.
4. Paste the following query:

   ```kusto
   StorageBlobLogs
   | where TimeGenerated > ago(1h) and OperationName == "GetBlob"
   | project TimeGenerated, AuthenticationType, RequesterObjectId, OperationName, Uri
   ```
5. Click **Run**.
6. View the results to confirm that the download was logged.

---

**Delete all the resources.**

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

