# Lab 14: Create and manage a Virtual Machine Scale Set Using Azure CLI

**Duration:** 45m


---
---

### **After logging in with your credentials:**

---

### **Task 1: Launch the Azure Cloud Shell**

1. Click the **Cloud Shell** icon at the top of the Azure Portal.
2. Select **Bash** as the shell environment.
3. Choose **No storage account required**, select the available subscription, and click **Apply**.

---

### **Task 2: Create a Virtual Machine Scale Set**

1. Run the following command to create a **Virtual Machine Scale Set** (VMSS). Replace `<resource group name>` with your actual resource group name:

   ```bash
   az vmss create \
     --resource-group <resource group name> \
     --name myScaleSet \
     --orchestration-mode flexible \
     --image Ubuntu2204 \
     --vm-sku Standard_B2s \
     --admin-username azureuser \
     --generate-ssh-keys \
     --storage-sku Standard_LRS
   ```

2. Verify the VMSS creation by listing virtual machines in the resource group:

   ```bash
   az vm list --resource-group <resource group name> --output table
   ```

---

### **Task 3: Change the Capacity of the Scale Set**

1. Increase the capacity (i.e., number of VM instances) in the scale set:

   ```bash
   az vmss scale --resource-group <resource group name> --name myScaleSet --new-capacity 3
   ```

2. Confirm the updated instance count:

   ```bash
   az vm list --resource-group <resource group name> --output table
   ```

---

### **Task 4: Stop and Deallocate VM Instances**

1. To stop all VM instances in the scale set:

   ```bash
   az vmss stop --resource-group <resource group name> --name myScaleSet
   ```

2. To stop an individual VM (replace `<vm-name>` appropriately):

   ```bash
   az vm stop --resource-group <resource group name> --name <vm-name>
   ```

3. To deallocate a specific VM:

   ```bash
   az vm deallocate --resource-group <resource group name> --name <vm-name>
   ```

---

### **Task 5: Start and Restart VM Instances**

1. To start an individual VM:

   ```bash
   az vm start --resource-group <resource group name> --name <vm-name>
   ```

2. To start all VMs in the scale set:

   ```bash
   az vmss start --resource-group <resource group name> --name myScaleSet
   ```

3. To restart an individual VM:

   ```bash
   az vm restart --resource-group <resource group name> --name <vm-name>
   ```

4. To restart all VMs in the scale set:

   ```bash
   az vmss restart --resource-group <resource group name> --name myScaleSet
   ```

---

### **Final Step**

**Delete all the resources.**

---
---

## **Lab Summary: Create and Manage a Virtual Machine Scale Set Using Azure CLI**

---

### **Purpose of the Lab**

The goal of this lab is to provide hands-on experience with creating and managing a **Virtual Machine Scale Set (VMSS)** using the **Azure CLI** in **Azure Cloud Shell**. Learners will:

* Deploy a VMSS from the command line.
* Adjust the number of VM instances (scale in/out).
* Start, stop, and restart specific or all VMs within the scale set.
* Understand the practical use of CLI in a scalable, real-world infrastructure.

This is ideal for learning **DevOps**, **cloud administration**, or **automation** using Azure.

---

### **Azure Tools and Commands Used**

---

### **1. Azure CLI**

* **Description**: A cross-platform command-line tool for managing Azure resources.
* **Role in Lab**: Primary interface for deploying and controlling all infrastructure.
* **Example**:

  ```bash
  az login
  ```

---

### **2. Azure Cloud Shell**

* **Description**: An in-browser shell environment with **Azure CLI** pre-installed.
* **Role in Lab**: Used to run all CLI commands from within the Azure portal.
* **Access**: Click the **Cloud Shell** icon at the top of the portal and select **Bash**.

---

### **3. Virtual Machine Scale Set (VMSS)**

* **Description**: A group of identical VMs used for load balancing and auto-scaling.
* **Role in Lab**: Main infrastructure deployed and managed via CLI.

---

### **4. `az vmss create`**

* **Description**: Command to create a new **VM Scale Set**.
* **Purpose**: Initializes a new VMSS deployment with given parameters.
* **Example**:

  ```bash
  az vmss create \
    --resource-group myResourceGroup \
    --name myScaleSet \
    --orchestration-mode flexible \
    --image Ubuntu2204 \
    --vm-sku Standard_B2s \
    --admin-username azureuser \
    --generate-ssh-keys \
    --storage-sku Standard_LRS
  ```

---

### **5. `az vm list`**

* **Description**: Lists all virtual machines in a resource group.
* **Purpose**: Verifies that VMs were created successfully within the scale set.
* **Example**:

  ```bash
  az vm list --resource-group myResourceGroup --output table
  ```

---

### **6. `az vmss scale`**

* **Description**: Scales the number of VM instances in a scale set.
* **Purpose**: To dynamically change capacity based on load or cost.
* **Example**:

  ```bash
  az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 3
  ```

---

### **7. `az vmss stop`**

* **Description**: Stops all VM instances in a scale set.
* **Purpose**: Useful for pausing operations and saving compute costs.
* **Example**:

  ```bash
  az vmss stop --resource-group myResourceGroup --name myScaleSet
  ```

---

### **8. `az vm stop`**

* **Description**: Stops a single virtual machine.
* **Purpose**: Isolate or troubleshoot a single instance.
* **Example**:

  ```bash
  az vm stop --resource-group myResourceGroup --name myVM1
  ```

---

### **9. `az vm deallocate`**

* **Description**: Releases VM resources while retaining metadata.
* **Purpose**: Optimizes cost when the VM isn’t needed temporarily.
* **Example**:

  ```bash
  az vm deallocate --resource-group myResourceGroup --name myVM1
  ```

---

### **10. `az vm start`**

* **Description**: Starts a specific virtual machine.
* **Purpose**: Re-activate a previously stopped or deallocated instance.
* **Example**:

  ```bash
  az vm start --resource-group myResourceGroup --name myVM1
  ```

---

### **11. `az vmss start`**

* **Description**: Starts all instances in a VMSS.
* **Purpose**: Resume operations after a pause or shutdown.
* **Example**:

  ```bash
  az vmss start --resource-group myResourceGroup --name myScaleSet
  ```

---

### **12. `az vm restart`**

* **Description**: Restarts a specific VM.
* **Purpose**: Useful for patching or refreshing a single node.
* **Example**:

  ```bash
  az vm restart --resource-group myResourceGroup --name myVM1
  ```

---

### **13. `az vmss restart`**

* **Description**: Restarts all VM instances in a scale set.
* **Purpose**: Helps apply updates across all VMs simultaneously.
* **Example**:

  ```bash
  az vmss restart --resource-group myResourceGroup --name myScaleSet
  ```

---

### **Summary**

This lab provides foundational experience with **Azure VM Scale Sets** using the **Azure CLI**, showing how to:

* Automate large-scale VM deployments.
* Scale infrastructure elastically.
* Manage VM lifecycle operations from the command line.

These practices are essential in modern **cloud engineering**, **DevOps pipelines**, and **cost-effective infrastructure design**.

---
---

## **Scenario: Auto-Scaling for a Startup Web Application Using Azure CLI**

### **Background**

**Evelyn**, a DevOps Engineer at a growing e-commerce startup called **BrightKart**, is tasked with preparing their web backend infrastructure for a seasonal traffic spike. The team wants an **automated, scalable solution** without manual VM provisioning. Evelyn decides to use **Azure Virtual Machine Scale Sets (VMSS)** to deploy and manage multiple virtual machines efficiently.

---

## **Step-by-Step Walkthrough with CLI and Real-World Value**

### **Step 1: Launch Azure Cloud Shell and Set Up**

**Why:** Evelyn prefers **Azure Cloud Shell** because it comes with the **Azure CLI** pre-installed and doesn’t require local setup.

She clicks the **Cloud Shell** icon in the Azure portal, selects **Bash**, and starts the session. Then she sets the correct subscription and ensures it’s ready.

---

### **Step 2: Create a Virtual Machine Scale Set**

**Goal:** Launch an initial set of VMs under a **scale set** to host the application backend.

**CLI Command Example:**

```bash
az vmss create \
  --resource-group BrightKartRG \
  --name WebAppScaleSet \
  --orchestration-mode flexible \
  --image Ubuntu2204 \
  --vm-sku Standard_B2s \
  --admin-username azureadmin \
  --generate-ssh-keys \
  --storage-sku Standard_LRS
```

**Explanation:**
This command creates a **Virtual Machine Scale Set** named **WebAppScaleSet** in the **BrightKartRG** resource group. It uses the **Ubuntu 22.04** image and sets the **VM size** to a lightweight SKU for cost-efficiency. Evelyn uses the `--generate-ssh-keys` flag for secure access.

---

### **Step 3: Verify the Deployed Instances**

**Why:** Evelyn checks whether the VMSS has spun up the instances correctly using:

```bash
az vm list --resource-group BrightKartRG --output table
```

This command lists all virtual machines in a **human-readable format**, confirming successful deployment.

---

### **Step 4: Scale Out the Environment**

As traffic increases during a promotional event, Evelyn needs more backend VMs to handle the load.

**CLI Command Example:**

```bash
az vmss scale \
  --resource-group BrightKartRG \
  --name WebAppScaleSet \
  --new-capacity 3
```

**Result:**
The scale set now has **3 instances**, improving load handling. Azure will automatically spread them across availability zones if needed for **high availability**.

---

### **Step 5: Stop and Deallocate Instances During Low Load**

After the peak event ends, Evelyn wants to pause the VMs overnight to **save costs**.

```bash
az vmss stop \
  --resource-group BrightKartRG \
  --name WebAppScaleSet
```

For individual VM control, she uses:

```bash
az vm stop --resource-group BrightKartRG --name WebAppScaleSet_1
az vm deallocate --resource-group BrightKartRG --name WebAppScaleSet_1
```

These commands help **pause resources** while preserving configuration and metadata.

---

### **Step 6: Resume Operations the Next Day**

Evelyn starts the scale set again in the morning:

```bash
az vmss start --resource-group BrightKartRG --name WebAppScaleSet
```

Or if she wants to bring up just a single VM:

```bash
az vm start --resource-group BrightKartRG --name WebAppScaleSet_1
```

---

### **Step 7: Restart After Applying Updates**

After patching the backend code, Evelyn restarts all VMs in the scale set to ensure a **fresh, consistent state**:

```bash
az vmss restart --resource-group BrightKartRG --name WebAppScaleSet
```

This guarantees that all VMs run the latest codebase without logging into each instance.

---

## **Conclusion: Value Delivered**

Thanks to **Azure VM Scale Sets**, Evelyn was able to:

* **Automate deployment** of multiple VMs with consistent configuration.
* **Scale on-demand** based on traffic spikes.
* **Optimize cost** by stopping and deallocating instances.
* Use **Azure CLI** commands to maintain full control without needing a GUI or extra tools.

This approach saved BrightKart **time**, **money**, and **manual effort**, ensuring reliable performance during their high-demand period.

---
---

### ✅ **Evelyn’s Achievement: A Clean, Efficient Deployment Journey**

**Evelyn**, as the DevOps Engineer for her growing startup **BrightKart**, was given a critical responsibility:
**Prepare a scalable backend infrastructure** for an upcoming seasonal sales spike. The challenge demanded a solution that was **automated**, **cost-effective**, and **responsive to traffic demands** — all without relying on manual interventions.

---

### 🧩 **Her Strategy and Tools**

To meet this challenge, Evelyn smartly chose to use:

* **Azure Virtual Machine Scale Sets (VMSS)** for automatic scaling and uniform VM management
* **Azure CLI** to maintain precise control, using scriptable, repeatable commands in the **Azure Cloud Shell**

---

### 🛠️ **Step-by-Step Summary of What She Did**

1. **Launched Cloud Shell**:
   Without needing to install anything locally, Evelyn used **Azure Cloud Shell with Bash** to get started instantly in a browser-based environment.

2. **Created a VM Scale Set**:
   She deployed a **scale set of Ubuntu virtual machines** using the CLI, specifying all the key configurations like VM size, image, and admin credentials.

3. **Scaled the Set Up**:
   When the event went live, Evelyn quickly **increased the number of instances from 1 to 3** to manage the growing customer demand.
   This gave the backend more capacity **without any service disruption**.

4. **Managed the VMs**:
   After the event, to control costs:

   * She **stopped and deallocated** the VMs during off-hours.
   * Later, she **started them again** as traffic returned.
   * She also used **restart commands** after updates, ensuring all VMs were running fresh and consistently.

5. **Monitored with Precision**:
   Every step was backed by **CLI output checks** to confirm status, scale, and availability.

---

### 🌟 **Why Her Approach Was Successful**

* ✅ **Efficient Use of Resources**: Only the VMs needed at any given time were running.
* ✅ **Automation-Ready**: All commands could be scripted, making this repeatable for future campaigns.
* ✅ **Cost-Aware**: By stopping/deallocating instances, she avoided unnecessary billing.
* ✅ **Business-Aligned**: She delivered exactly what the business needed — a fast, scalable, resilient backend.

---

### 💬 **Final Thoughts**

**Evelyn’s work is a textbook example of modern cloud efficiency**. She used the right tools for the right tasks, stayed aligned with business goals, and minimized manual overhead. Thanks to her thoughtful execution using **Azure CLI** and **Virtual Machine Scale Sets**, BrightKart stayed fully operational and cost-efficient during one of their most crucial periods.

---
---
## Lab-Based Conceptual MCQs

1. **What is the primary benefit of using a Virtual Machine Scale Set (VMSS) in Azure?**
   - (a) It guarantees 100% uptime of all services
   - (b) It enables automatic scaling and simplified VM management
   - (c) It reduces Azure CLI command syntax
   - (d) It removes the need for a resource group
   
   **Correct answer: (b)**  
   *Explanation: VMSS allows for easy scaling and management of a group of identical, load-balanced VMs, helping maintain application performance and availability under varying loads.*

2. **Which Azure CLI command is used to create a Virtual Machine Scale Set?**
   - (a) `az vm create`
   - (b) `az vmss create`
   - (c) `az scale-set create`
   - (d) `az group create`

   **Correct answer: (b)**  
   *Explanation: `az vmss create` is specifically used to deploy a Virtual Machine Scale Set in Azure.*

3. **Why is it recommended to use `--generate-ssh-keys` in the CLI command for VMSS?**
   - (a) To enable Azure backups
   - (b) To auto-generate secure SSH keys for authentication
   - (c) To store passwords in Azure Vault
   - (d) To delete existing VMs

   **Correct answer: (b)**  
   *Explanation: This flag creates SSH keys for secure, password-less authentication, which is a best practice for managing Linux VMs.*

4. **Which CLI command can be used to increase the number of VM instances in a scale set?**
   - (a) `az vmss resize`
   - (b) `az vmss scale`
   - (c) `az vm scale`
   - (d) `az group scale`

   **Correct answer: (b)**  
   *Explanation: `az vmss scale` adjusts the number of VM instances in the scale set, either increasing or decreasing capacity.*

5. **What is the effect of deallocating a VM using the CLI?**
   - (a) It deletes the VM permanently
   - (b) It powers off the VM and releases the compute resources
   - (c) It restarts the VM
   - (d) It converts the VM to a container

   **Correct answer: (b)**  
   *Explanation: Deallocating a VM stops it and releases its compute resources, helping reduce costs.*

6. **How can you start all VMs in a scale set using CLI?**
   - (a) `az vm start-all`
   - (b) `az scale-set boot`
   - (c) `az vmss start`
   - (d) `az group deploy`

   **Correct answer: (c)**  
   *Explanation: `az vmss start` is the correct command to power on all VM instances in a given scale set.*

7. **What command is used to list all VM instances in a resource group?**
   - (a) `az group list`
   - (b) `az vm list`
   - (c) `az vmss show`
   - (d) `az vm instance list`

   **Correct answer: (b)**  
   *Explanation: `az vm list` displays all VM instances in a specified resource group or subscription.*

8. **Which feature of VMSS ensures high availability and fault tolerance?**
   - (a) Nested VMs
   - (b) Load balancers only
   - (c) Distribution across fault and update domains
   - (d) Reserved IPs

   **Correct answer: (c)**  
   *Explanation: VMSS uses fault domains and update domains to ensure high availability during hardware or software failures.*

9. **What must be provided when using `az vmss create` to authenticate with the VMs?**
   - (a) A VM image
   - (b) A firewall rule
   - (c) An admin username and SSH key or password
   - (d) A static public IP

   **Correct answer: (c)**  
   *Explanation: VMSS requires user credentials (SSH key or password) for secure login during deployment.*

10. **When would restarting VM instances in a scale set be necessary?**
    - (a) After resizing the scale set capacity
    - (b) After applying system updates or configuration changes
    - (c) After deleting the resource group
    - (d) Before creating a new VMSS

    **Correct answer: (b)**  
    *Explanation: Restarting helps apply new updates or settings and ensures VM instances function as expected post-configuration.*
---
