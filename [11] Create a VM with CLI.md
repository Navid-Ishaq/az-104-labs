# Lab 11: Create a VM with CLI

**Duration:** 30m

After logging in with your credentials:

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

