# Lab 15: Implementing Virtual Network Peering

**Duration:** 1h 30m

---
---

### After logging in with your credentials:

### **Step 1: Create the First Virtual Network**

1. In the portal, select **Create a Resource**.
2. Search for **Virtual Network** and select the result.
3. Click **Create**.
4. On the **Basics** tab:

   * Choose your **Resource Group** (e.g., `rg_westeurope_XXXXXX`)
   * Set **Virtual Network Name** to `Net1`
   * Set **Region** to `West Europe`
5. Go to the **IP Addresses** tab:

   * Set **IPv4 address space** to `10.1.0.0/16`
6. Remove the default subnet by selecting it and clicking **Remove Subnet**.
7. Click **Add Subnet** and fill in:

   * **Subnet Name**: `SubnetA`
   * **Subnet Address Range**: `10.1.0.0/24`
   * Leave other options as default, then click **Add**
8. Click **Review + Create**, then click **Create**

### **Step 2: Create the Second Virtual Network**

1. Repeat the process to create another Virtual Network:

   * **Virtual Network Name**: `Net2`
   * **Region**: `West Europe`
   * **IPv4 address space**: `10.2.0.0/16`
2. In the **IP Addresses** tab, add:

   * **Subnet Name**: `SubnetB`
   * **Subnet Address Range**: `10.2.0.0/24`
3. Complete the creation as in Step 1

### **Step 3: Peer the Two Virtual Networks**

1. In the search bar, locate and open the **Net1** virtual network.
2. In the left panel under **Settings**, select **Peerings**.
3. Click **Add** and configure:

   * **Peering Link Name (from Net1 to Net2)**: `Net1-Net2`
   * **Peering Link Name (from Net2 to Net1)**: `Net2-Net1`
   * **Virtual Network**: select `Net2`
4. Click **Add** to complete the peering configuration.

### **Step 4: Create the First Virtual Machine**

1. In the portal, search for **Virtual Machines** and click **Create > Azure Virtual Machine**
2. On the **Basics** tab:

   * **Virtual Machine Name**: `VM1`
   * **Region**: `West Europe`
   * **Image**: `Windows Server 2019 Datacenter - Gen2`
   * **Size**: `Standard_B2s`
   * **Username**: e.g., `vmuser1`
   * **Password**: enter and confirm
   * **Public inbound ports**: allow **RDP (3389)**
3. On the **Disks** tab:

   * Select **Standard SSD**
4. On the **Networking** tab:

   * **Virtual Network**: `Net1`
   * **Subnet**: `SubnetA`
5. Click **Review + Create**, then click **Create**

### **Step 5: Create the Second Virtual Machine**

1. Repeat the process to create another VM:

   * **Virtual Machine Name**: `VM2`
   * **Region**: `West Europe`
   * **Image**: `Windows Server 2019 Datacenter - Gen2`
   * **Size**: `Standard_B2s`
   * **Username**: e.g., `vmuser2`
   * **Password**: enter and confirm
   * **Public inbound ports**: **None**
2. On the **Disks** tab:

   * Select **Standard SSD**
3. On the **Networking** tab:

   * **Virtual Network**: `Net2`
   * **Subnet**: `SubnetB`
4. Click **Review + Create**, then click **Create**

### **Step 6: Enable Communication Between VMs**

1. Open the **VM1** resource and click **Connect > RDP**
2. Download and open the RDP file
3. Enter the VM credentials when prompted
4. After login, open **PowerShell** and run:

   ```powershell
   New-NetFirewallRule –DisplayName "Allow ICMPv4-In" –Protocol ICMPv4
   ```
5. To connect to **VM2** via internal IP:

   * Run the command (replace `10.2.0.4` with the private IP of `VM2`):

     ```powershell
     mstsc /v:10.2.0.4
     ```
   * Authenticate using `VM2`'s credentials when prompted

### Delete all the resources.

---
---

## **Lab Summary: Implementing Virtual Network Peering**

### **Purpose of the Lab**

The purpose of this lab is to demonstrate how to **create two isolated virtual networks**, **peer them together**, and then establish **communication between virtual machines (VMs)** deployed in each network. This simulates real-world scenarios where applications or services hosted in separate networks need secure and seamless communication without relying on public internet access.

This lab helps learners understand how to build **scalable, secure, and interconnected cloud networks** that support enterprise-level deployments and communication policies.

---

### **Azure Tools Used in the Lab**

Below is a list of **Azure services and tools** utilized in the lab, with a **brief description**, **their function**, and **examples** to clarify their real-world usage.

---

### 1. **Azure Portal**

* **Description**: A web-based user interface for managing all Azure resources.
* **Role in Lab**: Used for creating and managing **virtual networks**, **peerings**, and **virtual machines**.
* **Example**: Logging into [https://portal.azure.com](https://portal.azure.com) to create a **Virtual Network** named `Net1` in the **West Europe** region.

---

### 2. **Virtual Network (VNet)**

* **Description**: A logically isolated section of the Azure cloud where you can launch Azure resources in a secure network.
* **Role in Lab**: Two VNets (`Net1` and `Net2`) were created to simulate isolated network environments.
* **Example**: `Net1` with IP address space `10.1.0.0/16` and subnet `SubnetA (10.1.0.0/24)`.

---

### 3. **Subnet**

* **Description**: A sub-division of a VNet that segments the network into smaller, manageable parts.
* **Role in Lab**: Used to host specific resources such as VMs.
* **Example**: `SubnetA` under `Net1` and `SubnetB` under `Net2`.

---

### 4. **Virtual Network Peering**

* **Description**: A service that connects two VNets so they can communicate as if they are on the same network.
* **Role in Lab**: Peering was established between `Net1` and `Net2` to allow communication between VMs in separate networks.
* **Example**: Created peering from `Net1` to `Net2` with the link name `Net1-Net2`, and vice versa.

---

### 5. **Azure Virtual Machines**

* **Description**: Scalable computing resources that act like traditional servers.
* **Role in Lab**: Two VMs were created in separate VNets to test peered communication.
* **Example**: `VM1` was deployed in `Net1` and `VM2` in `Net2`, both running **Windows Server 2019 Datacenter**.

---

### 6. **RDP (Remote Desktop Protocol)**

* **Description**: A protocol for remotely accessing Windows-based machines.
* **Role in Lab**: Used to access `VM1` and initiate a connection to `VM2` via its **private IP**.
* **Example**: Downloaded an `.rdp` file to connect to `VM1` and used:

  ```powershell
  mstsc /v:10.2.0.4
  ```

  to connect to `VM2`.

---

### 7. **Private IP Address**

* **Description**: An IP address accessible only within a specific network or peered networks.
* **Role in Lab**: Used for VM-to-VM communication without exposing public endpoints.
* **Example**: `VM2` assigned private IP `10.2.0.4`, reachable only by `VM1` through VNet peering.

---

### 8. **New-NetFirewallRule (PowerShell Cmdlet)**

* **Description**: Adds a rule to allow traffic through the Windows Firewall.
* **Role in Lab**: Enabled **ICMP** traffic (ping) to verify connectivity.
* **Example**:

  ```powershell
  New-NetFirewallRule –DisplayName "Allow ICMPv4-In" –Protocol ICMPv4
  ```

---

### 9. **Resource Group**

* **Description**: A container that holds related resources for an Azure solution.
* **Role in Lab**: All resources (VNets, VMs) were created under a common **resource group** for easy management and deletion.
* **Example**: `rg_westeurope_123456`

---

## **Conclusion**

By completing this lab, users gain hands-on experience in setting up **interconnected cloud environments** using **virtual networks**, **VMs**, and **peering configurations**. This is highly relevant for designing modern, distributed systems in the cloud where different application tiers or services must communicate securely across isolated networks.

---
---

## **Scenario: Enabling Secure Communication Between Application Tiers Using Azure Virtual Network Peering**

### **Background**

**Evelyn**, a cloud engineer at a mid-sized healthcare company called **MediSync Solutions**, has been assigned the task of improving the security and network architecture of their new patient data management system.

The company is designing this system using a **multi-tier architecture**:

* The **front-end application** will reside in one **virtual network** (VNet A).
* The **backend database** will live in a separate **virtual network** (VNet B) for security isolation.

However, these components still need to **communicate securely** with each other **without exposing any public IPs**.

To implement this, Evelyn decides to use **Azure Virtual Network Peering**, which enables **private and high-speed connectivity** between **two VNets** within the **same region**.

---

## **Step-by-Step Story**

### **Step 1: Creating Two Virtual Networks**

Evelyn opens the **Azure Portal** and clicks **Create a Resource**. She searches for **Virtual Network** and creates two VNets:

* **VNet1**

  * Name: `AppVNet`
  * Address space: `10.1.0.0/16`
  * Subnet: `SubnetApp` (`10.1.0.0/24`)

* **VNet2**

  * Name: `DataVNet`
  * Address space: `10.2.0.0/16`
  * Subnet: `SubnetData` (`10.2.0.0/24`)

These VNets simulate **application** and **database** tiers, keeping them isolated from each other for **network security and compliance**.

---

### **Step 2: Creating Virtual Machines in Each Network**

To test communication between the tiers, Evelyn creates two **virtual machines (VMs)**:

* **AppVM** in `AppVNet`

  * Name: `AppVM`
  * Image: **Windows Server 2019**
  * Admin username: `adminuser`
  * Public RDP: **enabled** for testing
  * Subnet: `SubnetApp`

* **DBVM** in `DataVNet`

  * Name: `DBVM`
  * Image: **Windows Server 2019**
  * Admin username: `dbadmin`
  * Public RDP: **disabled**
  * Subnet: `SubnetData`

This simulates **real-world deployment** where the **frontend** has public access, but the **backend** is completely private.

---

### **Step 3: Enabling VNet Peering**

Evelyn now peers the two VNets using the **Azure Portal**:

1. She selects **AppVNet**, navigates to **Peerings**, and clicks **Add**.
2. She names the peering links:

   * Local to remote: `AppToData`
   * Remote to local: `DataToApp`
3. She selects **DataVNet** as the remote network.
4. She ensures that **Allow traffic between VNets** is enabled.

Now, both VNets are **logically connected** and their resources can talk **privately using internal IPs**.

---

### **Step 4: Verifying Communication**

Evelyn logs into **AppVM** via **Remote Desktop (RDP)** and wants to test connectivity to **DBVM**.

But first, she opens **PowerShell** on AppVM and runs the following command to allow ping responses (ICMP):

```powershell
New-NetFirewallRule –DisplayName "Allow ICMPv4-In" –Protocol ICMPv4
```

Then, she checks the **private IP address** of **DBVM** from the Azure portal (e.g., `10.2.0.4`) and runs this command from **AppVM**:

```powershell
ping 10.2.0.4
```

The ping is successful, confirming that **VNet peering is working** and both VMs can communicate securely using **private IP addresses** only.

---

### **Business Impact**

By implementing this setup, Evelyn has achieved:

* **Network isolation** for security compliance.
* **Private communication** between application components.
* **No dependency** on public internet for internal traffic.
* **Scalability**, as more VNets and VMs can now be peered securely.

This pattern is widely used in **microservices architectures**, **hybrid deployments**, and **multi-environment setups** (e.g., dev, test, prod) where secure traffic segregation is critical.

---

### **Conclusion**

Thanks to **Virtual Network Peering**, Evelyn successfully enabled **secure, high-speed communication** between isolated Azure networks, aligning perfectly with enterprise **security and performance goals**.

This approach also forms the foundation for more advanced scenarios such as **hub-and-spoke network topologies**, **hybrid cloud**, and **service chaining** using Azure-native features.

---
---

## ✅ Did Evelyn Complete Her Task Efficiently?

**Yes, Evelyn completed her task both efficiently and correctly.**
Here’s how — explained step-by-step in a clear and easy way:

---

### 🧠 **What Was Evelyn’s Task?**

Evelyn was asked to:

* Set up two separate **private networks** in the cloud.
* Allow them to **safely talk to each other** without using the public internet.
* Make sure the system is secure, organized, and reliable for a healthcare company’s application and database.

---

### 🧩 **How Did She Do It?**

#### 🔹 Step 1: Created Two Virtual Networks (Like Two Offices)

Evelyn created two **virtual networks** (called VNets) — one for the app and one for the database.

📌 *Think of this like setting up two separate offices in different buildings, each with its own staff and private rooms.*

#### 🔹 Step 2: Set Up One Virtual Machine in Each Network

She created one **virtual computer (VM)** in each network:

* One to run the **application**
* One to store **data**

📌 *This is like setting up one computer in each office for employees to use.*

#### 🔹 Step 3: Connected the Two Networks Using “Peering”

Evelyn used a feature called **Virtual Network Peering** to link the two networks **internally**.

📌 *Imagine she built a secure hallway between the two offices — so staff could visit each other directly without going outside.*

#### 🔹 Step 4: Checked If Everything Was Working

She tested the connection by:

* Logging into one VM.
* Sending a message (ping) to the other VM’s private address.
* It worked — which means the setup was successful.

📌 *It’s like calling someone in the next office using an internal extension — and they pick up the phone right away!*

---

### 🔒 **Was It Safe and Smart?**

**Yes. Very much so.**

Evelyn:

* Avoided exposing sensitive data to the public internet.
* Ensured internal communication stayed private and secure.
* Followed best practices for cloud networking.

---

### 📈 **What’s the Business Benefit?**

* The company’s systems are **now ready to scale** securely.
* It reduces the **risk of security breaches**.
* Makes the IT setup **faster and more reliable** for doctors, patients, and staff.

---

## 🎯 Final Verdict

**Evelyn completed her job efficiently, smartly, and securely.**
She used modern cloud tools correctly and made sure everything was set up to work both safely and effectively — just like a true professional.

---
---
## Lab-Based Conceptual MCQs

1. **Why is Virtual Network Peering used in Azure environments?**  
   (a) To connect Azure VMs to the internet  
   (b) To allow secure communication between different virtual networks  
   (c) To host web applications  
   (d) To create virtual machines faster  
   **Correct answer: (b)**  
   Virtual Network Peering enables private communication between virtual networks, avoiding the public internet for better security and performance.

2. **Which protocol must be enabled in the firewall to successfully test communication using ping?**  
   (a) TCP  
   (b) HTTP  
   (c) ICMP  
   (d) FTP  
   **Correct answer: (c)**  
   Ping relies on the Internet Control Message Protocol (ICMP), which must be allowed through the Windows firewall.

3. **What is the main benefit of placing application and database VMs in separate virtual networks with peering?**  
   (a) Reduced licensing cost  
   (b) Simplified internet access  
   (c) Enhanced isolation with secure connectivity  
   (d) More storage options  
   **Correct answer: (c)**  
   Separating components in different virtual networks improves isolation, and peering allows secure internal communication.

4. **Which component in Azure defines the IP range and segmentation of your cloud network?**  
   (a) Virtual Machine  
   (b) Virtual Network  
   (c) Load Balancer  
   (d) Availability Set  
   **Correct answer: (b)**  
   A Virtual Network (VNet) allows you to define IP address ranges and subnets for your cloud environment.

5. **What does the subnet 10.1.0.0/24 signify in network configuration?**  
   (a) A public IP address  
   (b) A subnet with 16 IP addresses  
   (c) A subnet with 256 IP addresses  
   (d) A NAT gateway  
   **Correct answer: (c)**  
   A /24 subnet provides 256 IP addresses, of which 254 are usable.

6. **Why should default subnets be removed when customizing a Virtual Network?**  
   (a) To save cost  
   (b) They prevent VM creation  
   (c) They may not align with required IP ranges or naming standards  
   (d) They are not secure  
   **Correct answer: (c)**  
   Customizing subnets allows administrators to define specific address ranges and policies suitable for the application’s architecture.

7. **In a peered VNet configuration, what kind of traffic can flow between the networks?**  
   (a) Only encrypted web traffic  
   (b) Internet-bound traffic  
   (c) Private traffic across Azure backbone  
   (d) VPN-based traffic only  
   **Correct answer: (c)**  
   Peering uses Azure's private backbone network to enable low-latency, secure communication between VNets.

8. **Which VM configuration ensures that only internal access is allowed from another VM?**  
   (a) Public inbound ports: All  
   (b) Public inbound ports: HTTP  
   (c) Public inbound ports: RDP  
   (d) Public inbound ports: None  
   **Correct answer: (d)**  
   Setting public inbound ports to "None" means the VM can only be accessed privately, such as from a peered VNet.

9. **What must you check when a VM in one VNet cannot connect to a VM in another peered VNet?**  
   (a) Storage SKU  
   (b) The OS version  
   (c) Peering status and firewall rules  
   (d) Admin password  
   **Correct answer: (c)**  
   Communication failure is often due to misconfigured peering or firewalls blocking traffic like ICMP or RDP.

10. **What is a key security benefit of using VNet peering instead of routing traffic through the public internet?**  
    (a) It increases latency  
    (b) It requires less configuration  
    (c) It eliminates egress data charges  
    (d) It avoids exposure to external threats  
    **Correct answer: (d)**  
    Peering enables internal traffic over the Azure backbone, reducing exposure to potential internet-based threats.

---
---
