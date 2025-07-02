# Lab 1: Creating Azure resource locks

**Duration:** 45m
---
---

**After logging in with your credentials:**

---

### **Task 1: Create a Virtual Machine**

1. In the Azure portal, click on **Create a resource**.
2. Select **Virtual Machine** from the list and click **Create**.
3. Fill in the following configuration:

   * **Resource Group**: Select any existing or create a new one (e.g., `rg-labresources`)
   * **Virtual Machine Name**: `MyLabVM`
   * **Availability Options**: `No infrastructure redundancy required`
   * **Security Type**: `Trusted launch virtual machines`
   * **Image**: `Ubuntu Server 20.04 LTS Gen2`
   * **Size**: Click **See all sizes**, choose `B2s`
   * **Authentication Type**: `Password`
   * **Username**: `LabUser`
   * **Password**: `StrongPassword@123`
   * **Confirm Password**: `StrongPassword@123`
4. Click **Next: Disks >**
5. Under the **Disks** tab, select:

   * **OS Disk Type**: `Standard SSD (Locally-redundant Storage)`
6. Click **Review + create**, then **Create** to deploy the VM.

---

### **Task 2: Add a Delete Lock to the Virtual Machine**

1. Navigate to the newly created VM.
2. In the left menu, go to **Locks** under **Settings**.
3. Click **Add**, and enter:

   * **Lock Name**: `VMDeleteLock`
   * **Lock Type**: `Delete`
4. Click **OK** to apply the lock.

---

### **Task 3: Add a Read-Only Lock to the Resource Group**

1. Go to the Resource Group associated with the VM.
2. In the left menu, click **Locks** under **Settings**.
3. Click **Add**, and provide:

   * **Lock Name**: `RGReadOnly`
   * **Lock Type**: `Read-only`
4. Click **OK**.

---

**Delete all the resources.**

---
---
---
## **🔍 Lab Summary: Azure Resource Locks and Virtual Machine Deployment**

### **🎯 Purpose of the Lab**

The purpose of this lab is to provide hands-on experience with deploying a virtual machine (VM) in Microsoft Azure and configuring resource locks to control access and modification rights. This lab emphasizes the use of **Delete** and **Read-only** locks to protect resources from accidental or unauthorized changes or deletions. It helps learners understand how resource governance and access control can be enforced in cloud environments using built-in Azure features.

---

### **🛠 Azure Tools and Services Used**

#### 1. **Azure Portal**

* **Description**: A web-based unified console that allows users to manage Azure resources and services.
* **Role in the Lab**: Serves as the primary interface for completing all tasks—creating a virtual machine, applying locks, and managing resources.

#### 2. **Resource Group**

* **Description**: A container that holds related resources for an Azure solution.
* **Role in the Lab**: Acts as a logical grouping for the virtual machine and associated resources. The Read-only lock is applied at this level to restrict modification access.

#### 3. **Virtual Machine (VM)**

* **Description**: A scalable, on-demand computing resource offered by Azure, enabling the deployment of Windows or Linux environments.
* **Role in the Lab**: The core resource deployed to demonstrate how Azure locks work. It is configured with specific settings including OS, size, authentication, and disk type.

#### 4. **Resource Locks**

* **Description**: Built-in Azure feature to prevent accidental deletion or modification of critical resources by applying either Delete or Read-only locks.
* **Types Used in the Lab**:

  * **Delete Lock**: Prevents a resource (in this case, the virtual machine) from being deleted.
  * **Read-only Lock**: Prevents any modifications to a resource group, including adding, updating, or deleting any resources within it.
* **Role in the Lab**: Demonstrates how resource locks can be configured and enforced to safeguard infrastructure.

#### 5. **Azure Compute**

* **Description**: A category of Azure services used for hosting and running applications or workloads (includes VMs, containers, etc.).
* **Role in the Lab**: Provides the compute resources needed for deploying and managing the virtual machine.

#### 6. **Azure Storage (Disk)**

* **Description**: Manages the storage of the operating system and data disks for Azure VMs.
* **Role in the Lab**: The VM is configured with a Standard SSD OS disk to demonstrate storage selection and configuration during VM deployment.

---

This lab not only demonstrates how to deploy a basic virtual machine but also introduces governance tools like Azure resource locks, providing foundational knowledge in protecting and managing cloud infrastructure effectively.

---


