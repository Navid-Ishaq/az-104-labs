# Lab 17: Creating an Application Gateway

**Duration:** 1h 0m

---
---

**After logging in with your credentials:**

### **Step 1: Create a Virtual Network**

1. Navigate to **Create a resource**.
2. Search for and select **Virtual Network**.
3. In the **Basics** tab:

   * Choose the appropriate **resource group**.
   * Set the **Virtual Network Name** to `vnet1`.
   * Select **East US** for the region.
4. Proceed to the **IP Addresses** tab:

   * Set the **IPv4 address space** to `10.1.0.0/16`.
5. Remove the **default subnet**.
6. Add a new subnet:

   * Name: `myBackendPool`
   * Address range: `10.1.0.0/24`
7. Add another subnet:

   * Name: `myApplicationGatewaySubnet`
   * Address range: `10.1.1.0/24`
8. Click **Review + Create**, then **Create**.

---

### **Step 2: Create Two Virtual Machines**

Repeat the following steps to create **two** virtual machines (VM1 and VM2):

1. Go to **Virtual Machines** and click **+ Create**.
2. In the **Basics** tab:

   * Select the resource group.
   * Set the VM name (e.g., `vm1`, then `vm2`).
   * Region: **East US**
   * Image: **Windows Server 2019 Datacenter - Gen1**
   * Size: **Standard\_B2s**
   * Username: Choose a valid name (e.g., `vm1`)
   * Password: Set and confirm
   * Public inbound ports: Select **HTTP (80)** and **RDP (3389)**
3. In the **Disks** tab:

   * Choose **Standard SSD**
4. In the **Networking** tab:

   * Choose **vnet1**
   * Subnet: **myBackendPool**
5. In the **Monitoring** tab:

   * Disable **Boot diagnostics**
6. Click **Review + Create**, then **Create**

---

### **Step 3: Install IIS and Configure Content**

Perform the following steps for **both** VMs using **RDP**:

1. Connect to the VM using RDP.
2. Launch **Server Manager**, then choose **Add Roles and Features**.
3. Install the **Web Server (IIS)** role.
4. Open a browser inside the VM and verify IIS by visiting `http://localhost/`.
5. Navigate to `C:\inetpub\wwwroot`.
6. Create a new folder:

   * For VM1: `images`
   * For VM2: `videos`
7. Inside each folder, create a file named `Default.html`.
8. Paste the following content as appropriate:

   * VM1:

     ```html
     <h1>This is the Images Server</h1>
     ```
   * VM2:

     ```html
     <h1>This is the Videos Server</h1>
     ```

---

### **Step 4: Create an Application Gateway**

1. Search for and select **Application Gateway**.
2. Click **+ Create** and fill out the **Basics**:

   * Name: `AppGateway`
   * Tier: **Standard V2**
   * Region: **East US**
   * Virtual Network: `vnet1`
   * Subnet: `myApplicationGatewaySubnet`
   * Max instance count: 2
3. In the **Frontends** tab:

   * Choose **Public**
   * Add a new public IP: Name it `AppGatewayIP`
4. In the **Backends** tab:

   * Add a backend pool `imagepool` with VM1
   * Add a backend pool `videopool` with VM2
5. In the **Configuration** tab:

   * Add a routing rule:

     * Rule name: `RuleA`
     * Listener:

       * Name: `ListenerA`
       * Frontend IP: Public
       * Protocol: HTTP
       * Port: 80
     * Backend settings:

       * Name: `SettingA`
       * Protocol: HTTP
       * Port: 80
     * Path-based routing:

       * `/images/` → `imagepool`
       * `/videos/` → `videopool`
6. Skip **Tags**, review settings, and click **Create**

---

### **Step 5: Test the Application Gateway**

1. Go to the **Application Gateway** you created.
2. Copy the **public IP address**.
3. In a browser:

   * Visit: `http://<public_ip>/images/Default.html`
     → You should see the **Images Server** message.
   * Visit: `http://<public_ip>/videos/Default.html`
     → You should see the **Videos Server** message.

---

**Delete all the resources.**

---
---

## **Lab Summary: Creating an Application Gateway**

### **Purpose of the Lab**

The purpose of this lab is to help learners understand how to configure an **Azure Application Gateway**, which is a load balancing and traffic routing solution for web applications. This lab demonstrates how to:

* Set up a **virtual network (VNet)** with appropriate subnets.
* Create **virtual machines (VMs)** to simulate backend servers.
* Install **IIS web servers** on VMs to serve web content.
* Configure an **Application Gateway** to distribute HTTP traffic based on **URL path-based routing**.
* Verify connectivity and load balancing by testing the setup through a browser.

This is a practical exercise commonly performed by **Azure administrators** and **cloud engineers** to implement scalable, secure, and efficient web application delivery.

---

## **Azure Tools and Services Used**

### 1. **Virtual Network (VNet)**

* **Description**: A logically isolated network in Azure where resources like virtual machines and application gateways are deployed.
* **Role in Lab**: Acts as the foundational network structure connecting all components. Subnets are used to isolate application services.
* **Example**: The VNet named `vnet1` includes two subnets: `myBackendPool` for VMs and `myApplicationGatewaySubnet` for the gateway.

---

### 2. **Subnets**

* **Description**: Sub-segments within a VNet to logically separate workloads.
* **Role in Lab**: Segregates backend VMs and the Application Gateway for network management and security.
* **Example**:

  * `myBackendPool` — hosts two virtual machines.
  * `myApplicationGatewaySubnet` — reserved for the Application Gateway.

---

### 3. **Virtual Machines (VMs)**

* **Description**: Scalable computing resources that run Windows or Linux operating systems.
* **Role in Lab**: Hosts the **IIS web servers** that serve as backend targets for the Application Gateway.
* **Example**: `vm1` hosts image content, and `vm2` hosts video content.

---

### 4. **Internet Information Services (IIS)**

* **Description**: A Windows-based web server used to host and serve web pages.
* **Role in Lab**: Provides a simple test web page (`Default.html`) to validate routing.
* **Example**: On `vm1`, the file displays “**This is the Images Server**”; on `vm2`, it displays “**This is the Videos Server**”.

---

### 5. **Application Gateway**

* **Description**: A web traffic load balancer that enables application-level routing and features like SSL offloading, URL-based routing, and web application firewall integration.
* **Role in Lab**: Routes HTTP requests based on the request path to the appropriate backend pool (i.e., image or video servers).
* **Example**:

  * Requests to `/images/` are routed to `imagepool` (vm1).
  * Requests to `/videos/` are routed to `videopool` (vm2).

---

### 6. **Backend Pools**

* **Description**: A collection of backend servers that receive traffic from the Application Gateway.
* **Role in Lab**: Define which VM receives which type of traffic.
* **Example**:

  * `imagepool` → `vm1`
  * `videopool` → `vm2`

---

### 7. **Routing Rules and Path-Based Routing**

* **Description**: Rules that determine how the Application Gateway routes incoming traffic.
* **Role in Lab**: Enables the Application Gateway to inspect URL paths and direct traffic accordingly.
* **Example**:

  * `/images/Default.html` → goes to image server.
  * `/videos/Default.html` → goes to video server.

---

### 8. **Public IP Address**

* **Description**: An address that enables access to Azure resources over the internet.
* **Role in Lab**: Used by external users to access the Application Gateway and test its routing rules.
* **Example**: Accessed in a browser as `http://<public_ip>/images/Default.html`.

---

## **Conclusion**

By completing this lab, learners gain hands-on experience in:

* Structuring networks using **VNets** and **subnets**.
* Hosting and serving content with **virtual machines**.
* Configuring an **Application Gateway** to route traffic efficiently.
* Demonstrating **path-based routing**, a key feature in managing modern web applications.

These tasks are crucial for professionals preparing for roles in **cloud infrastructure**, **web hosting**, and **application delivery optimization**.

---
---

## **Scenario: Deploying an Application Gateway for a Media Company**

### **Background**

David is a **Cloud Administrator** at **StreamEdge Media**, a growing company that provides multimedia content online. Their website serves two categories of users: those who want to browse **images** and those who want to watch **videos**.

To improve **scalability**, **performance**, and **security**, David has been asked to deploy an **Azure Application Gateway** with **path-based routing**. This will allow requests for **images** and **videos** to be intelligently routed to different **backend servers**.

---

## **Step-by-Step Execution with Real-World Context**

### **Step 1: Set Up the Network Infrastructure**

David starts by creating a **Virtual Network (VNet)** called `whizNet1` in the **East US** region. This **VNet** includes two **subnets**:

* **myBackendPool** — This subnet will host the **virtual machines** (VMs) that serve image and video content.
* **myApplicationGatewaySubnet** — This subnet is reserved for the **Application Gateway** itself.

This **network segmentation** ensures security and proper routing within the environment.

> **Example**: The **IP address space** used is `10.1.0.0/16`, and each subnet is assigned its own `/24` block.

---

### **Step 2: Create Virtual Machines for Content Hosting**

David then creates two **Windows Server 2019** VMs:

* **myWhizlabsVM1** (user: `vm1`) – will serve image content.
* **myWhizlabsVM2** (user: `vm2`) – will serve video content.

Both are placed in the **myBackendPool** subnet and allow **HTTP (80)** and **RDP (3389)** traffic to enable both content serving and remote administration.

He chooses the **Standard\_B2s** VM size and uses **Standard SSD** as the disk type to keep costs low while meeting performance needs.

---

### **Step 3: Install IIS and Create Web Content**

Using **Remote Desktop Protocol (RDP)**, David logs into each VM and installs **Internet Information Services (IIS)** to enable web serving capabilities.

* On **VM1**, he navigates to `C:\inetpub\wwwroot\images\` and creates a `Default.html` file with the content:

  ```html
  <h1>This is the Images Server</h1>
  ```

* On **VM2**, he does the same under the `videos` folder with:

  ```html
  <h1>This is the Videos Server</h1>
  ```

This step simulates how each server will serve content based on user intent — one for images, one for videos.

---

### **Step 4: Deploy the Application Gateway**

Now that the backend servers are ready, David creates an **Azure Application Gateway** named `WhizlabsGateway` (placed in the `myApplicationGatewaySubnet`). It uses the **Standard V2** tier and supports **path-based routing**.

He attaches a **public IP address** named `WhizlabsGatewayIP`, allowing users to access the gateway from the internet.

---

### **Step 5: Configure Backend Pools and Routing Rules**

David defines two **backend pools**:

* **imagepool** → linked to `myWhizlabsVM1`
* **videopool** → linked to `myWhizlabsVM2`

He then sets up a **routing rule** named `RuleA` using **path-based routing**:

* Requests to `/images/*` go to the **imagepool**
* Requests to `/videos/*` go to the **videopool**

Each rule uses **HTTP** on port **80** and relies on a **Backend HTTP setting** called `SettingA`.

This setup ensures traffic is routed intelligently without needing separate load balancers.

---

### **Step 6: Test the Application Gateway**

After deployment, David copies the **public IP** of the **Application Gateway** and performs two tests:

1. **http\://\<gateway\_ip>/images/Default.html**
   ✅ Displays: *"This is the Images Server"*

2. **http\://\<gateway\_ip>/videos/Default.html**
   ✅ Displays: *"This is the Videos Server"*

The routing works perfectly, confirming that the **Application Gateway** is correctly directing traffic.

---

## **Business Value and Justification**

By completing this setup, David has achieved the following for StreamEdge Media:

* **Centralized traffic control** using **Application Gateway**
* **Improved scalability** via multiple backend pools
* **Seamless user experience** using **path-based routing**
* **Reduced cost and complexity**, avoiding the need for third-party load balancers
* **Security best practices** through subnet isolation and minimal port exposure

This solution is now ready for production use or further scaling using **autoscaling** or **integration with Azure Web Application Firewall (WAF)**.

---

## **Summary of Key Concepts Used**

* **Virtual Network (VNet)** – Logical isolation for Azure resources
* **Subnet** – Used to separate backend servers and gateway
* **Virtual Machine (VM)** – Hosts web content (IIS)
* **IIS (Internet Information Services)** – Web server for Windows
* **Application Gateway** – Layer 7 load balancer with URL path routing
* **Public IP Address** – Used for external access
* **Backend Pool** – Group of backend servers
* **Path-Based Routing** – Routes based on URL paths like `/images/` and `/videos/`

---
---

## ✅ Did David Complete His Job Efficiently?

**Yes, David completed his job efficiently and professionally.**
Let’s break it down in a way that's easy to understand for anyone — even with no technical background.

---

## 🧠 Who is David?

David is a **Cloud Administrator** working for a media company. His job is to make sure that the company’s website runs smoothly, quickly, and securely. He was asked to set up a system where users can:

* View **images** on one part of the site
* Watch **videos** on another part

And all of this should happen in a **safe**, **organized**, and **fast** way.

---

## 📋 What Was David Asked to Do?

His goal was to:

1. Set up **two servers** – one for images, one for videos
2. Build a **gateway** that routes people to the right server
3. Make sure it's secure and easy to access

This helps the company handle more users, avoid confusion, and reduce the chance of website problems.

---

## 🛠️ What Did David Do (In Simple Steps)?

| Step | What David Did                               | Why It Was Important                                                                    |
| ---- | -------------------------------------------- | --------------------------------------------------------------------------------------- |
| 1️⃣  | Created a **virtual network**                | So all parts can talk to each other privately and securely                              |
| 2️⃣  | Set up **two virtual machines (servers)**    | One for image content, one for video content                                            |
| 3️⃣  | Installed **IIS (a web server)** on both     | To let each server show content on the website                                          |
| 4️⃣  | Added **custom web pages** to each server    | So users can see either images or videos                                                |
| 5️⃣  | Built an **Application Gateway**             | This acts like a traffic manager, deciding where each visitor should go                 |
| 6️⃣  | Set up **routing rules**                     | So requests to `/images/` go to the image server, and `/videos/` go to the video server |
| 7️⃣  | **Tested everything** to make sure it worked | Confirmed that the gateway is doing its job correctly                                   |

---

## 🎯 What Was the Outcome?

* Users can now **easily view images or videos**, without confusion
* The traffic is **well-managed** and goes to the right place
* The company’s website is **faster and more reliable**
* It’s **scalable** — more users can be added in the future
* Everything is done in a **cost-effective** and **secure** way

---

## 🌟 Final Verdict

✅ **Yes, David completed his job efficiently.**
He followed best practices, avoided mistakes, and created a solution that is reliable and ready for real users. He saved time, effort, and future problems by doing the job right from the beginning.

---
---
## Lab-Based Conceptual MCQs

**Note:** All keywords are consistently formatted in **bold**.

1. **Why is an Application Gateway preferred over a traditional Load Balancer for web traffic routing in Azure?**
   - (a) It supports DNS resolution only
   - (b) It allows SSL offloading and path-based routing
   - (c) It provides direct VM access
   - (d) It replaces Azure Firewall  
   **Correct answer: (b)**  
   **Explanation:** **Application Gateway** supports advanced features such as **SSL termination**, **path-based routing**, and **cookie-based session affinity**, making it more suitable for web applications.

2. **What is the purpose of defining multiple subnets in the same virtual network during Application Gateway setup?**
   - (a) To isolate VM instances by OS type
   - (b) To allow frontend and backend separation
   - (c) To support higher storage capacity
   - (d) To enable zone redundancy  
   **Correct answer: (b)**  
   **Explanation:** Defining **separate subnets** allows clear separation between the **Application Gateway** and **backend VMs**, supporting better **security** and **traffic control**.

3. **What is the function of a backend pool in an Azure Application Gateway?**
   - (a) It stores monitoring logs
   - (b) It serves as the outbound rule processor
   - (c) It defines the list of backend targets for routing
   - (d) It acts as a backup recovery unit  
   **Correct answer: (c)**  
   **Explanation:** The **backend pool** contains the **VMs or IPs** where the **Application Gateway** routes incoming traffic based on the defined rules.

4. **Why is installing IIS on the backend VMs necessary in this lab?**
   - (a) To install network drivers
   - (b) To host a simple web server for testing
   - (c) To activate RDP access
   - (d) To enable Azure Site Recovery  
   **Correct answer: (b)**  
   **Explanation:** **IIS (Internet Information Services)** is used to provide a **web interface** so that the Application Gateway can route traffic and display content.

5. **What is the significance of the custom HTML files placed under `wwwroot` in the lab?**
   - (a) They store security policies
   - (b) They define routing weights
   - (c) They display different backend content
   - (d) They monitor Azure health  
   **Correct answer: (c)**  
   **Explanation:** The **custom HTML files** represent **unique responses** (e.g., "Images Server" and "Videos Server") to confirm proper routing through the Application Gateway.

6. **What happens when a request is made to `/videos/Default.html` via the Application Gateway?**
   - (a) It is blocked by NSG rules
   - (b) It redirects to the image VM
   - (c) It is routed to the VM in the video backend pool
   - (d) It triggers autoscaling  
   **Correct answer: (c)**  
   **Explanation:** The **routing rule** configured in the Application Gateway **matches the path** and forwards it to the **correct VM** in the `videopool`.

7. **Why is a public IP address configured on the Application Gateway?**
   - (a) To enable DNS-based routing
   - (b) To allow internet users to access the gateway
   - (c) To perform health probes
   - (d) To update VM NICs  
   **Correct answer: (b)**  
   **Explanation:** The **public IP** provides a **frontend endpoint** for users to access services hosted behind the **Application Gateway**.

8. **What advantage does path-based routing provide in this architecture?**
   - (a) Increases virtual machine performance
   - (b) Enables different content to be served from one IP
   - (c) Assigns IPs dynamically
   - (d) Creates NAT rules automatically  
   **Correct answer: (b)**  
   **Explanation:** **Path-based routing** allows the same **public IP** to handle different traffic types (like `/images/` and `/videos/`) by directing them to the right backend.

9. **Which of the following is required to complete the Application Gateway configuration?**
   - (a) Route Table Association
   - (b) NAT Gateway setup
   - (c) A listener with HTTP settings
   - (d) Network Watcher agent installation  
   **Correct answer: (c)**  
   **Explanation:** A **listener** and **backend HTTP settings** are critical parts of the **Application Gateway rule** setup to define how traffic is handled.

10. **How does Azure ensure that traffic routing in this lab remains secure and isolated?**
    - (a) By using IP whitelisting
    - (b) Through NSG and subnet segmentation
    - (c) Using local admin credentials
    - (d) Enabling root access  
    **Correct answer: (b)**  
    **Explanation:** **Network Security Groups (NSGs)** and **separate subnets** for gateway and backend VMs help enforce **traffic control and isolation**.

---
---
## Professional Job Interview Questions – AZ-104 Labs

### 1. A company wants to host a high-availability web application using an **Application Gateway** with two backend VMs in different subnets. What is the primary reason for using **path-based routing** in this scenario?

(a) To reduce storage costs on virtual machines  
(b) To route traffic to specific VMs based on the URL path  
(c) To increase database performance  
(d) To implement Azure AD authentication  

**Correct answer: (b)**  
Path-based routing allows traffic to be directed to different backend pools depending on the URL path (e.g., `/images/` to one VM, `/videos/` to another), enabling better application design and resource use.

---

### 2. An administrator sets up an **Application Gateway** with two backend pools. Users report they're seeing incorrect pages when browsing. Which configuration should the admin verify?

(a) Inbound NAT rules in NSG  
(b) Public IP assignment on VM  
(c) Routing rules and path match settings  
(d) Disk type of backend VMs  

**Correct answer: (c)**  
Incorrect or missing routing rules can lead to misdirected traffic. The admin should verify that the correct paths (like `/images/`, `/videos/`) are properly mapped to the appropriate backend pools.

---

### 3. A team wants to ensure their **Application Gateway** doesn't overload backend VMs during high traffic. What built-in feature should they configure?

(a) Static Public IP  
(b) Auto-scaling for Application Gateway  
(c) Azure DNS  
(d) Storage replication  

**Correct answer: (b)**  
Application Gateway Standard v2 supports auto-scaling, which adjusts the number of instances based on traffic load, improving performance and reliability.

---

### 4. You’re tasked with isolating the **Application Gateway subnet** from other components in the **Virtual Network**. What’s a mandatory design rule for deploying the gateway?

(a) Deploy the gateway in the same subnet as VMs  
(b) Use a different region  
(c) Place the gateway in a dedicated subnet  
(d) Enable hybrid connections  

**Correct answer: (c)**  
An Application Gateway requires its own dedicated subnet that cannot be shared with other Azure resources.

---

### 5. During setup, an engineer skips assigning a **public frontend IP** to the **Application Gateway**. What’s the consequence?

(a) The gateway can only serve traffic on HTTPS  
(b) The gateway won’t be reachable from the internet  
(c) The gateway will be deleted  
(d) NSG rules won’t apply  

**Correct answer: (b)**  
Without a public frontend IP, the Application Gateway cannot accept traffic from the internet, which defeats the purpose of using it for external access.

---

### 6. A company needs each VM to serve different content. They want `/images/` to be handled by **VM1** and `/videos/` by **VM2**. Which Azure component enables this?

(a) Availability Set  
(b) Network Security Group  
(c) Application Gateway with path-based routing  
(d) Azure Load Balancer  

**Correct answer: (c)**  
The Application Gateway supports path-based routing, which allows traffic to be directed to specific backend pools based on URL paths.

---

### 7. What must be configured on the backend VMs to confirm **HTTP requests** are properly processed after **IIS installation**?

(a) NSG rules to deny port 80  
(b) Adding storage firewall rules  
(c) Checking IIS with http://localhost  
(d) Attaching a managed identity  

**Correct answer: (c)**  
Verifying that IIS responds locally using `http://localhost` confirms the web server is running properly on the backend VM.

---

### 8. You’ve created an **Application Gateway** but traffic isn't routing as expected. What’s the most likely misconfiguration?

(a) Resource group name  
(b) VM image type  
(c) Routing rule or path pattern  
(d) Storage account region  

**Correct answer: (c)**  
Routing and path configurations are essential. A misconfigured path (e.g., missing `/images/`) or target pool will prevent proper routing.

---

### 9. A user wants to test access to the application using the public IP assigned to the **Application Gateway**. Which format is correct?

(a) gateway_ip:8080  
(b) gateway_ip/index.html  
(c) gateway_ip/videos/Default.html  
(d) gateway_ip/virtual_machine_name  

**Correct answer: (c)**  
This format matches the path-based routing setup where `/videos/Default.html` routes traffic to the appropriate backend VM serving video content.

---

### 10. When deploying the two backend **Virtual Machines**, why is it important to disable **Boot Diagnostics**?

(a) It reduces storage billing and simplifies lab environments  
(b) It increases performance for web applications  
(c) It enables faster DNS resolution  
(d) It’s required to allow HTTP traffic  

**Correct answer: (a)**  
Disabling Boot Diagnostics avoids creating additional storage accounts, which is especially useful in controlled or cost-sensitive environments like labs.

---
---

### ☁️ Meet David, the Cloud Hero!

David works at a small video company. His boss says, “David, we need a smart way to show videos and images to users online… and it better be fast!” David smiles. “No problem! I’ll build something awesome using **cloud tools**!”

---

### 🛠️ Step 1: Build the Neighborhood (Virtual Network)

First, David creates a **Virtual Network (VNet)**. Think of this like building roads and spaces where his web servers (computers) will live. He makes two **subnets** — one for servers and one just for the **Application Gateway**. Good planning, right?

---

### 🧱 Step 2: Bring in the Workers (Virtual Machines)

David then adds two **Virtual Machines (VMs)** — one to show **images**, another to show **videos**. These are like two shops on the same street. He also installs **IIS (web server software)** on both VMs so they can show websites.

---

### 🏗️ Step 3: Build the Gate (Application Gateway)

Now, David builds an **Application Gateway**. Think of it as a smart security gate that checks incoming visitors and sends them to the right VM — images go to the **Image Server**, and videos to the **Video Server**. The gate watches traffic and handles it smoothly.

---

### 🔀 Step 4: Create Smart Routes

David tells the **Application Gateway**, “If someone visits `/images`, send them to the first server. If they go to `/videos`, send them to the second one.” These are called **routing rules**, and they help send visitors exactly where they need to go.

---

### 🌐 Step 5: Test It All Out

David grabs the **public IP** of the gateway, puts it in his browser with `/images/Default.html` — bam! It shows the image page. Then he tries `/videos/Default.html` — awesome, the video page works too!

---

### 🧹 Final Step: Clean Up

After showing his boss the setup, David deletes all the **cloud resources** to save money. “Job done!” he says, sipping his coffee.

---

### 🌟 The End (But the Learning Begins!)

David used **Virtual Network**, **Virtual Machines**, **Application Gateway**, and **routing rules** to solve a real business need. It’s like putting traffic signs and buildings in the cloud — smart, fast, and flexible!

---
---
