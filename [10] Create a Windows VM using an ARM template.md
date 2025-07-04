# Lab 10: Create a Windows VM using an ARM template

**Duration:** 30m
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
