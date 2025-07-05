# Lab 21: Creating Azure Firewall

**Duration:** 1h 30m

---
---

**After logging in with your credentials:**

### Step 1: Create a Virtual Network

1. Navigate to **Create a resource**, then search for **Virtual Network**.
2. Click **Create** and provide:

   * **Resource Group**: Use an existing or create a new one.
   * **Name**: e.g., `Net-Firewall-Lab`
   * **Region**: e.g., `West Europe`
3. Proceed to **IP Addresses** tab.
4. Delete the default subnet.
5. Add the following subnets:

   * **AzureFirewallSubnet** – starting address: `10.0.1.0`
   * **Workload-SN** – starting address: `10.0.2.0`, subnet size `/24`
   * **Jump-SN** – starting address: `10.0.3.0`
   * **AzureFirewallManagementSubnet** – starting address: `10.0.4.0`
6. Click **Review + Create** > **Create**.

---

### Step 2: Deploy Two Virtual Machines

**First VM (Jump Server):**

1. Go to **Virtual Machines** > **Create Azure Virtual Machine**.
2. Configure:

   * **Name**: `Srv-Jump`
   * **Region**: `West Europe`
   * **Image**: Windows Server 2019 Datacenter - Gen2
   * **Size**: Standard\_B2s
   * **Username**: `jump`
   * **Password**: (your choice)
   * **Inbound Port Rules**: Allow RDP (3389)
   * **Virtual Network**: previously created one
   * **Subnet**: `Jump-SN`
3. Use default settings for Public IP and Disks.
4. Click **Review + Create** > **Create**.

**Second VM (Workload Server):**

1. Repeat the process, but use:

   * **Name**: `Srv-Work`
   * **Username**: `work`
   * **Subnet**: `Workload-SN`
   * **Inbound Ports**: None
   * **Public IP**: None

---

### Step 3: Deploy Azure Firewall with Policy

1. Go to **Firewalls** > **Create**.
2. Set:

   * **Name**: e.g., `FirewallLab`
   * **Region**: `West Europe`
   * **Zone**: `Zone 1`
   * **SKU**: Basic
3. Under **Firewall Policy**, click **Add new**:

   * Name: e.g., `LabPolicy`
   * Tier: Basic
4. Select existing virtual network.
5. Create new public and management IP addresses.
6. Click **Review + Create** > **Create**.

---

### Step 4: Create a Route Table

1. Search for **Route Tables** > **Create**.
2. Provide:

   * **Name**: `FirewallRoute`
   * **Region**: `West Europe`
   * **Propagate gateway routes**: Yes
3. Click **Create** and go to the resource.
4. Add route:

   * Name: `Route1`
   * Destination: `0.0.0.0/0`
   * Next hop type: **Virtual Appliance**
   * Next hop address: Firewall’s private IP
5. Associate the route table with the `Workload-SN` subnet.

---

### Step 5: Add Application Rule to Firewall Policy

1. Go to the Firewall resource.
2. Open the attached **Firewall Policy**.
3. Under **Application rules**, click **+Add rule collection**:

   * Name: `AllowWeb`
   * Priority: 200
   * Action: Allow
   * Rule Name: `Allow-Google`
   * Source: `10.0.2.0/24` (Workload-SN)
   * Protocols: `http, https`
   * Destination: `www.google.com`
4. Save the rule.

---

### Step 6: Add Network Rule to Firewall Policy

1. Under the same **Firewall Policy**, go to **Network rules**.
2. Add a rule collection:

   * Name: `AllowDNS`
   * Priority: 200
   * Action: Allow
   * Rule Name: `Allow-DNS`
   * Source: `10.0.2.0/24`
   * Protocol: UDP
   * Port: 53
   * Destination: `209.244.0.3, 209.244.0.4`
3. Save the rule.

---

### Step 7: Add DNAT Rule to Firewall Policy

1. Go to **DNAT rules**.
2. Add a DNAT rule collection:

   * Name: `rdp`
   * Priority: 200
   * Rule Name: `rdp-nat`
   * Source: Any
   * Protocol: TCP
   * Destination Port: 3389
   * Destination IP: Firewall’s public IP
   * Translated Address: Private IP of `Srv-Work`
   * Translated Port: 3389

---

### Step 8: Set Custom DNS for Workload VM

1. Open **Network Interface** of `Srv-Work`.
2. Go to **DNS Servers**.
3. Select **Custom** and add:

   * `209.244.0.3`
   * `209.244.0.4`
4. Save settings.
5. Restart the `Srv-Work` virtual machine.

---

### Step 9: Test the Firewall

1. Connect to `Srv-Jump` via RDP.
2. Open **Remote Desktop Connection** (`mstsc`) from inside the VM.
3. Connect to the private IP of `Srv-Work`.
4. Disable **IE Enhanced Security Configuration** inside `Srv-Work`.
5. Open Internet Explorer:

   * Try accessing `www.google.com` → should work.
   * Try accessing `www.microsoft.com` → should be blocked.

---

**Delete all the resources.**

---
---
Certainly! Below is a **structured, copyright-free summary** of the Azure Lab titled:

---

## **Lab Summary: Creating Azure Firewall and Configuring Network Rules**

### **Purpose of the Lab**

The primary goal of this lab is to **deploy and configure Azure Firewall** as a centralized security solution to control and monitor network traffic in an Azure environment. Through the lab, learners gain hands-on experience in:

* Creating a **virtual network (VNet)** with multiple subnets.
* Deploying **Azure Firewall** and applying **Firewall policies**.
* Setting up **virtual machines** in different subnets.
* Defining **application**, **network**, and **DNAT rules**.
* Configuring **routing and DNS** settings for secure communication.
* Validating that the firewall allows or blocks traffic as expected.

This lab simulates a real-world scenario where a company wants to protect its workloads using a cloud-native firewall.

---

### **Azure Tools and Services Used**

#### 1. **Virtual Network (VNet)**

A **Virtual Network** is the foundation of the Azure networking model. It allows Azure resources to securely communicate with each other.
**Role in Lab:** Hosts the firewall and virtual machines within isolated **subnets** (e.g., Jump-SN, Workload-SN, Firewall subnets).
**Example:** `Net-Firewall-Lab` created with subnets for workload, jump host, and firewall management.

---

#### 2. **Subnets**

Subnets logically divide a VNet into segments, enabling better organization and control.
**Role in Lab:** Each subnet isolates traffic — for example:

* `AzureFirewallSubnet` for the firewall
* `Jump-SN` for the RDP jump server
* `Workload-SN` for workload VM
* `AzureFirewallManagementSubnet` for forced tunneling management

---

#### 3. **Virtual Machines (VMs)**

Azure **Virtual Machines** allow users to run Windows or Linux workloads.
**Role in Lab:**

* **Srv-Jump**: A jump box VM that allows secure RDP into internal resources.
* **Srv-Work**: A backend workload VM to test network connectivity and firewall rules.

---

#### 4. **Azure Firewall**

A **stateful, cloud-native network security service** that protects Azure Virtual Network resources.
**Role in Lab:** Controls inbound and outbound traffic using:

* **Application rules** (FQDN-based)
* **Network rules** (IP/protocol-based)
* **DNAT rules** (port forwarding)

---

#### 5. **Firewall Policy**

A **centralized set of rules** applied to Azure Firewall instances.
**Role in Lab:** Used to configure and apply consistent security rules to the deployed firewall.
**Example:** Policy includes rules to allow Google, DNS traffic, and RDP access.

---

#### 6. **Public IP Address**

A **static or dynamic IP address** used to communicate with Azure resources from the internet.
**Role in Lab:**

* The firewall receives a public IP to handle inbound DNAT requests.
* Enables internet access and management connectivity.

---

#### 7. **Route Table**

A **routing configuration** that defines how traffic is directed within a VNet.
**Role in Lab:** Forces all outbound traffic from the workload subnet to pass through the firewall using a **User-Defined Route (UDR)** with the firewall's private IP as the next hop.

---

#### 8. **DNS Configuration**

Custom **DNS settings** that allow name resolution based on user-defined servers.
**Role in Lab:** Workload VM is configured to use external DNS (`209.244.0.3`, `209.244.0.4`) for domain name resolution. Necessary for firewall policy testing with FQDNs.

---

#### 9. **Application Rule**

A firewall rule that filters **HTTP/S traffic based on domain names** (FQDN).
**Role in Lab:** Allows traffic to `www.google.com` while blocking other domains.
**Example:** Application rule for Google access only.

---

#### 10. **Network Rule**

A firewall rule based on **IP addresses and protocols**.
**Role in Lab:** Allows outbound **UDP traffic on port 53** (DNS queries) from the workload subnet.

---

#### 11. **DNAT Rule (Destination Network Address Translation)**

Used to **translate and forward inbound traffic** to a private IP address inside the network.
**Role in Lab:** Enables remote access to `Srv-Work` via RDP using the firewall’s public IP.

---

### **Conclusion**

This lab demonstrates how to build a **secure Azure network architecture** using **Azure Firewall**, **routing**, and **access control** mechanisms. By following this process, professionals can better secure their cloud infrastructure and manage traffic flow based on enterprise policies.

---
---
**Here's a **realistic, professional story-based scenario** that explains the Azure Firewall lab tasks in a relatable and step-by-step manner.**

---

## **Scenario: Securing Contoso’s Azure Network with Azure Firewall**

Meet **Alex**, a Cloud Administrator at **Contoso Ltd**, a mid-sized company that's rapidly moving its infrastructure to **Microsoft Azure**. The company runs several internal applications and backend services in the cloud, and Alex has been tasked with ensuring that **only authorized network traffic** flows between these resources, while **blocking unwanted internet access** from the internal VMs.

To meet this security requirement, Alex decides to implement **Azure Firewall** with a custom **Firewall Policy**, configure **Application**, **Network**, and **DNAT rules**, and route all traffic through the firewall using a **User-Defined Route**.

---

### **Step 1: Creating the Virtual Network and Subnets**

Alex starts by creating a **Virtual Network (VNet)** to host all Azure resources. He splits it into four **subnets**:

* **AzureFirewallSubnet**: Hosts the firewall itself.
* **Workload-SN**: Contains the application server (Srv-Work).
* **Jump-SN**: Hosts the jump server (Srv-Jump) for admin access.
* **AzureFirewallManagementSubnet**: Supports **forced tunneling** scenarios.

This layout gives Alex full control over how traffic flows between different parts of the network.

---

### **Step 2: Deploying Virtual Machines**

To simulate a real setup:

* He deploys **Srv-Jump**, a Windows VM in **Jump-SN**, which has a **public IP** and is configured to allow **RDP (port 3389)** access.
* Then, he deploys **Srv-Work** in **Workload-SN**, a backend VM **without a public IP**, meaning it can’t be accessed directly from the internet.

This approach aligns with the principle of **least privilege** and **network segmentation**, reducing the attack surface.

---

### **Step 3: Deploying Azure Firewall**

Alex then creates an **Azure Firewall** resource in the **AzureFirewallSubnet**. He also creates a **Firewall Policy** to define security rules. He assigns:

* A **Public IP** for DNAT and outbound access.
* A **Private IP** for internal routing.

He attaches the firewall to the existing VNet, ensuring it sits at the center of traffic flow.

---

### **Step 4: Defining Routing with Route Table**

To force all outbound traffic through the firewall, Alex creates a **Route Table** and associates it with the **Workload-SN** subnet.

He adds a **User-Defined Route**:

* Destination: **0.0.0.0/0** (all outbound traffic)
* Next Hop: The **firewall’s private IP**

This step ensures **no traffic leaves** the workload VM **without inspection**.

---

### **Step 5: Creating Firewall Rules**

Now comes the key part—**security rules**.

* **Application Rule**: Allows access to **[www.google.com](http://www.google.com)** only from the **Workload-SN** subnet using **FQDN-based filtering**. This simulates a real-world scenario where only approved domains are reachable.

* **Network Rule**: Allows **UDP port 53** traffic (DNS) to a specific DNS provider. Without this, **domain resolution won’t work**, which would break the application rule.

* **DNAT Rule**: Enables **RDP access** to **Srv-Work** through the firewall’s public IP. The rule translates incoming TCP requests on port 3389 to the **private IP** of **Srv-Work**.

---

### **Step 6: Custom DNS Configuration**

To support domain resolution (needed for the application rule), Alex manually sets **custom DNS servers** (`209.244.0.3`, `209.244.0.4`) on the **network interface** of **Srv-Work**, ensuring it can resolve domain names.

After saving, he restarts the VM to apply changes.

---

### **Step 7: Validating the Setup**

Using **RDP**, Alex logs into **Srv-Jump** and initiates a remote connection to **Srv-Work** using its **private IP**. From **Srv-Work**, he:

* Successfully browses to **[www.google.com](http://www.google.com)** (allowed by the Application rule).
* Is blocked when attempting to visit **[www.microsoft.com](http://www.microsoft.com)** (not in the allowlist).

This confirms that the **firewall is enforcing rules** correctly and outbound access is **tightly controlled**.

---

### **Outcome**

Alex has now implemented:

* **Centralized traffic control** with Azure Firewall.
* **Secure RDP access** without exposing workload VMs to the internet.
* **Granular rule-based access** to specific web domains.
* **Custom routing and DNS**, providing enhanced network security.

His manager, **Sophia**, is impressed and asks him to document the steps as a **best-practice reference** for future deployments.

---

### **Conclusion**

This practical lab shows how **Azure Firewall**, when combined with **networking, routing**, and **security policies**, empowers organizations to **protect cloud environments** efficiently. It reflects the daily responsibilities of an **Azure Administrator (AZ-104)** tasked with implementing enterprise-grade **network security**.

Alex’s setup is now a model for building **secure, compliant, and manageable Azure networks**.

---
---
**Here's a **comic-style, simplified explanation** of the Azure Firewall lab scenario, showing how **Alex** the Cloud Admin tackled his task. This version is perfect for beginners and easy to follow.**

---

## 🎯 Mission: Secure the Cloud Network

**Meet Alex**, an Azure Cloud Admin at Contoso Ltd. One morning, his manager **Sophia** says:

> “Alex, we need to make sure no one can sneak around our cloud network. Use a **firewall** and block everything except what we approve!”

Alex says, “Got it!”

---

## 🧱 Step 1: Build the Network Foundation

Alex logs into Azure and creates a **Virtual Network** — it's like building a digital city. Then he adds **four neighborhoods (subnets)**:

* One for the **Firewall**
* One for the **Workload Server**
* One for the **Jump Server**
* One for **Firewall Management**

These subnets help keep things organized, just like lanes in a highway.

---

## 🖥️ Step 2: Deploy the Virtual Machines

Next, Alex sets up two virtual machines:

* **Jump Server (Srv-Jump)**: Like a secure entry gate, it has a public door for admins.
* **Workload Server (Srv-Work)**: The secret machine inside with no public access!

He places them in their proper subnets so traffic can be controlled later.

---

## 🔥 Step 3: Bring in the Firewall!

Time to set up the **Azure Firewall** — the digital guard dog!
Alex deploys the firewall and gives it a **private IP** (for inside the network) and a **public IP** (to manage special traffic from outside).

He also creates a **Firewall Policy**, the rulebook the firewall must follow.

---

## 🛣️ Step 4: Control the Traffic Flow

To make sure everything passes through the firewall, Alex creates a **Route Table**.
He says,

> “All traffic from the workload must go through the firewall. No shortcuts!”

He connects the route table to the **Workload Subnet**, ensuring all traffic follows the rules.

---

## 🛡️ Step 5: Create Security Rules

Now Alex writes the **rules of the road**:

* **Application Rule**: Allow access only to **[www.google.com](http://www.google.com)**.
* **Network Rule**: Allow DNS traffic (so websites can be found).
* **DNAT Rule**: Let outsiders connect to the **Workload Server** using the firewall’s public door — only through port **3389 (RDP)**.

These rules are like telling the firewall who’s allowed in and what roads they can take.

---

## 🌐 Step 6: DNS and Final Setup

Oops! The server can’t browse websites.
Alex realizes he needs to **manually set DNS servers** to allow name resolution.
He adds DNS addresses and **restarts the VM**. Now it works!

---

## ✅ Step 7: Test Like a Pro

Alex connects to the **Jump Server**, then hops into the **Workload Server**.
He tries **[www.google.com](http://www.google.com)** — ✅ it works.
He tries **[www.microsoft.com](http://www.microsoft.com)** — ❌ blocked! The firewall did its job.

Sophia says,

> “Alex, you've secured our cloud just like a pro!”

---

## 🎉 Mission Accomplished!

Alex:

* Built a safe network
* Deployed virtual machines
* Implemented smart firewall rules
* Tested everything end-to-end

And yes — **Alex successfully completed his assigned task** 💪

---
---
## Lab-Based Conceptual MCQs

**Note:** These questions are based on the Azure Firewall lab.

1. **Why is a separate subnet required specifically for the Azure Firewall?**
    - (a) To reduce cost of firewall deployment  
    - (b) To isolate firewall resources from other services  
    - (c) To simplify routing  
    - (d) To ensure public access to all VMs  
    - **Correct answer: (b)**  
    **Azure Firewall** must be deployed in its own subnet called **AzureFirewallSubnet** to ensure proper isolation and enforce secure network boundaries.

2. **What is the role of a route table in this lab scenario?**
    - (a) Assign IP addresses to subnets  
    - (b) Provide default internet gateway settings  
    - (c) Redirect traffic through the firewall for inspection  
    - (d) Connect VMs to DNS servers  
    - **Correct answer: (c)**  
    A **route table** is used to redirect all outbound traffic from a subnet to the **Azure Firewall** for traffic inspection.

3. **Why is a jump server used in this lab setup?**
    - (a) It increases the performance of the firewall  
    - (b) It is used to launch cloud shell  
    - (c) It provides secure RDP access to internal VMs  
    - (d) It automatically installs firewall rules  
    - **Correct answer: (c)**  
    The **jump server** acts as an intermediary for administrators to securely access internal VMs without exposing them directly to the public internet.

4. **Which firewall rule allows outbound web access to specific domains?**
    - (a) Network rule  
    - (b) DNAT rule  
    - (c) Application rule  
    - (d) Route rule  
    - **Correct answer: (c)**  
    **Application rules** control outbound access to **FQDNs** (Fully Qualified Domain Names) such as **www.google.com**.

5. **Why was DNS traffic specifically allowed in the firewall configuration?**
    - (a) It improves performance of VM connections  
    - (b) It allows name resolution for outbound browsing  
    - (c) It encrypts data using DNS over HTTPS  
    - (d) It enables routing updates  
    - **Correct answer: (b)**  
    Without **DNS resolution**, VMs cannot translate domain names to IP addresses, which is necessary for browsing the internet.

6. **What is the main use of the DNAT rule in the context of this lab?**
    - (a) Block access to specific IPs  
    - (b) Redirect public IP traffic to an internal VM  
    - (c) Translate domain names  
    - (d) Manage application-level rules  
    - **Correct answer: (b)**  
    **DNAT (Destination NAT)** rules allow external clients to access internal resources like the **Srv-work VM** using the firewall’s public IP.

7. **Why was the IE Enhanced Security Configuration disabled on the internal VM?**
    - (a) To allow file sharing  
    - (b) To reduce login latency  
    - (c) To allow easier testing of outbound web access  
    - (d) To improve DNS resolution  
    - **Correct answer: (c)**  
    This configuration is disabled to avoid security warnings and allow smoother browsing when testing access through the **firewall**.

8. **What happens if the route table is not associated with the workload subnet?**
    - (a) All traffic is dropped by default  
    - (b) Traffic bypasses the firewall  
    - (c) DNS resolution fails  
    - (d) RDP connection fails  
    - **Correct answer: (b)**  
    Without association, the **workload subnet** sends traffic directly to the internet, bypassing the **firewall**, which defeats the lab’s security setup.

9. **Why are private IPs used for the workload and jump VMs?**
    - (a) They are cheaper than public IPs  
    - (b) To restrict access and enforce security  
    - (c) Azure does not allow public IPs for Windows VMs  
    - (d) To improve performance  
    - **Correct answer: (b)**  
    Using **private IPs** enhances security by ensuring VMs can only be accessed through the **firewall** or other internal routing mechanisms.

10. **What is the purpose of configuring a custom DNS in the NIC settings of the workload VM?**
    - (a) It speeds up boot time  
    - (b) It allows name resolution through allowed firewall rules  
    - (c) It enables dynamic routing  
    - (d) It blocks malicious domains  
    - **Correct answer: (b)**  
    Assigning **custom DNS** ensures the VM can resolve **FQDNs** like **www.google.com** since the default Azure DNS may be blocked or insufficient.

---
---
## Professional Job Interview Questions – AZ-104 Labs

### 1. You are setting up an Azure Firewall to restrict outbound internet traffic from a subnet. What is the most effective method to allow access only to **specific FQDNs** like `www.google.com`?

(a) Use a custom DNS server  
(b) Create an **Application Rule** in the firewall policy  
(c) Add an NSG rule  
(d) Configure a Route Table with a custom route  

**Correct answer: (b)**  
**Explanation:** An **Application Rule** allows the firewall to filter traffic based on fully qualified domain names (FQDNs), making it the appropriate tool for this scenario.

---

### 2. An Azure administrator wants to restrict all traffic to a VM except **DNS lookups**. Which rule should be configured in Azure Firewall?

(a) Application Rule for port 53  
(b) Network Rule with **UDP protocol** and destination port 53  
(c) NSG rule allowing DNS  
(d) Route Table pointing to a custom DNS  

**Correct answer: (b)**  
**Explanation:** **Network Rules** in Azure Firewall are used for protocol-level filtering like DNS (UDP port 53).

---

### 3. You need to ensure that a virtual machine without a public IP can access the internet through Azure Firewall. What must be done?

(a) Assign a static private IP to the VM  
(b) Associate a **Route Table** that forwards traffic to the firewall  
(c) Install a proxy agent on the VM  
(d) Enable accelerated networking on the VM  

**Correct answer: (b)**  
**Explanation:** A **Route Table** with a default route to the firewall ensures that outbound traffic is inspected and routed through the firewall.

---

### 4. A company wants to centrally manage rules for multiple firewalls. Which feature should they implement?

(a) Network Security Group  
(b) Firewall Policy  
(c) Application Gateway  
(d) DNS Resolver  

**Correct answer: (b)**  
**Explanation:** **Firewall Policies** provide a centralized way to manage rules across multiple Azure Firewalls.

---

### 5. What is the purpose of creating a **DNAT Rule** in Azure Firewall?

(a) To forward traffic from one internal VM to another  
(b) To allow internet users to access a **specific internal resource** using the firewall's public IP  
(c) To allow outbound internet access  
(d) To restrict SSH access to Azure VMs  

**Correct answer: (b)**  
**Explanation:** **DNAT (Destination Network Address Translation)** rules map a public IP and port to an internal private IP, enabling access from external sources.

---

### 6. Why is it important to configure **custom DNS servers** for a VM when using Azure Firewall?

(a) To bypass Azure's name resolution  
(b) To support hybrid identity  
(c) To enable name resolution for FQDNs used in Application Rules  
(d) To increase performance  

**Correct answer: (c)**  
**Explanation:** **Application Rules** depend on DNS name resolution. Without a proper DNS setup, FQDN filtering won’t work correctly.

---

### 7. How does Azure Firewall determine whether to **block or allow traffic**?

(a) Based on NSG configuration  
(b) Based on VM tags  
(c) Based on **Firewall Policy Rule Collections**  
(d) Based on subnet IP size  

**Correct answer: (c)**  
**Explanation:** All traffic decisions in Azure Firewall are controlled through **Firewall Policy Rule Collections**.

---

### 8. What must be associated with a subnet to enforce routing through Azure Firewall?

(a) A VPN Gateway  
(b) A Firewall IP on the VM  
(c) A **User-Defined Route (UDR)** pointing to the firewall  
(d) An NSG with Allow rules  

**Correct answer: (c)**  
**Explanation:** A **User-Defined Route (UDR)** forces traffic to pass through the firewall by setting the next hop to the firewall's IP.

---

### 9. What is the benefit of placing VMs in **separate subnets** like Jump-SN and Workload-SN?

(a) Easier backup configuration  
(b) Enhanced data redundancy  
(c) Improved **network segmentation and access control**  
(d) Faster VM deployment  

**Correct answer: (c)**  
**Explanation:** Isolating workloads into **separate subnets** helps apply different policies and improves security via segmentation.

---

### 10. An administrator wants to ensure that only selected Azure services can reach the VM. Which setting should be reviewed in the firewall?

(a) NSG logging  
(b) Threat intelligence mode  
(c) Public IP prefix  
(d) **Application Rule Destination** settings  

**Correct answer: (d)**  
**Explanation:** **Application Rule Destinations** define which FQDNs are allowed, effectively controlling access from Azure services.

---
---
**Here's a comic-style, easy-to-understand summary of the Azure Firewall lab:**

---

### 🧑‍💼 Meet Alex – The Cloud Admin on a Mission

Alex was given a big task: **secure a network in Azure**! He began by building a **Virtual Network** – kind of like setting up a private town with different neighborhoods (called **subnets**) for different purposes: one for a **firewall**, one for **servers**, and one just for **jumping in remotely**.

---

### 🏗️ Building the Town’s Defenses

Alex added **virtual machines** into his subnets. One machine, called **Srv-Jump**, had a public door (via **RDP**) so Alex could connect and manage other machines. Another one, **Srv-Work**, was tucked away safely inside with **no public access** — this one needed special permissions!

---

### 🔥 The Mighty Firewall Appears!

Then Alex deployed the **Azure Firewall**, the town’s chief gatekeeper! He attached it to the network and gave it rules – like allowing visits to **Google**, but **blocking Microsoft.com**. He even gave it **public and private IP addresses**, so it could talk to the outside world and the internal network securely.

---

### 🛣️ Setting the GPS and Traffic Rules

Next, Alex created a **Route Table** and pointed all outbound traffic from the workload subnet to the firewall — this made sure nothing could sneak out or in without **firewall approval**. He added **application rules**, **network rules**, and even a **DNAT rule** so he could RDP into internal servers using the firewall’s public IP.

---

### 🧪 Time for a Real Test!

Alex jumped into **Srv-Jump**, opened **Remote Desktop**, and tunneled into **Srv-Work** safely. From there, he browsed to **Google** — it worked! He tried **Microsoft** — BLOCKED! Success! His **firewall policies** were working like a charm. 💥

---

### 🧹 Wrapping It All Up

With everything configured and tested, Alex validated his work and then cleaned up the town — or rather, **deleted all the resources** to save costs and keep things tidy.

**Mission accomplished!** 🛡️

---
---

## Text-Based Diagram for the Lab: "Creating Azure Firewall and Securing Network Traffic"

```markdown
| **Step** | **Description** |
|---------|------------------|
| 1 | **Login to Azure Portal** using your credentials. |
| 2 | **Create a Virtual Network (VNet)** in West Europe with the following subnets:<br>• AzureFirewallSubnet<br>• Workload-SN<br>• Jump-SN<br>• AzureFirewallManagementSubnet |
| 3 | **Deploy Virtual Machines (VMs):**<br>• `Srv-Jump` (Jump box with public IP)<br>• `Srv-Work` (Internal VM with no public IP)<br>Assign VMs to appropriate subnets. |
| 4 | **Deploy Azure Firewall and Policy:**<br>• Attach firewall to the VNet<br>• Assign public and private IPs<br>• Create and attach a basic firewall policy |
| 5 | **Configure Route Table:**<br>• Create a route table<br>• Add default route (0.0.0.0/0) with next hop = Azure Firewall private IP<br>• Associate with `Workload-SN` |
| 6 | **Add Application Rule to Firewall Policy:**<br>• Allow HTTP/HTTPS to `www.google.com`<br>• Source: IP range of Workload-SN |
| 7 | **Add Network Rule to Firewall Policy:**<br>• Allow DNS (UDP port 53) to external DNS servers<br>• Source: Workload-SN IP range<br>• Destination: 209.244.0.3, 209.244.0.4 |
| 8 | **Add DNAT Rule to Firewall:**<br>• Allow RDP to `Srv-Work` via Firewall Public IP<br>• Translates to `Srv-Work` private IP:3389 |
| 9 | **Configure DNS on `Srv-Work` NIC:**<br>• Set custom DNS: 209.244.0.3 and 209.244.0.4<br>• Restart VM to apply changes |
| 10 | **Test Firewall Setup:**<br>• Connect to `Srv-Jump` via RDP<br>• RDP into `Srv-Work` using internal IP<br>• Test browsing:<br>✓ www.google.com = Allowed<br>✗ www.microsoft.com = Blocked |
| 11 | **Delete all the resources** |
```

---
---





