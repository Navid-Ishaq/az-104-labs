# Lab 11: Create a VM with CLI

**Duration:** 30m

---
---
---

**Lab Summary – Create a VM with CLI**

Naveed, the **Curious Cloud Explorer**, used **Azure CLI in Cloud Shell** to securely define credentials and deploy a **Windows Server 2019 virtual machine** along with all supporting resources like **VNet**, **NSG**, and **Public IP**.
He then connected to the VM using **Remote Desktop Protocol (RDP)** to verify successful deployment and access.
Finally, he cleaned up all the created resources, completing the task efficiently using command-line automation.

---
---
---
**After logging in with your credentials:**

### Create a Virtual Machine Using Azure CLI

1. In the Azure Portal, open **Azure Cloud Shell** by selecting the shell icon in the top menu bar.

2. When prompted, choose **Bash**.

3. If required, choose **No storage account required**, select the available subscription, and click **Apply**.

4. Once Cloud Shell initializes, define the administrator credentials securely using variables:

   ```bash
   username="demouser"
   password="YourSecurePassword123"
   ```

5. Create a Windows Server 2019 virtual machine by running the following command. Replace `<resource-group>` with your actual resource group name:

   ```bash
   az vm create \
     --name MyVm \
     --resource-group <resource-group> \
     --image win2019datacenter \
     --size Standard_B1s \
     --admin-username $username \
     --admin-password $password
   ```

   > This command provisions a Windows VM and automatically deploys associated resources such as a virtual network, subnet, public IP, NIC, and network security group.

### Connect to the Virtual Machine via RDP

1. In the Azure Portal, navigate to **Virtual Machines** from the left-hand menu.

2. Select the **MyVm** virtual machine from the list.

3. On the virtual machine's overview page, click **Connect**, then choose **RDP**.

4. Download the **RDP file**, open it, and log in using the previously defined `$username` and `$password`.

   > On Windows: Open the downloaded `.rdp` file and authenticate.
   > On Linux/Mac: Use an RDP client, enter the VM’s public IP, and authenticate with your credentials.

5. Once connected, confirm that the Windows OS boots and is ready for use.

Delete all the resources.

---
---
---

## 🔍 **Structured Summary: Create a VM with CLI**

### 🎯 **Purpose of the Lab**

This lab teaches how to **create a Windows virtual machine (VM)** using **Azure CLI** within **Azure Cloud Shell**. The objective is to equip learners like **Naveed**, the **Curious Cloud Explorer**, with the ability to automate resource deployment in Azure, including provisioning a VM along with its associated networking and security components. This approach enhances efficiency, repeatability, and control in real-world **DevOps** or **IT operations** tasks.

---

### 🛠️ **Azure Tools and Services Used**

1. ### **Azure Cloud Shell**

   * A browser-based command-line interface that provides pre-authenticated access to **Azure CLI** or **PowerShell**.
   * **Role in Lab**: Naveed uses **Cloud Shell (Bash)** to securely run CLI commands without requiring local configuration.
   * **Example**: Automating VM deployment directly from the portal without needing the Azure CLI installed locally.

2. ### **Azure CLI**

   * A cross-platform command-line tool for managing Azure resources.
   * **Role in Lab**: The central tool Naveed uses to define credentials, create the VM, and deploy the infrastructure components.
   * **Example**: `az vm create` command automates provisioning of the entire virtual machine stack.

3. ### **Virtual Machine (VM)**

   * A scalable computing resource in Azure, typically used to host apps or services.
   * **Role in Lab**: The end product that Naveed creates, using **Windows Server 2019 Datacenter** as the base image.
   * **Example**: A VM that hosts a test web application or development tools.

4. ### **Resource Group**

   * A logical container to group related Azure resources.
   * **Role in Lab**: All deployed resources are grouped under a specified resource group, such as **rg-learntech-naveed**.
   * **Example**: Helps manage costs, permissions, and cleanup of all resources at once.

5. ### **Virtual Network (VNet)**

   * A private network within Azure for securely communicating among resources.
   * **Role in Lab**: Automatically created to allow the VM to communicate with the internet or other Azure services.
   * **Example**: Enables the VM to connect to Azure services like databases or application gateways.

6. ### **Subnet**

   * A range of IP addresses within the VNet.
   * **Role in Lab**: Ensures the VM is placed in a defined IP range within the VNet.
   * **Example**: Helps isolate services or apply specific network rules.

7. ### **Network Interface Card (NIC)**

   * The component that allows the VM to communicate on the network.
   * **Role in Lab**: Assigned to the VM to connect it to the VNet.
   * **Example**: Used for monitoring traffic or applying security policies.

8. ### **Network Security Group (NSG)**

   * A set of firewall rules that control inbound and outbound traffic to network interfaces or subnets.
   * **Role in Lab**: Secures the VM by only allowing necessary traffic, such as **RDP (port 3389)**.
   * **Example**: Only allows remote desktop access while blocking other unauthorized ports.

9. ### **Public IP Address**

   * A unique IP that allows the VM to be accessed from the internet.
   * **Role in Lab**: Enables Naveed to connect via RDP to his Windows VM from any external location.
   * **Example**: Allows remote administration of the VM during setup or troubleshooting.

10. ### **RDP (Remote Desktop Protocol)**

* A protocol that allows users to connect to a Windows-based machine remotely.
* **Role in Lab**: Used by Naveed to verify successful VM creation and interact with the Windows OS.
* **Example**: Used by system admins for remote configuration and software installation.

---

### 🧠 **Clarification Example**

Let’s say Naveed works for **CloudTrainPro** and needs to rapidly spin up a development machine for a contractor. Instead of clicking through the portal, he runs a simple CLI command in **Cloud Shell** that provisions a **Windows VM** with all necessary components. He sends the RDP info to the contractor, who logs in within minutes. This real-world efficiency is why CLI automation is so critical.

---
---
---

### **Structured Summary: Create a VM with CLI (Azure Lab)**

---

#### **Purpose of the Lab**

The objective of this lab is to guide learners through the process of creating a **Windows Virtual Machine (VM)** using the **Azure Command-Line Interface (CLI)**. This hands-on exercise demonstrates how to securely define VM credentials, deploy infrastructure resources via scripted commands, and access the VM using **Remote Desktop Protocol (RDP)**. The lab emphasizes automation, repeatability, and secure practices using command-line tools, which are essential in real-world DevOps and system administration scenarios.

---

#### **Azure Tools Utilized**

1. **Azure Portal**

   * **Description**: A web-based user interface for managing Azure resources.
   * **Role in Lab**: Provides access to **Azure Cloud Shell**, **Virtual Machine overview**, and **resource group management**.

2. **Azure Cloud Shell**

   * **Description**: An in-browser terminal interface provided by Azure that supports **Bash** and **PowerShell** environments.
   * **Role in Lab**: Used to access the **Azure CLI** environment for executing deployment commands securely without local setup.

3. **Azure CLI**

   * **Description**: A cross-platform command-line tool for managing Azure resources via scripted commands or direct input.
   * **Role in Lab**: Used to define VM parameters, authenticate securely, and deploy a **Windows VM** using the `az vm create` command.

4. **Virtual Machine (VM)**

   * **Description**: A scalable computing resource available on demand in Azure, typically used to run applications, services, or test environments.
   * **Role in Lab**: The primary resource created during the lab, used to simulate hosting a Windows server environment.

5. **Resource Group**

   * **Description**: A container that holds related Azure resources, allowing for easier management and lifecycle control.
   * **Role in Lab**: Serves as the logical container into which the VM and all supporting infrastructure are deployed.

6. **Virtual Network (VNet)**

   * **Description**: A logically isolated network within Azure used to securely connect resources.
   * **Role in Lab**: Automatically provisioned during VM creation to provide private networking and subnet configurations.

7. **Network Interface Card (NIC)**

   * **Description**: A virtual network adapter assigned to a VM for communication with other resources over the network.
   * **Role in Lab**: Automatically attached to the VM to enable inbound and outbound traffic through the associated subnet.

8. **Network Security Group (NSG)**

   * **Description**: A firewall-like resource used to define security rules for inbound and outbound traffic.
   * **Role in Lab**: Automatically created to allow **RDP (port 3389)** access to the VM for remote desktop connection.

9. **Public IP Address**

   * **Description**: An IP address exposed to the internet to allow communication with Azure-hosted services.
   * **Role in Lab**: Automatically assigned to the VM to facilitate **RDP** connectivity from an external system.

10. **RDP (Remote Desktop Protocol)**

    * **Description**: A protocol developed by Microsoft that allows users to remotely connect to Windows-based machines.
    * **Role in Lab**: Used to log in to the deployed **Windows VM** to validate access and confirm successful deployment.

---

By the end of this lab, learners gain practical experience in securely automating VM deployments, understanding how CLI integrates with Azure resource provisioning, and how to remotely connect to VMs for further management.

---
---
---

## 🌍 **Real-World Story Scenario: Automating a VM Setup with Azure CLI**

At **CloudTrainPro**, the operations team was short on time and high on demand. They needed to quickly spin up a secure, lightweight **Windows Server 2019 virtual machine** for a developer to test a legacy .NET application. Enter **Naveed**, the ever-curious **CloudOps engineer**, ready to automate the task using the **Azure CLI**.

---

### 🚀 Step 1: The Shell Awakens

Instead of clicking through countless portal tabs, **Naveed** opened the **Azure Cloud Shell** right from the browser. Choosing **Bash** as his environment, he bypassed any local installations and went straight to work. This made it ideal for quick automation tasks, especially when working remotely or on shared workstations.

---

### 🔐 Step 2: Set Secure Credentials

He declared variables for **adminUsername** and **adminPassword** securely within **Cloud Shell**. This approach reduced the chance of mistyped credentials and allowed script reuse. For example:

```bash
username="naveedadmin"
password="StrongP@ssw0rd123!"
```

This made his scripts clean, readable, and easy to modify—important for audits or when sharing configurations with teammates at **SkyStack Labs**.

---

### 🛠️ Step 3: Automate the VM Deployment

The Curious Cloud Explorer then ran the **az vm create** command, targeting the resource group **rg-learntech-naveed**:

```bash
az vm create \
  --name vm-ncloudedge-web01 \
  --resource-group rg-learntech-naveed \
  --image win2019datacenter \
  --size Standard_B1s \
  --admin-username $username \
  --admin-password $password
```

This single command didn’t just create a **virtual machine**. It also deployed related infrastructure: a **virtual network**, **subnet**, **public IP**, **network interface card (NIC)**, and **network security group (NSG)** — all in one go. That’s the power of **CLI automation**: speed and precision.

---

### 🔗 Step 4: Connect and Verify

Minutes later, **Naveed** navigated to **Virtual Machines** in the Azure portal and selected **vm-ncloudedge-web01**. He clicked **Connect > RDP**, downloaded the connection file, and logged in using the secure credentials. The **Windows OS** loaded successfully, and he confirmed that the machine was ready to install testing tools.

This validation step ensures business continuity, as the VM needs to support testing without delays or manual troubleshooting.

---

### 🧹 Step 5: Clean Up

Once the developer confirmed successful testing, the CloudOps engineer ran cleanup operations. Deleting the **resource group rg-learntech-naveed** removed all associated components at once, ensuring no resources were left running, which could incur unnecessary costs.

---

## ✅ **Why This Matters in Real Life**

Using **Azure CLI** is not just a technical exercise — it's a **real-world skill** that improves agility and consistency. Whether provisioning test environments, rolling out dev stacks, or automating deployments in pipelines, CLI commands give **IT admins**, **DevOps engineers**, and **cloud architects** like Naveed a massive edge in managing cloud infrastructure efficiently.

This scenario is a perfect example of **infrastructure as code**, even at a simple level, helping professionals build repeatable, scalable, and secure solutions.

---
---
---
## Comic-Style Summary: **"Click-Free VM Creation with the Power of CLI!"**

---

### 🧢 The Curious Cloud Explorer’s New Challenge

Meet **Naveed**, our trusted CloudOps engineer at **CloudTrainPro**, also known as the **Curious Cloud Explorer**. Today, he was on a mission to quickly set up a **Windows Virtual Machine** — but with a twist: **no clicking around the portal**! He decided to flex his command-line muscles and do it all with the **Azure CLI**.

---

### 💻 Enter the Cloud Shell Arena

Naveed opened the **Azure Cloud Shell** right from the browser. Choosing **Bash**, he skipped any local software or installs — no fuss, just pure cloud power. Like a wizard prepping his tools, he declared his **admin username and password** as variables, ready to summon a VM from the command line.

---

### 🏗️ One Command, Many Resources

Then came the magic spell:

```bash
az vm create ...
```

With one mighty command, **Naveed** launched a **Windows Server 2019 VM** named **vm-ncloudedge-web01**. But that wasn’t all—it also created a **VNet**, **subnet**, **NIC**, **NSG**, and **public IP**—the full infrastructure package. No scroll, no click, no lag. Just **clean automation**.

---

### 🔐 Connect, Test, Success!

After a few minutes, the virtual machine was live. Naveed clicked **Connect > RDP**, downloaded the file, logged in, and — *voilà!* — his **VM was up and running**. Everything booted perfectly. The Curious Cloud Explorer smiled. His mission? ✅ **Complete**.

---

### 🧹 Cleanup Like a Pro

Being the professional he is, **our Azure admin** didn’t forget the final act — cleanup! With one command, he deleted all the resources from **rg-learntech-naveed**, keeping his subscription tidy and cost-effective. No leftovers, no surprises.

---

### 🏁 Final Words

So, did Naveed complete his task? **Absolutely!**
He didn’t just build a VM — he automated it, connected it, tested it, and cleaned up like a true cloud hero.
With **Azure CLI**, he proved that cloud tasks can be fast, reliable, and fun — if you know the magic commands. ✨

---
---
---

### **Practical Scenario: Deploying a Secure Windows VM via CLI for Remote Team Access**

---

**Meet Sarah**, a Cloud Engineer working for a mid-sized software development firm. Her team is working on a legacy Windows application that needs to be tested in a controlled, cloud-based environment. The testing environment must be deployed quickly, securely, and without relying on graphical interfaces—because the operations team automates infrastructure using scripts.

Her manager assigns her the task:

> “Sarah, we need a **Windows Virtual Machine** up and running in Azure by the end of the hour, using the **CLI** only. Ensure it’s accessible via **RDP**, and please make sure all resources are grouped logically for easy cleanup later.”

Let’s walk through Sarah’s journey step-by-step and see how she completes the task using **Azure CLI** in the **Azure Cloud Shell**.

---

#### **Step 1: Access Azure Cloud Shell**

Sarah opens the **Azure Portal** and clicks on the **Cloud Shell** icon at the top of the interface. She selects **Bash**, as her team standardizes on it for automation tasks.

Azure prompts her to create a temporary **Cloud Shell** storage (since none exists), and she clicks **Apply** using the default options.

---

#### **Step 2: Define Secure Credentials**

Sarah knows it's a security best practice not to hard-code usernames and passwords in the command directly. So, she stores them in variables:

```bash
username="demouser"
password="MyS3curePassw0rd123"
```

These values will be used in the next command without exposing them in logs.

---

#### **Step 3: Deploy the Virtual Machine**

Sarah now constructs her **Azure CLI** command to deploy the **Windows VM**. She gathers the name of the assigned **resource group** from the lab instructions and runs:

```bash
az vm create \
  --name MyVm \
  --resource-group TestGroup \
  --image win2019datacenter \
  --size Standard_B1s \
  --admin-username $username \
  --admin-password $password
```

This command tells Azure to:

* Create a VM named **MyVm**
* Use the **Windows Server 2019** image
* Use a **Standard\_B1s** size (suitable for light workloads)
* Automatically create related resources: **Virtual Network**, **Subnet**, **NIC**, **NSG**, and **Public IP Address**

Within a few minutes, Azure returns a success message along with the **public IP address** of the new VM.

---

#### **Step 4: Connect via RDP**

Sarah navigates to the **Virtual Machines** section in the **Azure Portal**, selects **MyVm**, and clicks **Connect**.

She downloads the **RDP file**, opens it on her Windows PC, and logs in using the username and password she defined earlier.

The VM boots up successfully, and the legacy test application is ready to be deployed.

---

#### **Step 5: Business Benefit**

Thanks to **Azure CLI** and **Cloud Shell**, Sarah:

* Deployed a Windows environment securely and quickly
* Avoided configuration drift by using CLI-based infrastructure setup
* Created all necessary **networking** and **security** components without touching the portal UI
* Made the environment disposable by grouping everything into one **resource group**

This approach aligns with her company’s **DevOps** and **Infrastructure as Code (IaC)** principles, supporting scalability, repeatability, and ease of cleanup.

---

#### **Conclusion**

Sarah demonstrates how using **Azure CLI** via **Cloud Shell** can enable fast, secure, and repeatable VM deployments, especially in environments where GUI access is discouraged or where automation is critical. This lab reflects a real-world need for IT professionals to rapidly deploy test environments, conduct patch testing, or support remote teams—with minimal effort and maximum control.

---
---
---

## Lab-Based Conceptual MCQs

1. **Why is it recommended to store the admin username and password in variables when creating a VM using Azure CLI?**
   - (a) To reduce typing effort
   - (b) To maintain script reusability
   - (c) To avoid exposing sensitive credentials directly in the command
   - (d) To comply with licensing requirements  
   **Correct answer: (c)**  
   Storing credentials in variables helps avoid exposing them in command history or logs, which is a security best practice.

2. **What is the purpose of the `--image` parameter in the `az vm create` command?**
   - (a) To name the virtual machine
   - (b) To select the VM size
   - (c) To specify the operating system image
   - (d) To allocate storage resources  
   **Correct answer: (c)**  
   The `--image` parameter defines which OS image (e.g., Windows or Linux) the VM will use during creation.

3. **Which Azure service automatically provisions networking components like public IP, NIC, and VNet when using `az vm create` with basic parameters?**
   - (a) **Azure Network Manager**
   - (b) **Azure Virtual Machine Extensions**
   - (c) **Azure CLI**
   - (d) **Azure Resource Manager**  
   **Correct answer: (d)**  
   **Azure Resource Manager** handles the orchestration and deployment of associated resources when a VM is created.

4. **Why might an organization prefer using the **Azure CLI** over the Azure Portal for VM creation?**
   - (a) It requires fewer permissions
   - (b) It allows more GUI-based control
   - (c) It supports automation and scripting
   - (d) It avoids resource dependencies  
   **Correct answer: (c)**  
   The **Azure CLI** enables infrastructure automation, making it suitable for scripting and DevOps workflows.

5. **Which Azure component provides secure remote access to Windows VMs created in Azure?**
   - (a) **SSH**
   - (b) **RDP**
   - (c) **FTP**
   - (d) **HTTP**  
   **Correct answer: (b)**  
   **RDP (Remote Desktop Protocol)** is used to connect securely to Windows virtual machines.

6. **What is the role of the `--resource-group` parameter in the VM creation command?**
   - (a) It selects the Azure subscription
   - (b) It defines the virtual network name
   - (c) It specifies where to logically group and manage the resources
   - (d) It assigns user permissions  
   **Correct answer: (c)**  
   The `--resource-group` parameter ensures all related resources are grouped logically for easy management.

7. **What happens if you omit the `--admin-password` parameter when creating a VM using CLI?**
   - (a) The VM is created without a password
   - (b) Azure auto-generates a password
   - (c) The command fails due to required parameter missing
   - (d) Azure uses a default password  
   **Correct answer: (c)**  
   The VM creation command requires an admin password; if omitted, the command will not execute.

8. **Why is Cloud Shell preferred over local CLI installations for quick lab-based tasks?**
   - (a) It provides a GUI interface
   - (b) It includes pre-installed tools and requires no setup
   - (c) It uses more computing resources
   - (d) It bypasses Azure subscriptions  
   **Correct answer: (b)**  
   **Cloud Shell** offers a browser-based environment with pre-configured Azure CLI and scripting tools, reducing setup time.

9. **Which command is used to create a new virtual machine using Azure CLI?**
   - (a) `az resource create`
   - (b) `az compute create`
   - (c) `az machine start`
   - (d) `az vm create`  
   **Correct answer: (d)**  
   The `az vm create` command is used to create a new virtual machine in Azure.

10. **After deploying a VM, which Azure CLI command would help you verify if it is correctly running?**
   - (a) `az vm stop`
   - (b) `az vm show`
   - (c) `az vm list-ip-addresses`
   - (d) `az vm restart`  
   **Correct answer: (b)**  
   The `az vm show` command provides the current state and configuration of a deployed VM.

---
---
---

## Professional Job Interview Questions – Create a VM with CLI

### Lab-Based Conceptual MCQs

1. **Naveed needs to create a Windows Server 2019 VM using the Azure CLI. Which Azure command-line tool should he use to automate this task?**  
   (a) Azure PowerShell  
   (b) Azure CLI  
   (c) Bash Scripting  
   (d) ARM Template  

   **Correct answer: (b)**  
   **Explanation:** Azure CLI provides a cross-platform command-line interface to manage Azure resources, and is ideal for creating VMs through scripted automation.

2. **While deploying a VM using Azure CLI, what happens if Naveed doesn’t specify a virtual network or subnet?**  
   (a) The deployment will fail  
   (b) Azure CLI will use the default VNet in the subscription  
   (c) Azure CLI will automatically create the required networking resources  
   (d) It will deploy without any network connectivity  

   **Correct answer: (c)**  
   **Explanation:** Azure CLI intelligently provisions supporting resources like VNet, subnet, NSG, and public IP if they’re not specified explicitly in the command.

3. **What is the primary benefit of using Azure CLI in Cloud Shell as Naveed did?**  
   (a) Better GUI performance  
   (b) Local VM integration  
   (c) Pre-installed tools with no configuration needed  
   (d) High data processing capacity  

   **Correct answer: (c)**  
   **Explanation:** Cloud Shell comes with pre-installed tools like Azure CLI and doesn’t require local setup, making it quick and easy for cloud administrators.

4. **Why did Naveed define adminUsername and adminPassword as variables in Bash before deploying the VM?**  
   (a) To encrypt credentials  
   (b) To simplify reuse across multiple commands  
   (c) To store them in Azure Key Vault  
   (d) To avoid using environment variables  

   **Correct answer: (b)**  
   **Explanation:** Defining credentials as variables allows for better scripting and reuse, particularly when multiple resources are deployed using the same values.

5. **After deploying the VM, what is the most secure way for Naveed to access it?**  
   (a) Using public IP via FTP  
   (b) RDP through the Azure portal  
   (c) Telnet into the VM  
   (d) HTTP access on port 80  

   **Correct answer: (b)**  
   **Explanation:** Remote Desktop Protocol (RDP) via the Azure portal is the recommended method to securely connect to a Windows VM.

6. **Which resource is automatically created when Naveed uses 'az vm create'?**  
   (a) Azure Database  
   (b) Managed Disk  
   (c) Azure Web App  
   (d) Azure Blob  

   **Correct answer: (b)**  
   **Explanation:** When deploying a VM, Azure automatically creates a managed disk to host the operating system.

7. **Why might Naveed prefer CLI deployment over the Azure Portal for VM provisioning in professional environments?**  
   (a) Faster browsing speed  
   (b) Reduced graphical overhead  
   (c) Automation and repeatability  
   (d) Better UI  

   **Correct answer: (c)**  
   **Explanation:** CLI is ideal for automating tasks, enabling repeatable deployments through scripting, which improves consistency in enterprise setups.

8. **Which networking component ensures internet traffic rules are defined for Naveed’s VM?**  
   (a) Azure DNS  
   (b) Application Gateway  
   (c) Network Security Group (NSG)  
   (d) Traffic Manager  

   **Correct answer: (c)**  
   **Explanation:** NSGs control inbound and outbound traffic rules, ensuring only allowed traffic reaches the VM.

9. **What is a reason to delete all the resources after the lab, as Naveed did?**  
   (a) To reduce CPU usage  
   (b) To free up GUI space  
   (c) To avoid ongoing costs  
   (d) To enable firewall  

   **Correct answer: (c)**  
   **Explanation:** Resources in Azure incur costs, so deleting them after a lab or test scenario avoids unnecessary charges.

10. **In a production setting, how can Naveed securely manage secrets like admin passwords when automating with CLI?**  
    (a) Store in plain text in the script  
    (b) Use Azure Key Vault  
    (c) Email them to the team  
    (d) Save in Notepad  

    **Correct answer: (b)**  
    **Explanation:** Azure Key Vault securely stores credentials and secrets, and integrates with CLI for secure automation workflows.

---
---
---

## Comic-Style Summary: **“Click, Type, Deploy – The Bashful VM Adventure!”**

### 🧠 The Curious Cloud Explorer Begins

Meet **Naveed**, the ever-curious Cloud Explorer from **TechWaveNaveed**. Today’s mission? To spin up a **Windows VM** using the mighty **Azure CLI**—all from the comfort of **Cloud Shell**. No mouse-clicking madness, just pure Bash magic!

### 🛠️ Variables Are the Secret Sauce

To keep things secure and slick, our Azure admin first sets up his **admin credentials** using shell variables. With a line or two of code, he defines the username and password for the upcoming VM deployment. No secrets spilled, no typos allowed!

### 🚀 Deploying the VM with One Command

With confidence and caffeine, Naveed types the golden command: `az vm create`. Instantly, **Azure CLI** swings into action—deploying a **Windows Server 2019 VM**, a **VNet**, **public IP**, **NIC**, and even a **Network Security Group**—all auto-magically. It’s like ordering a full infrastructure meal with one CLI line!

### 🖥️ Time to Connect and Test

After the VM is deployed, the CloudOps engineer heads over to the **Azure Portal**, finds his **MyVm**, and connects to it using **RDP**. Moments later, he's staring at a fresh Windows login screen—mission accomplished! He logs in using his earlier credentials, proving the setup was a success.

### 🧹 Cleanup Like a Pro

Being the responsible cloud warrior he is, Naveed wraps things up by deleting all the resources he created. Why? Because a clean cloud is a happy cloud—and budget-friendly too!

> 💡 **Key Takeaway**: This comic adventure shows how **Azure CLI** can simplify infrastructure deployment. From defining variables to verifying the VM—each step was fast, automated, and repeatable. Perfect for any real-world IT pro aiming for speed, control, and efficiency in the cloud!

---
---
---
## Text-Based Diagram for the Lab: **"Create a VM with CLI"**

```plaintext
+--------------------------------------------------+
|            Start Azure Portal Session            |
+--------------------------------------------------+
                      |
                      v
+--------------------------------------------------+
|      Click on Cloud Shell (top menu bar)         |
|      → Select Bash terminal                      |
|      → Skip storage config (if prompted)         |
+--------------------------------------------------+
                      |
                      v
+--------------------------------------------------+
|  Define Admin Credentials in Variables           |
|  username="demouser"                             |
|  password="YourSecurePassword123"                |
+--------------------------------------------------+
                      |
                      v
+--------------------------------------------------+
|  Run az vm create Command                        |
|  → --name MyVm                                   |
|  → --image win2019datacenter                     |
|  → --resource-group <resource-group>             |
|  → --admin-username $username                    |
|  → --admin-password $password                    |
+--------------------------------------------------+
                      |
                      v
+--------------------------------------------------+
|  Azure Auto-Provisions Resources:                |
|  → Virtual Machine (Windows)                     |
|  → VNet, Subnet                                  |
|  → NIC, Public IP                                |
|  → Network Security Group                        |
+--------------------------------------------------+
                      |
                      v
+--------------------------------------------------+
|  Navigate to Virtual Machines in Portal          |
|  → Select "MyVm"                                 |
|  → Click "Connect" > Choose RDP                  |
|  → Download and Open RDP File                    |
+--------------------------------------------------+
                      |
                      v
+--------------------------------------------------+
|   Log in with credentials and test connection    |
|   Confirm Windows Server boots successfully      |
+--------------------------------------------------+
                      |
                      v
+--------------------------------------------------+
|             Delete All Created Resources         |
+--------------------------------------------------+
```

### 📝 Diagram Summary:

This **text-based diagram** illustrates the **end-to-end process** of deploying a **Windows Virtual Machine** using **Azure CLI** via **Cloud Shell**. It starts with accessing the **Bash environment**, defining **secure credentials**, executing the **VM deployment**, and then **verifying access** via **RDP**. The diagram ensures a beginner can visualize how different **Azure resources** (like **VNet**, **NSG**, **Public IP**) are automatically provisioned during the process.

---
---
---
