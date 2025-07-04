# Lab 5: Create a Storage Account

**Duration:** 30m

---
---
---

### After logging in with your credentials:

#### **Task 1: Understand Performance, Redundancy, and Access Tiers**

1. Review the differences between **Standard** and **Premium** performance tiers for storage accounts.
2. Understand redundancy options:

   * **LRS**: Locally-redundant storage (3 replicas in one datacenter).
   * **ZRS**: Zone-redundant storage (replication across 3 availability zones).
   * **GRS**: Geo-redundant storage (replication to a secondary region).
   * **GZRS**: Geo-zone-redundant storage (combines ZRS + GRS).
3. Learn about blob **access tiers**:

   * **Hot**: Frequently accessed data.
   * **Cool**: Infrequently accessed data (minimum 30 days).
   * **Cold**: Rarely accessed data (minimum 90 days).
   * **Archive**: Can be set after blob creation, not at the time of account creation.

---

#### **Task 2: Create a Storage Account**

1. Search for and select **Storage accounts** in the Azure portal.
2. Click **+ Create** to start creating a new storage account.
3. In the **Basics** tab, enter the following:

   * Resource Group: Select an existing group (e.g., `rg_eastus_XXXXX`)
   * Storage Account Name: `mystorageacc[yourname]`
   * Region: `East US`
   * Performance: `Standard`
   * Redundancy: `Locally-redundant storage (LRS)`
4. Leave remaining settings as default.
5. Click **Review + Create**, then click **Create**.

---

#### **Task 3: Create a Blob Container**

1. Go to the newly created storage account.
2. Under **Data Storage**, select **Containers**.
3. Click **+ Container**, enter the name `mycontainer25`, and click **Create**.

---

#### **Task 4: Upload a Blob Object**

1. On your local machine, create an HTML file:

   * Open Notepad and enter `<h1>This is a sample document!</h1>`.
   * Save the file as `sample.html`.
2. In the Azure portal, navigate to your container (`mycontainer25`) and click **Upload**.
3. Browse to the `sample.html` file and upload it.

---

#### **Task 5: Create a File Share**

1. In the same storage account, select **File shares** under **Data storage**.
2. Click **+ File share**.
3. Name the share `myfile123`, choose the **Hot** access tier, and click **Create**.

---

#### **Task 6: Upload a File to File Share**

1. Open the `myfile123` file share.
2. Click **Upload**, select any file from your local system, and upload it.

---

Delete all the resources.

---
---
---

## **Lab Summary: Creating and Managing an Azure Storage Account**

### **Purpose of the Lab**

The purpose of this lab is to provide hands-on experience in creating and managing an **Azure Storage Account**, configuring its **performance**, **redundancy**, and **access tiers**, and working with its components such as **blob containers** and **file shares**. Learners will understand the practical use of **Azure Storage** for hosting structured and unstructured data, managing lifecycle policies, and preparing storage infrastructure suitable for enterprise workloads.

---

### **Azure Tools and Services Used**

1. **Azure Portal**
   A web-based management interface used to access and manage **Azure services**. In this lab, it serves as the primary tool for deploying and configuring the **storage account**, **containers**, and **file shares**.

2. **Storage Account**
   A fundamental building block in **Azure Storage**, it provides a namespace to store data objects like **blobs**, **files**, **queues**, and **tables**. This lab walks through creating a storage account with selected configurations.

3. **Performance Tiers**
   Determines the speed and workload suitability:

   * **Standard**: Backed by magnetic drives, optimized for general-purpose workloads.
   * **Premium**: Backed by solid-state drives (SSD), optimized for low-latency applications.

4. **Redundancy Options**
   Critical for durability and high availability of data:

   * **LRS (Locally Redundant Storage)**: Replicates data within a single data center.
   * **ZRS (Zone-Redundant Storage)**: Replicates data across multiple availability zones in a region.
   * **GRS (Geo-Redundant Storage)**: Combines LRS with asynchronous replication to a secondary region.
   * **GZRS (Geo-Zone Redundant Storage)**: Combines ZRS with GRS for maximum availability and disaster recovery.

5. **Access Tiers (for Blob Storage)**
   Used to optimize cost based on data usage patterns:

   * **Hot Tier**: For frequently accessed data.
   * **Cool Tier**: For infrequently accessed data, stored for at least 30 days.
   * **Cold Tier**: For rarely accessed data, stored for at least 90 days.
   * **Archive Tier**: For long-term storage, must be set after data upload.

6. **Containers**
   Logical units within a **storage account** for storing **blob objects**. In this lab, a **container** is created to upload a sample HTML file.

7. **Blob Storage**
   **Azure Blob Storage** is used for storing large amounts of unstructured data. This lab includes the creation of a simple **blob object**.

8. **File Shares**
   Part of **Azure Files**, allowing creation of **SMB-compatible file shares** in the cloud. The lab covers creating a file share and uploading a file to it.

9. **Upload Operations**
   Demonstrates how to upload data (HTML file and general file) into **Azure Storage** via the portal, simulating common file ingestion scenarios.

---

By completing this lab, learners develop practical understanding of **Azure Storage capabilities**, how to configure and optimize them for different workloads, and how they integrate with broader **cloud architecture** for scalable, secure, and resilient storage solutions.

---
---
---
### **Scenario: Implementing Azure Storage for Business Continuity at Contoso Ltd.**

**Contoso Ltd.**, a mid-sized digital services company, recently decided to migrate its file storage and document hosting services to the cloud for better **scalability**, **security**, and **cost management**. Sarah, a **Cloud Engineer**, was tasked with setting up the required **Azure Storage** infrastructure to support internal team collaboration and application-level storage needs.

---

### **Step-by-Step Use Case**

After logging in with her credentials, Sarah begins configuring the cloud storage environment.

#### **Step 1: Understand Storage Requirements**

Sarah first reviews the types of **Azure Storage performance tiers** and **redundancy models**. Since the application deals with frequently accessed documents and doesn't require premium speed, she opts for the **Standard performance** tier. To ensure cost-effective redundancy within a single region, she chooses **Locally-redundant storage (LRS)**.

She also notes the available **access tiers**:

* **Hot** for frequently accessed data.
* **Cool** for infrequently accessed data.
* **Cold** for rarely accessed data with longer retention.
  These access tiers will help manage costs across different storage use cases.

---

#### **Step 2: Create a Storage Account**

Using the **Azure Portal**, Sarah navigates to **Storage accounts** and creates a new account named **mystorageaccsarah** under the company’s resource group. She configures it with **Standard performance**, **East US region**, and **LRS redundancy**, leaving other settings default. This account will serve as the base for managing files and blobs.

---

#### **Step 3: Create a Container for Blob Storage**

Next, Sarah creates a **container** named **mycontainer25**. This will be used to store **blob objects** like HTML files, PDFs, and images that the team shares through internal tools.

---

#### **Step 4: Upload a Blob Object**

Sarah creates a simple **HTML** file on her local machine and uploads it into the blob container using the **Upload** feature. This file could represent documentation or a static web resource accessed via other Azure services or users with proper access.

---

#### **Step 5: Create a File Share**

For teams that need traditional shared drives, Sarah creates an **Azure File Share** named **myfile123** in the **Hot tier**. This allows users to mount the file share from virtual machines or on-premises systems using **SMB protocol**.

---

#### **Step 6: Upload Files to File Share**

Sarah uploads a sample **spreadsheet** to the file share, which users in the finance team will use collaboratively. This file could later be accessed directly through mapped network drives or integrated applications.

---

### **Business Impact**

By completing this setup:

* Sarah enables secure, cloud-based file hosting with **redundancy**.
* Teams can collaborate in real-time with **file shares**.
* Developers and apps can retrieve static content through **blob containers**.
* Costs are controlled through thoughtful selection of **tiers** and **replication** options.

This foundational setup supports Contoso’s move toward a modern, cloud-native infrastructure while maintaining business continuity and cost efficiency.

---

**Delete all the resources.**

---
---
---
## Lab-Based Conceptual MCQs

### 1. What is the primary use case of an **Azure Storage Account**?

**(a)** Running virtual machines  
**(b)** Hosting databases  
**(c)** Storing structured and unstructured data  
**(d)** Managing user authentication  

**✅ Correct answer: (c)**  
**Explanation**: An **Azure Storage Account** is designed to hold data objects like **blobs**, **files**, **queues**, and **tables**, making it ideal for storing both structured and unstructured data.

---

### 2. Which **redundancy option** offers protection against regional failures?

**(a)** **LRS**  
**(b)** **ZRS**  
**(c)** **GRS**  
**(d)** **Standard**  

**✅ Correct answer: (c)**  
**Explanation**: **Geo-Redundant Storage (GRS)** replicates data to a secondary region, providing durability during regional outages.

---

### 3. What is the function of a **container** in **Azure Blob Storage**?

**(a)** To store network policies  
**(b)** To manage user access  
**(c)** To logically group blob objects  
**(d)** To manage VM snapshots  

**✅ Correct answer: (c)**  
**Explanation**: A **container** organizes **blob objects** within a **storage account**, similar to how folders organize files.

---

### 4. Which **access tier** is best suited for data that is accessed frequently?

**(a)** **Cool**  
**(b)** **Hot**  
**(c)** **Archive**  
**(d)** **Cold**  

**✅ Correct answer: (b)**  
**Explanation**: The **Hot tier** is optimized for frequent data access and provides low-latency and high-throughput.

---

### 5. Why would an organization choose **ZRS** over **LRS**?

**(a)** To reduce cost  
**(b)** To increase performance  
**(c)** To provide zone-level fault tolerance  
**(d)** To enable serverless compute  

**✅ Correct answer: (c)**  
**Explanation**: **Zone-Redundant Storage (ZRS)** replicates data across availability zones, improving resilience to zone failures.

---

### 6. What must be created in order to store **blob data** within a **storage account**?

**(a)** A file share  
**(b)** A container  
**(c)** A queue  
**(d)** A disk  

**✅ Correct answer: (b)**  
**Explanation**: **Blob data** must be stored inside a **container**, which resides within a **storage account**.

---

### 7. What distinguishes the **Archive** tier from other access tiers?

**(a)** It provides faster retrieval  
**(b)** It requires no replication  
**(c)** It offers the lowest storage cost  
**(d)** It is the default setting  

**✅ Correct answer: (c)**  
**Explanation**: The **Archive tier** is intended for long-term storage and is priced lower than **Hot**, **Cool**, or **Cold** tiers due to slower access times.

---

### 8. In the context of **Azure File Shares**, what is the purpose of uploading a file?

**(a)** To trigger an Azure Function  
**(b)** To monitor traffic  
**(c)** To share data using SMB protocol  
**(d)** To assign RBAC roles  

**✅ Correct answer: (c)**  
**Explanation**: **Azure File Shares** allow data to be shared across machines using the **SMB protocol**, making it suitable for legacy app compatibility.

---

### 9. What determines the geographic location of stored data in a **storage account**?

**(a)** Storage key  
**(b)** Access policy  
**(c)** Selected region during account creation  
**(d)** Container name  

**✅ Correct answer: (c)**  
**Explanation**: When creating a **storage account**, the user selects the **region**, which dictates where the data will be physically stored.

---

### 10. Why might an organization change the **performance tier** of a storage account?

**(a)** To change authentication methods  
**(b)** To reduce storage capacity  
**(c)** To meet latency or IOPS requirements  
**(d)** To upgrade the subscription  

**✅ Correct answer: (c)**  
**Explanation**: **Premium tiers** are chosen when low-latency and high-input/output workloads are needed, making them suitable for performance-critical apps.

---
