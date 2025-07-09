# Lab 2: Working with resource tags


---
---

### 🚀 Azure Lab – Organizing Resources with Tags

**After logging in with your credentials:**

---

### **Task 1: Create a Virtual Machine**

1. In the Azure Portal, go to **Virtual Machines**.
2. Click **+ Create** > **Azure Virtual Machine**.
3. In the **Basics** tab, enter the following:

   * **Resource Group**: Select or create one (e.g., `rg-labresources`)
   * **VM Name**: `resizeVM`
   * **Region**: `East US`
   * **Availability options**: `No infrastructure redundancy required`
   * **Security type**: `Standard`
   * **Image**: `Windows Server 2019 Datacenter - x64 Gen2`
   * **Size**: Click **See all sizes**, select `B1s`, click **Select**
   * **Username**: `LabUser`
   * **Password**: `StrongPassword@123`
4. Leave **Azure Spot Instance** unchecked.
5. Leave **Public inbound ports** as default.
6. Go to the **Disks** tab and select:

   * **OS Disk Type**: `Standard SSD`
7. Click **Review + Create**, then click **Create**.

---

### **Task 2: Apply Tags to the Virtual Machine**

1. In the **Azure Portal**, go to **Resource Groups**.
2. Open your resource group (e.g., `rg-labresources`).
3. Click on the **resizeVM** virtual machine.
4. In the left panel, select **Tags** under Settings.
5. Add a tag with:

   * **Name**: `Department`
   * **Value**: `IT`
6. Click **Apply**.

---

### **Task 3: Filter Resources by Tag**

1. Go to **Resource Groups** again from the Azure menu.
2. Select your resource group.
3. Click **Add filters** on the toolbar.
4. Select the tag **Department**, choose the value `IT`, then click **Apply**.
5. You should now see all resources tagged as `Department = IT`.

---

**Delete all the resources.**

---
---
---
## **📘 Azure Lab Summary: Organizing Azure Resources Using Tags**

---

### **🎯 Purpose of the Lab**

The objective of this lab is to demonstrate how to effectively organize and manage Azure resources using **resource tags**. Through the deployment of a virtual machine and the application of tags at the resource level, this lab teaches how tagging enhances **resource categorization**, **cost tracking**, and **administrative control**. It also shows how to **filter and locate** resources based on tag values, a key skill for managing large-scale environments efficiently.

---

### **🛠 Azure Tools and Services Used**

#### 1. **Azure Portal**

* **Description**: A web-based interface to create, manage, and monitor Azure services.
* **Role in the Lab**: Used to create the virtual machine, apply tags, and perform filtering actions — the central interface for completing all tasks.

#### 2. **Virtual Machine (VM)**

* **Description**: A scalable compute resource that allows you to run applications and services on a virtualized server.
* **Role in the Lab**: Serves as the main resource to which tags are applied. Demonstrates how to organize and manage compute resources with metadata.

#### 3. **Resource Group**

* **Description**: A container in Azure that holds related resources for a solution.
* **Role in the Lab**: Hosts the virtual machine and provides a scope for managing the VM and its tags. Tag filtering is demonstrated within the resource group context.

#### 4. **Resource Tags**

* **Description**: Key-value pairs assigned to Azure resources for metadata organization (e.g., `Department: IT`).
* **Role in the Lab**: Central to the lab objective. Tags are applied to the VM and later used to **filter resources** in the portal, helping with organization, automation, and cost management.

#### 5. **Tag-Based Filtering**

* **Description**: A search and filter capability within the Azure Portal to locate resources based on specific tag values.
* **Role in the Lab**: Used to demonstrate how tags enable efficient resource discovery and management when dealing with multiple assets.

---

### **🔑 Real-World Relevance**

Tagging is widely used in production environments to:

* Track **costs per department or project**,
* Enforce **governance policies**,
* Automate resource management via **Azure Policy** or **scripts**.

Mastering tagging and resource filtering is essential for **Azure Administrators**, **Cloud Architects**, and **DevOps Engineers** who manage complex cloud infrastructures.

---
---
---
Here's a **practical and professional story** that brings the **Azure resource tagging lab** to life through a relatable real-world scenario:

---

## **🏢 Scenario: Managing Departmental Cloud Costs in a Growing Tech Company**

**Meet Imran**, a cloud operations engineer at **CloudSmart Solutions**, a growing SaaS company offering business intelligence tools to multiple clients. As the organization scales, multiple departments—**IT, HR, Marketing, and Development**—are requesting new virtual machines in Azure for running demos, analytics jobs, and internal tools.

After several months, leadership starts noticing unpredictable spikes in the monthly Azure billing. When asked which departments are consuming the most cloud resources, Imran realizes that there's **no clear way to categorize or filter resources** based on ownership or purpose.

To solve this issue, Imran decides to implement a **resource tagging strategy** using Azure’s native features. He begins by deploying a new **Windows Server 2019 virtual machine**, and then attaches a **tag** to identify the department using the resource. This helps align usage with cost accountability.

---

### **🔧 Step-by-Step: What Imran Does and Why**

---

### **1. Deploying the Virtual Machine**

Imran logs into the **Azure Portal** and navigates to **Virtual Machines**. He clicks **+ Create** to provision a new VM named `resizeVM`, selecting **Windows Server 2019 Datacenter** as the image. He places it under the resource group `rg-labresources`, located in the **East US** region.

* He sets a **Standard B1s size** to minimize cost.
* Enters credentials to allow secure remote access.
* Chooses **Standard SSD** for the OS disk to balance performance and cost.

🧠 **Why it matters**: This VM will be used for an internal IT tool, so tagging it now will make it easier to trace usage and allocate costs later.

---

### **2. Applying Tags to the VM**

After deployment, Imran opens the VM settings and navigates to the **Tags** section. He creates a tag:

* **Name**: `Department`
* **Value**: `IT`

✅ **Impact**: Now this resource is clearly marked as owned by the IT department. In billing reports or dashboards, it will show up under that tag.

---

### **3. Filtering Resources by Tag**

To demonstrate the power of tagging, Imran goes back to the **Resource Groups** section in the Azure Portal, selects `rg-labresources`, and clicks **Add Filters**. He filters by the tag `Department = IT`.

🔍 He now sees a filtered list of resources used by the IT team only — perfect for:

* Reviewing assets,
* Estimating departmental cost impact,
* Reporting to management.

---

### **📈 Business Impact**

Thanks to tagging:

* **Finance** can now generate more accurate departmental billing.
* **Operations** can identify unused or over-provisioned resources.
* **Governance** is easier to enforce — automation tools like Azure Policy can use these tags to control access, apply policies, or trigger alerts.

What started as a small VM deployment is now part of a **larger resource management strategy** that supports transparency, accountability, and better cloud cost control across the business.

---

**Delete all the resources.**

---
---
---
## Comic-Style Summary: **“Tag It Before You Drag It!”**

👨‍💻 **Meet Imran**, a sharp cloud engineer working at **CloudSmart Solutions**. His company is growing fast, and different departments—like **IT, Marketing, and HR**—are creating lots of **virtual machines** in the cloud. But soon, **the Azure bill starts looking like a mystery novel**—no one knows who’s spending what!

---

### 💻 Step 1: Creating the Virtual Machine

Imran logs into the **Azure Portal**, clicks **+ Create**, and spins up a **Windows Server 2019 VM**.
He names it **resizeVM**, places it in the **East US** region, and uses a **Standard B1s size** to save money.
For the disk, he picks **Standard SSD**—fast enough, but still affordable.

✅ **Why?** This VM is for the **IT department** to test internal tools. But without labels, it would be lost in a sea of unnamed resources!

---

### 🏷️ Step 2: Adding a Tag to the VM

Once the VM is running, Imran goes into the **Tags** section. He creates a tag:

* **Name**: `Department`
* **Value**: `IT`

✅ **Why?** With this tag, anyone can now see that this VM belongs to the **IT team**. It's like putting a sticky note saying: *“Hey, this is ours!”*

---

### 🔍 Step 3: Filtering Resources by Tag

Imran goes back to the **Resource Groups** and filters all resources where **Department = IT**.
Boom 💥 — he gets a clean list of only IT-owned assets. No more guessing!

✅ **Now**:

* Finance can **see who’s using what** and bill them.
* IT can **track costs** and plan better.
* Automation tools can even use tags to apply **rules or alerts**.

---

### 📊 Business Win!

By doing something as simple as **adding a tag**, Imran helped his company:

* Get **clarity** on spending,
* Improve **governance**,
* And reduce **wasted resources**.

What started as just creating a VM turned into a **smart cost-management solution**.
**Tagging isn’t just neat—it’s powerful!**

---

### 🧼 Final Step

Imran cleans up the lab environment by **deleting all the resources**, keeping the Azure playground tidy and ready for the next big challenge.

🎉 **Mission accomplished, Imran! Cloud chaos turned into cloud control.**

---
---
---

## 🧠 Lab-Based MCQs: Azure Resource Tagging (Exam-Style)

---

### 1. What is the primary benefit of using tags in Azure?

**(a)** Encrypt virtual machines  
**(b)** Set RBAC permissions  
**(c)** Organize resources for cost management and filtering  
**(d)** Prevent accidental deletion of resources  

**✅ Correct answer: (c)**  
**Explanation**: Tags are used to logically group and organize Azure resources. They help with cost tracking, automation, filtering, and reporting.

---

### 2. You’ve applied a tag `Department = HR` to multiple Azure resources. What is the best way to find all such resources in the portal?

**(a)** Use Azure Policy  
**(b)** Use Azure Monitor  
**(c)** Use tag-based filtering in the Resource Groups view  
**(d)** Use Azure Advisor  

**✅ Correct answer: (c)**  
**Explanation**: The Azure Portal allows filtering resources using tag values, making it easy to locate all resources associated with a specific department or purpose.

---

### 3. Which Azure tool allows you to create and manage virtual machines through a visual interface?

**(a)** Azure CLI  
**(b)** Azure Portal  
**(c)** Azure PowerShell  
**(d)** Azure Resource Graph  

**✅ Correct answer: (b)**  
**Explanation**: The Azure Portal is a web-based graphical UI that enables users to deploy and manage Azure resources visually, including VMs and tags.

---

### 4. You need to track resource usage per department for internal billing. What Azure feature helps accomplish this?

**(a)** Role-Based Access Control (RBAC)  
**(b)** Availability Zones  
**(c)** Tags  
**(d)** Virtual Networks  

**✅ Correct answer: (c)**  
**Explanation**: Tags can be used to label resources (e.g., by department), which can then be used in cost analysis tools like Azure Cost Management.

---

### 5. After applying tags to resources, which Azure service can generate cost reports grouped by those tags?

**(a)** Azure Advisor  
**(b)** Azure Policy  
**(c)** Azure Cost Management  
**(d)** Azure Monitor  

**✅ Correct answer: (c)**  
**Explanation**: Azure Cost Management supports tag-based cost breakdowns, enabling organizations to allocate spending by project, team, or department.

---

### 6. Which of the following resources can be tagged in Azure?

**(a)** Virtual machines only  
**(b)** Resource groups only  
**(c)** Most Azure resources including VMs, storage accounts, and resource groups  
**(d)** Only networking resources  

**✅ Correct answer: (c)**  
**Explanation**: Tags can be applied to most Azure resource types, allowing broad support for metadata-driven organization.

---

### 7. What is the structure of an Azure tag?

**(a)** Value only  
**(b)** Role assignment  
**(c)** Key-value pair  
**(d)** XML block  

**✅ Correct answer: (c)**  
**Explanation**: Tags in Azure are applied as key-value pairs, such as `Environment = Production`, to help identify and manage resources.

---

### 8. Which service is used to deploy infrastructure like virtual machines in Azure?

**(a)** Azure AD  
**(b)** Azure Compute  
**(c)** Azure SQL  
**(d)** Azure DevOps  

**✅ Correct answer: (b)**  
**Explanation**: Azure Compute is the service category that provides the capability to run virtual machines, containers, and other compute workloads.

---

### 9. You want to apply the same tag to multiple resources quickly. Which method would be most efficient?

**(a)** Tag each resource manually in the Azure Portal  
**(b)** Use a calculator tool  
**(c)** Use Azure CLI or PowerShell script  
**(d)** Reboot all VMs  

**✅ Correct answer: (c)**  
**Explanation**: Scripting tools like Azure CLI and PowerShell can automate the tagging of multiple resources, which is efficient and scalable.

---

### 10. How do tags enhance Azure governance in an enterprise environment?

**(a)** By preventing DDoS attacks  
**(b)** By improving bandwidth  
**(c)** By enabling structured management, cost control, and automation  
**(d)** By speeding up VM provisioning  

**✅ Correct answer: (c)**  
**Explanation**: Tags contribute to better governance by enabling structured organization, applying policies, and tracking costs across large environments.

---

### 11. In Azure, how does the platform handle tag names with different cases (e.g., `Environment` vs `environment`)?

**(a)** They are stored as two separate tags  
**(b)** Azure treats them as duplicate and merges them  
**(c)** It raises an error during deployment  
**(d)** Tags must always be lowercase in Azure  

**✅ Correct answer: (b)**  
**Explanation**: Azure treats tag names as case-insensitive, so `Environment` and `environment` refer to the same tag key. The last value overwrites the previous one.

---

### 12. Which of the following is true about Azure tag values?

**(a)** They are case-insensitive like tag names  
**(b)** Azure blocks values with uppercase letters  
**(c)** They are case-sensitive and treated as distinct  
**(d)** Azure converts all tag values to lowercase  

**✅ Correct answer: (c)**  
**Explanation**: Tag values in Azure are case-sensitive, meaning `IT` and `it` are treated as different values — important when filtering or generating cost reports.

---
---
---
## Professional Job Interview Questions – AZ-104 Labs

### Based on the Lab: **Working with Resource Tags**

1. **Imran wants to track cloud usage by department. What is the most effective Azure feature to use?**  
(a) Azure Policies  
(b) Resource Tags  
(c) Resource Groups  
(d) Azure Monitor  
**Correct answer: (b)**  
**Explanation**: **Resource Tags** allow users to label resources with metadata, such as department or cost center, enabling effective categorization and cost tracking.

2. **A finance team needs a report showing cloud costs by department. What prerequisite must be ensured in Azure?**  
(a) Billing alerts are enabled  
(b) Virtual Machines are grouped in separate resource groups  
(c) Tags are consistently applied to all resources  
(d) Azure budgets are configured  
**Correct answer: (c)**  
**Explanation**: Consistent use of **tags** like `Department` enables the generation of cost reports broken down by those tags.

3. **What happens if a resource in Azure lacks tags in a cost management scenario?**  
(a) Azure denies resource access  
(b) The resource is automatically deleted  
(c) It cannot be filtered in billing reports by department  
(d) Azure blocks its deployment  
**Correct answer: (c)**  
**Explanation**: Without **tags**, the resource will not appear under departmental cost breakdowns, reducing cost visibility.

4. **Why might an organization apply a tag like `Environment=Production` to resources?**  
(a) To restrict access to resources  
(b) To specify the Azure region  
(c) To group and identify resources by their role  
(d) To encrypt the resource  
**Correct answer: (c)**  
**Explanation**: Tags like **Environment** help identify whether a resource is used for development, staging, or production.

5. **Imran wants to filter all virtual machines belonging to the IT department. What should he use?**  
(a) Subscription filter  
(b) Azure Active Directory  
(c) Tag-based filtering  
(d) Role-based access control  
**Correct answer: (c)**  
**Explanation**: Filtering resources by **tags** is the simplest way to group and display assets for a particular purpose or owner.

6. **What is a key benefit of using resource tags for governance?**  
(a) They increase performance of virtual machines  
(b) They enable policy enforcement and automation  
(c) They replicate resources across regions  
(d) They act as firewalls  
**Correct answer: (b)**  
**Explanation**: **Tags** support automation, reporting, and governance policies like auto-deletion or cost tracking based on tagged metadata.

7. **An engineer accidentally deletes a tagged virtual machine. Which of the following could have prevented this?**  
(a) Role-based access control  
(b) DNS failover  
(c) Locking the resource  
(d) Adding more tags  
**Correct answer: (c)**  
**Explanation**: **Locks**, not tags, are used to prevent accidental deletion. Tags are for classification, not access control.

8. **How can tags improve collaboration across departments in a cloud environment?**  
(a) By allowing direct access to each other’s VMs  
(b) By encrypting departmental data  
(c) By providing visibility into resource ownership and usage  
(d) By changing subscription types  
**Correct answer: (c)**  
**Explanation**: **Tags** make it easier to track who owns which resources, helping in cost control and resource planning.

9. **Which of the following is a best practice when assigning tags to resources in Azure?**  
(a) Assign unique tag names to each resource  
(b) Use tags only on VMs  
(c) Standardize tag names and values organization-wide  
(d) Avoid tagging resources to reduce overhead  
**Correct answer: (c)**  
**Explanation**: Standardizing **tags** ensures consistency and helps teams query, report, and automate effectively.

10. **What Azure tool or feature can leverage tags to enforce policy compliance automatically?**  
(a) Azure CLI  
(b) Azure Resource Graph  
(c) Azure Policy  
(d) Azure Key Vault  
**Correct answer: (c)**  
**Explanation**: **Azure Policy** can audit and enforce rules based on **tags**, such as requiring certain tags for resource creation.

---
---
---
## Comic-Style Summary: **“Tag It Before You Track It!”**

Meet **Imran**, a smart cloud engineer at a growing tech company. His team spins up **virtual machines** like coffee in a tech startup—fast and everywhere! But when the monthly cloud bill arrived, no one knew **which department was spending what**. Chaos? Almost!

So Imran came up with a plan: use **Azure resource tags**. First, he created a new **Windows VM** named `resizeVM` and added it to a shared resource group. Pretty basic stuff—pick an image, select a size, secure it with a password, and go!

Then, Imran went to the **Tags** section and added:
**Name** = `Department`, **Value** = `IT`.
Boom! Now Azure could track exactly **who used what**, like a name tag at a company party. Every team’s cloud spend could finally be **filtered, tracked, and reported**.

Last step? Imran showed the magic to management: go to **Resource Groups**, filter by `Department = IT`, and voilà—clear visibility!
**Finance cheered**, **Ops nodded**, and **governance got stronger**. All thanks to the humble but powerful **tag**.

**Lesson?** Tag your resources. Because when cloud costs rise, **you don’t want to be the one guessing where the money went!** 😅💰💻

---
---
---
## Text-Based Diagram for the Lab: "Working with Resource Tags"

```text
+--------------------------+
|   Login to Azure Portal |
+--------------------------+
            |
            v
+------------------------------------+
| Navigate to "Virtual Machines"    |
| and click "+ Create"              |
+------------------------------------+
            |
            v
+----------------------------------------+
| Configure VM Details:                 |
| - Name: resizeVM                      |
| - OS: Windows Server 2019             |
| - Size: Standard B1s                  |
| - Disk: Standard SSD                  |
| - Location: East US                   |
| - Credentials for access              |
+----------------------------------------+
            |
            v
+--------------------------+
|     Click "Create"      |
+--------------------------+
            |
            v
+-------------------------------+
| After VM is deployed:        |
| Navigate to VM > "Tags"      |
+-------------------------------+
            |
            v
+----------------------------------------+
| Add a Tag:                             |
| - Name: Department                     |
| - Value: IT                            |
+----------------------------------------+
            |
            v
+----------------------------------------------------+
| Navigate to "Resource Groups" > rg-labresources    |
| Click "Add Filters"                                |
| Apply Filter: Department = IT                      |
+----------------------------------------------------+
            |
            v
+-------------------------------------------------+
| View and Analyze Resources Tagged with "IT"     |
| → Enables cost tracking, reporting, and audits  |
+-------------------------------------------------+
            |
            v
+--------------------------+
|  Delete all the resources |
+--------------------------+
```
---
---
