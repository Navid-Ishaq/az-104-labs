# Lab 9: Create an SMB Azure file share and connect it to a Windows VM using the Azure portal

**Duration:** 1h 0m

---
---
---

**After logging in with your credentials:**

### 1. Create a Storage Account

1. Navigate to **Storage accounts**.
2. Click **+ Create**.
3. In the **Basics** tab, enter the following:

   * Storage account name: a globally unique name.
   * Region: **East US**.
   * Performance: **Standard**.
   * Redundancy: **Locally redundant storage (LRS)**.
4. Leave other settings as default.
5. Click **Review** and then **Create**.

### 2. Create a File Share

1. Once deployment completes, click **Go to resource**.
2. Select **File shares** from the side menu.
3. Click **+ File share**.
4. Enter name as `qsfileshare`.
5. Keep **Transaction optimized** tier selected.
6. In the **Backup** tab, disable backup if enabled.
7. Click **Review + Create**, then **Create**.

### 3. Upload a File to File Share

1. Create a `.txt` file named `qsTestFile.txt` on your local machine.
2. Open the file share `qsfileshare`.
3. Click **Upload**.
4. Browse and select the `qsTestFile.txt`, then click **Upload**.

### 4. Deploy a Virtual Machine

1. In the search bar, type **Virtual machines** and select it.
2. Click **+ Create** > **Azure virtual machine**.
3. In the **Basics** tab:

   * Resource group: use existing one.
   * Name: your VM name.
   * Region: **East US**.
   * Availability: No infrastructure redundancy.
   * Security type: **Standard**.
   * Image: **Windows Server 2019 Datacenter – x64 Gen2**.
   * Size: **Standard B2s**.
   * Administrator account: set username and password.
   * Inbound ports: **RDP**, **HTTP**.
4. Go to **Disks** tab, select OS disk type as **Standard SSD**.
5. Click **Review + Create**, then **Create**.
6. After deployment, click **Go to resource**.

### 5. Connect to the VM

1. In the VM overview page, click **Connect**.
2. Under **RDP**, click **Download RDP file**.
3. Open the RDP file and click **Connect**.
4. Choose **Use a different account**.
5. Enter the VM credentials and log in.
6. Accept certificate warning if prompted.

### 6. Map Azure File Share to the VM

1. In Azure portal, navigate to the `qsfileshare`.
2. Click **Connect**.
3. Select a **Drive letter**, then click **Show script**.
4. Copy the PowerShell script.
5. In the VM, open **PowerShell**.
6. Paste and run the script to map the file share.

### 7. Create a Share Snapshot

1. In Azure portal, go to the file share `qsfileshare`.
2. Click **Snapshots**.
3. Click **+ Add snapshot**, then **OK**.
4. In the VM, open `qsTestFile.txt` from the mapped drive.
5. Add the line: `this file has been modified`, then save and close.
6. Return to portal and create another snapshot.

### 8. Browse a Snapshot

1. Go to the file share and click **Snapshots**.
2. Open the first snapshot in the list.
3. Open `qsTestFile.txt` to view its content.

### 9. Restore a File from Snapshot

1. In Snapshots tab, right-click `qsTestFile.txt`.
2. Click **Restore**, select **Overwrite original file**, and click **OK**.
3. In VM, verify the file is reverted to its original state.

### 10. Delete a Snapshot

1. Go to the storage account and open **Settings > Locks**.
2. Delete any locks if present.
3. Go back to file share > **Snapshots**.
4. Select the latest snapshot and click **Delete**.

### 11. View Previous Versions on VM

1. In the VM, open **File Explorer**, go to the mapped drive.
2. Right-click `qsTestFile.txt`, select **Properties**.
3. Go to **Previous Versions** tab.
4. Select a version and click **Open**.

### 12. Restore from Previous Version

1. In the **Previous Versions** tab, click **Restore**.

**Delete all the resources.**

---
**🔹 Structured Summary of Azure Lab: Create an SMB Azure File Share and Connect it to a Windows VM**

---
---
---

## **Structured Lab Summary – Azure Lab 9: Connect File Shares Like a Pro**

### 🎯 **Purpose of the Lab**

This lab demonstrates how to **create an SMB-compatible Azure File Share**, map it to a **Windows Virtual Machine**, and manage **snapshots** for **backup and restore** purposes. The goal is to simulate a real-world scenario where an organization uses **Azure Files** for shared storage across **VMs**, improving manageability, availability, and disaster recovery.

---

### 🔧 **Azure Tools and Services Used**

#### 1. **Azure Storage Account**

* **Definition**: A scalable container for storing structured and unstructured data such as blobs, files, queues, tables, and disks.
* **Role in Lab**: Used to host the **Azure File Share**, which supports SMB protocol for sharing files across cloud or hybrid environments.
* **Example**: `stcloudtrainprofiles01` under `rg-learntech-naveed`.

---

#### 2. **Azure File Share**

* **Definition**: A fully managed file share in the cloud that uses the **SMB** (Server Message Block) protocol.
* **Role in Lab**: Acts as a network file system, which is later **mounted** to a Windows VM for file access and collaboration.
* **Example**: A file share named `qsfileshare` is created for uploading and sharing files.

---

#### 3. **Azure Virtual Machine**

* **Definition**: An on-demand, scalable computing resource hosted on Azure that allows you to run Windows or Linux-based applications.
* **Role in Lab**: A **Windows Server 2019 VM** is deployed to map and access the file share, simulating a typical file-server client interaction.
* **Example**: VM named `vm-ncloudedge-win01` running under the same resource group.

---

#### 4. **PowerShell Script (Mounting Script)**

* **Definition**: A command-line script used to map a network drive on Windows using the SMB protocol.
* **Role in Lab**: Enables the Azure File Share to be **mapped as a drive** on the deployed VM using credentials.
* **Example**: Script provided by the portal and executed in the VM’s **PowerShell console**.

---

#### 5. **Snapshots in Azure Files**

* **Definition**: Point-in-time backups of file shares or individual files, allowing users to **restore previous states** if needed.
* **Role in Lab**: Used to test **data recovery and file versioning** by taking snapshots before and after modifying a file.
* **Example**: Snapshots created after uploading `qsTestFile.txt` and after modifying its contents inside the VM.

---

#### 6. **File Explorer – Previous Versions**

* **Definition**: A native Windows feature that integrates with SMB shares to display and restore **older versions** of a file.
* **Role in Lab**: Allows the user to **revert a file to an earlier state** directly from within the VM via right-click properties.
* **Example**: Reverting `qsTestFile.txt` to its original form before modification.

---

#### 7. **Azure Resource Group**

* **Definition**: A logical container that holds related Azure resources.
* **Role in Lab**: Ensures all related components (storage account, file share, VM) are grouped together for **management and cleanup**.
* **Example**: `rg-learntech-naveed`

---

### ✅ **Real-World Example Use Case**

Imagine a company like **SkyStack Labs** needing to set up a **shared document repository** accessible by its support team across multiple virtual desktops. Instead of building and maintaining an on-premises file server, they use **Azure Files** with **snapshots** enabled. This allows quick access, secure sharing, and version recovery, all managed from the Azure portal.

---
---
---

### **📌 Purpose of the Lab**

This lab is designed to demonstrate how to **create an Azure SMB file share** within a **Storage Account** and **connect it to a Windows-based Virtual Machine (VM)**. Through this practical exercise, users learn to **provision cloud resources**, **configure secure file sharing**, and **manage snapshots** for backup and restore. It showcases the interoperability of Azure storage services with compute resources, enabling **enterprise-level file sharing solutions** in the cloud.

---

### **🧰 Azure Tools Used in the Lab**

---

#### **1. Azure Portal**

* **Description**: A web-based unified console for managing Azure resources.
* **Role**: Serves as the primary interface for performing all tasks in this lab — from creating the storage account to deploying the virtual machine.

---

#### **2. Azure Storage Account**

* **Description**: A container that holds all Azure storage data objects, including blobs, file shares, queues, and tables.
* **Role**: Hosts the **Azure File Share** used to store and manage files that can be accessed by the VM.

---

#### **3. Azure File Share**

* **Description**: A fully managed cloud file share that can be mounted using the SMB protocol.
* **Role**: Enables shared access to files from the Azure VM, simulating a network file server environment.

---

#### **4. Virtual Machine (Windows Server 2019 Datacenter)**

* **Description**: An on-demand, scalable computing resource hosted in Azure.
* **Role**: Acts as the client machine used to **map** the file share, **edit files**, and **interact** with Azure storage.

---

#### **5. PowerShell (Inside VM)**

* **Description**: A task automation and configuration management framework.
* **Role**: Used to run the script for mounting the Azure file share to a local drive in the VM.

---

#### **6. RDP (Remote Desktop Protocol)**

* **Description**: A secure protocol for remotely connecting to a Windows machine.
* **Role**: Allows the user to log in to the VM and access the file system.

---

#### **7. Azure Snapshots**

* **Description**: A point-in-time backup of files in the file share.
* **Role**: Enables file versioning, backup, and restore functionality.

---

#### **8. Previous Versions (Windows Feature)**

* **Description**: A Windows feature that allows users to view and restore previous states of files/folders.
* **Role**: Demonstrates how Azure file share snapshots can integrate with Windows’ native file versioning interface.

---

#### **9. Resource Groups**

* **Description**: Logical containers that hold related Azure resources.
* **Role**: Used to organize and delete all resources created during the lab as a single unit.

---

#### **10. Locks (Azure Resource Lock)**

* **Description**: Prevents accidental deletion or modification of Azure resources.
* **Role**: Must be removed before deleting snapshots or resources.

---

### ✅ **Outcome**

By completing this lab, users gain hands-on experience in integrating **Azure Storage**, **Compute**, and **File Services**, and they develop an understanding of **enterprise file sharing**, **resource management**, and **backup strategy** using Azure-native tools.

---
---
---

## 🌐 Real-World Scenario: **"The Curious Cloud Explorer Builds a Shared File System"**

Naveed, the ever-curious **CloudOps Engineer** at **TechWaveNaveed**, received a request from the HR department. They needed a **shared folder** accessible by all team members working from a virtual desktop environment. The requirement was simple: a central place to **upload, modify, and restore documents** — without relying on traditional on-premises file servers.

To solve this professionally and efficiently, the Curious Cloud Explorer decided to implement a cloud-native solution using **Azure File Share** backed by **SMB protocol**, connected to a **Windows Virtual Machine**.

---

### 🚀 Step 1: Laying the Foundation – **Create a Storage Account**

Naveed started by provisioning a **Storage Account** named `stcloudtrainproshare01` in the **East US** region. He selected **Locally Redundant Storage (LRS)** for cost efficiency and ensured it was configured for **standard performance** — perfect for transactional workloads.

> 📌 *Why?* A **Storage Account** acts as the container for all storage services including **Azure Files**, enabling a cost-effective and scalable solution for shared access.

---

### 📁 Step 2: File Sharing Magic – **Create an Azure File Share**

Inside the storage account, Naveed created a **File Share** named `qsfileshare` and selected the **Transaction-optimized tier** to enhance small file operations like open/read/write — ideal for shared HR documents.

He uploaded a test file `qsTestFile.txt` as a placeholder to simulate real usage.

> 📌 *Why?* **Azure File Share** provides a centralized, managed location for hosting files that can be accessed over **SMB** from multiple machines or users.

---

### 💻 Step 3: Building the Workspace – **Deploy and Access the VM**

To access the file share securely, he spun up a **Windows Server 2019 Virtual Machine** called `vm-ncloudedge-win01` in the same region. After configuring **RDP**, **HTTP**, and admin credentials, he downloaded the **RDP file**, logged into the VM, and prepared it for mounting the file share.

> 📌 *Why?* A **Virtual Machine** allows internal users to access the **file share** using standard Windows file explorer or mapped drives, just like in an office environment.

---

### 🔗 Step 4: Connect the Dots – **Map File Share to VM**

From the Azure portal, Naveed navigated to the file share, selected “**Connect**”, and generated a **PowerShell script**. Back inside the VM, he ran the script in **PowerShell**, instantly mapping the share to a drive letter (e.g., Z:).

> 📌 *Why?* The mapping gives the user a familiar experience — accessing files from **Windows Explorer** without needing to know about Azure infrastructure.

---

### 🕐 Step 5: Snapshots & Recovery – **Test Backup and Restore**

Naveed modified `qsTestFile.txt` from the VM and saved changes. He then used **Azure Snapshots** to capture the current state of the file. After creating another snapshot, he tested the **Restore** feature by reverting the file to its original version.

Later, using **File Explorer** inside the VM, he right-clicked the file > Properties > **Previous Versions**, confirming that **backup and recovery** worked like a charm!

> 📌 *Why?* **Snapshots** are essential for data protection and audit recovery scenarios where a user accidentally deletes or corrupts shared files.

---

### 🧹 Step 6: Wrap Up – **Resource Cleanup**

Once the validation was complete, the CloudOps engineer cleaned up all resources under `rg-learntech-naveed` to avoid unnecessary billing — always a best practice!

---

### ✅ Final Result

Naveed successfully deployed a **cloud-native file sharing solution** for HR without needing any physical infrastructure. His setup was **scalable**, **resilient**, **secure**, and **easy to restore** — everything a modern business demands from its IT team.

---
---
---
## Comic-Style Summary: **“Files in the Cloud, Accessed with Style!”**

### 🎯 The File-Sharing Mission Begins

Our favorite **Curious Cloud Explorer**, **Naveed**, received a new task at **LearnTechCloud**. The HR team needed a **secure, shared folder** that employees could access from a **Windows VM**. No more emailing documents back and forth! Naveed, ready with his virtual cape, decided to take this mission to the **Azure skies**.

---

### 🧱 Step 1: Building the Cloud Basement

First things first! Naveed created a **Storage Account** named `stlearntechnaveed01` with **Locally Redundant Storage (LRS)**. This was like creating a big digital warehouse to keep all the files safe. Then, he added a **File Share** called `qsfileshare`, perfect for team collaboration.

> “Now we’ve got cloud shelves to put the files on!” thought the explorer proudly.

---

### 💻 Step 2: Bringing the Windows Worker

To make those files accessible, Naveed deployed a **Windows Virtual Machine** named `vm-ncloudedge-web01`. This machine acted like an office computer — but in the cloud. Once it was ready, he connected to it using **Remote Desktop Protocol (RDP)** and opened the doors to the cloud warehouse.

---

### 🔗 Step 3: Connect and Drive!

Inside the Azure portal, Naveed clicked **Connect** on the file share and copied a **PowerShell script**. Back in the VM, he ran the script and—voila!—a **Z: drive** appeared with `qsfileshare`. It was like plugging in a USB drive, but way cooler… and virtual!

---

### 📝 Step 4: Snapshots to the Rescue

After uploading and editing a text file named `qsTestFile.txt`, the TechWaveNaveed admin took a **snapshot** — a mini time-machine backup. He then changed the file and took another snapshot. Wanting to test recovery, he restored the file from the first snapshot and—boom!—the original version was back!

> “Snapshots are like save-points in a video game,” he joked. “One click and you’re back in time!”

---

### 🧹 Step 5: Clean-Up Time

Once everything was tested and working, the CloudOps engineer deleted all the resources under `rg-learntech-naveed`. He smiled, knowing he had built a secure, cloud-powered **file-sharing solution** without a single server in the office.

---

### ✅ Mission Status: SUCCESS!

Yes, **Naveed completed his task successfully**! He gave the HR team a **reliable, scalable, and recoverable** file system that lives in the cloud. And most importantly, he proved once again that curiosity, combined with **Azure skills**, can turn complex problems into simple cloud solutions.

---
---
---

**🌐 Practical Scenario: Simplifying File Access Across Remote Teams with Azure**

---

### **Scenario Title: "Central Files, Anywhere Access — Sarah's Cloud Upgrade"**

**Character**: Sarah, an **IT Administrator** at a fast-growing architecture firm
**Business Goal**: Enable remote teams to access, edit, and share project files securely — without relying on traditional on-premises file servers.

---

### **📌 Business Problem**

Sarah’s firm has multiple teams working from different cities. Each team needs to access **AutoCAD blueprints**, **project documentation**, and **client folders** in real-time. Their old **on-premises file server** is slow, difficult to scale, and inaccessible from remote locations. Managing VPNs, backup schedules, and file versioning has become a full-time headache.

Sarah needs a **secure**, **scalable**, and **centralized** solution to:

* Share files across remote locations
* Keep backups/version history
* Ensure access control and easy restore in case of file changes or deletions

That’s where **Azure** comes in.

---

### **🔧 Solution with Azure Tools**

#### **Step 1: Creating a Centralized File Store**

Sarah logs in to the **Azure Portal** and creates a **Storage Account**. This will be the container for all project-related data.

In it, she creates an **Azure File Share**, naming it **"projectfileshare"**, optimized for **transaction-based access**. This acts like a traditional network drive — but it's now in the **cloud**, always accessible.

#### **Step 2: Uploading Key Documents**

Sarah uploads a sample **project plan file** (like `Q1_ProjectScope.txt`) directly into the **Azure File Share**. This is to ensure files can be manually uploaded and managed before setting up automation later.

#### **Step 3: Setting Up a Windows Server for Team Use**

To simulate the architecture team's computers, Sarah deploys a **Windows Server 2019 VM** via **Azure Virtual Machines**. She selects **RDP and HTTP** as allowed ports so she can log in remotely.

Using **PowerShell**, she maps the cloud **file share** to the VM’s local drive (e.g., drive **Z:**). This way, any user logged into the VM sees the shared folder like it’s part of their own computer.

#### **Step 4: Real-Time Backup and Recovery**

Sarah edits the `Q1_ProjectScope.txt` file on the VM and then creates a **Snapshot** of the **Azure File Share**. Later, she modifies the file and demonstrates that she can **restore** it from a previous state using the **Snapshot** — giving her peace of mind for version control.

#### **Step 5: Enabling Local Recovery via Previous Versions**

She right-clicks the file and goes to **Properties > Previous Versions** on the VM. She confirms that **Azure Snapshots** are accessible just like native **Windows VSS snapshots**, making file recovery easy for her team.

#### **Step 6: Final Cleanup and Governance**

Sarah uses **Resource Groups** to organize all lab-created items. She removes any **resource locks** and then **deletes** all assets from the group in one go — keeping Azure clean and cost-effective.

---

### ✅ **Professional Outcome**

Thanks to this setup:

* Her remote teams can now **access and collaborate on files in real time**
* File changes can be **backed up and rolled back with a few clicks**
* No need for complex VPNs or external drives
* All solutions are **secure, scalable, and managed through a unified interface**

By using **Azure Storage Accounts**, **File Shares**, **Virtual Machines**, **Snapshots**, and **PowerShell**, Sarah solved a **real-world business problem** with **cloud-native tools**.

---

### 💼 Real-World Application

Many organizations — from legal firms to design studios — face similar collaboration challenges. This lab shows how **Azure File Shares** can modernize workflows, **reduce IT overhead**, and offer **enterprise-grade access and backup** without complex infrastructure.

The lab not only teaches *how* to configure these tools, but *why* they matter — and how they translate into real, measurable business value.

---

**This is not just a lab — it's a modern IT story in action.**

---

## Lab-Based Conceptual MCQs

### 1. What is the primary advantage of using an **Azure File Share** over traditional on-premises file servers for remote teams?
(a) Higher internet speed  
(b) Requires no authentication  
(c) Easy integration with on-prem backups  
(d) Cloud-based access from anywhere with built-in redundancy  
**Correct answer: (d)**  
**Explanation:** Azure File Share enables remote teams to access files via SMB protocol from anywhere, with high availability and redundancy without the need for traditional infrastructure.

### 2. Why is it beneficial to create an **Azure Snapshot** of a file share?
(a) To increase performance  
(b) To back up the storage account credentials  
(c) To create a recovery point that can restore data at a specific moment  
(d) To reduce file size  
**Correct answer: (c)**  
**Explanation:** Snapshots allow for point-in-time recovery, making it easy to restore files if data is accidentally modified or deleted.

### 3. What role does the **Resource Group** play in the lab setup?
(a) It defines user access levels  
(b) It acts as a firewall for VMs  
(c) It organizes and manages Azure resources as a single group  
(d) It encrypts virtual machines  
**Correct answer: (c)**  
**Explanation:** Resource groups help manage and monitor related Azure resources collectively, simplifying resource lifecycle operations like deployment and deletion.

### 4. Why is mapping the **Azure File Share** to a **Windows VM** useful in enterprise scenarios?
(a) It reduces cloud storage costs  
(b) It enables local access to cloud-stored files using standard protocols  
(c) It improves VM CPU utilization  
(d) It replaces Active Directory  
**Correct answer: (b)**  
**Explanation:** Mapping provides seamless access to cloud-hosted file shares as if they were local drives, making it ideal for hybrid work environments.

### 5. Which Azure feature allows a user to track and restore previous versions of files in an **Azure File Share**?
(a) File Audit Logs  
(b) Role-Based Access Control  
(c) Share Snapshots  
(d) File Sync  
**Correct answer: (c)**  
**Explanation:** Share Snapshots allow tracking of file changes and offer the ability to restore previous versions of a file.

### 6. What is the reason for using **PowerShell** in the process of mapping the Azure file share?
(a) PowerShell is faster than GUI  
(b) The Azure Portal does not support file share mapping  
(c) Scripting provides precise, repeatable automation for mounting shares  
(d) It encrypts data in transit  
**Correct answer: (c)**  
**Explanation:** PowerShell offers scripting capabilities to automate and reliably repeat tasks such as mounting SMB shares.

### 7. Why should an administrator disable the backup option when creating a test file share in a lab environment?
(a) To avoid snapshot conflicts  
(b) To reduce lab cost and simplify the test scope  
(c) Backup is required only for Linux VMs  
(d) Backup enables HTTP access only  
**Correct answer: (b)**  
**Explanation:** In test environments, backup services add unnecessary cost and complexity, especially when manual snapshots are sufficient.

### 8. What is a major benefit of deploying **Windows Server 2019 Datacenter** as the VM image in this lab?
(a) It includes built-in Office 365 integration  
(b) It supports Active Directory only  
(c) It supports SMB protocol and mirrors on-prem file server behavior  
(d) It does not require a license  
**Correct answer: (c)**  
**Explanation:** Windows Server 2019 provides compatibility with SMB file sharing, closely mimicking on-prem scenarios for realistic cloud testing.

### 9. Why are **inbound port rules (RDP, HTTP)** configured during VM deployment?
(a) To allow Azure billing access  
(b) To enable remote desktop and web access  
(c) To block external threats  
(d) To manage DNS settings  
**Correct answer: (b)**  
**Explanation:** Opening RDP and HTTP ports ensures administrators can remotely access the VM and test services such as file sharing or web apps.

### 10. What is the purpose of **deleting resources** at the end of the lab?
(a) To reset Azure subscription  
(b) To prevent unauthorized access  
(c) To avoid unnecessary billing and maintain a clean environment  
(d) To reduce VM load  
**Correct answer: (c)**  
**Explanation:** Deleting unused resources prevents incurring additional charges and keeps the Azure environment organized.

---
---
---

## Professional Job Interview Questions – **Create an SMB Azure File Share and Connect It to a Windows VM**

### 1. **Naveed needs to create a shared cloud-based file system accessible from a Windows VM. Which Azure service should he use?**
(a) **Azure Blob Storage**  
(b) **Azure File Share**  
(c) **Azure Disk Storage**  
(d) **Azure Archive Storage**  
**Correct answer:** (b)  
**Explanation:** **Azure File Share** supports the **SMB protocol**, making it ideal for mounting on **Windows virtual machines** to replicate traditional file server functionality in the cloud.

### 2. **Why would Naveed choose the “Transaction optimized” performance tier for his file share?**
(a) To minimize latency for small I/O workloads  
(b) To support cold file archiving  
(c) To allow read-intensive backup workloads  
(d) To host VM OS disks  
**Correct answer:** (a)  
**Explanation:** The **Transaction optimized** tier is designed for **frequent access with small file operations**, such as reads and writes, making it ideal for general file-sharing needs with consistent usage.

### 3. **Naveed uploads a file to Azure File Share and wants to access it from a VM. What must he do after connecting to the VM via RDP?**
(a) Install a third-party sync tool  
(b) Mount the share using NFS  
(c) Run a PowerShell script provided by Azure  
(d) Use Azure CLI inside the VM  
**Correct answer:** (c)  
**Explanation:** Azure provides an **auto-generated PowerShell script** in the File Share’s **Connect** blade, which can be executed in the VM to mount the file share using the **SMB protocol**.

### 4. **What is the main purpose of creating a snapshot in Azure File Share?**
(a) To migrate data to another region  
(b) To enable automated backups  
(c) To create a point-in-time backup for file recovery  
(d) To sync files with other VMs  
**Correct answer:** (c)  
**Explanation:** A **snapshot** is a **read-only, point-in-time backup** of a file share that enables data recovery in case of accidental modification or deletion.

### 5. **After modifying a file, Naveed wants to restore its original version. Which feature allows him to do that?**
(a) Azure Site Recovery  
(b) File share snapshot  
(c) Application Gateway  
(d) Managed Disks  
**Correct answer:** (b)  
**Explanation:** **Snapshots** allow Naveed to **restore a file to its previous state** directly from within the Azure portal or mapped drive.

### 6. **Why should the Curious Cloud Explorer use RDP to connect to the VM instead of SSH?**
(a) Because Azure only supports RDP  
(b) Because RDP is more secure than SSH  
(c) Because the VM is running Windows OS  
(d) Because SSH requires additional licensing  
**Correct answer:** (c)  
**Explanation:** **RDP (Remote Desktop Protocol)** is used for connecting to **Windows VMs**, whereas **SSH** is typically used for Linux VMs.

### 7. **In a business use case, what makes Azure File Share a suitable alternative to traditional on-prem file servers?**
(a) Supports only Linux clients  
(b) Doesn't support snapshots or backups  
(c) Offers centralized, cloud-hosted, scalable file access  
(d) Requires dedicated hardware  
**Correct answer:** (c)  
**Explanation:** **Azure File Share** provides a **centralized, scalable file system** accessible via **SMB**, eliminating the need for on-premise file servers and hardware.

### 8. **What type of redundancy did Naveed choose for the storage account, and why might it be ideal for test or development scenarios?**
(a) Geo-redundant storage (GRS)  
(b) Zone-redundant storage (ZRS)  
(c) Locally-redundant storage (LRS)  
(d) Read-access geo-redundant storage (RA-GRS)  
**Correct answer:** (c)  
**Explanation:** **LRS** is cost-effective and stores data **within a single data center**, making it a practical choice for non-critical, dev/test environments.

### 9. **If Naveed wanted to allow multiple VMs across regions to access the file share concurrently, which configuration might be more suitable?**
(a) Increase snapshot frequency  
(b) Use NFS protocol with Azure Blob Storage  
(c) Use Azure File Sync  
(d) Create a separate storage account for each VM  
**Correct answer:** (c)  
**Explanation:** **Azure File Sync** enables **centralized file sharing** with local performance and allows replication to **multiple on-prem servers or VMs** across regions.

### 10. **Why is it important for Naveed to disable backup during the lab when creating the file share?**
(a) Backups consume extra IP addresses  
(b) To reduce cost and complexity for a test scenario  
(c) Backups make file share inaccessible  
(d) Azure blocks backups on new file shares  
**Correct answer:** (b)  
**Explanation:** Disabling backup during lab/testing helps **reduce unnecessary costs** and ensures a simpler, controlled environment.

### 11. **Naveed wants to verify file recovery from snapshots directly within the VM. Which method should he use?**
(a) Use Azure Resource Manager template  
(b) Use RDP, then right-click file > Properties > Previous Versions  
(c) Download the file from the portal  
(d) Recreate the file manually  
**Correct answer:** (b)  
**Explanation:** In **Windows VM**, the **Previous Versions** tab under file **Properties** shows available snapshot versions for quick recovery.

### 12. **Why is a storage account required before creating a file share in Azure?**
(a) To connect with Microsoft Teams  
(b) It stores metadata only  
(c) It acts as a container for file shares and other storage services  
(d) It generates the DNS name for virtual machines  
**Correct answer:** (c)  
**Explanation:** A **Storage Account** is a **foundational service** in Azure that acts as the **container** for all types of storage like blobs, files, tables, and queues.

---
---
---
## Comic-Style Summary: **“Files in the Cloud — Sharing Like a Pro!”**

### 🌩️ Mission: File Sharing in the Sky

Naveed, our **Curious Cloud Explorer**, was assigned a fun challenge — connect a **Windows VM** to a **cloud-based file share**. He rolled up his sleeves, opened the **Azure Portal**, and created a **Storage Account** under his signature tag `rg-learntech-naveed`. It had to be **locally redundant**, just in case the clouds misbehaved!

---

### 📂 Enter: The Azure File Share

Our CloudOps hero then created a **file share** named `qsfileshare` and uploaded a test file called **qsTestFile.txt**. It was like putting snacks in a lunchbox — the file was ready to be shared with the VM in the cloud world. This file share would later become a drive letter in the VM. Fancy, right?

---

### 💻 Meet the Virtual Machine

Next, the TechWaveNaveed admin spun up a **Windows Server 2019 VM** — let’s call it `vm-ncloudedge-web01`. With RDP access enabled and credentials set, he zoomed into the VM’s desktop and opened **PowerShell** like a magician holding his wand. He pasted the secret **mapping script**, and voilà — the cloud share appeared as a drive!

---

### 🕰️ Time Travel with Snapshots

Naveed wasn’t done. He edited the file, then created a **snapshot** to capture its original state. After modifying the file again, he restored it from the **snapshot** like pressing "Undo" on history. He even explored the **Previous Versions tab** from within the VM — a great way to recover files from accidents or oops-moments!

---

### 🧹 Clean Up Time!

Once the testing was complete, our Azure admin cleaned up everything — the **storage account**, **VM**, and **snapshots** — leaving the cloud spotless. The Curious Cloud Explorer had once again completed his mission with elegance, proving that managing file shares on **Azure** is not only powerful but also... kinda fun!

---

This comic-style summary breaks down the entire lab in a beginner-friendly tone while showcasing **Azure Storage Accounts**, **Azure File Share**, **VM deployment**, **snapshot creation**, and **file restore** — all through Naveed’s confident, curious journey in the cloud! 🌐🚀

---
---
---
## Text-Based Diagram for the Lab: **"Create an SMB Azure File Share and Connect it to a Windows VM"**

```
+-----------------------------+
| Step 1: Create Storage      |
| - Storage Account (Standard)|
| - LRS Redundancy            |
| - Region: East US           |
+-------------+---------------+
              |
              v
+-----------------------------+
| Step 2: Create File Share   |
| - Name: qsfileshare         |
| - Tier: Transaction Optimized|
+-------------+---------------+
              |
              v
+-----------------------------+
| Step 3: Upload File         |
| - File: qsTestFile.txt      |
+-------------+---------------+
              |
              v
+-----------------------------+
| Step 4: Deploy VM           |
| - OS: Windows Server 2019   |
| - Region: East US           |
| - Inbound: RDP, HTTP        |
+-------------+---------------+
              |
              v
+-----------------------------+
| Step 5: Connect to VM       |
| - RDP to VM                 |
+-------------+---------------+
              |
              v
+-----------------------------+
| Step 6: Map File Share      |
| - Use PowerShell script     |
| - Map drive to qsfileshare  |
+-------------+---------------+
              |
              v
+-----------------------------+
| Step 7: Create Snapshot     |
| - Take Snapshot             |
| - Modify File               |
| - Take another Snapshot     |
+-------------+---------------+
              |
              v
+-----------------------------+
| Step 8: Browse Snapshots    |
| - View and compare versions |
+-------------+---------------+
              |
              v
+-----------------------------+
| Step 9: Restore File        |
| - Restore from snapshot     |
| - File reverts successfully |
+-------------+---------------+
              |
              v
+-----------------------------+
| Step 10: Clean Up           |
| - Delete snapshots, file    |
| - Delete VM & Storage       |
+-----------------------------+
```

### 📘 **What This Diagram Shows**

This diagram illustrates how **Naveed**, the Curious Cloud Explorer, created an **Azure File Share**, mapped it to a **Windows VM**, and used **snapshots** to protect and restore file versions. It highlights the use of **Storage Account**, **File Share**, **VM Deployment**, **PowerShell**, **Snapshot Management**, and **File Version Control** — all crucial skills for real-world Azure administration.

---
---
---
