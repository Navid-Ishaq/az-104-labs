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

Certainly. Here's a structured summary for the lab:

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


