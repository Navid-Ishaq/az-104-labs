# Lab 6: Network Access to Storage Accounts
**Date:** 2025-07-05  
**Duration:** 1h 0m  

---

### After logging in with your credentials:

---

### ✅ Create a Virtual Network

1. Navigate to **Create a resource** and search for **Virtual Network**.
2. Click **Create** and fill in the following:
   - **Resource Group**: `rg-learntech-naveed`
   - **Virtual Network Name**: `vnet-ncloudedge-west1`
   - **Region**: West Europe
3. Go to the **IP Addresses** tab:
   - Remove the default address space.
   - Add a new **IPv4 address space**.
   - Click **+ Add a Subnet** and set:
     - **Subnet Name**: `subnet-nxt-app`
     - **Address Range**: `10.0.0.0/24`
4. Click **Review + Create**, then **Create**.

---

### ✅ Create a Storage Account with a Private Endpoint

1. Go to **Storage accounts** and click **Create**.
2. In the **Basics** tab:
   - **Resource Group**: `rg-learntech-naveed`
   - **Storage Account Name**: `stgnxtnav001`
   - **Region**: West Europe
   - **Performance**: Standard
   - **Redundancy**: GRS (default)
3. Go to the **Networking** tab:
   - **Network access**: Select **Disable public access** and **use private access**
   - Click **+ Add private endpoint** and configure:
     - **Name**: `pe-nxtblob01`
     - **Sub-resource**: `blob`
     - **Virtual Network**: `vnet-ncloudedge-west1`
     - **Subnet**: `subnet-nxt-app`
4. Click **OK**, then **Review + Create**, and finally **Create**.
5. Once deployed, go to the resource and select **Access keys**.
   - Reveal and copy the **connection string** for **Key 1** for later use.

---

### ✅ Create a Virtual Machine

1. Search for and open **Virtual Machines**, then click **+ Create**.
2. On the **Basics** tab:
   - **Resource Group**: `rg-learntech-naveed`
   - **VM Name**: `vm-ncloudedge-access`
   - **Region**: West Europe
   - **Image**: Windows Server 2019 Datacenter - Gen2
   - **Size**: Standard_B2s
   - **Username**: `cloudadmin`
   - **Password**: Set and confirm
   - **Inbound Ports**: Allow RDP (3389)
3. On the **Disks** tab:
   - Select **OS disk type**: Standard SSD
4. On the **Networking** tab:
   - **Virtual Network**: `vnet-ncloudedge-west1`
   - **Subnet**: `subnet-nxt-app`
5. Click **Review + Create**, then **Create**.

---

### ✅ Access Storage Account from the Virtual Machine

1. Open **Virtual Machines** and select `vm-ncloudedge-access`.
2. Click **Connect > RDP** and download the RDP file.
3. Use the downloaded file to connect. When prompted:
   - Click **More choices > Use a different account**
   - Enter your VM credentials
   - Accept the certificate warning to continue.
4. Once inside the VM, open **PowerShell** and run:
   ```
   nslookup stgnxtnav001.blob.core.windows.net
   ```
5. In the **Start** menu, open **Server Manager > Local Server**.
   - Turn off **IE Enhanced Security Configuration**
6. Download and install **Azure Storage Explorer** inside the VM.
7. In **Storage Explorer**:
   - Select **Connect to Azure resources**
   - Choose **Storage account or service > Connection string**
   - Paste the **connection string** copied earlier
   - Click **Next**, verify details, then **Connect**
   - Browse to your storage account and access **Blob Containers > $logs**

---

### ✅ Final Step
**Delete all the resources.**

---
---
---
## **Structured Summary – Lab 6: Network Access to Storage Accounts**

---

### **🎯 Purpose of the Lab**

The purpose of this lab is to demonstrate how to **securely access an Azure Storage Account** through a **Private Endpoint** within a **Virtual Network (VNet)**. This setup ensures that data communication between resources occurs entirely over a private, internal network, rather than the public internet — meeting security and compliance standards. The lab also showcases how a **Virtual Machine (VM)** in the same subnet can access the storage account using **Azure Storage Explorer** with a **connection string**, simulating real-world enterprise configurations.

---

### **🛠️ Azure Tools and Their Roles**

| **Azure Tool**             | **Description**                                                             | **Role in the Lab**                                                                                   | **Example Resource Name**           |
| -------------------------- | --------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------- |
| **Virtual Network (VNet)** | A private network space in Azure to isolate and connect resources securely. | Used to isolate resources and enable secure access to storage via private IP.                         | `vnet-learntech-naveed`             |
| **Subnet**                 | A segment within a VNet with its own address space.                         | Hosts both the VM and private endpoint for resource communication.                                    | `subnet-naveedcloudops-data`        |
| **Storage Account**        | A scalable Azure service to store blobs, files, and other data.             | Stores blob data and is secured to allow access only via the private endpoint.                        | `stg-cloudlabx-secure01`            |
| **Private Endpoint**       | A private IP-based access point to an Azure resource inside a VNet.         | Connects the storage account privately to the subnet, disabling public internet access.               | `pe-cloudlabx-stg01`                |
| **Virtual Machine (VM)**   | A Windows-based compute resource used to test networked access.             | Installed with **Azure Storage Explorer** to test and validate private access to the storage account. | `vm-ncloudedge-monitor01`           |
| **Connection String**      | An authentication method used to connect to a storage account.              | Used in Azure Storage Explorer inside the VM to authenticate and access the storage blob securely.    | Retrieved from storage account keys |
| **Azure Storage Explorer** | A GUI tool to explore and manage Azure Storage resources.                   | Installed inside the VM to test blob access using the connection string over the private endpoint.    | N/A (client-side application)       |

---

### **📘 Clarification Example**

Imagine **Naveed**, a cloud administrator at **TechWaveNaveed**, needs to ensure secure, internal-only access to his storage account for hosting sensitive client logs. He creates a **Virtual Network** named `vnet-techwave-prod`, a **subnet** called `subnet-logs`, and a **storage account** named `stg-techwave-client01`. Then, he configures a **private endpoint** within that subnet and deploys a **VM** (`vm-techwave-admin01`) into the same subnet to validate connectivity. Inside the VM, he uses **Azure Storage Explorer** with the **connection string** to browse the storage — all without exposing the storage account to the public internet.

---

### **🔐 Conclusion**

This lab equips learners like **Naveed**, the Curious Cloud Explorer, with practical skills in:

* **Creating secure storage access paths** using **Private Endpoints**
* **Deploying and configuring VNets and subnets**
* **Implementing internal-only access policies**
* **Testing connectivity** using **Azure Storage Explorer**

Such practices are vital for industries such as **finance, government, and healthcare**, where **data privacy, compliance**, and **internal resource segmentation** are mission-critical.

---
---
---
## Comic-Style Summary: **“Storage in the Shadows – The Private Way!”**

### 🌩️ The Mission: Keep It Private, Keep It Safe

**Naveed**, the **Curious Cloud Explorer** from **TechWaveNaveed**, was on a quest to secure sensitive client data. His challenge? Build a system where **no storage resource is publicly accessible** — but still usable internally for business-critical operations. Like a digital ninja, he planned to work behind the scenes, using **private endpoints** and **virtual networks** to keep things stealthy and secure.

---

### 🛠️ Building the Secret Tunnel – A Virtual Network

First, Naveed crafted a secure digital road: a **Virtual Network** called `vnet-techwave-prod`, and within it, a hidden alley known as **`subnet-logs`**. This would be the private passage for accessing storage without ever stepping into the internet's spotlight.

> 🔐 **Key Concept**: A **Virtual Network** isolates resources from public exposure and forms the foundation for private connectivity in Azure.

---

### 📦 The Hidden Vault – A Private Storage Account

Next, he created a **Storage Account** called `stg-techwave-client01` and made a big move — **disabled public access**. Then, like installing a secure door into a private room, he attached a **Private Endpoint** connecting the Blob storage to the `subnet-logs` network. No public internet snoopers allowed!

> 🔍 **Private Endpoint** = Secure connection over a private IP address, hiding the storage from public access while still making it usable internally.

---

### 🧪 The Field Test – A Private-Access Virtual Machine

To test everything, he summoned a new **Windows Virtual Machine**, `vm-techwave-admin01`, and dropped it right into the same subnet. He logged in, installed **Azure Storage Explorer**, and connected to the storage using the **access key** — and boom! It worked. Storage access without ever touching the open internet.

> 💡 **Virtual Machines in the same subnet** can securely connect to private resources without public endpoints — a key element of enterprise cloud security.

---

### ✅ Mission Accomplished: Silent and Secure

Naveed successfully **completed his task**. All storage access was locked down inside a secure Azure environment. Sensitive logs were shielded, compliance was achieved, and the internet never knew what hit it.

---

### 📌 What We Learned:

* Use **Virtual Networks** and **subnets** to segment and isolate traffic.
* Attach **Private Endpoints** to services like **Storage Accounts** for secure internal access.
* Validate with tools like **Azure Storage Explorer** inside VMs that live in the same private network.
* Keep naming consistent with real-world conventions like `vm-ncloudedge-web01` or `stg-techwave-client01`.

---

**In the end**, the Curious Cloud Explorer didn't just store files. He stored **trust**, **security**, and **confidence** — all tucked neatly away in Azure's invisible, private corridor. 🌐✨

---
---
---
### 🚀 Real-World Business Impact

By combining **Azure Virtual Network**, **Private Endpoints**, and **Storage Explorer**, Naveed:

* Prevents data leaks by **removing public exposure**
* Aligns with **zero-trust networking models**
* Improves **auditing and access control**
* Simplifies compliance with financial and data residency regulations

This lab is a **blueprint for secure enterprise cloud design**, where storage resources are only accessible from approved internal systems—making it ideal for businesses that prioritize **data privacy and control**.

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
---
---
## Professional Job Interview Questions – Lab 6: Network Access to Storage Accounts

### 1. Naveed, a cloud administrator at TechWaveNaveed, needs to ensure secure access to a storage account that hosts sensitive client logs. Which of the following configurations will help him keep the storage account accessible only from within a private Azure network?

(a) Enable public endpoint with firewall restrictions  
(b) Create a **Private Endpoint** linked to a **Virtual Network**  
(c) Enable HTTPS access and SAS token  
(d) Use a service endpoint on a public subnet  

**Correct answer: (b)**  
**Explanation:** A **Private Endpoint** allows secure access to a **Storage Account** through a private IP within a **Virtual Network**, eliminating exposure to the public internet.

### 2. Naveed creates a **Virtual Network** called `vnet-techwave-prod` and a **Subnet** named `subnet-logs`. What is the purpose of isolating resources into specific subnets in this context?

(a) To increase data redundancy  
(b) To provide public access to blob containers  
(c) To segregate and control access at the network level  
(d) To automate virtual machine scaling  

**Correct answer: (c)**  
**Explanation:** Subnets in a **Virtual Network** help isolate resources, enforce **network security rules**, and control internal traffic routing, aligning with secure architecture.

### 3. When Naveed disables public access on a **Storage Account**, which of the following best describes the resulting behavior?

(a) The storage account is deleted  
(b) It blocks all access including internal Azure services  
(c) It restricts internet-based access to the account  
(d) The account becomes read-only  

**Correct answer: (c)**  
**Explanation:** Disabling public access prevents all public endpoint requests, securing the **Storage Account** from unauthorized access while allowing private/internal connections.

### 4. What is the role of the **Connection String** retrieved from the **Storage Account** in Naveed’s task?

(a) It allows uploading to an Azure SQL database  
(b) It is used to authenticate and connect with the account in **Storage Explorer**  
(c) It creates a key vault for encryption  
(d) It connects to a virtual machine over SSH  

**Correct answer: (b)**  
**Explanation:** The **Connection String** contains authentication information needed by tools like **Azure Storage Explorer** to access **blob containers** or **file shares**.

### 5. Naveed creates a virtual machine named `vm-techwave-admin01`. Why does he place it inside the same subnet (`subnet-logs`) as the storage private endpoint?

(a) For pricing benefits  
(b) To increase disk throughput  
(c) To allow network-level access to the private endpoint  
(d) To create a load balancer configuration  

**Correct answer: (c)**  
**Explanation:** Placing the VM in the same **Subnet** ensures it can resolve the **Private Endpoint's** private IP and access the **Storage Account** internally.

### 6. Why would Naveed choose **Azure Storage Explorer** inside the virtual machine instead of accessing the storage account via the browser?

(a) Browsers are incompatible with Azure  
(b) Browsers expose data to more security risks  
(c) **Azure Storage Explorer** can connect using private endpoints from within the VNet  
(d) Storage Explorer provides cost optimization features  

**Correct answer: (c)**  
**Explanation:** **Azure Storage Explorer** supports connecting via **connection strings** and respects private IP configurations, enabling access from within the **Virtual Network**.

### 7. What DNS record is resolved when Naveed runs `nslookup stg-techwave-client01.blob.core.windows.net` from his VM?

(a) The VM IP address  
(b) The public IP of the subnet  
(c) The private IP of the private endpoint  
(d) Azure Front Door hostname  

**Correct answer: (c)**  
**Explanation:** **nslookup** resolves the DNS to the **Private Endpoint’s** IP address, validating the secure internal routing to the **Storage Account**.

### 8. Naveed wants to ensure the **Virtual Machine** cannot access other services on the internet while maintaining access to the storage account. What should he configure?

(a) A NAT Gateway  
(b) A Network Security Group with outbound restrictions  
(c) A route table pointing to Azure Firewall  
(d) An Application Gateway  

**Correct answer: (b)**  
**Explanation:** Applying an **NSG** to limit **outbound internet access** while allowing specific internal traffic maintains security boundaries around the VM.

### 9. Why is it important for Naveed to turn off **IE Enhanced Security Configuration** inside the VM before downloading **Azure Storage Explorer**?

(a) It increases download speed  
(b) It allows DNS updates  
(c) It allows downloading external resources without prompts  
(d) It’s required for blob encryption  

**Correct answer: (c)**  
**Explanation:** **IE Enhanced Security Configuration** restricts internet downloads. Disabling it allows tools like **Azure Storage Explorer** to be downloaded without interruptions.

### 10. After all resources are deployed, Naveed validates access to **blob storage logs** using **Storage Explorer**. Which container would typically contain Azure service logs?

(a) $metrics  
(b) blob-archive  
(c) system-storage  
(d) $logs  

**Correct answer: (d)**  
**Explanation:** The special container **$logs** is used to store **Azure diagnostics and activity logs**, which are critical for monitoring and auditing.

---
---
---
## Professional Job Interview Questions – Network Access to Storage Accounts

1. **Naveed**, a cloud engineer at **TechWaveNaveed**, needs to ensure that a storage account is only accessible within a virtual network. Which configuration should he use?
   - (a) Enable public access and configure NSG rules
   - (b) Use a private endpoint within the virtual network
   - (c) Create a service endpoint on a different subnet
   - (d) Use an ExpressRoute circuit
   - **Correct answer: (b)**  
     Using a **private endpoint** ensures that the storage account is accessible only through the selected **virtual network**, maintaining security by bypassing public access.

2. While creating a VM named **vm-techwave-admin01**, the Curious Cloud Explorer wants it to access a storage account privately. What must be true about the virtual network setup?
   - (a) It must be in a different region from the storage account
   - (b) The VM must have a public IP
   - (c) The VM and storage account must share the same **virtual network and subnet**
   - (d) DNS must be disabled on the VM
   - **Correct answer: (c)**  
     For a **VM to communicate with a storage account via private endpoint**, both must be part of the **same virtual network and subnet** or properly peered networks.

3. A storage account in **rg-learntech-naveed** is set to allow **private access only**. What outcome should Naveed expect when trying to access it over the public internet?
   - (a) Success if credentials are correct
   - (b) Access is denied due to the private access configuration
   - (c) Access succeeds via Azure Storage Explorer
   - (d) Access is redirected to another region
   - **Correct answer: (b)**  
     **Disabling public access** restricts access to the storage account from any source not connected via a **private endpoint**.

4. The CloudOps engineer wants to confirm DNS resolution for the storage account **stg-techwave-client01** from within a VM. What PowerShell command should he use?
   - (a) `Resolve-DnsName blob.core.windows.net`
   - (b) `nslookup stg-techwave-client01.blob.core.windows.net`
   - (c) `Test-NetConnection`
   - (d) `ping stg-techwave-client01`
   - **Correct answer: (b)**  
     **nslookup** verifies **DNS resolution** for the private endpoint's hostname from the VM, ensuring correct name-to-IP mapping.

5. After configuring a **private endpoint** on blob storage, what’s an expected side effect if DNS integration isn't correctly set up?
   - (a) Slower storage performance
   - (b) Public access is restored
   - (c) VM fails to resolve the storage account hostname
   - (d) Storage data is lost
   - **Correct answer: (c)**  
     Without correct **DNS setup**, the VM won't resolve the **private IP address** tied to the storage account, causing access failures.

6. Naveed needs to ensure that his storage account is not accessible publicly and can only be reached from a specific subnet. What Azure feature should he use to enforce this configuration?

(a) Service Endpoints  
(b) Network Security Groups  
(c) Private Endpoints  
(d) Application Gateway  

**Correct answer: (c)**  
**Explanation**: **Private Endpoints** allow secure, private connectivity to Azure services over the Azure backbone network, which is ideal for internal-only access to storage accounts.

7. The Curious Cloud Explorer has deployed a virtual machine in the same subnet as the storage account’s private endpoint. What tool can he use inside the VM to verify access to blob storage using a connection string?

(a) Azure CLI  
(b) Azure Storage Explorer  
(c) Azure Monitor  
(d) Disk Management  

**Correct answer: (b)**  
**Explanation**: **Azure Storage Explorer** allows users to connect to and manage storage accounts. Using a connection string, resources like blob containers can be accessed securely from inside a VM.

8. While troubleshooting, the CloudOps engineer runs an `nslookup` for the storage account’s blob endpoint inside the VM. What is the purpose of this step?

(a) To fetch the access key  
(b) To test DNS resolution through the private endpoint  
(c) To open a public port  
(d) To check disk size  

**Correct answer: (b)**  
**Explanation**: The `nslookup` command helps verify that the blob endpoint resolves through the **private endpoint**, ensuring the storage is reachable only via the configured VNet.

9. Naveed wants to allow RDP access to the VM deployed in the same subnet. What port should he ensure is open during the VM configuration?

(a) 80  
(b) 22  
(c) 443  
(d) 3389  

**Correct answer: (d)**  
**Explanation**: **Port 3389** is the default port for **Remote Desktop Protocol (RDP)**, which is required to connect to a Windows VM remotely.

10. In the context of private access to a storage account, why is disabling public network access critical?

(a) It reduces disk latency  
(b) It improves data compression  
(c) It prevents exposure of the storage account to the public internet  
(d) It enables auto-scaling  

**Correct answer: (c)**  
**Explanation**: **Disabling public network access** ensures that only clients within the private network (e.g., a specific subnet with a private endpoint) can access the storage account, thereby enhancing security.
"""

---
---
---
## Comic-Style Summary: **“Private by Design: Locking Down Storage Access”**

### 🛠️ The Plan: Keep It Private!

Naveed, the **Curious Cloud Explorer**, was on a mission at **TechWaveNaveed**. His challenge? To make sure sensitive storage data was only accessible within the private network — no public exposure allowed. This wasn’t just about deploying resources; it was about mastering secure, internal-only access using **Private Endpoints**.

### 🌐 Building the Safe Zone

The **CloudOps engineer** began by creating a virtual network called **vnet-techwave-prod** with a subnet named **subnet-logs**. This subnet would be the secret passageway connecting internal resources. He knew this virtual fortress would be the first step in keeping things tidy and traffic controlled.

### 🧱 Sealing the Storage Vault

Next, the **TechWaveNaveed admin** spun up a **Storage Account** named **stg-techwave-client01**. Instead of exposing it to the wild internet, he added a **Private Endpoint** — linking it directly to the subnet. Now, even curious outsiders couldn’t peek inside.

### 🖥️ Access Without Exposure

To prove his setup worked, our **Azure admin** deployed a VM named **vm-techwave-admin01** inside the same subnet. He hopped into the machine, ran a DNS test with `nslookup`, and confirmed the private IP resolution was working like a charm.

### 🔐 Browsing the Blob — Securely

Inside the VM, the **Curious Cloud Explorer** launched **Azure Storage Explorer**. With the **connection string** copied earlier, he accessed the blob storage — viewing the contents without ever needing public access. Mission accomplished. Quiet, secure, and beautifully executed.

### 🧹 Clean-Up Crew

After validating everything, he removed all deployed resources. No leftover mess. Just clean, professional cloud work — the kind of job Naveed does best.

> ✅ **Final Note:** This story shows how combining **Private Endpoints**, **Virtual Networks**, and **secure access tools** can help enforce internal data policies while giving admins like Naveed full control over who sees what — and from where.

---
---
---
## Text-Based Diagram for the Lab: "Network Access to Storage Accounts"

```text
+----------------------------------------------------+
|           Start: Log in to Azure Portal           |
+----------------------------------------------------+
                        |
                        v
+----------------------------------------------------+
|         Create Virtual Network (vnet-techwave-prod)|
|        - Resource Group: rg-techwave-naveed        |
|        - Region: West Europe                       |
+----------------------------------------------------+
                        |
                        v
+----------------------------------------------------+
|            Add Subnet to VNet (subnet-logs)        |
|        - Address Range: 10.0.0.0/24                |
+----------------------------------------------------+
                        |
                        v
+----------------------------------------------------+
|        Create Storage Account (stg-techwave-client01) |
|        - Region: West Europe                       |
|        - Redundancy: GRS                           |
+----------------------------------------------------+
                        |
                        v
+----------------------------------------------------+
|     Configure Networking: Disable Public Access    |
|     and Add Private Endpoint (private-endpoint)    |
|        - Sub-resource: blob                        |
|        - VNet/Subnet: vnet-techwave-prod/subnet-logs|
+----------------------------------------------------+
                        |
                        v
+----------------------------------------------------+
|       Retrieve Storage Account Key 1 Connection    |
|                String for Access                   |
+----------------------------------------------------+
                        |
                        v
+----------------------------------------------------+
|      Create Virtual Machine (vm-techwave-admin01)  |
|        - Image: Windows Server 2019                |
|        - Size: Standard_B2s                        |
|        - VNet/Subnet: vnet-techwave-prod/subnet-logs|
+----------------------------------------------------+
                        |
                        v
+----------------------------------------------------+
|          Connect to VM via RDP                     |
|      - Turn off IE Enhanced Security               |
|      - Install Azure Storage Explorer              |
+----------------------------------------------------+
                        |
                        v
+----------------------------------------------------+
|      Use nslookup to test DNS resolution of blob   |
|      Use Storage Explorer to connect via string    |
|      and browse blob container ($logs)             |
+----------------------------------------------------+
                        |
                        v
+----------------------------------------------------+
|               Delete All Resources                 |
+----------------------------------------------------+
```

### 📌 Summary:

This diagram visually outlines the **step-by-step process** for securely accessing an **Azure Storage Account** using **Private Endpoints**. The process involves setting up a **Virtual Network**, deploying a **Storage Account**, creating a **Private Endpoint**, launching a **Virtual Machine**, and validating access internally with **Azure Storage Explorer** — all while avoiding public exposure to the internet.

---
---
---
