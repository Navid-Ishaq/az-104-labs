# Lab 10: Create a Windows VM using an ARM template

**Duration:** 30m
---

---
---
---

**Lab 10 Summary – “Deploy Smarter with Templates”**
Naveed, the Curious Cloud Explorer, explored and customized an **ARM template** to automate the deployment of a **Windows virtual machine** with its full network setup.
He used **Azure Cloud Shell** to upload and deploy the template, verifying all components—like **VNet**, **NSG**, **NIC**, and **Storage Account**—were provisioned seamlessly.
Finally, our CloudOps engineer cleaned up the environment by deleting all deployed **Azure resources**, completing the lab efficiently with infrastructure-as-code mastery.

---
---
---

**After logging in with your credentials:**

### Step 1: Explore the ARM Template

1. Download the `template.json` file from the provided lab resources and extract it to your local machine.
2. Review the structure of the ARM template. It includes:

   * **Parameters** such as `adminUsername`, `adminPassword`, `dnsLabelPrefix`, and VM configuration options.
   * **Variables** for commonly reused values (e.g., subnet name, virtual network name).
   * **Resources** including a storage account, public IP, network security group (NSG), virtual network (VNet), network interface (NIC), and a virtual machine.
   * **Outputs** to return the public DNS hostname of the deployed VM.

### Step 2: Upload the Template to Cloud Shell

1. Open **Cloud Shell** from the top-right menu in the Azure Portal.
2. Select **Bash** when prompted.
3. If asked to configure storage, select **No storage account required**, and choose the appropriate subscription.
4. Use the **Upload** option in Cloud Shell to upload your `template.json` file into the shell environment.

### Step 3: Deploy the ARM Template

1. Use the following command in Cloud Shell to deploy the template:

   ```bash
   az deployment group create \
     --name <deployment-name> \
     --template-file template.json \
     --parameters '{
       "adminUsername": {"value": "<admin-username>"},
       "adminPassword": {"value": "<admin-password>"}
     }' \
     --resource-group <resource-group-name>
   ```

   Replace the placeholders:

   * `<deployment-name>`: A unique name for this deployment.
   * `<admin-username>`: Your chosen VM administrator username.
   * `<admin-password>`: A strong password (12+ characters) for the VM.
   * `<resource-group-name>`: The name of the target resource group.

2. Wait for the command to complete. This may take several minutes.

### Step 4: Verify Deployment in the Portal

1. In the Azure Portal, navigate to the **Resource groups** blade.
2. Open the resource group used in the deployment.
3. Confirm that resources were successfully created:

   * A Windows virtual machine.
   * Network components such as a NIC, VNet, and NSG.
   * A public IP address.
   * A storage account for diagnostics.

### Step 5: Delete All the Resources

Delete all the resources.

---
---
---

## **Lab 10: Create a Windows VM using an ARM Template**

---

### 🎯 **Purpose of the Lab**

The purpose of this lab is to enable **Naveed**, the Curious Cloud Explorer, to provision a complete **Windows Virtual Machine (VM)** environment in **Azure** using an **ARM (Azure Resource Manager) template**. This demonstrates how to define infrastructure as code for consistency, automation, and repeatability in cloud deployments—critical for modern DevOps and enterprise cloud practices.

---

### 🧰 **Azure Tools Utilized in the Lab**

Each of the following **Azure services and components** played a vital role in automating the VM deployment:

---

#### 1. **ARM Template**

* **Definition**: A JSON-based file that defines the structure and configuration of Azure resources.
* **Role**: Naveed used this template to describe the **parameters**, **variables**, **resources**, and **outputs** required for automated VM deployment.
* **Example**: Parameters like `"adminUsername"`, `"adminPassword"` were passed at deployment time to customize the virtual machine setup.

---

#### 2. **Azure Resource Group**

* **Definition**: A logical container for Azure resources that share the same lifecycle.
* **Role**: The ARM template was deployed into a named resource group (e.g., **rg-learntech-naveed**) to keep related resources grouped and manageable.
* **Example**: All deployed components—VM, VNet, NSG, IP—were created inside this resource group.

---

#### 3. **Azure Virtual Machine (VM)**

* **Definition**: A scalable compute resource in Azure.
* **Role**: The core component of the deployment, created using the template to host workloads and applications.
* **Example**: A **Windows Server 2019 Datacenter** VM was automatically spun up and configured via the template.

---

#### 4. **Virtual Network (VNet)**

* **Definition**: A representation of a network within Azure that provides isolation and segmentation.
* **Role**: Ensured that the deployed VM had a secure and private communication channel.
* **Example**: VNet was defined in the template and automatically provisioned.

---

#### 5. **Network Security Group (NSG)**

* **Definition**: A firewall-like service that controls inbound and outbound traffic.
* **Role**: Allowed or denied network traffic to the VM based on security rules.
* **Example**: Configured to allow **RDP** traffic for accessing the VM remotely.

---

#### 6. **Network Interface (NIC)**

* **Definition**: Connects the virtual machine to the VNet.
* **Role**: The VM required a NIC to be attached to the network and communicate with other resources.
* **Example**: The NIC was provisioned as part of the ARM template and bound to the VM.

---

#### 7. **Public IP Address**

* **Definition**: An IP address accessible from the internet.
* **Role**: Provided Naveed with the ability to remotely connect to the VM using RDP.
* **Example**: Assigned dynamically through the template for secure, external access.

---

#### 8. **Storage Account**

* **Definition**: A resource that provides durable and highly available storage.
* **Role**: Used for **diagnostic logs** and **boot diagnostics** for the VM.
* **Example**: Automatically created by the template and linked to the VM.

---

#### 9. **Azure Cloud Shell**

* **Definition**: An interactive, browser-accessible shell environment in the Azure portal.
* **Role**: Allowed Naveed to upload the **template.json** and deploy it using **CLI commands**.
* **Example**: He ran `az deployment group create` from Cloud Shell to kick off the deployment.

---

#### 10. **Azure CLI**

* **Definition**: A command-line tool to manage Azure resources programmatically.
* **Role**: Helped automate and execute the deployment using `az` commands within Cloud Shell.
* **Example**: Simplified complex infrastructure provisioning through scripting.

---

### ✅ **Conclusion**

This lab taught Naveed how to implement **Infrastructure as Code (IaC)** using an **ARM template**, ensuring repeatable, consistent deployments for production-ready infrastructure. This practice is essential for any **DevOps engineer**, **Azure administrator**, or **CloudOps specialist** to scale efficiently and reduce human error in enterprise environments.

---
---
---

## **Structured Summary: Deploy a Windows VM Using an ARM Template**

### **Purpose of the Lab**

The purpose of this lab is to demonstrate how to deploy a **Windows Virtual Machine (VM)** using an **Azure Resource Manager (ARM) template** through the **Azure Cloud Shell**. This approach emphasizes the use of **infrastructure as code (IaC)** to automate resource deployment, enhance repeatability, and reduce manual configuration errors in cloud environments. The lab helps learners understand how declarative JSON-based templates can define and deploy complex Azure infrastructures in a consistent and scalable manner.

---

### **Azure Tools and Services Utilized**

#### 1. **Azure Resource Manager (ARM) Template**

* **Description**: A JSON file that defines the infrastructure and configuration for Azure resources.
* **Role in Lab**: The core mechanism used to declaratively provision a **Windows VM** along with its supporting network and storage components.

#### 2. **Azure Cloud Shell (Bash)**

* **Description**: An interactive, browser-accessible shell for managing Azure resources using command-line tools.
* **Role in Lab**: Used to upload the ARM template and execute the deployment command using the **Azure CLI**.

#### 3. **Azure CLI**

* **Description**: A cross-platform command-line tool for managing Azure resources.
* **Role in Lab**: Executes the `az deployment group create` command to deploy resources defined in the **ARM template**.

#### 4. **Virtual Machine (VM)**

* **Description**: A software emulation of a physical computer running Windows Server.
* **Role in Lab**: The main compute resource deployed using the ARM template to simulate a server workload.

#### 5. **Resource Group**

* **Description**: A logical container that holds related Azure resources.
* **Role in Lab**: All deployed resources (VM, network components, etc.) are created within a specific **resource group** to simplify management and cleanup.

#### 6. **Virtual Network (VNet)**

* **Description**: A logically isolated network in Azure where VMs and other resources can securely communicate.
* **Role in Lab**: Provides a private network space for the VM, enabling internal and external connectivity.

#### 7. **Subnet**

* **Description**: A segmented range within a **VNet** that allows for more granular control over resource placement.
* **Role in Lab**: The VM is deployed within a specific **subnet** to define its network boundaries.

#### 8. **Network Interface (NIC)**

* **Description**: Connects a VM to a virtual network.
* **Role in Lab**: Associates the **VM** with the **VNet**, allowing it to send and receive network traffic.

#### 9. **Network Security Group (NSG)**

* **Description**: A security feature that contains inbound and outbound rules to control traffic to network interfaces.
* **Role in Lab**: Configured with rules to allow **RDP (port 3389)** access to the VM for remote administration.

#### 10. **Public IP Address**

* **Description**: An externally accessible IP assigned to a resource like a VM.
* **Role in Lab**: Enables access to the **VM** from the internet using **Remote Desktop Protocol (RDP)**.

#### 11. **Storage Account**

* **Description**: Provides scalable cloud storage for data including blobs, files, queues, and diagnostic logs.
* **Role in Lab**: Used to store **boot diagnostics logs** for the deployed VM.

---

By combining these tools and services, this lab equips learners with the practical skills needed to automate infrastructure provisioning in Azure using a structured, reusable, and version-controllable method.

---
---
---

## **📘 Real-World Scenario: "Naveed Automates Like a Pro"**

At **LearnTechCloud**, business was booming, and the IT team needed to spin up **Windows virtual machines** frequently to support development and testing projects. But the process of clicking through the portal every time was slow and error-prone. That’s when **Naveed**, the **Curious Cloud Explorer**, stepped in with a bold plan: automate the entire deployment using an **ARM template**.

---

### **📁 Step 1: Understanding the Blueprint**

First, our Azure admin opened the **template.json** file. This wasn't just a simple config—it was a **blueprint**. It included **parameters** like `"adminUsername"` and `"adminPassword"`, **variables** for network names, and a **set of resources** like **virtual networks**, **NSGs**, **NICs**, and even **storage accounts**. Naveed realized that by editing this single file, he could control the entire infrastructure like a conductor leads an orchestra.

📌 *Example*: The **VM size**, region, and even network security rules were defined without clicking a single button.

---

### **🌐 Step 2: Uploading to Azure Cloud Shell**

To get started, Naveed fired up **Azure Cloud Shell**—a command-line interface right in the portal. He uploaded the ARM template using the “Upload” option and verified that it landed in the shell environment. This step brought the deployment code into Azure’s environment, making it ready to launch.

---

### **🚀 Step 3: Deploy with a Single Command**

In true DevOps fashion, he ran a single **Azure CLI** command:

```bash
az deployment group create --name deployVM01 --template-file template.json --parameters ...
```

The magic began. Azure read the **template**, accepted the **parameter values**, and within minutes, a fully configured **Windows VM**, complete with networking, security, diagnostics, and storage, was born inside **rg-learntech-naveed**.

---

### **📊 Step 4: Verifying Everything Works**

After deployment, Naveed opened the **Resource Groups** blade and confirmed that all components were successfully created:

* A **Windows VM** ready for RDP
* A **VNet** and **Subnet**
* A **Network Security Group (NSG)** allowing secure access
* A **Storage Account** holding diagnostic logs
* A **Public IP** bound to the VM

He even tested the **VM login** using the assigned public DNS and verified connectivity.

---

### **🧹 Step 5: Cleaning Up Resources**

Because Naveed was working in a training environment, he deleted all the resources once testing was complete—just as a responsible **CloudOps engineer** should. This not only kept costs low but also avoided clutter in his subscription.

---

### ✅ **Why This Matters**

By using an **ARM template**, Naveed ensured:

* **Consistency** in resource provisioning
* **Time-saving automation** for repetitive tasks
* **Reusability** for future deployments
* **Compliance** with company standards

📦 *In a real enterprise*, this approach supports version-controlled infrastructure, ideal for production environments where reliability is key.

---
---
---
## Comic-Style Summary: **“Deploy It Like a Template Boss!”**

### 🎯 The Mission Begins: One File to Rule Them All

**Naveed**, our **Curious Cloud Explorer**, had a mission from his team at **LearnTechCloud**: deploy a fully configured **Windows virtual machine** quickly and cleanly. But instead of clicking around the portal, he smiled and said, “Let’s automate this!” He opened up his **ARM template**, a powerful blueprint that defines entire Azure infrastructures in code.

---

### 📂 Upload and Launch: Magic in the Cloud Shell

Our Azure admin headed straight to **Azure Cloud Shell**, uploaded the magical `template.json` file, and typed in a single **Azure CLI** command. With a tap of the Enter key, **Azure started deploying** everything — the **VM**, **network**, **security group**, **public IP**, and **storage** — just like that. It was like casting a cloud spell!

---

### 🕵️‍♂️ Checking His Work Like a Pro

Once the deployment finished, the **TechWaveNaveed admin** visited the **Azure Portal** and opened the resource group named **rg-learntech-naveed**. He saw all the pieces in place: the **virtual machine**, the **NIC**, the **VNet**, and the **NSG**. Everything was exactly as described in the template. He even connected to the VM to confirm it worked. *Smooth as butter!*

---

### 🧹 Clean Desk Policy: Deleting the Lab

After verifying success, the **CloudOps engineer** followed best practices and cleaned up by **deleting all resources** to avoid unnecessary charges. “No leftover clutter on my watch!” he grinned. The task was complete, and the mission was a win.

---

### ✅ So… Did Naveed Succeed?

**Yes!** Naveed not only completed the task, but he did it like a professional — using **automation**, **efficiency**, and **best practices**. This comic journey showed that with a little learning and a solid **ARM template**, even complex deployments can feel simple, repeatable, and fun.

---
---
---

## **Professional Scenario: Automating VM Deployment with ARM Templates**

**Background:**

Meet **Emma**, a Cloud Engineer working at **Contoso Financial Services**, a mid-sized company moving its infrastructure to the cloud. Her team is responsible for managing development and test environments in **Microsoft Azure**. The developers frequently request Windows-based **Virtual Machines (VMs)** with similar configurations. Emma needs a way to standardize and automate these requests without manually clicking through the **Azure portal** every time.

**The Challenge:**

Manual VM creation is time-consuming and error-prone. Each VM requires setting up networking, assigning a **Public IP address**, configuring **Network Security Groups (NSGs)**, and enabling **boot diagnostics**. Emma needs a repeatable, auditable, and scalable way to deploy infrastructure consistently. That's where **ARM templates** come into play.

---

## **Scenario Walkthrough**

### **Step 1: Understanding the ARM Template**

Emma starts by reviewing an **ARM template** named `template.json`, which is a **JSON** file defining all the infrastructure components needed to deploy a Windows **Virtual Machine**. This includes:

* **Virtual Network (VNet)** and **Subnet** for network isolation
* **Network Interface (NIC)** for network connectivity
* A **Network Security Group (NSG)** to allow **RDP** access
* A **Storage Account** for diagnostics
* A **Public IP address** for remote access
* The **VM** itself with custom parameters like OS version, size, and admin credentials

By using this template, Emma ensures that every VM deployment is uniform and compliant with organizational standards.

---

### **Step 2: Deploying the Template via Azure Cloud Shell**

Emma logs into the **Azure portal** and launches **Azure Cloud Shell (Bash)**, which provides a browser-based CLI environment without any local setup. She uploads the `template.json` file using the **Manage file** option.

Using the **Azure CLI** inside Cloud Shell, Emma runs the deployment command:

```bash
az deployment group create \
  --name dev-vm-deployment \
  --template-file template.json \
  --parameters '{
    "adminUsername": {"value": "emmaadmin"},
    "adminPassword": {"value": "StrongPassword123!"}
  }' \
  --resource-group DevResources
```

This command triggers the **ARM template** deployment, which orchestrates the creation of all resources in the specified **Resource Group**.

---

### **Step 3: Verifying the Deployment**

Once the deployment finishes, Emma navigates to the **Resource Group** in the **Azure portal**. She sees:

* A fully provisioned **Windows VM**
* A connected **NIC** attached to a **VNet**
* An assigned **Public IP**
* An associated **NSG** with **RDP** port open
* A configured **Storage Account** for diagnostics

The best part? All of this was done with a single command using infrastructure defined in code.

---

### **Step 4: Real-World Benefits**

Thanks to the **ARM template**, Emma can now:

* **Automate** repetitive infrastructure tasks
* **Version control** templates using Git for auditability
* **Scale** deployments across teams and environments
* Ensure **consistency** and compliance with security policies

When a developer like **Liam** needs a test machine, Emma can redeploy the template in minutes without worrying about missing configuration details.

---

### **Step 5: Tearing Down the Resources**

After the environment is no longer needed, Emma simply navigates to the **Resource Group**, selects all associated resources, and deletes them. This helps avoid unnecessary costs and keeps the cloud environment tidy.

---

## **Conclusion**

Through this scenario, Emma effectively leverages **ARM templates** and **Azure CLI** in **Azure Cloud Shell** to deploy and manage infrastructure. Her workflow not only simplifies her job but also accelerates development and aligns with modern **DevOps** practices.

This lab isn't just an academic exercise—it's a real-world solution to the challenges of manual, error-prone infrastructure provisioning in a dynamic cloud environment.

---
---
---
## Lab-Based Conceptual MCQs

### 1. What is the primary benefit of using an **ARM template** for deploying infrastructure in Azure?
(a) Reduced network latency  
(b) Manual resource configuration flexibility  
(c) Consistent and repeatable deployments  
(d) Enhanced GUI experience  

**Correct answer: (c)**  
*ARM templates allow for consistent, repeatable, and automated deployments of Azure resources, minimizing human error and increasing efficiency.*

### 2. Which Azure feature provides a browser-based command-line interface to deploy the **ARM template**?
(a) Azure Monitor  
(b) Azure DevOps  
(c) Azure Cloud Shell  
(d) Azure Resource Graph  

**Correct answer: (c)**  
*Azure Cloud Shell offers a browser-accessible shell experience for managing resources, including template deployments using Azure CLI.*

### 3. In the context of the lab, what is the purpose of the **Network Security Group (NSG)**?
(a) Encrypt disk data on the VM  
(b) Assign dynamic IP addresses  
(c) Control inbound and outbound traffic rules  
(d) Monitor performance metrics  

**Correct answer: (c)**  
*NSGs are used to define security rules that allow or deny network traffic to Azure resources.*

### 4. What command is used to deploy an **ARM template** in Azure using CLI?
(a) az vm create  
(b) az template deploy  
(c) az deployment group create  
(d) az resource apply  

**Correct answer: (c)**  
*The correct command to deploy an ARM template to a resource group is `az deployment group create`.*

### 5. Why is a **Storage Account** created as part of the ARM template deployment?
(a) To host user documents  
(b) To store backup images  
(c) To enable boot diagnostics for the VM  
(d) To assign public IPs  

**Correct answer: (c)**  
*A storage account is required to store boot diagnostics logs for troubleshooting the virtual machine.*

### 6. Which parameter in the ARM template defines the username for the virtual machine?
(a) dnsLabelPrefix  
(b) vmSize  
(c) adminUsername  
(d) computerName  

**Correct answer: (c)**  
*The `adminUsername` parameter specifies the login name for the Windows VM.*

### 7. What role does the **Public IP Address** play in this deployment?
(a) Connects VM to internal network only  
(b) Hosts DNS services  
(c) Allows remote access via RDP  
(d) Replaces storage diagnostics  

**Correct answer: (c)**  
*The public IP address enables remote access to the VM over the internet using RDP.*

### 8. What is the function of the **dependsOn** property in an ARM template?
(a) Assigns metadata tags  
(b) Specifies OS type  
(c) Ensures resources are created in order  
(d) Links diagnostics to log analytics  

**Correct answer: (c)**  
*`dependsOn` ensures that resources are created in a specific sequence, respecting their dependencies.*

### 9. What happens when you upload an **ARM template** file to **Azure Cloud Shell**?
(a) It runs automatically  
(b) It becomes available for CLI commands  
(c) It deploys the VM instantly  
(d) It gets validated for syntax only  

**Correct answer: (b)**  
*Uploading the template makes it available to reference in commands like `az deployment group create`.*

### 10. Which resource is created in the ARM template to connect the VM to the virtual network?
(a) Load balancer  
(b) Network Interface Card (NIC)  
(c) Azure Bastion  
(d) Application Gateway  

**Correct answer: (b)**  
*The NIC connects the virtual machine to the subnet within a virtual network and links it to the public IP address.*

---
---
---
## Professional Job Interview Questions – **Create a Windows VM using an ARM Template**

Below are conceptual, scenario-based multiple-choice questions (MCQs) that evaluate practical understanding of **ARM templates**, **Azure virtual machine deployment**, and **resource automation**, aligned with **AZ-104** certification skills.

---

### 1. **Naveed needs to deploy a Windows VM along with its networking components in a consistent and repeatable manner. What Azure feature is best suited for this task?**

(a) Azure Policy  
(b) Azure ARM Template  
(c) Azure Monitor  
(d) Azure Advisor  

**Correct answer: (b)**  
**Explanation:** An **ARM template** allows the declarative deployment of Azure resources in a structured and repeatable way, ideal for automating complex infrastructure setups.

---

### 2. **Which Azure service allows Naveed to deploy his ARM template directly from the Azure Portal without requiring local tools?**

(a) Azure Automation  
(b) Azure DevOps  
(c) Azure Cloud Shell  
(d) Azure Logic Apps  

**Correct answer: (c)**  
**Explanation:** **Azure Cloud Shell** provides a browser-based command-line interface that supports **Azure CLI** and **PowerShell**, allowing easy deployment of templates.

---

### 3. **In his ARM template, Naveed wants to use the same subnet name in multiple resources. What should he define to avoid repetition?**

(a) Output section  
(b) Variables section  
(c) Parameters section  
(d) Metadata section  

**Correct answer: (b)**  
**Explanation:** The **variables section** in an ARM template is used for values that are reused internally within the template to simplify maintenance and avoid redundancy.

---

### 4. **Naveed includes parameters in his ARM template such as `adminUsername` and `adminPassword`. What is the purpose of parameters?**

(a) To define resource output  
(b) To log deployment history  
(c) To allow user input at deployment time  
(d) To create diagnostic settings  

**Correct answer: (c)**  
**Explanation:** **Parameters** allow for user-provided values at deployment time, increasing the flexibility and reusability of the ARM template.

---

### 5. **Naveed has successfully deployed a VM using an ARM template. Which Azure resource stores deployment logs and history by default?**

(a) Azure Monitor  
(b) Azure Storage  
(c) Azure Resource Group  
(d) Azure Activity Log  

**Correct answer: (d)**  
**Explanation:** **Azure Activity Log** captures all deployment and resource-level actions, including ARM template deployments for tracking and auditing.

---

### 6. **Which CLI command should Naveed use to initiate a group deployment from an ARM template file within Cloud Shell?**

(a) az group create  
(b) az resource create  
(c) az deployment group create  
(d) az vm create  

**Correct answer: (c)**  
**Explanation:** The **az deployment group create** command is used to deploy resources defined in an ARM template to a specific resource group.

---

### 7. **Why would Naveed choose to deploy infrastructure using an ARM template instead of manually through the portal?**

(a) To increase cost of deployment  
(b) To disable monitoring  
(c) To ensure consistency, automation, and scalability  
(d) To avoid using parameters and variables  

**Correct answer: (c)**  
**Explanation:** **ARM templates** promote **infrastructure as code (IaC)**, enabling repeatable, consistent deployments across environments with minimal manual intervention.

---

### 8. **Which section of the ARM template is used to define what values are returned after deployment (like public DNS hostname)?**

(a) Resources  
(b) Parameters  
(c) Outputs  
(d) Variables  

**Correct answer: (c)**  
**Explanation:** The **outputs** section is used to return information post-deployment, such as IP addresses or hostnames of created resources.

---

### 9. **Naveed is asked to store sensitive input values such as admin credentials securely. What best practice should he follow when using parameters?**

(a) Store credentials as plaintext in the template file  
(b) Use secure strings and reference Key Vault if possible  
(c) Hardcode them in the variable section  
(d) Use the diagnostic settings  

**Correct answer: (b)**  
**Explanation:** Using **secure string parameters** and referencing **Azure Key Vault** ensures that sensitive values like passwords remain protected during deployments.

---

### 10. **After deploying a VM using an ARM template, which resource should Naveed verify to ensure that network security rules are correctly applied?**

(a) Public IP address  
(b) Network Interface  
(c) Virtual Machine extension  
(d) Network Security Group (NSG)  

**Correct answer: (d)**  
**Explanation:** The **Network Security Group (NSG)** controls inbound and outbound traffic. Verifying it ensures that the VM has the correct access rules for functionality and security.

---

### 11. **How does Naveed make the deployment modular and reusable across different environments (e.g., dev, test, prod)?**

(a) Use static IP addresses  
(b) Hardcode resource names  
(c) Define parameters and template modularity  
(d) Use custom scripts post-deployment  

**Correct answer: (c)**  
**Explanation:** Using **parameters and modular templates** allows the same template to be reused across multiple environments by simply changing the values.

---
---
---
## Comic-Style Summary: **“Script It, Ship It – Deploying VMs the Smart Way!”**

---

### 🚀 The Curious Cloud Explorer’s Mission

Meet **Naveed**, our ever-curious Cloud Explorer at **TechWaveNaveed**. His manager assigned him a task: **"Deploy a Windows Virtual Machine... but with an ARM template!"** With a confident nod (and maybe a nervous gulp), Naveed rolled up his sleeves and opened the **Azure Portal**.

---

### 📦 Unboxing the ARM Template

Naveed downloaded the mysterious `template.json` file. Inside it were superpowers: **parameters** for usernames, **variables** for resources like **VNets** and **NICs**, and detailed blueprints of a complete VM setup. “So this file basically builds the whole VM world for me?” he whispered with awe.

---

### ☁️ Cloud Shell to the Rescue

Naveed jumped into **Azure Cloud Shell**, uploaded the template, and ran the magical **`az deployment group create`** command. He filled in the blanks like a true DevOps artist—admin username, strong password, and a shiny resource group name like `rg-learntech-naveed`.

---

### 🕵️ Verifying the Creation Spell

After the deployment spell finished, our Azure admin opened the **Resource Group** in the portal. “Aha! Here's my **Windows VM**, complete with a **public IP**, **VNet**, **NSG**, and **storage account**. All born from one file!” he beamed.

---

### 🧹 Clean-up Like a Pro

Being the responsible TechWaveNaveed admin he is, Naveed didn’t forget to delete all the resources once he confirmed the lab worked. “A clean cloud is a happy cloud!” he chuckled, clicking **Delete Resource Group** like a boss.

---

### 💡 Moral of the Lab

Templates are like recipes. Instead of building resources one by one, Naveed learned how to use **ARM templates** to automate everything. It’s faster, repeatable, and very **pro-level cloud engineering**.

---

✅ **Mission Accomplished**: Yes, **Naveed successfully completed his assigned task**, and he’s now one step closer to becoming an **Azure Infrastructure Wizard**! 🧙‍♂️✨

---
---
---
## Text-Based Diagram for the Lab: **"Create a Windows VM using an ARM Template"**

```plaintext
+---------------------------------------------------+
|             Start: The Curious Cloud Explorer     |
|                      (Naveed) logs in             |
+---------------------------------------------------+
                          |
                          v
+---------------------------------------------------+
|        Step 1: Download & Review ARM Template     |
|  - Includes parameters, variables, resources,     |
|    and outputs                                    |
+---------------------------------------------------+
                          |
                          v
+---------------------------------------------------+
|     Step 2: Upload Template to Azure Cloud Shell  |
|  - Open Cloud Shell (Bash)                        |
|  - Use Upload to add template.json                |
+---------------------------------------------------+
                          |
                          v
+---------------------------------------------------+
|           Step 3: Deploy Template via CLI         |
|  - Run `az deployment group create`               |
|  - Set admin credentials, deployment name         |
|  - Specify resource group                         |
+---------------------------------------------------+
                          |
                          v
+---------------------------------------------------+
|         Step 4: Verify Deployment in Portal       |
|  - Navigate to resource group                     |
|  - Confirm creation of:                           |
|     * Windows VM                                  |
|     * NIC, NSG, Public IP, VNet, Storage Account  |
+---------------------------------------------------+
                          |
                          v
+---------------------------------------------------+
|          Step 5: Delete All Deployed Resources    |
|  - Clean up by deleting the resource group        |
+---------------------------------------------------+
                          |
                          v
+---------------------------------------------------+
|                End: Task Successfully Done!       |
|  Naveed becomes an ARM Template deployment pro 🧠 |
+---------------------------------------------------+
```

### 🔍 Diagram Summary:

This diagram outlines how **Naveed**, the **Curious Cloud Explorer**, used an **ARM template** to deploy a **Windows Virtual Machine**. It breaks the process into 5 key stages: downloading the template, uploading it to **Cloud Shell**, deploying with **CLI**, verifying in the **Azure Portal**, and cleaning up resources. Each step uses core Azure services like **Resource Groups**, **Virtual Machines**, **Network Interfaces**, and **Storage Accounts** to deliver infrastructure-as-code in a structured and automated fashion.

---
---
---
