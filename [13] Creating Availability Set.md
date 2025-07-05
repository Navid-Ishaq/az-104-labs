# Lab 13: Creating Availability Set

**Duration:** 1h 0m

---
---

After logging in with your credentials:

### Step-by-Step Instructions to Create an Availability Set and Deploy VMs

---

### **Create an Availability Set**

1. In the Azure portal, select **Create a resource** from the menu or Home page.
2. In the search box, enter **Availability Set** and select it from the results.
3. Click **Create**.
4. Fill in the following details:

   * **Resource group**: Choose your assigned resource group (e.g., `rg_eastus_XXXXX`).
   * **Name**: Enter `WhizAvail`.
   * **Region**: Select `Central US`.
   * **Use managed disks**: Choose `Yes (Aligned)`.
5. Click **Review + Create**, then **Create** to provision the availability set.

---

### **Deploy the First Virtual Machine in the Availability Set**

1. From the portal menu or Home page, select **Create a resource**.
2. Under **Compute**, select **Virtual Machine**.
3. Provide the following configuration:

   * **Resource group**: Select the same resource group used for the availability set.
   * **Virtual machine name**: Enter `WhizlabAvail1`.
   * **Region**: Choose `Central US`.
   * **Availability options**: Select `Availability Set`.
   * **Availability set**: Select `WhizAvail`.
   * **Image**: Choose `Ubuntu Server 20.04 LTS - x64 Gen2`.
   * **Size**: Click **See all sizes**, then choose `B2s`, and select it.
   * **Authentication type**: Select `Password`.
   * **Username**: Enter `Whizlabavail1`.
   * **Password**: Enter `Avail@1234567`.
   * **Confirm password**: Enter the same password again.
4. In the **Disks** tab, choose `Standard SSD` or `HDD` for the OS disk type.
5. Click **Review + Create**, then click **Create** to deploy the VM.

---

### **Deploy the Second Virtual Machine in the Same Availability Set**

1. Again, go to **Create a resource**.
2. Under **Compute**, select **Virtual Machine**.
3. Configure with the following settings:

   * **Resource group**: Use the same resource group.
   * **Virtual machine name**: Enter `WhizlabAvail2`.
   * **Region**: Select `Central US`.
   * **Availability options**: Select `Availability Set`.
   * **Availability set**: Choose `WhizAvail`.
   * **Image**: Select `Ubuntu Server 24.04 LTS - x64 Gen2`.
   * **Size**: Choose `B2s` from **See all sizes**, then select it.
   * **Authentication type**: Select `Password`.
   * **Username**: Enter `Whizlabavail2`.
   * **Password**: Enter `Avail2@1234567`.
   * **Confirm password**: Enter the same password again.
4. In the **Disks** tab, select `Standard SSD` or `HDD` for the OS disk type.
5. Click **Review + Create**, then **Create**.

---

**Delete all the resources.**

---
---

## **Lab Summary: Creating an Availability Set in Azure**

### **Purpose of the Lab**

The primary objective of this lab is to demonstrate how to improve the **availability** and **resiliency** of virtual machines in **Microsoft Azure** by deploying them within an **Availability Set**. This setup helps ensure high availability for applications by distributing VMs across multiple **fault domains** and **update domains**, thereby reducing the risk of simultaneous failure. The lab walks through the steps to create an **Availability Set**, deploy two **Virtual Machines (VMs)** into that set, and understand how this configuration supports business continuity and disaster recovery strategies.

---

### **Azure Tools Utilized in the Lab**

1. ### **Azure Portal**

   * **Description**: A web-based unified console for managing Azure resources.
   * **Role in Lab**: Used to create and manage all Azure resources, including the **Availability Set** and **Virtual Machines**.

2. ### **Availability Set**

   * **Description**: A logical grouping capability for isolating VM resources from each other when deployed.
   * **Role in Lab**: Provides **fault domain** and **update domain** isolation to ensure that VMs deployed together are distributed across different physical hardware and update cycles. This enhances the application’s availability during planned or unplanned maintenance.

3. ### **Virtual Machine (VM)**

   * **Description**: An on-demand, scalable computing resource offered by Azure.
   * **Role in Lab**: Two VMs (Ubuntu-based) are deployed within the **Availability Set** to simulate a production-like environment and test redundancy capabilities.

4. ### **Resource Group**

   * **Description**: A container that holds related resources for an Azure solution.
   * **Role in Lab**: Used to logically group all resources created in the lab (e.g., VMs and availability sets), allowing for easier management and deletion.

5. ### **Managed Disks**

   * **Description**: Azure-managed block-level storage volumes used with Azure VMs.
   * **Role in Lab**: Ensures that disk storage is handled automatically with high availability and alignment with the **Availability Set**.

6. ### **VM Image**

   * **Description**: A template used to create new VMs, including OS and software.
   * **Role in Lab**: Predefined Ubuntu Server images are used to create the two VMs, demonstrating cross-version deployments within the same **Availability Set**.

7. ### **Authentication Type (Password)**

   * **Description**: One of the secure methods to access the VM via SSH or RDP.
   * **Role in Lab**: Used to set up access credentials for each VM during deployment.

8. ### **Review + Create**

   * **Description**: A validation checkpoint before deploying resources.
   * **Role in Lab**: Ensures all configurations are correct before provisioning each VM and the availability set.

---

This lab reinforces essential cloud architecture practices by teaching how to implement **fault-tolerant infrastructure** using native Azure services. By following this guided exercise, learners understand how to minimize service disruptions and architect solutions aligned with **high availability** best practices.

---
---

## **Real-World Scenario: Ensuring Application Uptime with Azure Availability Sets**

**Background**

Emily is a Cloud Infrastructure Engineer at a mid-sized e-commerce company called **NorthCraft Retail**. The company’s operations rely on a custom-built order processing application that must be available 24/7, especially during high-traffic seasons like Black Friday. Recently, Emily's team experienced downtime when both VMs hosting the app were rebooted during scheduled maintenance. This incident prompted leadership to mandate a redesign of the architecture for improved **availability**.

To address this, Emily decides to implement an **Azure Availability Set** to ensure that the virtual machines (VMs) hosting the application are distributed across different **fault domains** and **update domains**. This will significantly reduce the likelihood of simultaneous VM outages due to hardware failures or maintenance events.

---

## **Implementation Journey**

### **Step 1: Create an Availability Set**

Emily logs into the **Azure Portal**, navigates to **Create a resource**, and searches for **Availability Set**. She names the set **WhizAvail**, places it in the **rg\_eastus\_XXXXXX** **resource group**, and selects **Central US** as the region. By enabling **Managed Disks**, she ensures the infrastructure is aligned for maximum uptime and compatibility.

> ✅ **Benefit**: This ensures the application components are distributed across different physical servers, avoiding single points of failure.

---

### **Step 2: Deploy the First VM in the Availability Set**

Emily creates the first VM named **WhizlabAvail1** using the **Ubuntu Server 20.04 LTS** image. She assigns it to the **WhizAvail** **availability set**, ensuring it will be placed in a separate **fault domain** and **update domain** than other VMs in the same set. She chooses **B2s** as the VM **size**, sets **Whizlabavail1** as the **username**, and configures a secure **password**.

> ✅ **Benefit**: Even if one VM is rebooted during Azure maintenance or due to unexpected hardware failure, the other VM continues to serve traffic.

---

### **Step 3: Deploy the Second VM in the Same Availability Set**

After waiting a few minutes to let the platform distribute resources, Emily creates a second VM named **WhizlabAvail2**, this time using **Ubuntu Server 24.04 LTS**. She also places this VM into the same **WhizAvail** **availability set**, following a similar configuration approach with different **username** and **password** credentials.

> ✅ **Benefit**: By having two VMs in different **fault domains**, high availability is achieved without needing more expensive services like **Availability Zones** or **Azure Load Balancer** (though they can be added later).

---

### **Step 4: Application Deployment and Monitoring**

With both VMs in place, Emily can now install the application across both servers. She can use a script or CI/CD pipeline to automate deployment. She monitors both VMs using **Azure Monitor** to ensure they operate independently and maintain performance.

---

## **Outcome**

Thanks to her use of **Availability Sets**, Emily ensures that no single update or physical server issue can bring down the application completely. This aligns with her company's **business continuity** and **SLA (Service Level Agreement)** commitments, while also optimizing costs by using **standard VM SKUs**.

> 💼 **Professional Insight**: For any mission-critical application not yet migrated to **Azure Availability Zones**, **Availability Sets** remain a cost-effective and reliable method for fault isolation.

---

## **Conclusion**

This lab reflects a realistic scenario faced by cloud engineers in maintaining system uptime. It teaches how to strategically distribute virtual machines using **Azure Availability Sets** to protect against outages, support scaling, and align infrastructure with **high availability** design principles.

---
---
## Lab-Based Conceptual MCQs

### 1. What is the primary benefit of using an **Availability Set** in Azure?
(a) It increases virtual machine performance  
(b) It distributes VMs across multiple fault and update domains  
(c) It allows auto-scaling of virtual machines  
(d) It reduces the need for managed disks  
**Correct answer: (b)**  
Explanation: **Availability Sets** ensure that VMs are spread across different physical hardware to improve fault tolerance and availability during maintenance events.

---

### 2. Why should two virtual machines be placed in the same **Availability Set**?
(a) To allow shared network interfaces  
(b) To ensure simultaneous updates  
(c) To distribute VMs across fault domains  
(d) To enable free licensing  
**Correct answer: (c)**  
Explanation: Placing VMs in the same **Availability Set** allows Azure to distribute them across fault and update domains for higher availability.

---

### 3. What would happen if both VMs in a service were placed outside of an **Availability Set**?
(a) They would perform better  
(b) They could be impacted by the same maintenance event  
(c) They would auto-scale  
(d) They would use different OS images  
**Correct answer: (b)**  
Explanation: Without an **Availability Set**, VMs may reside on the same hardware and be rebooted at the same time during maintenance.

---

### 4. In the lab, which operating system image was used for the second VM?
(a) Ubuntu Server 20.04  
(b) Windows Server 2019  
(c) Ubuntu Server 24.04  
(d) CentOS 7  
**Correct answer: (c)**  
Explanation: The second VM was configured with **Ubuntu Server 24.04 LTS**, a newer Linux distribution image.

---

### 5. What is the significance of choosing **Managed Disks** in an **Availability Set**?
(a) They are required for auto-scaling  
(b) They allow manual backup  
(c) They align the infrastructure for redundancy  
(d) They increase VM speed  
**Correct answer: (c)**  
Explanation: **Managed Disks** ensure that VMs in an **Availability Set** align with fault domain guarantees.

---

### 6. Which authentication method was used when creating the virtual machines?
(a) SSH Public Key  
(b) Managed Identity  
(c) Password  
(d) OAuth  
**Correct answer: (c)**  
Explanation: The VMs were created using **Password** authentication, as specified in the lab.

---

### 7. What is the role of the **Review + create** button during resource deployment?
(a) To connect VMs over a private network  
(b) To perform validation before creation  
(c) To auto-assign availability sets  
(d) To back up VM disks  
**Correct answer: (b)**  
Explanation: The **Review + create** button validates configuration settings before initiating deployment.

---

### 8. If a VM is part of an **Availability Set**, what can still occur?
(a) Guaranteed 100% uptime  
(b) Network IP duplication  
(c) Downtime due to application failure  
(d) Shared OS image between VMs  
**Correct answer: (c)**  
Explanation: While **Availability Sets** protect against hardware failures, they don’t prevent downtime caused by software or application issues.

---

### 9. What type of disks were used for OS installation in the lab VMs?
(a) Premium SSD  
(b) Ultra Disk  
(c) Standard SSD or HDD  
(d) Ephemeral OS Disk  
**Correct answer: (c)**  
Explanation: The lab used **Standard SSD or HDD** for the OS disk type to balance performance and cost.

---

### 10. Why is it recommended to wait a few minutes before deploying the second VM in the **Availability Set**?
(a) To allow licensing sync  
(b) To refresh the set's internal configuration  
(c) To enable load balancing  
(d) To change disk encryption  
**Correct answer: (b)**  
Explanation: Waiting ensures that the **Availability Set** updates its backend configurations to distribute new VMs properly across domains.

---
