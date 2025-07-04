# Lab 6: Network Access to Storage Accounts

**Duration:** 1h 0m

---
After logging in with your credentials:
---

### **Create a Virtual Network**

1. Navigate to **Create a resource** and search for **Virtual Network**.
2. Select **Create** and fill in the following:

   * **Resource Group**: Use the designated lab resource group.
   * **Virtual Network Name**: `whizNet1`
   * **Region**: `West Europe`
3. Proceed to the **IP Addresses** tab:

   * Remove the default address space.
   * Add a new **IPv4 address space**.
   * Click **+ Add a Subnet**, and set:

     * **Subnet Name**: `SubnetA`
     * **Address Range**: `10.0.0.0/24`
4. Click **Review + Create**, then **Create**.

---

### **Create a Storage Account with a Private Endpoint**

1. Go to **Storage accounts** and click **Create**.
2. In the **Basics** tab:

   * **Resource Group**: Use the existing one.
   * **Storage Account Name**: Use a unique name.
   * **Region**: `West Europe`
   * **Performance**: `Standard`
   * **Redundancy**: `GRS` (default)
3. Move to the **Networking** tab:

   * **Network access**: Select `Disable public access and use private access`
4. Click **+ Add private endpoint** and configure:

   * **Name**: `privateEndpoint`
   * **Sub-resource**: `blob`
   * **Virtual Network**: `whizNet1`
   * **Subnet**: `SubnetA`
5. Click **OK**, then **Review + Create**, and finally **Create**.
6. Once deployed, go to the resource and select **Access keys**.
7. Reveal and copy the **connection string** for **Key 1** for later use.

---

### **Create a Virtual Machine**

1. Search for and open **Virtual Machines**, then click **+ Create**.
2. On the **Basics** tab:

   * **Resource Group**: Use the existing one.
   * **VM Name**: `myWhizlabsVM1`
   * **Region**: `West Europe`
   * **Image**: `Windows Server 2019 Datacenter - Gen2`
   * **Size**: `Standard_B2s`
   * **Username**: `vm1`
   * **Password**: Set and confirm
   * **Inbound Ports**: Allow `RDP (3389)`
3. On the **Disks** tab:

   * Select **OS disk type**: `Standard SSD`
4. On the **Networking** tab:

   * **Virtual Network**: `whizNet1`
   * **Subnet**: `SubnetA`
5. Click **Review + Create**, then **Create**.

---

### **Access Storage Account from the Virtual Machine**

1. Open **Virtual Machines** and select `myWhizlabsVM1`.

2. Click **Connect > RDP** and download the RDP file.

3. Use the downloaded file to connect. When prompted:

   * Click **More choices > Use a different account**
   * Enter your VM credentials

4. Accept the certificate warning to continue.

5. Once inside the VM, open **PowerShell** and run:

   ```powershell
   nslookup <your-storage-account-name>.blob.core.windows.net
   ```

6. In the Start menu, open **Server Manager > Local Server**.

   * Turn off **IE Enhanced Security Configuration**

7. Download and install **Azure Storage Explorer** inside the VM.

8. In Storage Explorer:

   * Select **Connect to Azure resources**
   * Choose **Storage account or service > Connection string**
   * Paste the **connection string** copied earlier
   * Click **Next**, verify details, then **Connect**

9. Browse to your storage account and access **Blob Containers > \$logs**

---

Delete all the resources.

---
---
---

### **Purpose of the Lab**

The objective of this lab is to demonstrate how to **secure access to Azure Storage Accounts** by using **private endpoints**, thereby ensuring that storage traffic remains within the **Azure Virtual Network (VNet)**. This enhances **data security** by avoiding exposure to the public internet. Additionally, the lab illustrates how to use a **Virtual Machine (VM)** within the same VNet to access the storage account securely and verify the configuration using **Azure Storage Explorer**.

---

### **Azure Tools and Services Utilized**

#### **1. Azure Virtual Network (VNet)**

* **Description**: A logically isolated network within the Azure cloud that enables secure communication between Azure resources.
* **Role in Lab**: A **VNet** (`whizNet1`) is created to host the **SubnetA**, which is used to isolate both the **Virtual Machine** and **Private Endpoint**, ensuring traffic stays internal.

#### **2. Azure Subnet**

* **Description**: A range of IP addresses within a **VNet**.
* **Role in Lab**: A subnet (`SubnetA`) is defined to house both the VM and the private endpoint, enabling network isolation and control.

#### **3. Azure Storage Account**

* **Description**: A service for storing structured and unstructured data, including blobs, files, queues, and tables.
* **Role in Lab**: The storage account is created with **public access disabled** and **private access enabled**, ensuring it can only be reached through the **private endpoint**.

#### **4. Private Endpoint**

* **Description**: A network interface that connects you privately and securely to a service powered by **Azure Private Link**.
* **Role in Lab**: A **Private Endpoint** is created for the storage account’s **Blob** service, linking it to the **VNet** so only internal resources can access it.

#### **5. Azure Virtual Machine (VM)**

* **Description**: A scalable computing resource that behaves like a traditional server and runs Windows or Linux operating systems.
* **Role in Lab**: A **Windows Server 2019 VM** (`myWhizlabsVM1`) is created in the same **VNet** and **SubnetA** to test access to the storage account using the **connection string**.

#### **6. Azure Storage Explorer**

* **Description**: A free, standalone app from Microsoft that allows easy access and management of Azure cloud storage resources.
* **Role in Lab**: Installed on the VM to connect to the **Storage Account** using the **connection string**, validating the **private access** setup.

#### **7. NSLookup**

* **Description**: A network administration command-line tool used for querying the Domain Name System (DNS).
* **Role in Lab**: Used inside the VM to confirm that the storage account’s **Blob** endpoint resolves to a **private IP address**, verifying the **private endpoint** functionality.

#### **8. Access Keys / Connection String**

* **Description**: A set of credentials used to programmatically access Azure Storage services.
* **Role in Lab**: The **connection string** is used in **Storage Explorer** to authenticate and securely access the storage account from the VM.

---

### **Conclusion**

This lab emphasizes best practices in **network security** and **data access control** within Azure. By combining **VNets**, **private endpoints**, and **role-based access**, organizations can ensure that their critical data in **Azure Storage Accounts** remains protected from unauthorized public access, aligning with enterprise-grade **compliance** and **security requirements**.

---
---
---


### **Scenario: Securing Access to Storage for a Financial Application**

**Background**

Sarah is a **Cloud Engineer** at a financial services company named **FinSecure Ltd.** The company is migrating sensitive customer data into **Azure Storage Accounts** and must ensure that access to this data is strictly controlled — **no public access** is allowed. Sarah is tasked with setting up a secure architecture where only internal systems from a **private network** can connect to the storage service.

To meet **compliance** and **security** requirements, Sarah decides to use a combination of **Azure Virtual Networks (VNets)**, **Private Endpoints**, and **Virtual Machines (VMs)** to create and test a locked-down, secure environment for data access.

---

### **Step-by-Step Actions and Purpose**

1. **Creating a Virtual Network**

   Sarah begins by creating a **Virtual Network (VNet)** named **whizNet1** in the **West Europe** region. She adds a **subnet** called **SubnetA** with the address range **10.0.0.0/24**. This **VNet** will host all internal resources, isolating them from the public internet.

   > **Why?** To build a secure network boundary and control which resources can communicate with each other internally.

2. **Creating a Storage Account with Private Access**

   Next, Sarah creates a **Storage Account** and configures it to **disable public access**. Instead, she adds a **Private Endpoint** that links the storage account’s **Blob** service to **SubnetA**.

   > **Why?** This ensures that the storage service is only reachable from within the **VNet**, protecting it from external threats and unauthorized access.

3. **Saving the Connection String**

   After the storage account is deployed, Sarah copies the **connection string** from the **Access keys** section. This string will later be used by internal applications to connect to the storage securely.

   > **Why?** The **connection string** is a secure way to authenticate and connect to the storage service without relying on public endpoints.

4. **Deploying a Virtual Machine**

   Sarah then deploys a **Windows Server 2019 Virtual Machine (VM)** named **myWhizlabsVM1** in the same **VNet** and **SubnetA**. She enables **RDP** to connect to the VM and installs **Azure Storage Explorer** on it.

   > **Why?** This VM simulates an internal application host that will access the **Storage Account** privately, validating that the **Private Endpoint** is working as intended.

5. **Verifying Network Isolation**

   Inside the VM, Sarah uses the **nslookup** command to check if the **blob service endpoint** of the storage account resolves to a **private IP address**. It does.

   > **Why?** This confirms that traffic to the storage account is routed internally via the **Private Endpoint** — not over the internet.

6. **Accessing the Storage Account**

   Sarah opens **Azure Storage Explorer** on the VM, selects the option to connect using a **Connection String**, and pastes the string she copied earlier. She successfully connects to the **Blob** container without requiring any public internet access.

   > **Why?** This proves that internal applications hosted in the **VNet** can securely access storage services through private network paths.

---

### **Business Outcome**

Thanks to this setup, **FinSecure Ltd.** can now move its sensitive financial data into Azure Storage with confidence. Only authorized systems inside the company's **private network** can access the storage account, ensuring compliance with regulatory standards such as **ISO 27001** and **GDPR**.

This architecture also positions the company to scale securely — future microservices or analytics tools can be added to the **VNet**, all while maintaining strict data access control using **Private Endpoints** and **Azure Role-Based Access Control (RBAC)**.

---

### **Conclusion**

This story illustrates how a common enterprise need — secure data access — can be achieved using **Azure VNets**, **Storage Accounts**, **Private Endpoints**, and **VMs**. Each step in the lab supports a real-world objective: safeguarding data in the cloud without sacrificing accessibility for internal systems.

---
---
---
## Lab-Based Conceptual MCQs

### 1. Why would a storage account use a **Private Endpoint** in Azure?

**(a)** To enable access from multiple subscriptions  
**(b)** To ensure secure access within a **Virtual Network**  
**(c)** To provide cheaper storage performance  
**(d)** To allow unrestricted internet access  

**✅ Correct answer: (b)**  
**Explanation**: A **Private Endpoint** allows resources within a **Virtual Network** to access the storage account privately, avoiding exposure to the public internet.

---

### 2. What is the role of the **Connection String** in Azure Storage?

**(a)** It limits the data transfer speed  
**(b)** It serves as a backup method  
**(c)** It provides authentication and connection information  
**(d)** It encrypts the storage container  

**✅ Correct answer: (c)**  
**Explanation**: A **Connection String** contains the keys and endpoint required to authenticate and connect to a storage account.

---

### 3. Why must **IE Enhanced Security Configuration** be turned off inside the **Virtual Machine**?

**(a)** To reduce Azure costs  
**(b)** To allow installation of Microsoft updates  
**(c)** To enable downloading and using tools like **Storage Explorer**  
**(d)** To speed up virtual network provisioning  

**✅ Correct answer: (c)**  
**Explanation**: **IE Enhanced Security** blocks downloads and external websites, so it must be disabled to access resources like **Storage Explorer**.

---

### 4. What ensures that only internal traffic can reach an Azure **Storage Account**?

**(a)** Enabling HTTP only access  
**(b)** Adding a **Private Endpoint** and disabling public access  
**(c)** Assigning a static IP  
**(d)** Enabling encryption  

**✅ Correct answer: (b)**  
**Explanation**: Disabling public access and using a **Private Endpoint** ensures that storage can only be accessed from within the **Virtual Network**.

---

### 5. What would the **nslookup** command verify when run inside the **Virtual Machine**?

**(a)** The public IP of the VM  
**(b)** If DNS resolves the storage account via private IP  
**(c)** The subnet address  
**(d)** The cost of storage  

**✅ Correct answer: (b)**  
**Explanation**: **nslookup** helps confirm that the **Storage Account** blob service resolves to a **private IP**, indicating private access is working.

---

### 6. Which component allows connecting securely from a **VM** to an Azure **Storage Account**?

**(a)** NAT Gateway  
**(b)** Azure Firewall  
**(c)** Private Endpoint  
**(d)** Route Table  

**✅ Correct answer: (c)**  
**Explanation**: A **Private Endpoint** links the storage account to the **Virtual Network**, enabling secure, internal access from the **VM**.

---

### 7. Why is **Azure Storage Explorer** used in this lab?

**(a)** To monitor billing  
**(b)** To test secure storage access from the **VM**  
**(c)** To configure virtual networks  
**(d)** To deploy new VMs  

**✅ Correct answer: (b)**  
**Explanation**: **Storage Explorer** is used to test if a client machine like a **VM** can connect to and manage blob containers using a **Connection String**.

---

### 8. What is the significance of placing the **VM** and **Private Endpoint** in the same **Virtual Network**?

**(a)** It enables pricing optimization  
**(b)** It ensures the VM can resolve the private DNS zone  
**(c)** It improves disk IOPS  
**(d)** It guarantees VM scaling  

**✅ Correct answer: (b)**  
**Explanation**: Being in the same **Virtual Network** ensures that the **VM** can access the **Private Endpoint** and resolve DNS internally.

---

### 9. Which setting should be selected to ensure no public traffic reaches the **Storage Account**?

**(a)** Public access  
**(b)** Performance Tier  
**(c)** Disable public access and use private access  
**(d)** Enable HTTPS only  

**✅ Correct answer: (c)**  
**Explanation**: This setting disables all public endpoints, forcing all traffic through the configured **Private Endpoint**.

---

### 10. What is the key benefit of using a **Private Endpoint** over service endpoints?

**(a)** Lower cost  
**(b)** No authentication needed  
**(c)** Fully private IP-based access  
**(d)** Better performance  

**✅ Correct answer: (c)**  
**Explanation**: **Private Endpoints** provide fully private, IP-based access over the internal network without using public routing paths.

---

