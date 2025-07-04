# Lab 12: Deploying Software with VM Extensions

**Duration:** 45m

After logging in with your credentials:

### Step-by-Step Instructions to Deploy Software with VM Extensions

---

### **Create a Windows Virtual Machine**

1. In the Azure Portal, search for **Virtual Machines** from the top search bar.
2. Click on **Create** > **Azure virtual machine**.
3. In the **Basics** tab, fill in the following:

   * **Resource group**: Select `rg_eastus_XXXXX`.
   * **Virtual machine name**: `WhizlabsVM`.
   * **Region**: `East US`.
   * **Availability options**: `No infrastructure redundancy required`.
   * **Security type**: `Standard`.
   * **Image**: `Windows Server 2019 Datacenter - x64 Gen2`.
   * **Size**: Click on **See all sizes**, select `B2s`, and confirm selection.
   * **Username**: `WhizlabUser`.
   * **Password**: `User@1234567`.
   * **Confirm password**: `User@1234567`.
4. Under **Disk options**, set **OS disk type** to `Standard SSD`.
5. Leave all other options at their default values and click **Next: Disks >**.
6. In the **Disks** tab, confirm **OS disk type** is set to `Standard SSD`.
7. Click **Review + create**, then click **Create** to deploy the VM.

---

### **Deploy Software Using VM Extensions**

1. After the VM deployment completes, click **Go to resource**.
2. In the left-hand menu, under **Settings**, select **Extensions + applications**.
3. Click **Add** to add a new extension.
4. In the extension list, search for **Network Watcher Agent for Windows** and select it.
5. Click **Next**, then click **Review + create**, and finally **Create**.
6. After deployment, return to **Extensions + applications** to verify the extension was successfully added.

---

### **Remote Desktop into the Windows VM**

1. From the left menu, go to the **Overview** tab of the virtual machine.
2. Click on the **Connect** button, then select **RDP**.
3. Click **Download RDP File**, open the file after download.
4. In the RDP window:

   * Click **Connect**.
   * Choose **Use a different account**.
   * Enter the following:

     * **Username**: `WhizlabUser`
     * **Password**: `User@1234567`
   * Click **OK**.
   * Click **Yes** on the certificate warning prompt.
5. You are now connected to the Windows VM.

---

### **Verify the Software Deployment**

1. On the Windows VM, click the **Windows** start menu and open **Server Manager**.
2. Click **Tools**, then select **Services**.
3. In the Services list, locate and confirm that **Azure Network Watcher Agent** is running.

---

Delete all the resources.

---
---

## **Structured Lab Summary**

### **Purpose of the Lab**

The primary purpose of this lab is to demonstrate how to **deploy software automatically onto an Azure Virtual Machine (VM)** using **VM extensions**. This method allows IT administrators and DevOps professionals to simplify software installation and configuration on Azure VMs without manually logging into each system. It enhances automation, scalability, and consistency when managing enterprise-level infrastructure.

---

### **Azure Tools Utilized and Their Roles**

1. ### **Azure Virtual Machines (VMs)**

   * **Description**: Scalable computing resources in Azure that provide the flexibility of virtualization without needing to buy and maintain physical hardware.
   * **Role in Lab**: A **Windows VM** is provisioned to serve as the target host for software deployment and testing of extensions.

2. ### **Azure Resource Group**

   * **Description**: A logical container that holds related Azure resources.
   * **Role in Lab**: Used to group all resources like the VM, extensions, and network components under one manageable entity.

3. ### **Azure VM Extensions**

   * **Description**: Small applications that provide post-deployment configuration and automation on Azure VMs.
   * **Role in Lab**: The lab deploys the **Network Watcher Agent for Windows** extension to the VM, demonstrating how software and agents can be automatically installed after VM creation.

4. ### **Azure Network Watcher Agent**

   * **Description**: A diagnostic and monitoring agent that collects network traffic data from Azure VMs.
   * **Role in Lab**: Deployed via extension to validate automated software deployment capabilities and provide network monitoring functions.

5. ### **Azure RDP (Remote Desktop Protocol)**

   * **Description**: Allows remote access to the graphical interface of a Windows VM in Azure.
   * **Role in Lab**: Used to verify the successful deployment of the software extension by accessing the VM and checking the running services.

6. ### **Server Manager (within the VM)**

   * **Description**: A Windows tool for managing server roles and features.
   * **Role in Lab**: Used to open the **Services** window and confirm that the **Network Watcher Agent** is running as expected.

7. ### **Azure Portal**

   * **Description**: A web-based interface for managing Azure resources.
   * **Role in Lab**: Used throughout the lab to create, configure, and verify the VM and extensions deployment.

8. ### **Azure Disk Options (Standard SSD)**

   * **Description**: Disk performance and redundancy settings for VM OS disks.
   * **Role in Lab**: Configured to use **Standard SSD**, which provides a balance between performance and cost for general workloads.

9. ### **Azure Connect and RDP Download Tools**

   * **Description**: Features within the Azure portal to establish remote connections to VMs.
   * **Role in Lab**: Used to download the RDP file and connect to the VM for validation purposes.

---

By completing this lab, learners understand how to automate software deployments using **Azure VM extensions**, manage remote access securely, and confirm the success of deployments through standard verification tools — all key skills in modern cloud operations and DevOps workflows.

---
---

## **Real-World Scenario: Automating Software Deployment for a Remote Team**

**Context:**

Meet **Emily**, a Cloud Infrastructure Engineer at a global consulting firm, **SkyTech Solutions**. Her team is responsible for provisioning and maintaining virtual machines for developers working on client environments. A new requirement arises: deploy a **network monitoring agent** to a batch of new **Windows VMs** in the **East US** region — without manually logging in to each instance. Time is tight, and consistency is critical.

---

### **Step 1: Create the Virtual Machine**

Emily logs into the **Azure Portal** and searches for **Virtual Machines**. She clicks **Create > Azure Virtual Machine** to begin the setup.

She selects an existing **resource group** named **rg\_eastus\_DevOps**, then configures the VM with the following:

* **Virtual Machine Name**: `WhizlabsVM`
* **Region**: `East US`
* **Image**: `Windows Server 2019 Datacenter - x64 Gen2`
* **Size**: `Standard B2s`
* **Username/Password**: `WhizlabUser / User@1234567`
* **OS Disk Type**: `Standard SSD`

This ensures the VM is both cost-effective and compatible with standard enterprise applications.

> **Why this matters**: Emily avoids manual setup by defining consistent VM specs upfront. This is important for automating environments for developers or QA teams.

---

### **Step 2: Deploy the Software Using VM Extensions**

Once the VM is created, Emily selects **Go to Resource** and navigates to the **Extensions + applications** tab under Settings.

She clicks **Add**, searches for **Network Watcher Agent for Windows**, and selects it.

After reviewing the configuration, she clicks **Create**.

> **Why this matters**: Instead of logging in and installing the agent manually, Emily uses **VM Extensions** to push the software silently in the background. This eliminates the risk of human error and ensures faster deployment at scale.

---

### **Step 3: Connect via RDP and Verify Deployment**

Emily goes to the **Overview** page of the VM, clicks **Connect**, and downloads the **RDP file**. Using her credentials (**WhizlabUser / User\@1234567**), she connects to the VM.

Inside the VM, she launches the **Server Manager**, goes to **Tools > Services**, and confirms that the **Azure Network Watcher Agent** is up and running.

> **Why this matters**: This step validates that the extension-based deployment worked as intended — a crucial QA step in production rollouts.

---

### **Outcome and Business Value**

By using **Azure VM Extensions**, Emily achieves:

* **Faster deployment** of monitoring agents across multiple machines.
* **Consistent configuration**, reducing the risk of missed or incorrect installations.
* **Improved scalability**, as this method can be integrated into automation pipelines or Infrastructure as Code (IaC) models.
* **Secure and remote access** using **RDP**, helping her work efficiently from anywhere.

---

**Conclusion:**

Emily’s approach aligns with modern DevOps and cloud best practices. Through this lab, learners adopt the same workflow used in real enterprises — making this exercise highly applicable to everyday cloud operations.

---
---

## Lab-Based Conceptual MCQs

**1. Why would an organization use a VM extension to deploy software in Azure?**  
(a) To reduce the VM size  
(b) To avoid configuring disks  
(c) To automate the software installation process  
(d) To change VM location post-deployment  
**Correct answer: (c)**  
**Explanation**: **VM Extensions** allow automation of post-deployment tasks such as software installation, saving time and ensuring consistency.

**2. What is the role of the ‘**Network Watcher Agent for Windows**’ in the VM extension deployment?**  
(a) It enhances disk I/O performance  
(b) It enables network monitoring and diagnostics  
(c) It prevents RDP attacks  
(d) It provides backup services  
**Correct answer: (b)**  
**Explanation**: The **Network Watcher Agent** helps monitor and diagnose networking issues within the VM environment.

**3. Why is **RDP (Remote Desktop Protocol)** used in the context of this lab?**  
(a) To encrypt data in transit  
(b) To connect to the Azure Portal  
(c) To remotely access and manage the Windows VM  
(d) To upload VM extensions  
**Correct answer: (c)**  
**Explanation**: **RDP** is a remote access protocol used to log into and interact with the Windows VM’s desktop environment.

**4. What benefit does using **VM Extensions** provide in a large-scale enterprise environment?**  
(a) Manual error induction  
(b) Redundant infrastructure  
(c) Centralized and automated deployments  
(d) Increased storage limits  
**Correct answer: (c)**  
**Explanation**: **VM Extensions** allow IT admins to centrally manage and automate deployment tasks across many VMs.

**5. During VM creation, why is a **Standard SSD** chosen for OS disk type?**  
(a) It is cheaper than Premium SSD and offers acceptable performance  
(b) It encrypts the OS  
(c) It is required for using VM extensions  
(d) It supports Linux only  
**Correct answer: (a)**  
**Explanation**: **Standard SSD** offers a balanced choice between cost and performance for general workloads.

**6. In what scenario might a **Network Watcher Agent** be most valuable?**  
(a) When configuring DNS settings  
(b) When monitoring traffic flow between VMs  
(c) When installing anti-virus software  
(d) When resizing virtual machines  
**Correct answer: (b)**  
**Explanation**: The **Network Watcher Agent** is used for monitoring and diagnosing network conditions and traffic flow.

**7. Why is the use of variables like `$username` and `$password` recommended in CLI operations?**  
(a) To avoid keyboard errors  
(b) To simplify memory usage  
(c) To enhance scripting and secure credential handling  
(d) To improve CLI rendering  
**Correct answer: (c)**  
**Explanation**: Using variables for **username** and **password** enhances script security and reusability by avoiding hardcoded credentials.

**8. What ensures that the VM extension is successfully installed post-deployment?**  
(a) Viewing the Azure activity log  
(b) RDP into the VM and checking Services  
(c) Monitoring subscription alerts  
(d) Increasing VM size  
**Correct answer: (b)**  
**Explanation**: After deployment, connecting via **RDP** and checking the **Services** list confirms that the extension was installed and is running.

**9. What makes **VM Extensions** an important part of Azure DevOps workflows?**  
(a) They reduce the billing cycle  
(b) They eliminate the need for monitoring  
(c) They support Infrastructure as Code for automation  
(d) They increase Azure credit  
**Correct answer: (c)**  
**Explanation**: **VM Extensions** are often embedded in automation templates to support continuous deployment and configuration as code.

**10. Why might you prefer installing software using VM extensions rather than manually via RDP?**  
(a) Manual installations are faster  
(b) VM extensions are less secure  
(c) Extensions scale better and reduce manual errors  
(d) Manual steps are more documented  
**Correct answer: (c)**  
**Explanation**: **VM Extensions** provide scalable, consistent, and automated software deployment, ideal for enterprise-grade deployments.

---

