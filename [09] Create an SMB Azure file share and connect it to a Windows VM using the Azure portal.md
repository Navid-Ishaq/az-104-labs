# Lab 9: Create an SMB Azure file share and connect it to a Windows VM using the Azure portal

**Duration:** 1h 0m

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
