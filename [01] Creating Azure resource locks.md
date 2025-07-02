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
---
---
## **🏢 Scenario: Securing a Production VM for a Financial Services App**

**Meet Aisha**, a cloud engineer working for **FinSecure Ltd.**, a mid-sized financial services company. Her team is tasked with deploying a new backend **Ubuntu server** in Azure, which will run core APIs for the company's mobile banking app. Because of the sensitivity of financial data and regulatory requirements, any accidental deletion or modification of infrastructure could lead to downtime, data loss, or compliance issues.

To avoid these risks, Aisha decides to follow a **cloud governance strategy** by deploying the VM and applying **resource locks** — a native Azure feature to protect mission-critical resources from accidental or unauthorized actions.

---

### **🔧 Step-by-Step Story**

### **1. Deploying the Virtual Machine**

Aisha logs into the **Azure Portal** and starts by clicking **Create a resource**. She selects **Virtual Machine**, giving it the name **MyLabVM** and placing it under the **rg-labresources** resource group.

She chooses:

* **Ubuntu Server 20.04 LTS Gen2** as the operating system to ensure stability and long-term support,
* A modestly sized **B2s VM** to optimize costs during the testing phase,
* And sets up credentials using a **secure password-based login** with a non-admin username `LabUser`.

In the **Disks** section, she selects **Standard SSD** to balance performance and cost. After reviewing all settings, she clicks **Create**.

✅ **Why it matters**: A well-configured VM provides the compute power for her APIs, but without protection, it's vulnerable to unintended actions.

---

### **2. Applying a Delete Lock to the VM**

Now that the VM is running, Aisha wants to **prevent any team member from accidentally deleting it** — especially during cleanup tasks or automation runs.

She opens the VM in the Azure Portal, navigates to **Settings > Locks**, and adds a new lock:

* **Name**: `VMDeleteLock`
* **Type**: `Delete`

✅ **Benefit**: Even users with high-level access can't delete the VM unless the lock is removed. This is crucial for safeguarding production workloads.

---

### **3. Applying a Read-Only Lock on the Resource Group**

Next, Aisha wants to go a step further: **freeze the entire resource group** to prevent any modifications during a company audit next week.

She navigates to the **rg-labresources** resource group, goes to **Locks**, and adds another lock:

* **Name**: `RGReadOnly`
* **Type**: `Read-only`

✅ **Impact**: Now, nothing in the group — not even the VM’s network interface or disk — can be changed, deleted, or altered. Azure enforces this lock across the board.

---

### **🧠 Real-World Relevance**

Aisha’s actions reflect **best practices in cloud governance** — especially in industries like finance, healthcare, or government where **uptime, data integrity, and change control** are non-negotiable. By using **Azure Resource Locks**, she's proactively **reducing risk**, ensuring **regulatory compliance**, and building **trust with stakeholders**.

---

### **🧼 Final Cleanup**

Once the audit period ends or the infrastructure is no longer needed, Aisha removes the locks and proceeds to shut down the environment.

---

**Delete all the resources.**

---

