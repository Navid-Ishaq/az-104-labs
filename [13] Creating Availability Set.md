# Lab 13: Creating Availability Set

**Duration:** 1h 0m

---
---

**After logging in with your credentials:**

### **Create an Availability Set**

1. From the portal dashboard, select **Create a resource**.
2. Search for **Availability Set** and choose the first option in the list.
3. Click **Create**.
4. Fill in the following details:

   * **Resource group**: Choose the assigned resource group (e.g., `rg_eastus_XXXXX`).
   * **Name**: Enter a descriptive name (e.g., `AvailabilitySet1`).
   * **Region**: Select `Central US` or your preferred region.
   * **Use managed disks**: Select **Yes (Aligned)**.
5. Click **Review + Create**, then click **Create** to deploy the availability set.

---

### **Deploy the First Virtual Machine in the Availability Set**

1. From the portal, select **Create a resource**.
2. Under **Compute**, choose **Virtual Machine**.
3. Configure the virtual machine with the following settings:

   * **Resource group**: Use the same group as the availability set.
   * **Virtual machine name**: Enter `VM-Primary`.
   * **Region**: Select `Central US`.
   * **Availability options**: Choose **Availability Set**.
   * **Availability set**: Select the set you just created.
   * **Image**: Select **Ubuntu Server 20.04 LTS - x64 Gen2**.
   * **Size**: Click **See all sizes**, then choose **B2s**, and confirm.
   * **Authentication type**: Choose **Password**.
   * **Username**: Enter a desired username (e.g., `adminuser1`).
   * **Password**: Enter a secure password (e.g., `SecurePass123!`).
   * **Confirm password**: Re-enter the same password.
4. In the **Disks** tab, select the OS disk type as **Standard SSD** or **Standard HDD**.
5. Click **Review + Create**, then click **Create** to deploy the virtual machine.

---

### **Deploy the Second Virtual Machine in the Same Availability Set**

1. Select **Create a resource** again.
2. Under **Compute**, choose **Virtual Machine**.
3. Provide the following configuration:

   * **Resource group**: Use the same one as before.
   * **Virtual machine name**: Enter `VM-Secondary`.
   * **Region**: Select `Central US`.
   * **Availability options**: Choose **Availability Set**.
   * **Availability set**: Select the previously created set.
   * **Image**: Choose **Ubuntu Server 24.04 LTS - x64 Gen2**.
   * **Size**: Choose **B2s** under **See all sizes**, then confirm.
   * **Authentication type**: Select **Password**.
   * **Username**: Enter a different user name (e.g., `adminuser2`).
   * **Password**: Enter a secure password (e.g., `SecurePass456!`).
   * **Confirm password**: Re-enter the password.
4. In the **Disks** tab, choose **Standard SSD** or **Standard HDD** as the OS disk type.
5. Click **Review + Create**, then click **Create** to complete deployment.

---

**Delete all the resources.**

---
---

## **Lab Summary: Creating an Availability Set in Azure**

### **Purpose of the Lab**

The primary objective of this lab is to demonstrate how to improve the **high availability** of applications running in **Azure virtual machines (VMs)** by using **Availability Sets**. An **Availability Set** ensures that VMs are distributed across multiple physical servers, compute racks, storage units, and network switches within a region. This distribution helps protect applications from single points of failure in the data center infrastructure.

By the end of the lab, users will have:

* Created an **Availability Set**.
* Deployed two **Virtual Machines** within the same **Availability Set**.
* Understood how **fault domains** and **update domains** improve reliability and availability.

---

### **Azure Tools Utilized**

#### 1. **Azure Portal**

* **Description**: A web-based management interface provided by Azure.
* **Role in Lab**: Used for all resource creation and configuration tasks including VMs and availability sets.

#### 2. **Availability Set**

* **Description**: A logical grouping of VMs that allows Azure to distribute these VMs across fault domains and update domains.
* **Role in Lab**: Central to the lab objective; it ensures that if one VM goes down due to planned maintenance or hardware failure, the others remain operational.

#### 3. **Virtual Machine (VM)**

* **Description**: A compute resource in Azure that emulates a physical computer.
* **Role in Lab**: Two VMs are deployed in the same **Availability Set** to demonstrate resilience and distribution across domains.

#### 4. **Resource Group**

* **Description**: A container that holds related Azure resources.
* **Role in Lab**: All resources (VMs and the availability set) are created within a designated **Resource Group** for organized management and easier deletion.

#### 5. **Managed Disks**

* **Description**: Azure-managed block-level storage volumes used with Azure VMs.
* **Role in Lab**: Enables high availability for VM storage within an **Availability Set** using aligned storage configurations.

#### 6. **OS Images (Ubuntu Server)**

* **Description**: Pre-configured operating system templates used to create VMs.
* **Role in Lab**: Ubuntu Server 20.04 LTS and 24.04 LTS are used as the base images for the virtual machines in this lab.

#### 7. **Compute Category**

* **Description**: A classification in the Azure Marketplace where all computing-related resources are listed.
* **Role in Lab**: Selected during the resource creation process to launch new **Virtual Machines**.

---

### **Real-World Relevance**

In production environments, **Availability Sets** are critical for meeting **Service-Level Agreements (SLAs)**. By understanding how to deploy VMs using **Availability Sets**, organizations can build resilient architectures that maintain uptime during system maintenance or unexpected hardware failures. This lab simulates a practical scenario for IT professionals, system administrators, and cloud architects working on enterprise-grade infrastructure.

---
---

## **Practical Scenario: Ensuring Application Availability with Azure Availability Sets**

### **Scenario:**

Emma is a **Cloud Infrastructure Engineer** working for a medium-sized e-commerce company called **NorthTrade Solutions**. The company hosts its product catalog and internal order management system on a set of **Linux-based virtual machines**. Recently, NorthTrade experienced unexpected downtime when maintenance updates affected both of their servers at once, interrupting business operations for nearly 45 minutes.

To prevent such issues in the future, Emma is tasked with redesigning the infrastructure to improve **availability** and meet the company's internal **uptime SLA** of 99.95%. After consulting with her team and reviewing Azure’s built-in capabilities, she decides to deploy the web application VMs using an **Availability Set** in **Azure**.

---

### **Implementation Steps:**

#### **Step 1: Create an Availability Set**

Emma logs into the **Azure portal**, navigates to **Create a resource**, and searches for **Availability Set**. She selects her existing **resource group**, assigns a name to the set, chooses the **Central US** region, and enables **managed disks** to ensure storage reliability. This **Availability Set** will distribute VMs across different **fault domains** and **update domains**, protecting against both hardware failures and scheduled maintenance events.

> **Benefit:** By using an **Availability Set**, Emma ensures that not all VMs are impacted simultaneously during Azure’s infrastructure updates.

---

#### **Step 2: Deploy the First Virtual Machine**

Emma proceeds to deploy her first **Virtual Machine** named **AppServer01**. She selects the **Ubuntu Server 20.04 LTS** image, configures a **B2s** size, and enters secure credentials. She explicitly selects the previously created **Availability Set**, ensuring that this VM becomes part of a fault-tolerant infrastructure.

> **Benefit:** Including the VM in the **Availability Set** guarantees it will reside on separate physical hardware than other VMs in the same set, minimizing single points of failure.

---

#### **Step 3: Deploy the Second Virtual Machine**

After the first VM is deployed, Emma refreshes the **Availability Set** and begins creating the second **Virtual Machine**, named **AppServer02**, this time using **Ubuntu Server 24.04 LTS** to test the newer OS version. Again, she chooses the same **Availability Set** and configures a different username and secure password.

> **Benefit:** Deploying multiple VMs within an **Availability Set** ensures redundancy. Even if one VM is rebooted during maintenance, the other continues to serve traffic.

---

#### **Step 4: Connect and Verify**

Emma RDPs (for Windows) or SSHs (for Linux) into the newly created VMs, verifies system performance, and checks connectivity between the two servers. Both machines are up and running, each residing in different **update domains** and **fault domains**.

---

### **Business Impact and Conclusion**

By leveraging **Azure Availability Sets**, Emma’s team now benefits from a more resilient architecture. The application will remain operational even during routine platform maintenance or localized hardware failures. This simple design decision ensures that **NorthTrade Solutions** maintains service continuity, improves customer trust, and aligns with IT compliance policies.

This scenario clearly demonstrates how using native Azure features like **Availability Sets**, **Virtual Machines**, and **Managed Disks** can help businesses meet their **high availability** goals without incurring additional costs or complexity.

---
---
## Lab-Based Conceptual MCQs

1. **What is the primary purpose of using an Availability Set in Azure?**  
(a) To increase storage capacity of VMs  
(b) To automatically scale applications  
(c) To ensure VMs are distributed across fault and update domains  
(d) To reduce bandwidth usage  
**Correct answer: (c)**  
**Explanation**: **Availability Sets** ensure that VMs are placed across multiple **fault domains** and **update domains**, minimizing downtime during hardware failure or maintenance.

2. **Why is it recommended to use managed disks with Availability Sets?**  
(a) Managed disks cost less than unmanaged disks  
(b) They support automatic backups  
(c) They simplify disk management and are aligned with high availability scenarios  
(d) They allow external data migration  
**Correct answer: (c)**  
**Explanation**: **Managed disks** are more reliable and support placement rules that enhance the effectiveness of **Availability Sets**.

3. **What does an update domain in an Availability Set represent?**  
(a) A physical rack of servers  
(b) A group of VMs that are updated together  
(c) A region-wide backup location  
(d) A logical container for OS upgrades  
**Correct answer: (b)**  
**Explanation**: An **update domain** groups VMs that may be rebooted together during planned maintenance.

4. **How does an Availability Set contribute to SLA guarantees?**  
(a) By encrypting all VM data  
(b) By ensuring zero-cost deployment  
(c) By reducing the chance of simultaneous VM downtime  
(d) By enabling multi-region backup  
**Correct answer: (c)**  
**Explanation**: **Availability Sets** reduce simultaneous downtime, helping achieve higher **availability SLAs**.

5. **Which VM property must match when adding VMs to the same Availability Set?**  
(a) VM size  
(b) Disk type  
(c) Region  
(d) Public IP address  
**Correct answer: (c)**  
**Explanation**: All VMs in an **Availability Set** must reside in the same **region** to ensure correct fault domain allocation.

6. **What happens if you try to add an existing VM to an Availability Set?**  
(a) It gets reallocated automatically  
(b) You must delete and recreate the VM  
(c) Azure adds it to a new set  
(d) A warning is shown but allowed  
**Correct answer: (b)**  
**Explanation**: An existing VM cannot be moved into an **Availability Set**. It must be redeployed.

7. **What is the benefit of deploying VMs across multiple fault domains?**  
(a) To enable faster networking  
(b) To isolate VMs on different hardware to prevent simultaneous failure  
(c) To ensure application load balancing  
(d) To reduce VM pricing  
**Correct answer: (b)**  
**Explanation**: **Fault domains** provide hardware separation to improve resilience.

8. **Why is a refresh required before deploying the second VM into the same Availability Set?**  
(a) To enable internet access  
(b) To clear cache issues  
(c) To ensure the set updates with the newly created infrastructure  
(d) To install monitoring tools  
**Correct answer: (c)**  
**Explanation**: A refresh allows Azure to reflect changes made to the **Availability Set** for use with subsequent VM deployments.

9. **Which operating systems were deployed in the lab's virtual machines?**  
(a) Windows Server 2022 and Ubuntu 18.04  
(b) Ubuntu 20.04 and Ubuntu 24.04  
(c) CentOS 7 and Ubuntu 20.04  
(d) Ubuntu 16.04 and Windows 10  
**Correct answer: (b)**  
**Explanation**: The lab used **Ubuntu Server 20.04 LTS** and **Ubuntu Server 24.04 LTS** to demonstrate fault-tolerant deployment.

10. **What is a key operational requirement when deploying VMs in an Availability Set?**  
(a) Ensure VM names are identical  
(b) Use different OS images  
(c) Use the same resource group and region  
(d) Avoid using managed disks  
**Correct answer: (c)**  
**Explanation**: VMs in an **Availability Set** must be deployed in the same **resource group** and **region** to be placed correctly across domains.

---
