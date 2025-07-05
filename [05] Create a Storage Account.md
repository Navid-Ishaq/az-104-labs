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

## 🌍 Real-World Scenario: Building Smart Cloud Storage with Precision

**Meet Naveed**, the **Curious Cloud Explorer** at a data-driven startup called **DataNest Labs**. The company is preparing to launch a new internal tool that handles both **frequently accessed reports** and **archived compliance data**. As the lead on the cloud infrastructure team, Naveed is exploring ways to **organize files intelligently**, **control costs**, and **ensure high availability** — all using **Azure Storage services**.

---

### 🛠️ Step 1: Laying the Groundwork – Understanding Storage Options

Before creating anything, Naveed dives into the **Azure Storage account** settings to understand the different **performance tiers** and **redundancy models**.

* He learns that **Standard** storage is great for cost efficiency, while **Premium** storage offers high-speed IOPS.
* For redundancy, he evaluates options like **LRS**, **ZRS**, **GRS**, and **GZRS**, weighing the balance between **availability**, **resiliency**, and **cost**.
* He also notes the **access tiers**: **Hot**, **Cool**, **Cold**, and **Archive**, and how they influence **storage cost vs. access frequency**.

✅ **Why it matters**: This knowledge helps Naveed **make smart decisions** about where to store which kind of data — a critical task when optimizing for performance and budget.

---

### 📦 Step 2: Creating a Storage Account

Naveed opens the **Azure Portal**, searches for **Storage accounts**, and begins the creation process:

* He places it in the resource group **rg\_eastus\_xyz**
* Names the account **mystorageaccnaveed**
* Chooses **East US** as the **region**
* Selects **Standard performance** and **Locally-redundant storage (LRS)** for reliability at low cost

✅ **Why this step is important**: The **storage account** acts as the **container hub** for all kinds of Azure storage — **blobs**, **files**, **queues**, and **tables**. It's the foundation of cloud-based data operations.

---

### 📂 Step 3: Organizing Data with a Blob Container

Naveed creates a **blob container** named **mycontainer25** under the storage account. This container will hold **web assets**, **documents**, or **logs** that need structured access and categorization.

He then uploads a **sample HTML file** (`sample.html`) to test the blob upload feature.

✅ **Business value**: Blob containers make it easy to manage and control access to unstructured data like documents, images, and backups, especially for **web hosting** or **data lakes**.

---

### 📁 Step 4: Setting Up File Shares for Collaboration

To enable **team collaboration**, Naveed moves on to **Azure File Share**:

* He creates a file share named **myfile123**
* Assigns the **Hot access tier**, knowing that the team will use these files daily
* Uploads a sample file to ensure it's functional

✅ **Why this is relevant**: With **Azure File Shares**, teams can **mount cloud storage as a network drive**, enabling cross-location collaboration with no physical hardware.

---

### 💼 Business Impact

By completing these steps, **Naveed** has:

* Built a **cost-effective**, **highly available** storage environment
* Set up the tools for both **frequent access** and **long-term archiving**
* Laid the groundwork for **secure**, **scalable**, and **departmentalized** data management

Whether it's for app development, business continuity, or compliance, **Azure Storage** gives organizations the **flexibility to handle all data scenarios**.

---
---
---
## Comic-Style Summary: **“Storage Sorted, Cloud Smart!”**

### 🚀 Meet the Curious Cloud Explorer

**Naveed**, the ever-curious and eager-to-learn **Cloud Explorer**, was handed a task: set up cloud storage for a growing company. With scattered files and rising costs, it was time to bring **order to chaos** — using nothing but **Azure Storage tools** and a smart plan.

---

### 🧱 Step 1: Know Before You Build

Naveed didn’t just jump in. First, he explored the **performance tiers** like **Standard** vs. **Premium**, and learned the difference between **LRS**, **ZRS**, **GRS**, and **GZRS**. He also understood **access tiers** like **Hot**, **Cool**, and **Archive**.

**Why?** So that he could pick the **right mix of performance, resilience, and cost-efficiency** for his company’s storage needs.

---

### 🏗️ Step 2: Create the Storage Account

Next, our explorer set up a **storage account** in **East US**, named it **mystorageaccnaveed**, and selected **Standard performance** with **Locally-redundant storage (LRS)**. With just a few clicks, he laid the **foundation** for all future storage operations.

**Mission?** ✅ Build a reliable home for company files.

---

### 📦 Step 3: Blob It Like a Pro

Inside the account, he created a **blob container** called **mycontainer25**. He even uploaded a fun HTML file (`sample.html`) to test it.

**Cool move!** This showed how **unstructured files** (like documents or media) could be neatly stored and accessed — even for future web-based tools.

---

### 📁 Step 4: File Sharing Made Easy

Naveed then created a **file share** named **myfile123** with the **Hot tier**, perfect for frequently accessed team files. He uploaded a sample file to verify everything was working smoothly.

**Lesson?** Now the team could work together, using **cloud-based file shares**, just like a traditional network drive!

---

### 🎯 The Final Word

Yes! **Naveed successfully completed his mission**. He not only set up storage — he did it with **clarity**, **efficiency**, and **a learner's curiosity**.

By exploring Azure Storage options and building smart from the start, our **Curious Cloud Explorer** helped his team save **time**, **money**, and **future headaches**.

✅ **Cloud storage? Sorted.** 
✅ **Learner journey? Leveled up.**

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
---
---
## Professional Job Interview Questions – **Create a Storage Account**

## Lab-Based Conceptual MCQs

1. **Naveed**, the Curious Cloud Explorer, needs to store frequently accessed files for his team using Azure Storage. Which **blob access tier** should he choose to ensure optimal performance at a reasonable cost?

   - (a) **Cool**
   - (b) **Hot**
   - (c) **Archive**
   - (d) **Cold**

   **Correct answer: (b)**  
   The **Hot** tier is best for frequently accessed data. It provides low latency and high throughput access, ideal for active workloads.

2. When creating a new storage account, **Naveed** chooses **Locally-redundant storage (LRS)**. What does this redundancy option provide?

   - (a) Replication across three regions globally  
   - (b) Backup to an on-premises server  
   - (c) Three replicas within a single Azure datacenter  
   - (d) Replication to another availability zone in the same region

   **Correct answer: (c)**  
   **LRS** ensures that three copies of the data are maintained within a **single datacenter**, offering protection from hardware failures.

3. Which Azure service allows **Naveed** to store HTML, images, and documents in a flat namespace and access them over HTTP/S?

   - (a) **File Share**
   - (b) **Blob Storage**
   - (c) **SQL Database**
   - (d) **Table Storage**

   **Correct answer: (b)**  
   **Blob Storage** is optimized for storing unstructured data like HTML files and documents, and can be accessed via HTTP/S.

4. Why would **Naveed** use the **Hot tier** when creating a file share in Azure Storage?

   - (a) For rarely accessed archival data  
   - (b) To reduce write speeds  
   - (c) For frequently accessed files with higher performance needs  
   - (d) To save cost on network throughput

   **Correct answer: (c)**  
   The **Hot** tier is suitable for **frequently accessed data**, offering faster access times though at a slightly higher cost.

5. **Naveed** uploads a file to a **blob container** named `mycontainer25`. What must be true for users to **publicly access** that file?

   - (a) The storage account must use Premium performance  
   - (b) A container-level access policy must be set to allow public access  
   - (c) A virtual machine must be linked  
   - (d) Tags must be enabled on the storage account

   **Correct answer: (b)**  
   Public access to blobs requires the **container** to be configured with the correct **access level policy**, such as container or blob level.

6. **Naveed** is deciding between **Standard** and **Premium** performance tiers for his Azure Storage account. When is **Premium** performance most appropriate?

   - (a) For archiving backup files  
   - (b) For workloads needing low latency and high IOPS  
   - (c) For saving cost on rarely used files  
   - (d) For compliance-related metadata tagging

   **Correct answer: (b)**  
   **Premium** performance is best for workloads with **high transaction rates or low latency requirements**, like transactional systems.

7. Which of the following is **not** a valid Azure Storage redundancy option?

   - (a) **GZRS**  
   - (b) **LRS**  
   - (c) **ZRS**  
   - (d) **TRS**

   **Correct answer: (d)**  
   **TRS** is not a recognized Azure storage redundancy model. Valid options include **LRS**, **ZRS**, **GRS**, and **GZRS**.

8. While configuring a file share, **Naveed** selects the **Hot tier**. What is one **limitation** he should be aware of?

   - (a) Files cannot be encrypted  
   - (b) Cannot upload large files  
   - (c) Higher cost per GB compared to Cool or Archive  
   - (d) Access only from the Azure CLI

   **Correct answer: (c)**  
   The **Hot** tier provides faster access but comes with **higher storage costs per GB** compared to **Cool** or **Archive** tiers.

9. In the Azure portal, **Naveed** selects **Containers** under Data Storage. What is the **primary use** of this feature?

   - (a) To store structured database tables  
   - (b) To enable long-term log file retention  
   - (c) To manage and organize **blob data**  
   - (d) To replicate storage accounts across regions

   **Correct answer: (c)**  
   **Containers** are used in **Blob Storage** to logically group **blob objects**, allowing better organization and access control.

10. After uploading a file to a file share, **Naveed** wants to allow his team to access it. What must he configure?

   - (a) Assign RBAC to a SQL server  
   - (b) Create a private endpoint to the blob container  
   - (c) Share the UNC path of the file share  
   - (d) Configure a NAT gateway

   **Correct answer: (c)**  
   To allow access to a file share, the standard practice is to **share the UNC path** and ensure **appropriate permissions** are in place.

11. Why can **Naveed** not select the **Archive** tier during the initial storage account setup?

   - (a) It's not supported in East US  
   - (b) It can only be set **after** blob creation  
   - (c) It requires Premium performance  
   - (d) It only works with table storage

   **Correct answer: (b)**  
   The **Archive** tier is **not available at storage account creation**. It can be applied **only to individual blobs after upload**.

12. How does choosing **Geo-redundant storage (GRS)** benefit disaster recovery strategies?

   - (a) Encrypts the data on local disks  
   - (b) Replicates data across multiple subscriptions  
   - (c) Replicates data to a secondary **region**  
   - (d) Disables blob-level tiering

   **Correct answer: (c)**  
   **GRS** replicates your data to a **secondary geographic region**, ensuring **business continuity** in case of a regional outage.

---
---
---
## Professional Job Interview Questions – Create a Storage Account

1. **Naveed**, the **Curious Cloud Explorer**, is tasked with storing frequently accessed documents for the marketing team in Azure. Which **blob access tier** should he select for optimal performance?
   - (a) **Cool**
   - (b) **Hot**
   - (c) **Archive**
   - (d) **Cold**  
   **Correct answer: (b)**  
   **Explanation**: The **Hot** tier is optimized for data that is accessed frequently, making it ideal for actively used files.

2. While creating a **storage account**, Naveed must ensure low-cost, highly durable data replication within a single datacenter. Which **redundancy option** should he choose?
   - (a) **GRS**
   - (b) **ZRS**
   - (c) **LRS**
   - (d) **GZRS**  
   **Correct answer: (c)**  
   **Explanation**: **Locally-redundant storage (LRS)** replicates data three times within a single datacenter, offering a cost-effective redundancy solution.

3. Naveed wants to upload an HTML file to the cloud for sharing internally. Which **Azure storage service** should he use?
   - (a) **File Share**
   - (b) **Blob Container**
   - (c) **Queue Storage**
   - (d) **Table Storage**  
   **Correct answer: (b)**  
   **Explanation**: A **Blob Container** is ideal for storing unstructured data such as documents, images, or HTML files.

4. To organize and share documents across departments, Naveed needs a structure similar to a shared drive. Which Azure feature should he implement?
   - (a) **Blob Container**
   - (b) **File Share**
   - (c) **Virtual Network**
   - (d) **Key Vault**  
   **Correct answer: (b)**  
   **Explanation**: **Azure File Share** provides a shared file system accessible from Windows, Linux, and macOS.

5. Naveed is testing a rarely accessed dataset for long-term archival. Which **blob tier** should he apply to minimize costs?
   - (a) **Cool**
   - (b) **Archive**
   - (c) **Hot**
   - (d) **Premium**  
   **Correct answer: (b)**  
   **Explanation**: The **Archive** tier is best for data that is rarely accessed and stored for a long period.

6. What is a valid reason for Naveed to choose **Standard SSD** for the OS disk of the VM in this lab?
   - (a) Highest performance needed
   - (b) Cost-effective performance for general workloads
   - (c) Replication across regions
   - (d) Requirement for bursting capability  
   **Correct answer: (b)**  
   **Explanation**: **Standard SSD** offers a balance between performance and cost, suitable for typical workloads.

7. Naveed needs to ensure that data uploaded to his storage account is stored in a region with multiple datacenter zones. Which **redundancy option** meets this requirement?
   - (a) **LRS**
   - (b) **ZRS**
   - (c) **GRS**
   - (d) **Archive**  
   **Correct answer: (b)**  
   **Explanation**: **Zone-redundant storage (ZRS)** replicates data across multiple availability zones within a region.

8. What is a limitation of the **Archive** blob tier that Naveed should be aware of?
   - (a) Cannot store metadata
   - (b) Must be set during account creation
   - (c) Has a minimum storage duration of 90 days
   - (d) Cannot be used for images  
   **Correct answer: (c)**  
   **Explanation**: The **Archive** tier is designed for long-term storage with a minimum 90-day retention.

9. If Naveed wants to set different storage options for backup, which Azure storage feature allows defining policies and lifecycle rules?
   - (a) **Access tiers**
   - (b) **Azure Policy**
   - (c) **Storage lifecycle management**
   - (d) **Disk encryption**  
   **Correct answer: (c)**  
   **Explanation**: **Lifecycle management** in Azure Storage lets you define rules to automatically move data between tiers or delete it.

10. Why might Naveed use the **Cool** access tier for certain blobs in his storage account?
    - (a) To enable real-time analytics
    - (b) To lower costs for infrequently accessed data
    - (c) To prevent accidental deletions
    - (d) To encrypt the data at rest  
    **Correct answer: (b)**  
    **Explanation**: The **Cool** tier is designed for data that is not accessed frequently, offering lower storage costs with slightly higher access costs.

---
---
---
## Comic-Style Summary: **“From Bytes to the Cloud: Naveed’s Storage Quest!”**

---

### **🚀 Meet Naveed – The Curious Cloud Explorer**

Naveed, always eager to learn something new, was handed a new mission — to explore **Azure Storage Accounts**. With his explorer’s cap on (figuratively!), he logged into the **Azure Portal**, ready to create a cloud home for files, blobs, and more. His goal? Understand the storage types, access tiers, and create an organized system.

---

### **🏗️ Building the Storage Account Base**

He first launched into the **Storage accounts** section and created a new account called **mystorageacc**. He picked **Standard performance** for balanced speed and cost, and chose **Locally Redundant Storage (LRS)** to keep three safe copies of every file in a single data center. Naveed smiled — **mission base established!**

---

### **🪣 Blob Container? More Like a Magic Bucket!**

Next, our Curious Cloud Explorer moved on to **Blob Storage**. He created a container named **mycontainer25**, kind of like a big online bucket. Then, like a proud digital artist, he wrote a mini HTML file on his laptop and uploaded it into the blob. “That’s my little cloud webpage,” he chuckled.

---

### **📂 Let’s Get File-Sharing Friendly**

Naveed wasn’t done yet. He clicked on **File Shares** and created **myfile123** with the **Hot access tier**, perfect for frequently accessed data. He uploaded a random file from his desktop — it was a family recipe, but hey, even the cloud deserves good food!

---

### **🌈 What Naveed Learned**

By the end, Naveed saw how **storage accounts**, **blob containers**, **file shares**, and **access tiers** all play roles in smart cloud organization. Now he knows how to align storage choices with real-world needs — whether it's for cost-saving, performance, or secure access.

And with that, Naveed closed his laptop, grinning: “Cloud storage? Cracked it!”

---

✅ **Key Concepts Covered**:
**Storage Accounts**, **Redundancy Options**, **Blob Storage**, **Access Tiers**, **File Shares**, and real-world decision-making by a **Curious Cloud Explorer**!

---
---
---
## Text-Based Diagram for the Lab: "Create a Storage Account"

```plaintext
Start
  │
  ├──▶ Login to Azure Portal
  │
  ├──▶ ⬇️ Task 1: Understand Key Concepts
  │      ├─ Review **Performance tiers** (Standard vs Premium)
  │      ├─ Learn **Redundancy options** (LRS, ZRS, GRS, GZRS)
  │      └─ Understand **Blob access tiers** (Hot, Cool, Cold, Archive)
  │
  ├──▶ ⬇️ Task 2: Create a Storage Account
  │      ├─ Go to **Storage accounts**
  │      ├─ Click **+ Create**
  │      ├─ Configure:
  │      │    ├─ **Resource Group**
  │      │    ├─ **Storage Account Name**
  │      │    ├─ **Region: East US**
  │      │    ├─ **Performance: Standard**
  │      │    └─ **Redundancy: LRS**
  │      └─ Click **Review + Create → Create**
  │
  ├──▶ ⬇️ Task 3: Create a Blob Container
  │      ├─ Navigate to newly created storage account
  │      ├─ Go to **Containers**
  │      └─ Create **mycontainer25**
  │
  ├──▶ ⬇️ Task 4: Upload a Blob
  │      ├─ Create **sample.html** locally
  │      └─ Upload file into **mycontainer25**
  │
  ├──▶ ⬇️ Task 5: Create a File Share
  │      ├─ Go to **File shares**
  │      └─ Create **myfile123** (Hot tier)
  │
  ├──▶ ⬇️ Task 6: Upload File to File Share
  │      └─ Upload any local file into **myfile123**
  │
  └──▶ Delete all the resources
End
```

---

**Summary**:
This diagram outlines the complete process for the lab **"Create a Storage Account"**, showing each task from setting up a **storage account**, creating and managing a **blob container**, and working with **file shares**. It introduces important cloud storage concepts like **redundancy**, **performance tiers**, and **access tiers**, all while helping a beginner grasp how to navigate and implement these components step by step using the **Azure Portal**.

---
---
---
