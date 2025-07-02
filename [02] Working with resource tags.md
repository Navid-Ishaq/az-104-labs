# Lab 2: Working with resource tags

**Duration:** 30m

---
---

### 🚀 Azure Lab – Organizing Resources with Tags

**After logging in with your credentials:**

---

### **Task 1: Create a Virtual Machine**

1. In the Azure Portal, go to **Virtual Machines**.
2. Click **+ Create** > **Azure Virtual Machine**.
3. In the **Basics** tab, enter the following:

   * **Resource Group**: Select or create one (e.g., `rg-labresources`)
   * **VM Name**: `resizeVM`
   * **Region**: `East US`
   * **Availability options**: `No infrastructure redundancy required`
   * **Security type**: `Standard`
   * **Image**: `Windows Server 2019 Datacenter - x64 Gen2`
   * **Size**: Click **See all sizes**, select `B1s`, click **Select**
   * **Username**: `LabUser`
   * **Password**: `StrongPassword@123`
4. Leave **Azure Spot Instance** unchecked.
5. Leave **Public inbound ports** as default.
6. Go to the **Disks** tab and select:

   * **OS Disk Type**: `Standard SSD`
7. Click **Review + Create**, then click **Create**.

---

### **Task 2: Apply Tags to the Virtual Machine**

1. In the **Azure Portal**, go to **Resource Groups**.
2. Open your resource group (e.g., `rg-labresources`).
3. Click on the **resizeVM** virtual machine.
4. In the left panel, select **Tags** under Settings.
5. Add a tag with:

   * **Name**: `Department`
   * **Value**: `IT`
6. Click **Apply**.

---

### **Task 3: Filter Resources by Tag**

1. Go to **Resource Groups** again from the Azure menu.
2. Select your resource group.
3. Click **Add filters** on the toolbar.
4. Select the tag **Department**, choose the value `IT`, then click **Apply**.
5. You should now see all resources tagged as `Department = IT`.

---

**Delete all the resources.**

---
---
---
## **📘 Azure Lab Summary: Organizing Azure Resources Using Tags**

---

### **🎯 Purpose of the Lab**

The objective of this lab is to demonstrate how to effectively organize and manage Azure resources using **resource tags**. Through the deployment of a virtual machine and the application of tags at the resource level, this lab teaches how tagging enhances **resource categorization**, **cost tracking**, and **administrative control**. It also shows how to **filter and locate** resources based on tag values, a key skill for managing large-scale environments efficiently.

---

### **🛠 Azure Tools and Services Used**

#### 1. **Azure Portal**

* **Description**: A web-based interface to create, manage, and monitor Azure services.
* **Role in the Lab**: Used to create the virtual machine, apply tags, and perform filtering actions — the central interface for completing all tasks.

#### 2. **Virtual Machine (VM)**

* **Description**: A scalable compute resource that allows you to run applications and services on a virtualized server.
* **Role in the Lab**: Serves as the main resource to which tags are applied. Demonstrates how to organize and manage compute resources with metadata.

#### 3. **Resource Group**

* **Description**: A container in Azure that holds related resources for a solution.
* **Role in the Lab**: Hosts the virtual machine and provides a scope for managing the VM and its tags. Tag filtering is demonstrated within the resource group context.

#### 4. **Resource Tags**

* **Description**: Key-value pairs assigned to Azure resources for metadata organization (e.g., `Department: IT`).
* **Role in the Lab**: Central to the lab objective. Tags are applied to the VM and later used to **filter resources** in the portal, helping with organization, automation, and cost management.

#### 5. **Tag-Based Filtering**

* **Description**: A search and filter capability within the Azure Portal to locate resources based on specific tag values.
* **Role in the Lab**: Used to demonstrate how tags enable efficient resource discovery and management when dealing with multiple assets.

---

### **🔑 Real-World Relevance**

Tagging is widely used in production environments to:

* Track **costs per department or project**,
* Enforce **governance policies**,
* Automate resource management via **Azure Policy** or **scripts**.

Mastering tagging and resource filtering is essential for **Azure Administrators**, **Cloud Architects**, and **DevOps Engineers** who manage complex cloud infrastructures.

---
---
---
