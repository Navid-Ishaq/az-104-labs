# Lab 18: Troubleshoot routing, traffic control and load balancing in Microsoft Azure

**Duration:** 2h 0m

---
---

**After logging in with your credentials:**

### Task 1: Create a Virtual Network

1. Search for **Virtual Network** in the top search bar and select **Virtual Networks**.
2. Click on **+ Create**.
3. Under **Basics**:

   * Select the provided resource group.
   * Name the virtual network: `MyVNet`.
   * Region: Select **West Europe**.
4. Go to the **Security** tab and enable **Azure Bastion**.
5. Go to the **IP Addresses** tab:

   * Set IP address space to `10.1.0.0/16`.
   * Click on the existing **default** subnet and update:

     * Name: `myBackendSubnet`
     * Starting address: `10.1.0.0`
     * Subnet size: `/24 (256 addresses)`
6. Edit **AzureBastionSubnet**:

   * Set Starting address to `10.1.1.0`
7. Click **Review + Create**, then click **Create**.

---

### Task 2: Create a NAT Gateway

1. Search for **NAT Gateway** and select **+ Create**.
2. Under **Basics**:

   * Resource group: Select the existing group.
   * Name: `MyNATGateway`
   * TCP Idle timeout: `15` minutes.
3. Under **Outbound IP**:

   * Create a new public IP: Name it `MyNATPublicIP`.
4. Under **Subnet**:

   * Associate with **myBackendSubnet** in `MyVNet`.
5. Click **Review + Create**, then click **Create**.

---

### Task 3: Create a Load Balancer

1. Search for **Load Balancer** and click **+ Create**.
2. Under **Basics**:

   * Name: `MyLoadBalancer`
   * SKU: `Standard`
   * Type: `Public`
   * Tier: `Regional`
3. Under **Frontend IP configuration**:

   * Add a new frontend IP:

     * Name: `MyFrontendIP`
     * Create a new public IP: Name it `MyPublicIP`.
4. Under **Backend Pools**:

   * Name: `MyBackendPool`
   * Select the virtual network: `MyVNet`
   * Backend configuration: `NIC`
   * Save.
5. Under **Inbound Rules**:

   * Add a load balancing rule:

     * Name: `MyHTTPRule`
     * Frontend IP: `MyFrontendIP`
     * Backend pool: `MyBackendPool`
     * Protocol: `TCP`
     * Port: `80`
     * Health probe: Create a new one:

       * Name: `MyHealthProbe`
       * Protocol: `TCP`
     * Session persistence: `Client IP and protocol`
     * Idle timeout: `15`
     * Enable TCP reset: checked
     * Floating IP: not checked
6. Click **Review + Create**, then **Create**.

---

### Task 4: Create Virtual Machines

1. Search for **Virtual Machines** and click **+ Create**.

2. Under **Basics**:

   * Name: `MyVM1`
   * Region: `West Europe`
   * Image: `Windows Server 2022 Datacenter`
   * Size: `B2s`
   * Username/password: enter credentials
   * Inbound ports: select **None**

3. Under **Disks**:

   * OS Disk Type: `Standard SSD`

4. Under **Networking**:

   * VNet: `MyVNet`
   * Subnet: `myBackendSubnet`
   * Public IP: `None`
   * Load Balancer: Select `MyLoadBalancer`
   * Backend Pool: Select `MyBackendPool`

5. Under **Network Security Group (NSG)**:

   * Select **Advanced**
   * Create new NSG: Name it `MyNSG`
   * Add an inbound rule:

     * Service: `HTTP`
     * Priority: `1001`
     * Name: `AllowHTTP`

6. Click **Review + Create**, then **Create**.

7. Repeat the steps above to create a second VM:

   * Name: `MyVM2`
   * Availability Zone: `Zone 3`
   * Use existing NSG: `MyNSG`

---

### Task 5: Install IIS on Both VMs

1. For each VM:

   * Connect using **Bastion**.
   * Open **PowerShell** and run the following:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
Remove-Item C:\inetpub\wwwroot\iisstart.htm
Add-Content -Path "C:\inetpub\wwwroot\iisstart.htm" -Value $("Hello World from " + $env:computername)
```

---

### Task 6: Test Load Balancer

1. Go to **Load Balancer** > **Frontend IP configuration**.
2. Copy the public IP and paste it in a browser.
3. Refresh the page several times. Initially, it may return responses from the same VM due to **session persistence**.

---

### Task 7: Troubleshoot Load Balancer Rule

1. Check:

   * Both VMs allow inbound traffic on port **80**.
   * Load balancer rule is configured correctly.
2. Identify that **Session persistence** is set to **Client IP and protocol**.

---

### Task 8: Fix Load Balancer Configuration

1. Edit the load balancing rule.
2. Change **Session persistence** to **None**.
3. Save and wait for the changes to apply.

---

### Task 9: Retest Load Balancer

1. Open the public IP in a browser.
2. Refresh multiple times. You should now see responses alternate between `MyVM1` and `MyVM2`.

---

**Delete all the resources.**

---
---

## **Lab Summary: Troubleshoot Routing, Traffic Control, and Load Balancing in Azure**

### **Purpose of the Lab**

This lab focuses on building and troubleshooting a cloud network infrastructure where web traffic is managed efficiently using **Azure Load Balancer** and **NAT Gateway**. It guides learners through creating a **Virtual Network**, deploying **Virtual Machines**, configuring **Network Security Groups**, and installing **IIS** to host sample web content. The key objective is to simulate and resolve a scenario where internet traffic is not being evenly distributed across backend servers, and demonstrate how to fix it by adjusting load balancer rules.

By the end of the lab, learners understand how to:

* Configure routing and traffic control using Azure tools.
* Diagnose and correct session persistence issues.
* Deploy scalable web architecture for better performance and high availability.

---

### **Azure Tools Used and Their Roles**

#### **1. Virtual Network (VNet)**

* **Description**: A logically isolated section of the Azure cloud where resources can securely communicate.
* **Role in the Lab**: Acts as the foundational network for deploying and connecting all services including VMs, NAT Gateway, and Load Balancer.
* **Example**: `MyVNet` was created with custom subnets for backend and bastion access.

---

#### **2. Subnet**

* **Description**: A subdivision within a **Virtual Network** that allows grouping of similar resources.
* **Role in the Lab**: Used to segment network traffic and apply policies per subnet.
* **Example**: `myBackendSubnet` was used for VMs; `AzureBastionSubnet` was used for secure remote access.

---

#### **3. NAT Gateway**

* **Description**: Provides internet access to resources in private subnets without exposing them with public IP addresses.
* **Role in the Lab**: Enables outbound internet connectivity for VMs hosted in the backend subnet.
* **Example**: `MyNATGateway` connected to `myBackendSubnet` ensures secure and scalable outbound communication.

---

#### **4. Load Balancer**

* **Description**: Distributes incoming network traffic across multiple virtual machines or instances.
* **Role in the Lab**: Balances HTTP traffic between two web servers and allows troubleshooting of uneven load distribution.
* **Example**: `MyLoadBalancer` was configured with rules and health probes to manage HTTP traffic over port 80.

---

#### **5. Public IP Address**

* **Description**: An address accessible from the internet, used to route external traffic to Azure resources.
* **Role in the Lab**: Attached to the **Load Balancer** and **NAT Gateway** to enable external access.
* **Example**: `MyPublicIP` was created for the load balancer's frontend.

---

#### **6. Backend Pool**

* **Description**: A group of **Virtual Machines** behind a load balancer that handle incoming requests.
* **Role in the Lab**: Defines which VMs should process traffic based on the load balancer’s rules.
* **Example**: `MyBackendPool` included both `MyVM1` and `MyVM2`.

---

#### **7. Load Balancing Rule**

* **Description**: A configuration rule that defines how traffic should be distributed to backend pool members.
* **Role in the Lab**: Used to direct traffic on port 80 to both VMs. Initially configured with session persistence, which was later removed to resolve uneven distribution.
* **Example**: `MyHTTPRule` handled TCP traffic to port 80 and was adjusted to disable session persistence.

---

#### **8. Health Probe**

* **Description**: Monitors the health of backend instances and ensures traffic is only sent to healthy VMs.
* **Role in the Lab**: Ensured that only available VMs receive traffic.
* **Example**: `MyHealthProbe` checked TCP connectivity to backend servers.

---

#### **9. Virtual Machine (VM)**

* **Description**: A software-based computer that runs an operating system and apps like a physical computer.
* **Role in the Lab**: Hosted the IIS web server and served HTTP content used to verify load balancing.
* **Example**: `MyVM1` and `MyVM2` were configured identically and deployed in the same VNet.

---

#### **10. IIS (Internet Information Services)**

* **Description**: A web server feature for Windows Server used to serve web pages.
* **Role in the Lab**: Allowed the VMs to display a webpage for HTTP load balancing testing.
* **Example**: Both VMs had a modified `iisstart.htm` file showing the server name to confirm traffic routing.

---

#### **11. Bastion**

* **Description**: A service that provides secure and seamless RDP/SSH connectivity to virtual machines over SSL via the Azure portal.
* **Role in the Lab**: Enabled secure access to VMs without exposing them with public IPs.
* **Example**: Used to connect to `MyVM1` and `MyVM2` to install and configure IIS.

---

#### **12. Network Security Group (NSG)**

* **Description**: A set of inbound and outbound security rules that control traffic to network interfaces.
* **Role in the Lab**: Allowed HTTP traffic (port 80) to the virtual machines.
* **Example**: `MyNSG` had an inbound rule to allow TCP traffic on port 80.

---

### **Conclusion**

This lab provided hands-on experience with configuring and troubleshooting **network routing**, **NAT**, and **load balancing** in a cloud environment. By following a realistic issue-resolution path, it helped develop practical skills required by infrastructure and operations professionals managing web traffic in Azure.

**Key takeaway**: Proper configuration of session persistence, subnet routing, and load balancing rules is essential to ensure high availability and even traffic distribution in real-world cloud deployments.

---
---

## **Scenario Story: Fixing the Load Balancer Issue for a Growing Online Business**

**Meet David**, a cloud administrator at a fast-growing e-commerce startup called **GreenBasket**. The company has recently launched a web application for customers in Europe. The app is hosted on **virtual machines** (VMs) in **Microsoft Azure**, and traffic is managed by a **load balancer**. However, users are reporting slow performance and inconsistent page loads.

David’s manager, Sarah, asks him to **investigate and fix** the issue as soon as possible.

---

### **Step 1: Building the Network Foundation**

David starts by creating a secure **virtual network (VNet)** named **MyVNet** with two subnets:

* **myBackendSubnet** for hosting web servers.
* **AzureBastionSubnet** for secure VM access without public IPs.

He enables **Azure Bastion** so that his team can connect to VMs securely through the browser using **RDP over SSL**, without exposing the machines to the internet.

---

### **Step 2: Enabling Outbound Internet Access**

To ensure the VMs can reach the internet for updates or software installation, David creates a **NAT Gateway**. He attaches it to the **myBackendSubnet**, assigns a **public IP address**, and sets the **TCP idle timeout** to a reasonable value of 15 minutes.

Now the backend VMs can connect to the internet, but remain protected from incoming public traffic.

---

### **Step 3: Distributing Incoming Traffic**

Next, David creates a **public load balancer** named **myLoadBalancer**. This will help distribute HTTP traffic to the backend VMs. He creates:

* A **frontend IP configuration** to receive traffic.
* A **backend pool** with the VMs.
* A **health probe** that checks if the VMs respond on **TCP port 80**.
* A **load balancing rule** to direct incoming requests to the backend pool using **port 80**.

He also ensures that the **session persistence** is initially set to **Client IP and protocol**, to observe behavior.

---

### **Step 4: Deploying Web Servers**

David then spins up two **Windows Server 2022** VMs: **MyVM1** and **MyVM2**. He connects to them using **Azure Bastion** and installs **IIS (Internet Information Services)** on both machines.

To help identify traffic distribution, he modifies the default IIS web page on each VM to display:

> “Hello from MyVM1”
> “Hello from MyVM2”

---

### **Step 5: Testing the Load Balancer**

With everything in place, David opens the **load balancer’s public IP** in a browser. He refreshes the page repeatedly, expecting to see traffic alternate between **MyVM1** and **MyVM2**.

However, the content always shows **MyVM1**. Something’s off.

---

### **Step 6: Troubleshooting the Issue**

David starts investigating. He verifies:

* The **network security group (NSG)** allows inbound traffic on port 80.
* Both VMs are healthy and reachable.
* The **health probe** is configured correctly.

Then he checks the **load balancing rule** settings and spots the issue:
The **session persistence** is locking traffic from one client to the same VM.

To fix this, David edits the rule and sets **session persistence** to **None**.

---

### **Step 7: Confirming the Fix**

David reloads the browser multiple times. This time, the responses alternate between:

> “Hello from MyVM1”
> “Hello from MyVM2”

Success! The load balancer is now **distributing traffic evenly**, which means users will have a **better experience** with **improved performance and reliability**.

---

### **Business Impact**

Thanks to David’s actions:

* The **web application is scalable and highly available**.
* Traffic is properly balanced across servers, avoiding overload.
* The network is secure, yet functional.

This setup can now handle more traffic as the company expands, with **minimal downtime and better customer satisfaction**.

---

**Key Takeaway**: Understanding how to properly configure **load balancers**, **VNets**, **NAT gateways**, and **session persistence** is essential for any cloud administrator. These tools ensure that traffic flows efficiently, securely, and reliably in cloud-hosted applications.

---
---

### 👨‍💻 **Meet David – The Cloud Hero!**

David is the IT guy at a company that runs a shopping website. One day, his boss, **Sarah**, says,
“David, our website is acting weird. People are getting stuck on the same server. Fix it!”

---

### 🌐 **David Builds a Safe Neighborhood (Virtual Network)**

First, David creates a **virtual network (VNet)** — like building a secure neighborhood for his servers.
He adds **two houses (subnets)**:

* One for **web servers**
* One for a **security gate** called **Azure Bastion**, which lets David visit the servers without opening their front doors (no public IPs!).

---

### 🚪 **David Adds an Internet Door (NAT Gateway)**

To let his servers **go online** (like downloading tools or updates), he sets up a **NAT Gateway**.
Now, the servers can **go out to the internet**, but strangers can’t knock directly on their doors. Smart, right?

---

### ⚖️ **Time to Balance the Crowd (Load Balancer)**

Next, David adds a **load balancer**. Think of it like a doorman at a busy restaurant.
It makes sure visitors don’t crowd one server, but go to whichever is free.
He sets up the doorman to use a **public IP**, watches for healthy servers, and sends visitors to the correct one on **port 80** (the website door).

---

### 🖥️ **David Builds Two Servers (Virtual Machines)**

David creates **two Windows servers** and connects to them securely using **Azure Bastion**.
He installs **IIS (a web server)** and changes the welcome sign:

* One says “Hello from **MyVM1**”
* The other says “Hello from **MyVM2**”

So, now each server can greet visitors differently!

---

### 🔍 **Something’s Off – It Always Shows MyVM1!**

When David visits the website, it always says **MyVM1**. Hmm... strange.
He keeps refreshing. Still the same. Looks like the **load balancer isn’t sharing visitors** properly.

---

### 🕵️ **David Investigates Like a Pro**

He checks:

* **Firewall rules?** ✅ Good
* **Server health?** ✅ Both fine
* **Load balancer settings?** 🤔 Aha!

He finds out the **session persistence** is ON. That means once you visit **MyVM1**, you’re stuck with it.

---

### 🔧 **The Fix – Switch OFF Session Stickiness**

David edits the **load balancing rule** and changes **session persistence** to **None**.
Now, every time someone visits the website, the doorman (load balancer) can pick **either server**, not just the first one.

---

### 🎉 **Victory! Traffic is Shared Perfectly**

David refreshes again. Now it says:

* “Hello from MyVM1”
* “Hello from MyVM2”
* Back to “MyVM1” — it’s **working perfectly!**

---

### 🏆 **Mission Accomplished!**

David saved the day. Now:

* The website works **faster and better**
* Visitors are spread out between servers
* The system is **scalable, reliable, and secure**

Boss Sarah says,
“Great job, David! You’re the load-balancing legend!”

---

### 💡 **Moral of the Story**

If your cloud app isn’t working right, check:

* Your **network settings**
* Your **load balancer rules**
* Use tools like **Azure Bastion**, **NAT Gateway**, and **Virtual Networks** wisely

David did, and now everything runs **smooth as butter** 🧈💻

---
---
## Lab-Based Conceptual MCQs

### 1. Why is it recommended to deploy a **NAT Gateway** alongside a **Virtual Network** in the context of the lab?

(a) To provide DNS name resolution  
(b) To ensure secure SSH access  
(c) To allow outbound internet access for private VMs  
(d) To balance incoming traffic across servers  

**Correct answer: (c)**  
A **NAT Gateway** enables **outbound internet access** from **private subnets** without exposing the virtual machines to inbound connections.

---

### 2. In a production-grade environment, what is the primary benefit of using a **Standard Load Balancer** with a **backend pool**?

(a) It provides DNS-level routing  
(b) It ensures traffic is encrypted end-to-end  
(c) It distributes incoming traffic across healthy VM instances  
(d) It acts as a firewall for the virtual network  

**Correct answer: (c)**  
The **Standard Load Balancer** monitors health probes and **distributes traffic across healthy VMs**, ensuring high availability.

---

### 3. What issue was resolved by changing **session persistence** in the **load balancing rule**?

(a) Multiple users were able to access the VM simultaneously  
(b) All traffic was routed to a single backend VM repeatedly  
(c) Health probes were failing intermittently  
(d) NAT gateway IP was being blocked  

**Correct answer: (b)**  
The **Client IP and protocol** setting was causing sticky sessions, resulting in traffic always hitting the same VM. Setting it to **None** allowed proper distribution.

---

### 4. Why is **Azure Bastion** used to connect to virtual machines in this lab?

(a) It encrypts outbound traffic  
(b) It avoids the need for public IPs on VMs  
(c) It provides automatic scaling  
(d) It acts as a load balancer  

**Correct answer: (b)**  
**Azure Bastion** provides **secure browser-based RDP/SSH** access without exposing the VM via public IP, improving security.

---

### 5. What is the role of a **Health Probe** in a **Load Balancer** configuration?

(a) To detect VM configuration errors  
(b) To monitor VM disk performance  
(c) To determine which backend VMs are healthy  
(d) To initiate automatic backups of VMs  

**Correct answer: (c)**  
A **Health Probe** checks the health of each VM in the **backend pool** and ensures only healthy instances receive traffic.

---

### 6. Why were the **Network Security Group (NSG)** rules modified during VM creation?

(a) To enable DNS zone replication  
(b) To ensure HTTP access was allowed on port 80  
(c) To throttle bandwidth between VMs  
(d) To control outbound traffic only  

**Correct answer: (b)**  
**NSG rules** were created to allow **inbound HTTP traffic on port 80**, enabling web browser access to the IIS page from the internet.

---

### 7. What would happen if the **Backend Pool** was not associated with the **Load Balancer**?

(a) The Load Balancer would route traffic randomly  
(b) VMs would automatically assign themselves to it  
(c) No VM would receive any traffic from the Load Balancer  
(d) The Load Balancer would convert to a NAT Gateway  

**Correct answer: (c)**  
Without a properly configured **backend pool**, the **Load Balancer** has no VMs to forward traffic to, resulting in failure to serve requests.

---

### 8. Which of the following best explains why two VMs were deployed with **IIS** installed?

(a) To simulate web traffic on multiple ports  
(b) To demonstrate DNS zone redundancy  
(c) To enable high availability through load balancing  
(d) To implement geo-replication  

**Correct answer: (c)**  
Deploying multiple **IIS-enabled VMs** allows the **Load Balancer** to distribute traffic, ensuring **high availability and fault tolerance**.

---

### 9. Why was the **default htm file** in IIS replaced with a custom file?

(a) To encrypt HTTP responses  
(b) To visually identify which VM is serving traffic  
(c) To restrict admin access  
(d) To improve browser caching  

**Correct answer: (b)**  
The modified **iisstart.htm** displayed the **computer name**, helping to identify which VM was responding to the request — useful for validating traffic distribution.

---

### 10. If the **frontend IP** of a Load Balancer is unreachable in a browser, what should be checked first?

(a) VM operating system version  
(b) NSG rules and load balancing rules  
(c) Bastion subnet configuration  
(d) DNS records  

**Correct answer: (b)**  
Incorrect **NSG or load balancer rules** may block traffic, especially on port 80 for HTTP, making the **frontend IP unreachable**.

---
---
## Professional Job Interview Questions – AZ-104 Labs

**Note:** These questions are based on real-world scenarios relevant to **Azure Administrator (AZ-104)** certification and are designed to assess conceptual understanding and practical decision-making skills.

---

1. You notice that users are always routed to the same virtual machine behind a load balancer. What configuration should be updated to ensure traffic is evenly distributed?

(a) Increase the number of virtual machines  
(b) Change **Session Persistence** to **None**  
(c) Upgrade the load balancer to premium tier  
(d) Disable health probes

**Correct answer: (b)**  
**Explanation:** Setting **Session Persistence** to **None** ensures that client requests can be routed to different backend VMs, allowing load to be balanced effectively.

---

2. A company needs to route outbound traffic from their private subnet to the internet using a secure and scalable approach. What Azure service should be implemented?

(a) Application Gateway  
(b) Azure Firewall  
(c) **NAT Gateway**  
(d) Load Balancer

**Correct answer: (c)**  
**Explanation:** A **NAT Gateway** allows outbound internet access for resources in a private subnet without exposing them to inbound traffic.

---

3. After deploying a load balancer, traffic isn’t being balanced properly. What is the most likely root cause if VMs respond individually to port 80?

(a) NSG blocking outbound port 80  
(b) VMs not installed  
(c) Health probe misconfigured  
(d) **Session Persistence** is enabled

**Correct answer: (d)**  
**Explanation:** When **Session Persistence** is set to **Client IP and protocol**, the same VM handles repeated requests, which defeats load balancing.

---

4. You need to install IIS on multiple virtual machines deployed behind a load balancer. What is the most efficient way to perform this task?

(a) Use Bastion and install manually on each VM  
(b) Use Azure Run Command  
(c) Use Azure Automation  
(d) **All of the above are valid approaches**

**Correct answer: (d)**  
**Explanation:** All listed methods can be used to install IIS. **Azure Automation** is more scalable for repeated tasks, while **Bastion** and **Run Command** are quicker for fewer instances.

---

5. Which subnet should be associated with a **NAT Gateway** to ensure private VMs have internet access?

(a) AzureBastionSubnet  
(b) Application Gateway Subnet  
(c) **Backend Subnet**  
(d) Frontend Subnet

**Correct answer: (c)**  
**Explanation:** The **Backend Subnet** contains the private virtual machines needing outbound internet, and should be associated with the **NAT Gateway**.

---

6. A developer cannot connect to their VM using RDP through the load balancer. What is the most likely configuration issue?

(a) Public IP not assigned  
(b) RDP port 3389 not open in NSG  
(c) Backend pool misconfigured  
(d) **NSG blocking inbound RDP traffic**

**Correct answer: (d)**  
**Explanation:** If the **Network Security Group (NSG)** blocks inbound RDP, the connection will be denied even if other components are correctly configured.

---

7. Which of the following is true about **Azure Load Balancer** and **Health Probes**?

(a) Health probes are optional  
(b) Probes must use port 443  
(c) **Probes determine the availability of backend VMs**  
(d) Load balancer cannot function without NSG

**Correct answer: (c)**  
**Explanation:** **Health Probes** monitor the status of VMs to ensure that only healthy instances receive traffic.

---

8. You want to access a VM that has no public IP. What is the best method to securely connect?

(a) Enable RDP from all IPs  
(b) Create a jump box with public IP  
(c) **Use Azure Bastion**  
(d) Assign a static IP

**Correct answer: (c)**  
**Explanation:** **Azure Bastion** allows secure and browser-based RDP/SSH connectivity to VMs in private networks without exposing public IPs.

---

9. Which Azure resource ensures that traffic is split across multiple VMs for high availability?

(a) Network Security Group  
(b) Application Gateway  
(c) **Load Balancer**  
(d) NAT Gateway

**Correct answer: (c)**  
**Explanation:** The **Load Balancer** distributes inbound traffic across healthy backend VMs to ensure **high availability** and performance.

---

10. Your virtual machines are not accessible on HTTP despite being healthy. What should you check first?

(a) OS disk size  
(b) **NSG inbound rule for port 80**  
(c) NAT Gateway  
(d) Load balancer rule priority

**Correct answer: (b)**  
**Explanation:** **NSGs** must allow inbound HTTP traffic (port 80) for the VMs to be accessible through a **Load Balancer**.

---
---

🌐 **Meet Alex**, a junior cloud admin at a mid-size tech company. His boss asks him to make sure that the company’s web traffic is properly balanced across two servers. Alex cracks his knuckles and logs into the **Azure portal** – it’s cloud hero time!

---

🏗️ First, Alex builds a **Virtual Network** to allow his resources to talk to each other. He creates two subnets: one for backend servers and one for the **Bastion service** so he can connect securely to the VMs without public IPs.

---

🧱 To manage internet traffic from the servers, Alex sets up a **NAT Gateway** and assigns it to the backend subnet. This lets his VMs make secure outbound connections without exposing them directly to the internet. Smart move, Alex!

---

🚦 Next, Alex creates a **Load Balancer** and configures a **frontend IP**, **backend pool**, and **health probe**. The load balancer is the traffic cop – it decides which server should handle incoming requests. He also sets up a **load balancing rule** using **TCP** on port **80**.

---

🧑‍💻 Time to create some **Virtual Machines**! Alex spins up two Windows servers in the backend subnet. No public IPs here – these machines are safe behind the scenes. He installs **IIS** using **PowerShell** and customizes the web page to show which server is responding.

---

🔁 But wait – all traffic goes to one VM only! That’s odd. Alex digs deeper. He finds the **Session Persistence** setting is making the load balancer stick to one machine. He flips it to **None** so traffic can be shared properly.

---

🎉 Refreshing the site now shows alternating messages from both servers! Success! The **Load Balancer** is working perfectly. Alex wraps it up by deleting all resources – cloud cleanliness is next to cloud godliness.

---

And that’s how Alex went from rookie to rockstar, using **Azure networking tools** like **Virtual Networks**, **NAT Gateways**, **Load Balancers**, and **Virtual Machines** to solve a real-world routing challenge. 🚀

---
---
