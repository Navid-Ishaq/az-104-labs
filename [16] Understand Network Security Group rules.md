# Lab 16: Understand Network Security Group rules

**Duration:** 1h 0m

---
---

**After logging in with your credentials:**

### Step 1: Create a Virtual Machine

1. In the Azure portal search bar, type **Virtual Machines** and select it.

2. Click on **+ Create** > **Azure virtual machine**.

3. In the **Basics** tab, configure the following:

   * **Resource group**: Select `rg_westeurope_XXXXX`
   * **Virtual machine name**: `myVM1`
   * **Region**: `West Europe`
   * **Availability options**: No infrastructure redundancy required
   * **Security type**: Standard
   * **Image**: Windows Server 2022 Datacenter – Azure Edition – Gen2
   * **Size**: Click **See all sizes**, choose **Standard\_B2s**, click **Select**
   * **Username**: Provide a username
   * **Password**: Provide and confirm a secure password
   * **Public inbound ports**: Select **None**

4. Click **Next: Disks**, and choose **Standard SSD** for OS disk type.

5. Click through **Networking**, **Management**, and in the **Monitoring** tab, set **Boot diagnostics** to **Disabled**.

6. Click **Review + create**, then click **Create**.

---

### Step 2: Create an NSG Rule to Allow RDP (Port 3389)

1. In the Azure portal, go to **Virtual Machines** and select `myVM1`.
2. In the VM’s menu, go to **Networking**.
3. Click **+ Add inbound port rule** and configure:

   * **Source**: Service Tag
   * **Source service tag**: Internet
   * **Destination**: Any
   * **Service**: RDP
   * **Action**: Allow
   * **Priority**: `100`
   * **Name**: `myport_3389`
4. Click **Add** to create the rule.

---

### Step 3: Connect to the Virtual Machine via RDP

1. Go to the **Overview** tab of the VM.
2. Click **Connect** > **RDP** > **Download RDP File**.
3. Open the RDP file and log in using the credentials set earlier.

---

### Step 4: Enable HTTP Traffic and Configure IIS Web Server

1. On the VM, open **Server Manager** > **Add Roles and Features**.
2. Proceed through the wizard until you reach **Server Roles**, then check **Web Server (IIS)**.
3. Click **Next** until the **Install** option appears, then click **Install**.
4. After installation, open **Microsoft Edge** and go to `http://localhost` to confirm IIS is running.

---

### Step 5: Create an NSG Rule to Allow HTTP (Port 80)

1. Back in the Azure portal, go to **Virtual Machines** > `myVM1` > **Networking**.
2. Click **+ Add inbound port rule** and configure:

   * **Source**: Service Tag
   * **Source service tag**: Internet
   * **Destination**: Any
   * **Destination port ranges**: `80`
   * **Action**: Allow
   * **Priority**: `110`
   * **Name**: `myport_80`
3. Click **Add** to save the rule.

---

### Step 6: Test Web Server Access

1. In the **Networking** section of your VM, copy the **public IP address**.
2. Open a web browser and go to `http://<public-ip>` to view the default IIS web page.

---

**Delete all the resources.**

---
---
## **Structured Lab Summary: Understanding Network Security Group (NSG) Rules**

### **Purpose of the Lab**

The purpose of this lab is to **demonstrate how to manage and control network traffic to and from an Azure Virtual Machine using Network Security Group (NSG) rules**. This includes allowing or denying traffic such as **Remote Desktop Protocol (RDP)** and **HTTP** through specified **inbound port rules**. By completing this lab, learners gain hands-on experience with **NSG rule creation, VM deployment, and security configuration**—skills that are critical for maintaining secure and accessible cloud infrastructure in real-world scenarios.

---

### **Azure Tools Utilized in the Lab**

Below is a detailed list of key **Azure tools and services** used in this lab, including their definitions, functions, and examples for better clarity.

---

### **1. Azure Virtual Machine (VM)**

**Definition**: A scalable computing resource in Azure that acts like a virtualized server running either Windows or Linux.
**Role in Lab**: A **Windows Server 2022** virtual machine is created to serve as the target for **NSG rule testing**, such as enabling **RDP** and hosting a **web server via IIS**.
**Example**:

```plaintext
Virtual Machine Name: myVM1  
Image: Windows Server 2022 Datacenter - Gen2  
Size: Standard_B2s
```

---

### **2. Network Security Group (NSG)**

**Definition**: A virtual firewall that filters network traffic to and from **Azure resources** based on **security rules**.
**Role in Lab**: **NSG rules** are created to explicitly **allow RDP (port 3389)** and **HTTP (port 80)** traffic to the VM.
**Example Rule for RDP**:

* **Source**: Service Tag → Internet
* **Destination**: Any
* **Port**: 3389
* **Action**: Allow
* **Priority**: 100

**Example Rule for HTTP**:

* **Port**: 80
* **Action**: Allow
* **Priority**: 110

---

### **3. RDP (Remote Desktop Protocol)**

**Definition**: A protocol used to remotely access the graphical interface of a Windows machine.
**Role in Lab**: Enabled via NSG to allow administrative access to the virtual machine.
**Example**:
Using RDP to connect to the VM after downloading the `.rdp` file from the Azure portal.

---

### **4. Internet Information Services (IIS)**

**Definition**: A web server software package designed for Windows Server to host web applications and services.
**Role in Lab**: Installed inside the virtual machine to test the **HTTP NSG rule**, confirming that web traffic can reach the VM.
**Example**:
Opening a browser inside the VM and visiting `http://localhost` should display the IIS welcome page.

---

### **5. Azure Portal**

**Definition**: A web-based user interface for managing all Azure services.
**Role in Lab**: Used to perform all steps—**creating resources**, **configuring NSGs**, **deploying the VM**, and **testing access**.
**Example**:
Navigating to “Virtual Machines” from the search bar to view or manage deployed VMs.

---

### **6. Resource Group**

**Definition**: A logical container that holds related Azure resources.
**Role in Lab**: The VM and its associated components (e.g., NSG, public IP, NIC) are organized under a specific **resource group** for management.
**Example**:
Resource Group: `rg_westeurope_XXXXX`

---

### **7. Public IP Address**

**Definition**: A unique IP address assigned to a VM or resource so it can be accessed from the internet.
**Role in Lab**: Used to **access the VM via RDP** and to **test HTTP access** from a browser.
**Example**:
Using the copied public IP in a browser: `http://<public-ip>`

---

### **8. Azure Disk (Standard SSD)**

**Definition**: A type of storage option for Azure VMs, offering a balance between cost and performance.
**Role in Lab**: Used as the OS disk for the deployed virtual machine.
**Example**:
OS disk type selected as **Standard SSD** during VM creation.

---

By the end of this lab, learners are expected to understand the **principles of access control** using NSGs, how to configure **RDP and web server access**, and how **Azure infrastructure components** work together to support secure deployments. These skills are vital for any cloud administrator, security engineer, or developer working in production-grade environments.

---
---
## **Professional Scenario: Implementing NSG Rules to Secure a Production VM**

### **Scenario Title: “David Secures a Web Server in Azure”**

**David**, a cloud engineer at a mid-sized IT services company, has just been assigned a task by his manager: deploy a **Windows Server virtual machine** in **Microsoft Azure**, configure it as a basic **web server**, and ensure that **only necessary ports are open** to reduce security risks. The project is for a client who needs a test environment to simulate real traffic to a public-facing application.

---

### **Step 1: Creating a Virtual Machine**

To begin, David signs into the **Azure Portal** using his organization’s credentials. He opens the **Virtual Machines** service and clicks **Create → Azure virtual machine**.

He configures the VM with the following:

* **Resource Group**: `rg-west-test`
* **Virtual Machine Name**: `ProdVM-Web1`
* **Region**: `West Europe`
* **Image**: `Windows Server 2022 Datacenter - Gen2`
* **Size**: `Standard_B2s`
* **Username**: `adminuser`
* **Password**: `StrongPa$$word123`
* **Inbound Ports**: **None** (David plans to control access via **Network Security Group (NSG)**)

He selects **Standard SSD** for the OS disk, leaves networking and management settings as default, **disables boot diagnostics**, and finally reviews and clicks **Create**.

🛠️ *At this point, David has provisioned a basic VM, but it’s not accessible from the outside yet because no network rules are applied.*

---

### **Step 2: Allowing RDP Access for Remote Management**

David now needs to access the VM remotely using **Remote Desktop Protocol (RDP)**. He goes to the **Networking** tab of the newly created VM and sees an attached **NSG**.

He clicks on **“Add inbound port rule”** to allow RDP traffic.

* **Source**: `Service Tag`
* **Source Service Tag**: `Internet`
* **Destination**: `Any`
* **Service**: `RDP`
* **Action**: `Allow`
* **Priority**: `100`
* **Name**: `Allow-RDP-3389`

After saving the rule, he goes back to the **Overview** tab, clicks **Connect → RDP**, and downloads the `.rdp` file. Using his credentials, David remotely logs into the server.

🎯 *He now has secure access to configure the machine as needed.*

---

### **Step 3: Installing IIS to Serve Web Content**

Inside the VM, David opens **Server Manager**, then uses the **Add Roles and Features** wizard to install **Web Server (IIS)**.

After installation, he launches **Microsoft Edge** on the VM and visits `http://localhost` to verify that the **IIS welcome page** is live.

---

### **Step 4: Creating an NSG Rule to Allow HTTP Traffic**

To make the IIS web server accessible to others, David needs to allow traffic on **port 80**. He returns to the **Azure Portal**, goes to the VM’s **Networking** section, and adds another inbound rule:

* **Source**: `Service Tag`
* **Source Service Tag**: `Internet`
* **Destination**: `Any`
* **Destination Port Ranges**: `80`
* **Protocol**: `TCP`
* **Action**: `Allow`
* **Priority**: `110`
* **Name**: `Allow-HTTP-80`

After applying the rule, David copies the **public IP address** of the VM and pastes it into his local browser:
`http://<public-ip>`

The **IIS welcome page** loads successfully, confirming that the **web server is publicly accessible** over **HTTP**, and access is securely controlled via **NSG rules**.

---

### **Why This Scenario Matters**

David’s actions reflect a **real-world use case**:

* He **only opens necessary ports** (**3389 for RDP**, **80 for HTTP**) — reducing attack surface.
* He uses **Network Security Groups** to enforce **inbound traffic control**.
* He ensures the VM is **secure yet accessible**, adhering to best practices in cloud deployments.

This workflow is foundational for many business applications — whether it’s hosting internal tools, staging web applications, or providing remote access to managed servers.

---

### **Summary of Key Azure Concepts Demonstrated**

* **Azure Virtual Machine**: Hosted workload that requires controlled access.
* **Network Security Group (NSG)**: Firewall-like rules applied at the network interface level.
* **Inbound Rules**: Explicitly allow or deny incoming traffic to the VM.
* **RDP (port 3389)**: Allows remote administration of Windows VMs.
* **HTTP (port 80)**: Used to serve web content from IIS.
* **Public IP Address**: Enables external users to reach the VM or service.

---

This scenario helps learners understand how to **securely expose services** in Azure while maintaining **network hygiene and control**—skills critical for cloud administrators and DevOps professionals.

---
---

## ✅ How David Completed His Task – Explained Simply

### 👨‍💼 Who is David?

David is a cloud engineer. That means he helps his company use online tools (like Microsoft Azure) to run computers, websites, and services without needing physical machines.

---

### 🎯 What Was David’s Goal?

David's boss asked him to:

* **Create a virtual computer** in the cloud.
* **Install a website on it** (called a web server).
* **Let people access it** safely from the internet.
* **Make sure only allowed traffic comes in** (to keep it secure).

---

## 🪜 Step-by-Step – What David Did

### 🖥️ Step 1: Created a Virtual Computer (VM)

* David logged into Microsoft Azure (a website where you can create online computers).
* He clicked to **create a virtual machine** (this is just a computer in the cloud).
* He gave it a name and chose settings like the location (**West Europe**) and operating system (**Windows Server**).
* He also set up a **username and password** to log in later.

🧠 *Think of this like buying a brand-new laptop, but it lives on the internet.*

---

### 🔐 Step 2: Allowed Remote Access (RDP)

* At first, the computer was created, but **no one could connect to it**.
* David opened something called **Network Security Group (NSG)** — it’s like a list of rules that control who can talk to the computer.
* He **added a rule** to allow remote access (called **RDP**, which is used to connect to Windows machines).
* After this, David was able to **log into the computer remotely**, just like using TeamViewer or Zoom screen share.

🧠 *Now David can "sit" at this virtual computer from anywhere.*

---

### 🌐 Step 3: Installed a Website Server (IIS)

* David used a tool inside the computer called **Server Manager**.
* He **installed IIS**, a program that lets the computer act like a website host.
* Then he tested it by visiting **[http://localhost](http://localhost)**, and it worked — the computer was ready to show a webpage.

🧠 *This step is like putting a sign on a shop window saying “We’re open!”*

---

### 🌎 Step 4: Let the Public See the Website

* Even though the website was working inside the computer, **no one outside could see it yet**.
* David added another rule in the NSG to **allow traffic on port 80** (used for websites).
* He copied the **public IP address** of the computer and pasted it in his own browser.

🎉 He saw the website live from the internet!

🧠 *This is like opening the shop doors to customers.*

---

## ✅ Why David’s Work Was Efficient

* He did everything **step by step**, without missing anything.
* He **only opened the ports he needed** (just RDP and HTTP), which is safe.
* He **tested** each part — the login, the website inside, and the public access.
* He kept it **clean, organized**, and **secure**.

---

## 🧾 Summary for Beginners

| What David Did                | Why It Was Important                         |
| ----------------------------- | -------------------------------------------- |
| Created a virtual computer    | To have a place to run the website           |
| Allowed remote access (RDP)   | So he could set it up from his own PC        |
| Installed web server (IIS)    | To host a basic website                      |
| Allowed website access (HTTP) | So users on the internet can view it         |
| Followed security rules       | To protect the computer from unwanted access |

---

### 💡 Final Thought

David followed **a simple but smart plan**. Even without being an expert, anyone can understand the logic:

> "Only allow what you need, test everything, and keep it secure."

That’s why **David completed his task efficiently and professionally.**

---
---
## Lab-Based Conceptual MCQs

**1. What is the primary purpose of a Network Security Group (NSG) in Azure?**  
(a) To manage DNS settings  
(b) To encrypt virtual machine disks  
(c) To control inbound and outbound traffic to network interfaces or subnets  
(d) To create virtual networks automatically  
**Correct answer: (c)**  
**Explanation:** **NSGs** are used to define and enforce **security rules** that allow or deny traffic to **network interfaces, VMs, and subnets**.

**2. Why is port 3389 allowed in the NSG for this lab scenario?**  
(a) To enable HTTP traffic  
(b) To enable remote desktop access to the VM  
(c) To allow database connections  
(d) To connect to Azure CLI  
**Correct answer: (b)**  
**Explanation:** **Port 3389** is used for **Remote Desktop Protocol (RDP)**, which allows users to connect to **Windows virtual machines**.

**3. What is the effect of setting a lower priority number in an NSG rule?**  
(a) It disables the rule  
(b) It increases latency  
(c) It makes the rule get evaluated earlier  
(d) It removes other rules  
**Correct answer: (c)**  
**Explanation:** **NSG rules** are evaluated in order of **priority**, and the **lower the number**, the **higher the priority**.

**4. When David installed the IIS role, what functionality did he add to his virtual machine?**  
(a) Database hosting capability  
(b) File sharing feature  
(c) Remote login feature  
(d) Web server capability  
**Correct answer: (d)**  
**Explanation:** **IIS (Internet Information Services)** allows a Windows server to host and serve **web content**, turning the VM into a **web server**.

**5. Why did David disable boot diagnostics during VM creation?**  
(a) To improve security  
(b) To reduce VM cost  
(c) To enable automatic scaling  
(d) To disable logs completely  
**Correct answer: (b)**  
**Explanation:** Disabling **boot diagnostics** avoids storing logs and screenshots, slightly reducing **costs**, which may be suitable in **lab or test environments**.

**6. What is the function of port 80 in this scenario?**  
(a) Used for secure HTTPS traffic  
(b) Used for file transfers  
(c) Used for web server HTTP traffic  
(d) Used for remote desktop login  
**Correct answer: (c)**  
**Explanation:** **Port 80** is the default port for **HTTP** traffic, which is essential for accessing websites hosted on a **web server**.

**7. What would happen if both RDP and HTTP rules were not added in the NSG?**  
(a) The VM would still be accessible publicly  
(b) The VM would be fully functional  
(c) The VM would not allow external access on those ports  
(d) Only outbound access would be affected  
**Correct answer: (c)**  
**Explanation:** Without explicit **inbound rules** in the **NSG**, the VM would **not allow traffic** on **ports 3389 and 80**.

**8. Why was the “Source” in NSG rules set to 'Service Tag: Internet'?**  
(a) It limits access to internal VMs only  
(b) It allows any traffic from the internet  
(c) It restricts traffic to VPN clients only  
(d) It blocks all external traffic  
**Correct answer: (b)**  
**Explanation:** Selecting **Service Tag: Internet** allows traffic from **any public IP**, enabling access from users across the **internet**.

**9. How does Azure uniquely identify and route traffic to a VM within a virtual network?**  
(a) MAC address  
(b) Public key  
(c) IP address  
(d) DNS hostname  
**Correct answer: (c)**  
**Explanation:** Azure uses **IP addresses** (public or private) to **route traffic** to and from a virtual machine.

**10. What is the primary benefit of using NSG over manually configuring the Windows firewall for access rules?**  
(a) NSG rules are automatically encrypted  
(b) NSG rules are easier to audit and manage at scale  
(c) Windows firewall offers better security  
(d) NSGs are only for internal traffic  
**Correct answer: (b)**  
**Explanation:** **NSG rules** allow centralized **management of traffic**, scalable across **multiple VMs**, which is more efficient than managing **firewall rules per VM**.

---
---
## Professional Job Interview Questions – AZ-104 Labs

1. **An Azure administrator** needs to enable secure remote access to a newly created **Windows virtual machine** that has no public inbound port open. What is the most appropriate step to take?

   (a) Create an outbound rule in the **NSG** to allow port 3389  
   (b) Add an inbound rule to the **NSG** to allow port 3389 from the Internet  
   (c) Assign a public IP to the VM without modifying **NSG** rules  
   (d) Install a VPN Gateway to the virtual network  

   **Correct answer:** (b)  
   **Explanation:** To allow remote desktop access via **RDP (port 3389)**, an inbound **NSG rule** must be created to permit traffic from the Internet. A public IP alone does not open the required port.

2. A company wants to host an internal website accessible only within their **virtual network**. Which of the following actions should the administrator take?

   (a) Open port 80 to the Internet via NSG  
   (b) Associate a public IP with the web server  
   (c) Use private IP and restrict **NSG** rules to internal subnets  
   (d) Use a Load Balancer with public frontend  

   **Correct answer:** (c)  
   **Explanation:** For internal websites, private IP addressing combined with **NSG rules** scoped to internal subnets ensures the website is isolated from public internet access.

3. After deploying a **virtual machine**, an admin installs the **IIS web server** and wants users to access it externally. What is the next required step?

   (a) Reboot the virtual machine  
   (b) Open port 443 via NSG  
   (c) Create a custom DNS record  
   (d) Add an inbound **NSG rule** for port 80  

   **Correct answer:** (d)  
   **Explanation:** To access a web server running on port 80, an inbound rule in the **Network Security Group** must be created to allow HTTP traffic.

4. Your security team has requested that only specific IP ranges access the VM through **RDP**. What should you configure?

   (a) Modify the subnet mask  
   (b) Set source as **IP Addresses** in the **NSG** rule  
   (c) Use a service tag for "Internet"  
   (d) Disable NSG entirely  

   **Correct answer:** (b)  
   **Explanation:** NSG rules allow fine-grained control, including setting specific source **IP ranges** to control who can access services like RDP.

5. You’ve created a **Windows Server VM** but cannot connect via RDP. What should you verify first?

   (a) The OS version compatibility  
   (b) Whether boot diagnostics are enabled  
   (c) That port 3389 is allowed via **NSG** inbound rule  
   (d) VM region availability  

   **Correct answer:** (c)  
   **Explanation:** RDP requires **NSG rules** that permit traffic on port 3389. Without this, the connection will be blocked.

6. An organization needs to deploy an application that listens on **port 8080**. What is the proper way to allow external access to it?

   (a) Change the application port to 80  
   (b) Add an **NSG inbound rule** for port 8080  
   (c) Use a VPN to route all traffic  
   (d) Install Azure Bastion  

   **Correct answer:** (b)  
   **Explanation:** To expose a non-standard port like 8080, an **NSG rule** must explicitly allow that port in the inbound direction.

7. A VM has been deployed but is not responding to **HTTP** requests from external users. What is the likely cause?

   (a) HTTP is blocked by the Windows firewall  
   (b) VM is not assigned a public IP  
   (c) Inbound rule for port 80 is missing in **NSG**  
   (d) VM diagnostics is turned off  

   **Correct answer:** (c)  
   **Explanation:** Access via HTTP requires port 80 to be open. This must be configured in the VM’s associated **NSG**.

8. To enhance security, an admin wants to remove RDP access after maintenance. What is the best approach?

   (a) Remove the public IP  
   (b) Stop the virtual machine  
   (c) Delete the NSG rule for port 3389  
   (d) Change the admin password  

   **Correct answer:** (c)  
   **Explanation:** Removing the **NSG rule** that allows port 3389 effectively disables RDP access without stopping the VM or affecting other services.

9. A developer deployed a web application but cannot access it using the public IP. What is the first step to troubleshoot?

   (a) Restart the application  
   (b) Check **NSG inbound rules** for port 80  
   (c) Redeploy the virtual machine  
   (d) Add a public load balancer  

   **Correct answer:** (b)  
   **Explanation:** Access to web applications over the Internet requires open port 80. **NSG rules** must be validated for correct configuration.

10. You want to prevent all internet access to a VM except for **RDP** from a specific subnet. What should you do?

   (a) Create a deny-all outbound NSG rule  
   (b) Allow Internet as the source  
   (c) Use **NSG rule** with subnet-level source filtering  
   (d) Remove the public IP  

   **Correct answer:** (c)  
   **Explanation:** Using subnet-level filtering in **NSG rules** allows access only from specific subnets while denying other traffic, including general Internet access.

---
---
