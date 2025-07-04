# Lab 7: Migrate data to cloud with AzCopy

**Duration:** 45m

```
---

# Azure Lab Instructions: Migrate Data to Cloud with AzCopy

**After logging in with your credentials:**

---

## Step 1: Create a Storage Account

1. In the Azure Portal, search for **Storage accounts** in the top search bar and select it.
2. Click **+ Create**.
3. Under the **Basics** tab:

   * **Resource group**: Select `rg_eastus_XXXXX`
   * **Storage account name**: Enter a globally unique name (e.g., `whizstorage<yourname>`)
   * **Region**: Select `East US`
   * **Performance**: Select `Standard`
   * **Redundancy**: Select `Geo-redundant storage (GRS)`
4. Go to the **Advanced** tab and set **Hierarchical namespace** to **Enabled**.
5. Click **Review + Create**, then click **Create**.
6. Once deployment is complete, select **Go to resource**.
7. From the left menu, choose **Containers** and click **+ Container**.
8. Name the container `democontainer` and click **Create**.

---

## Step 2: Download and Configure AzCopy

1. Download AzCopy from the official link:
   [https://aka.ms/downloadazcopy-v10-windows](https://aka.ms/downloadazcopy-v10-windows)
2. Extract the downloaded ZIP file to a local folder.
3. Open **Command Prompt** and navigate to the extracted folder using:

   ```
   cd <path-to-azcopy-folder>
   ```
4. Authenticate AzCopy with:

   ```
   azcopy login
   ```
5. Open the browser as instructed in the output, enter the given code, and log in.

---

## Step 3: Upload Files to Azure Blob Storage

1. Prepare your local folder with the files you want to upload.
2. Run the following command to copy files recursively:

   ```
   azcopy copy "<local-folder-path>" "https://<storage-account-name>.blob.core.windows.net/<container-name>" --recursive=true
   ```
3. Go back to the Azure Portal and confirm the files appear in the container.

---

## Step 4: Modify and Sync Data for Testing

1. Add or modify a file in your local folder.
2. Run the sync command to update Blob Storage:

   ```
   azcopy sync "<local-folder-path>" "https://<storage-account-name>.blob.core.windows.net/<container-name>" --recursive=true
   ```
3. Confirm the changes in the Azure container.

---

## Step 5: Create a Scheduled Task for Automated Sync

1. Open Notepad and paste the sync command from Step 4, updating the paths as needed.
2. Save the file as `script.bat` (e.g., `C:\script.bat`).
3. Open **Command Prompt as Administrator** and create a scheduled task:

   ```
   schtasks /CREATE /SC minute /MO 5 /TN "AzCopy Script" /TR C:\script.bat
   ```
4. Add a new file to your local folder and wait for the task to run and sync the file.

---

## Step 6: Final Step

**Delete all the resources.**

---
---

## **Lab Summary: Migrate Data to Cloud with AzCopy**

### **Purpose of the Lab**

The purpose of this lab is to demonstrate how to **migrate on-premises data to Azure Blob Storage** using **AzCopy**, a powerful command-line utility. Learners will gain hands-on experience in configuring a **storage account**, creating **Blob containers**, uploading and syncing files using **AzCopy**, and automating transfers with **Windows Task Scheduler**. The lab showcases a real-world scenario of securely transferring data to the cloud using efficient, scriptable methods.

---

## **Azure Tools Used in the Lab**

### 1. **Azure Portal**

* **Description**: A browser-based interface for managing Azure resources.
* **Role in Lab**: Used to create and manage the **Storage account** and **Blob containers**, and to verify that files have been successfully uploaded.

---

### 2. **Azure Storage Account**

* **Description**: A fundamental service in Azure used to store data objects such as blobs, files, queues, tables, and disks.
* **Role in Lab**: Serves as the target destination for data being migrated. A new **Storage account** is created to host the **Blob container** where files are uploaded.

---

### 3. **Azure Blob Storage**

* **Description**: A service for storing large amounts of unstructured data such as text or binary data.
* **Role in Lab**: A **Blob container** within the **Storage account** is created to hold the uploaded files. It supports scalable and secure object storage.

---

### 4. **AzCopy**

* **Description**: A command-line utility designed to copy data to and from Microsoft Azure Blob, File, and Table storage.
* **Role in Lab**: The core tool used to perform data transfer operations. Learners use **AzCopy** to:

  * Log in and authenticate
  * Upload files from a local folder to Azure Blob Storage
  * Sync updated files from the local source
  * Script and automate these transfers

---

### 5. **Hierarchical Namespace (HNS)**

* **Description**: An advanced feature in Azure Data Lake Storage Gen2 that allows directory-like file system structures within Blob Storage.
* **Role in Lab**: Enabled during storage account creation to support **Data Lake Gen2** features, which are often required for enterprise-scale data operations.

---

### 6. **Windows Command Prompt**

* **Description**: A terminal interface on Windows used for executing command-line tools and scripts.
* **Role in Lab**: Used to run **AzCopy** commands and navigate the local filesystem for file transfer operations.

---

### 7. **Windows Task Scheduler**

* **Description**: A Windows tool that allows users to automate the launching of programs or scripts at predefined times or events.
* **Role in Lab**: Used to create a scheduled task that runs an **AzCopy** script every 5 minutes. This simulates an automated, recurring data sync process.

---

## **Conclusion**

This lab integrates key Azure services with automation tools to provide a practical approach for migrating and synchronizing data to the cloud. By completing the steps, learners gain critical insights into **cloud storage management**, **secure data transfer**, and **automation using scripting tools**.

---
---

## **Story Scenario: Migrating Marketing Team Archives to Azure Blob Storage Using AzCopy**

**Character**: *Emily Roberts*, an IT Systems Engineer at a mid-sized marketing agency in Chicago.

### **Background**

Emily’s marketing agency recently moved to a hybrid cloud infrastructure to improve scalability and cost-efficiency. The creative team has years’ worth of campaign files—videos, graphics, documents—stored on an on-premises file server. With increasing remote collaboration and compliance requirements, management asked Emily to **migrate these assets securely and reliably to the cloud**.

Her goal is to **store these files in Azure Blob Storage**, ensure **efficient future syncs** for updated content, and implement **automated data transfer** on a regular schedule.

---

## **Step-by-Step Journey**

### **Step 1: Creating the Cloud Storage Environment**

Emily starts by logging into the **Azure Portal**, where she searches for **Storage Accounts** and clicks **+ Create**. She selects the appropriate **resource group** and names her **storage account** something unique like `marketingfilesemily`.

She selects **East US** as the **region**, sets the **performance** to **Standard**, and chooses **Geo-redundant storage (GRS)** to ensure data durability across regions.

Because the files will be organized in a directory-like structure, she enables the **Hierarchical Namespace (HNS)** option under the **Advanced** tab, turning her storage into a **Data Lake Storage Gen2-compatible account**.

Once deployment is complete, Emily navigates to the **Containers** section of the storage account and creates a **new container** named `creative-assets`.

> 📌 **Why it matters**: Creating a **Storage Account** with **Blob Storage** and enabling **HNS** provides scalable, secure, and structured cloud storage ideal for media-heavy departments like marketing.

---

### **Step 2: Preparing and Uploading with AzCopy**

To migrate the data, Emily decides to use **AzCopy**, a fast and lightweight **command-line tool** optimized for data transfers to Azure.

She downloads **AzCopy** from the official link, extracts it, and opens **Command Prompt**. She navigates to the extracted folder using the `cd` command.

To connect **AzCopy** to her Azure account, she runs:

```bash
azcopy login
```

This opens a browser prompt where she enters the provided code and logs in securely.

She then runs the following command to **upload the files** from her local `D:\MarketingArchives` folder to her new **Blob container**:

```bash
azcopy copy "D:\MarketingArchives" "https://marketingfilesemily.blob.core.windows.net/creative-assets" --recursive=true
```

> 📌 **Why it matters**: Using **AzCopy** ensures high-speed, scriptable, and resumable uploads—essential for large file sets or unreliable networks.

---

### **Step 3: Syncing New Files**

A few days later, the creative team adds new content to the local folder. Instead of re-uploading everything, Emily uses the **sync** command to only upload new or changed files:

```bash
azcopy sync "D:\MarketingArchives" "https://marketingfilesemily.blob.core.windows.net/creative-assets" --recursive=true
```

> 📌 **Why it matters**: The **AzCopy sync** feature improves efficiency by skipping already uploaded files, reducing bandwidth usage and transfer time.

---

### **Step 4: Automating Future Transfers**

Emily wants to automate this process so updates are pushed to Azure every 5 minutes. She creates a **batch script** (`sync_script.bat`) with the sync command and saves it to `C:\Scripts\`.

Using **Windows Task Scheduler**, she runs this command:

```bash
schtasks /CREATE /SC minute /MO 5 /TN "AzCopySyncTask" /TR C:\Scripts\sync_script.bat
```

> 📌 **Why it matters**: Automation via **Task Scheduler** ensures timely, consistent syncs without manual intervention, supporting business continuity and compliance.

---

### **Outcome and Business Value**

Emily verifies in the **Azure Portal** that all files are present in the **Blob container**. The marketing team can now access campaign files from anywhere using Azure-based tools or custom applications.

This setup ensures:

* **Data availability for remote teams**
* **Centralized cloud-based archival**
* **Reduced risk of local server failure**
* **Secure, auditable, and scalable storage**

---

## **Conclusion**

Emily successfully migrated legacy assets to **Azure Blob Storage** using **AzCopy**, implemented **efficient syncing**, and automated the process via **Task Scheduler**. This lab mirrors real-world enterprise needs and showcases how to use **Azure Storage**, **AzCopy**, and **automation tools** to solve critical business challenges.

---
---
## Lab-Based Conceptual MCQs

### 1. What is the primary benefit of using a **Private Endpoint** when configuring a **Storage Account** in Azure?

**(a)** To enable replication across regions  
**(b)** To access the storage account over a secure private IP  
**(c)** To create multiple containers  
**(d)** To allow anonymous access  

**✅ Correct answer: (b)**  
**Explanation**: A **Private Endpoint** ensures secure access to Azure services using a private IP address within your virtual network, eliminating exposure to the public internet.

---

### 2. Why is it important to associate the **Private Endpoint** with a **Virtual Network** and **Subnet**?

**(a)** To enable backup  
**(b)** To allocate public IP addresses  
**(c)** To enforce network isolation and control  
**(d)** To reduce VM provisioning time  

**✅ Correct answer: (c)**  
**Explanation**: Associating the **Private Endpoint** with a **Virtual Network** and **Subnet** enforces network segmentation and prevents exposure to external threats.

---

### 3. What is the role of the **Storage Explorer** tool in the lab?

**(a)** Monitor network latency  
**(b)** Encrypt VM disks  
**(c)** Interact with blob storage using a GUI  
**(d)** Assign RBAC roles  

**✅ Correct answer: (c)**  
**Explanation**: **Azure Storage Explorer** provides a graphical interface to manage and interact with blob containers, file shares, and queues in a storage account.

---

### 4. What does the `nslookup` command verify in the virtual machine?

**(a)** VM disk size  
**(b)** Azure DNS resolution of the **Storage Account**  
**(c)** Subscription ID  
**(d)** Network performance  

**✅ Correct answer: (b)**  
**Explanation**: Running `nslookup` helps confirm that the **Storage Account** resolves to a private IP, verifying that the **Private Endpoint** is working as expected.

---

### 5. Why is **IE Enhanced Security Configuration** turned off in the virtual machine?

**(a)** To reduce firewall rules  
**(b)** To improve browser performance  
**(c)** To enable downloading and installing tools like **Storage Explorer**  
**(d)** To improve IP resolution  

**✅ Correct answer: (c)**  
**Explanation**: Disabling **IE Enhanced Security Configuration** allows downloads and installation of tools, which would otherwise be blocked due to security restrictions.

---

### 6. What does enabling **Hierarchical Namespace** allow in the **Storage Account**?

**(a)** Redundant storage replication  
**(b)** Virtual network integration  
**(c)** Advanced access controls for blob objects  
**(d)** Directory-like structure for blob storage  

**✅ Correct answer: (d)**  
**Explanation**: Enabling **Hierarchical Namespace** allows blobs to be organized in a directory structure, supporting features like ACLs and optimized file operations.

---

### 7. Which type of Azure redundancy offers protection against regional outages?

**(a)** LRS  
**(b)** ZRS  
**(c)** GRS  
**(d)** None  

**✅ Correct answer: (c)**  
**Explanation**: **Geo-Redundant Storage (GRS)** replicates data to a secondary region, providing durability even in the case of a regional failure.

---

### 8. What is the purpose of using **Standard SSD** for VM disk configuration?

**(a)** To enable live migration  
**(b)** To reduce costs while maintaining moderate performance  
**(c)** To automatically encrypt the OS disk  
**(d)** To allow VM snapshots  

**✅ Correct answer: (b)**  
**Explanation**: **Standard SSD** provides a cost-effective disk solution with balanced performance, ideal for workloads that don’t require high throughput.

---

### 9. Why is **RDP** access configured when creating the virtual machine?

**(a)** To allow browser-based access  
**(b)** To allow command-line SSH  
**(c)** To allow remote desktop connectivity for GUI-based operations  
**(d)** To avoid using credentials  

**✅ Correct answer: (c)**  
**Explanation**: **Remote Desktop Protocol (RDP)** is configured to allow users to connect to the Windows VM and interact via its graphical user interface.

---

### 10. What does disabling **public access** on a **Storage Account** help achieve?

**(a)** Faster uploads  
**(b)** Increased availability  
**(c)** Enhanced security by restricting access to private networks only  
**(d)** More regions supported  

**✅ Correct answer: (c)**  
**Explanation**: Disabling **public access** ensures the **Storage Account** can only be accessed via **Private Endpoints**, thus enhancing network security.

---
