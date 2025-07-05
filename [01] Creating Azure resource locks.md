# Lab 1: Creating Azure resource locks

**Duration:** 45m
---
---

**After logging in with your credentials:**

---

### **Task 1: Create a Virtual Machine**

1. In the Azure portal, click on **Create a resource**.
2. Select **Virtual Machine** from the list and click **Create**.
3. Fill in the following configuration:

   * **Resource Group**: Select any existing or create a new one (e.g., `rg-labresources`)
   * **Virtual Machine Name**: `MyLabVM`
   * **Availability Options**: `No infrastructure redundancy required`
   * **Security Type**: `Trusted launch virtual machines`
   * **Image**: `Ubuntu Server 20.04 LTS Gen2`
   * **Size**: Click **See all sizes**, choose `B2s`
   * **Authentication Type**: `Password`
   * **Username**: `LabUser`
   * **Password**: `StrongPassword@123`
   * **Confirm Password**: `StrongPassword@123`
4. Click **Next: Disks >**
5. Under the **Disks** tab, select:

   * **OS Disk Type**: `Standard SSD (Locally-redundant Storage)`
6. Click **Review + create**, then **Create** to deploy the VM.

---

### **Task 2: Add a Delete Lock to the Virtual Machine**

1. Navigate to the newly created VM.
2. In the left menu, go to **Locks** under **Settings**.
3. Click **Add**, and enter:

   * **Lock Name**: `VMDeleteLock`
   * **Lock Type**: `Delete`
4. Click **OK** to apply the lock.

---

### **Task 3: Add a Read-Only Lock to the Resource Group**

1. Go to the Resource Group associated with the VM.
2. In the left menu, click **Locks** under **Settings**.
3. Click **Add**, and provide:

   * **Lock Name**: `RGReadOnly`
   * **Lock Type**: `Read-only`
4. Click **OK**.

---

**Delete all the resources.**

---
---
---
## **🔍 Lab Summary: Azure Resource Locks and Virtual Machine Deployment**

### **🎯 Purpose of the Lab**

The purpose of this lab is to provide hands-on experience with deploying a virtual machine (VM) in Microsoft Azure and configuring resource locks to control access and modification rights. This lab emphasizes the use of **Delete** and **Read-only** locks to protect resources from accidental or unauthorized changes or deletions. It helps learners understand how resource governance and access control can be enforced in cloud environments using built-in Azure features.

---

### **🛠 Azure Tools and Services Used**

#### 1. **Azure Portal**

* **Description**: A web-based unified console that allows users to manage Azure resources and services.
* **Role in the Lab**: Serves as the primary interface for completing all tasks—creating a virtual machine, applying locks, and managing resources.

#### 2. **Resource Group**

* **Description**: A container that holds related resources for an Azure solution.
* **Role in the Lab**: Acts as a logical grouping for the virtual machine and associated resources. The Read-only lock is applied at this level to restrict modification access.

#### 3. **Virtual Machine (VM)**

* **Description**: A scalable, on-demand computing resource offered by Azure, enabling the deployment of Windows or Linux environments.
* **Role in the Lab**: The core resource deployed to demonstrate how Azure locks work. It is configured with specific settings including OS, size, authentication, and disk type.

#### 4. **Resource Locks**

* **Description**: Built-in Azure feature to prevent accidental deletion or modification of critical resources by applying either Delete or Read-only locks.
* **Types Used in the Lab**:

  * **Delete Lock**: Prevents a resource (in this case, the virtual machine) from being deleted.
  * **Read-only Lock**: Prevents any modifications to a resource group, including adding, updating, or deleting any resources within it.
* **Role in the Lab**: Demonstrates how resource locks can be configured and enforced to safeguard infrastructure.

#### 5. **Azure Compute**

* **Description**: A category of Azure services used for hosting and running applications or workloads (includes VMs, containers, etc.).
* **Role in the Lab**: Provides the compute resources needed for deploying and managing the virtual machine.

#### 6. **Azure Storage (Disk)**

* **Description**: Manages the storage of the operating system and data disks for Azure VMs.
* **Role in the Lab**: The VM is configured with a Standard SSD OS disk to demonstrate storage selection and configuration during VM deployment.

---

This lab not only demonstrates how to deploy a basic virtual machine but also introduces governance tools like Azure resource locks, providing foundational knowledge in protecting and managing cloud infrastructure effectively.

---
---
---
## **🏢 Scenario: Securing a Production VM for a Financial Services App**

**Meet Aisha**, a cloud engineer working for **FinSecure Ltd.**, a mid-sized financial services company. Her team is tasked with deploying a new backend **Ubuntu server** in Azure, which will run core APIs for the company's mobile banking app. Because of the sensitivity of financial data and regulatory requirements, any accidental deletion or modification of infrastructure could lead to downtime, data loss, or compliance issues.

To avoid these risks, Aisha decides to follow a **cloud governance strategy** by deploying the VM and applying **resource locks** — a native Azure feature to protect mission-critical resources from accidental or unauthorized actions.

---

### **🔧 Step-by-Step Story**

### **1. Deploying the Virtual Machine**

Aisha logs into the **Azure Portal** and starts by clicking **Create a resource**. She selects **Virtual Machine**, giving it the name **MyLabVM** and placing it under the **rg-labresources** resource group.

She chooses:

* **Ubuntu Server 20.04 LTS Gen2** as the operating system to ensure stability and long-term support,
* A modestly sized **B2s VM** to optimize costs during the testing phase,
* And sets up credentials using a **secure password-based login** with a non-admin username `LabUser`.

In the **Disks** section, she selects **Standard SSD** to balance performance and cost. After reviewing all settings, she clicks **Create**.

✅ **Why it matters**: A well-configured VM provides the compute power for her APIs, but without protection, it's vulnerable to unintended actions.

---

### **2. Applying a Delete Lock to the VM**

Now that the VM is running, Aisha wants to **prevent any team member from accidentally deleting it** — especially during cleanup tasks or automation runs.

She opens the VM in the Azure Portal, navigates to **Settings > Locks**, and adds a new lock:

* **Name**: `VMDeleteLock`
* **Type**: `Delete`

✅ **Benefit**: Even users with high-level access can't delete the VM unless the lock is removed. This is crucial for safeguarding production workloads.

---

### **3. Applying a Read-Only Lock on the Resource Group**

Next, Aisha wants to go a step further: **freeze the entire resource group** to prevent any modifications during a company audit next week.

She navigates to the **rg-labresources** resource group, goes to **Locks**, and adds another lock:

* **Name**: `RGReadOnly`
* **Type**: `Read-only`

✅ **Impact**: Now, nothing in the group — not even the VM’s network interface or disk — can be changed, deleted, or altered. Azure enforces this lock across the board.

---

### **🧠 Real-World Relevance**

Aisha’s actions reflect **best practices in cloud governance** — especially in industries like finance, healthcare, or government where **uptime, data integrity, and change control** are non-negotiable. By using **Azure Resource Locks**, she's proactively **reducing risk**, ensuring **regulatory compliance**, and building **trust with stakeholders**.

---

### **🧼 Final Cleanup**

Once the audit period ends or the infrastructure is no longer needed, Aisha removes the locks and proceeds to shut down the environment.

---

**Delete all the resources.**

---
---

## 🧑‍💻 Comic-Style Summary: **“Lock It Before You Lose It!”**

### 🧑‍💻 Meet Aisha — The Cloud Hero!

Aisha is a **cloud engineer** working at a company that handles **sensitive financial data**. Her boss asks her to make sure their new **Linux server in Azure** is safe and can't be deleted or changed by mistake. That’s a big responsibility!

---

### 🛠️ Step 1: Building the Server

Aisha logs into the **Azure Portal** and creates a **Virtual Machine (VM)**.
She picks:

* **Ubuntu Server** (stable and secure),
* A cost-friendly size called **B2s**,
* And names it **MyLabVM** inside the **rg-labresources** group.

✅ **Why?** This server will run banking services, so it needs to be reliable!

---

### 🔒 Step 2: Lock the VM Against Deletion

Now Aisha adds a **Delete Lock** to the VM.
She goes to the VM settings, clicks **Locks**, and adds:

* **Name**: `VMDeleteLock`
* **Type**: `Delete`

✅ **Why?** Even if someone tries to delete the VM by accident or during cleanup — Azure will say, "Nope!" This keeps the server safe.

---

### 🧊 Step 3: Freeze the Entire Resource Group

Aisha wants to be extra careful. So, she goes to the **resource group** that contains the VM and adds a **Read-Only Lock**.

* **Name**: `RGReadOnly`
* **Type**: `Read-only`

✅ **Why?** This lock makes sure that **nothing inside the group can be changed or deleted** during an important company audit. It’s like putting everything in a glass case!

---

### 🧠 Why This Is Smart

Aisha’s use of **Azure Resource Locks** is a great example of **cloud governance**. In real-life work, especially in industries like finance, **mistakes can be costly**. These locks give protection and peace of mind to the entire team.

---

### ✅ Mission Accomplished

Thanks to Aisha:

* The VM was created successfully.
* **No one can delete it accidentally.**
* **All changes to the group are blocked** until they’re ready.
* The company’s cloud environment is safe and compliant!

🎉 Aisha nailed it! She's not just a cloud engineer — she's a **cloud superhero**!

---
---
## Lab-Based Conceptual MCQs

---

### 1. What is the primary purpose of applying a **Delete Lock** to an Azure resource?

**(a)** To prevent unauthorized access to a VM  
**(b)** To improve VM performance during scaling  
**(c)** To stop the resource from being accidentally or intentionally deleted  
**(d)** To reduce the billing costs for that resource  

**Correct answer: (c)**  
**Explanation**: A Delete Lock ensures that a resource cannot be deleted until the lock is removed, making it useful for protecting critical infrastructure.

---

### 2. Which Azure feature allows you to **restrict both updates and deletions** of a resource?

**(a)** Network Security Groups  
**(b)** Resource Policies  
**(c)** Read-Only Lock  
**(d)** Role-Based Access Control (RBAC)

**Correct answer: (c)**  
**Explanation**: A Read-Only Lock prevents any modifications or deletions to the resource, effectively making it view-only until the lock is removed.

---

### 3. How do Azure **Resource Locks** differ from **RBAC (Role-Based Access Control)**?

**(a)** Locks control access; RBAC prevents deletion  
**(b)** Locks apply to billing roles; RBAC applies to admin users  
**(c)** RBAC defines *who* can perform actions, while locks control *what* actions can happen, regardless of role  
**(d)** There is no difference; both are used to prevent access  

**Correct answer: (c)**  
**Explanation**: RBAC is identity-based access control, while resource locks enforce restrictions at the resource level regardless of the user’s role or permissions.

---

### 4. What happens when a **Delete Lock** is applied to a virtual machine?

**(a)** The VM becomes read-only  
**(b)** The VM can’t be stopped or restarted  
**(c)** The VM cannot be deleted until the lock is removed  
**(d)** All traffic to the VM is blocked

**Correct answer: (c)**  
**Explanation**: A Delete Lock specifically prevents the deletion of the resource it is applied to. Other operations like restarting or accessing are still allowed.

---

### 5. Why would an organization apply a **Read-Only Lock** on a **resource group** instead of on individual resources?

**(a)** It ensures encryption is enabled  
**(b)** It applies consistent protection to all resources in that group  
**(c)** It improves VM availability  
**(d)** It prevents the resource group from resizing

**Correct answer: (b)**  
**Explanation**: Applying a lock at the resource group level ensures that all resources within the group are protected under the same policy without setting individual locks.

---

### 6. If a contributor has permission to delete a VM, but a **Delete Lock** exists on that VM, what will happen?

**(a)** The delete operation will succeed because of the contributor role  
**(b)** The delete operation will be blocked due to the lock  
**(c)** The VM will restart instead of deleting  
**(d)** A backup of the VM will be created automatically

**Correct answer: (b)**  
**Explanation**: Resource Locks override RBAC permissions. Even with delete permissions, the contributor cannot delete the VM unless the lock is removed.

---

### 7. What is a key benefit of using **Azure Resource Locks** in a production environment?

**(a)** Automatically scales resources based on traffic  
**(b)** Reduces cost by limiting resource size  
**(c)** Prevents accidental deletion or changes to critical infrastructure  
**(d)** Encrypts data stored on the virtual machine

**Correct answer: (c)**  
**Explanation**: Resource Locks are commonly used to safeguard mission-critical workloads by preventing changes or deletions without administrator oversight.

---

### 8. Which of the following is **true** about Azure Resource Locks?

**(a)** They can only be applied by global administrators  
**(b)** They are inherited by child resources only in subscriptions  
**(c)** They can be applied at resource, resource group, or subscription level  
**(d)** They apply only to storage and compute services

**Correct answer: (c)**  
**Explanation**: Locks can be applied at various scopes — individual resources, resource groups, or even across an entire subscription — making them versatile for governance.

---

### 9. What is the outcome of applying a **Read-Only Lock** to a resource group that contains multiple VMs and storage accounts?

**(a)** All resources can still be modified individually  
**(b)** All resources become editable but not deletable  
**(c)** All modification and deletion actions are blocked on all contained resources  
**(d)** The lock only applies to newly added resources in the group

**Correct answer: (c)**  
**Explanation**: A Read-Only Lock on a resource group cascades to all resources within, making them unmodifiable unless the lock is removed.

---

### 10. In a DevOps pipeline, how can a **resource lock cause a deployment to fail**?

**(a)** It blocks new subscription creation  
**(b)** It causes IP address conflicts  
**(c)** It prevents updates or deletions of existing locked resources  
**(d)** It slows down the build process

**Correct answer: (c)**  
**Explanation**: If a pipeline tries to update or delete a locked resource, the operation will fail, as the lock enforces protection against those actions regardless of deployment method.

---
---
## Professional Job Interview Questions – AZ-104 Labs

### Lab Scenario: Creating Azure Resource Locks

1. **Aisha has deployed a production VM in Azure and wants to ensure it is not accidentally deleted by another team member. What is the most appropriate solution she should apply?**

(a) Configure RBAC with read-only permissions for all users  
(b) Apply a **Delete Lock** to the VM  
(c) Disable the VM from the portal  
(d) Move the VM to a separate subscription

**Correct answer: (b)**  
A **Delete Lock** ensures that even users with high privileges cannot delete the resource unless the lock is explicitly removed.

---

2. **A company undergoing a security audit wants to ensure that no changes are made to an entire resource group. What should an administrator do?**

(a) Remove all user permissions temporarily  
(b) Enable resource diagnostics logging  
(c) Apply a **Read-only Lock** on the resource group  
(d) Set the subscription to read-only mode

**Correct answer: (c)**  
A **Read-only Lock** on the resource group restricts any modifications to resources within that group during the audit.

---

3. **Which of the following best describes the effect of a ‘Read-only’ lock applied to a resource group?**

(a) Users can delete resources but cannot update them  
(b) Users can read and update resources but not delete them  
(c) Users can only view resources; updates and deletions are blocked  
(d) Users can update resources but are denied reading access

**Correct answer: (c)**  
A **Read-only Lock** restricts users from modifying or deleting resources, allowing only view operations.

---

4. **An engineer applied a 'Delete' lock on a VM but noticed that automation scripts still failed to delete it. Why did this happen?**

(a) The VM was in use by another resource  
(b) A **Delete Lock** prevents deletion regardless of user identity  
(c) The script lacked contributor access  
(d) The VM was part of a backup policy

**Correct answer: (b)**  
A **Delete Lock** blocks deletion of the resource even if the action comes from automation or users with contributor roles.

---

5. **What is a possible limitation of using resource locks in a DevOps CI/CD pipeline?**

(a) They increase billing costs  
(b) They interfere with automation that modifies or deletes resources  
(c) They require Azure CLI only  
(d) They reduce performance of VMs

**Correct answer: (b)**  
**Resource Locks** can block automation processes like deployments or deletions, requiring manual lock removal before scripts proceed.

---

6. **Which Azure role is still affected by resource locks, regardless of its elevated privileges?**

(a) Owner  
(b) Contributor  
(c) Security Reader  
(d) Global Administrator

**Correct answer: (a)**  
Even users with the **Owner** role cannot delete or modify a locked resource unless the lock is explicitly removed.

---

7. **Your organization wants to ensure that no one modifies a virtual network during the testing phase. Which strategy should be used?**

(a) Disable the network interface  
(b) Apply a **Read-only Lock** on the virtual network  
(c) Deny write permissions using IAM  
(d) Remove NSGs temporarily

**Correct answer: (b)**  
Applying a **Read-only Lock** prevents any changes to the virtual network configuration while still allowing read access.

---

8. **A junior admin accidentally removed a resource lock while trying to free up unused resources. How can an organization prevent such issues?**

(a) Use a more complex naming convention for locks  
(b) Enable alerting for resource deletions  
(c) Use role-based access control to restrict lock management  
(d) Disable lock removal in Azure policy

**Correct answer: (c)**  
Restricting permissions using **Role-Based Access Control (RBAC)** ensures only trusted users can modify or remove locks.

---

9. **You’re tasked with deploying critical production resources that must not be modified until further notice. Which two actions together should you take?**

(a) Disable all outbound ports and alert on usage  
(b) Assign a read-only role and apply **resource locks**  
(c) Use Azure Policy to deny all changes  
(d) Place resources in a separate VNet with traffic restrictions

**Correct answer: (b)**  
Combining **read-only RBAC roles** with **resource locks** provides a strong defense against accidental or unauthorized changes.

---

10. **Which tool or interface is commonly used to apply and manage resource locks in Azure?**

(a) Network Security Group  
(b) Azure CLI and Azure Portal  
(c) Power BI  
(d) Azure Advisor

**Correct answer: (b)**  
**Resource Locks** can be created and managed using either the **Azure Portal** or **Azure CLI**, offering flexibility for administrators.

---
---
**Here's a **comic-style summary** of the Azure lab scenario on **Creating Azure Resource Locks**, crafted in a fun, easy-to-follow way for a general audience:**

---

### **🔐 Comic-Style Summary: Lock It Down with Confidence!**

👩‍💻 **Meet Aisha**, the brilliant cloud engineer at FinSecure Ltd. Her mission? To set up a secure **Ubuntu virtual machine** for a mobile banking backend — but with one big twist: **no one should accidentally delete or tamper with it**!

🚀 Aisha jumps into the **Azure Portal**, spins up a shiny new VM called **MyLabVM**, and sets it to run on **Ubuntu 20.04 LTS**. It's fast, stable, and ready for the banking APIs. She secures it with a username and password — just like locking the front door before a party.

🔒 But wait! To keep this important server safe, Aisha applies a **Delete Lock**. Now, even the most powerful team member can’t hit “Delete” on the VM unless they remove the lock. It’s like putting a “DO NOT TOUCH” sticker on the server!

🧱 Not done yet, she goes to the **Resource Group** and adds a **Read-Only Lock**. This freezes all resources inside — no changes, no funny business. It’s like putting the whole toolbox behind glass during an audit.

🎯 With these **Azure Resource Locks** in place, Aisha ensures the infrastructure is **safe, compliant, and audit-proof**. She’s the hero the backend didn’t know it needed — and her team sleeps better knowing nothing critical will be deleted by mistake.

---
---
## Text-Based Diagram for the Lab: "Creating Azure Resource Locks"

```plaintext
+--------------------------------------------------+
|          Start: Logged into Azure Portal         |
+--------------------------------------------------+
                          |
                          v
+--------------------------------------------------+
|    Create a Virtual Machine (VM)                 |
|    - Name: MyLabVM                               |
|    - OS: Ubuntu Server 20.04 LTS                 |
|    - Size: B2s                                   |
|    - Admin: LabUser with password                |
|    - Disk: Standard SSD                          |
|    - Resource Group: rg-labresources             |
+--------------------------------------------------+
                          |
                          v
+--------------------------------------------------+
|    Apply a Delete Lock on the VM                 |
|    - Navigate to: MyLabVM > Settings > Locks     |
|    - Add Lock:                                   |
|        • Name: VMDeleteLock                      |
|        • Type: Delete                            |
+--------------------------------------------------+
                          |
                          v
+--------------------------------------------------+
|    Apply a Read-Only Lock on the Resource Group  |
|    - Navigate to: rg-labresources > Locks        |
|    - Add Lock:                                   |
|        • Name: RGReadOnly                        |
|        • Type: Read-only                         |
+--------------------------------------------------+
                          |
                          v
+--------------------------------------------------+
|       Outcome: Resources are Protected           |
|    - VM cannot be deleted                        |
|    - Entire resource group is locked for edits   |
|    - Ensures compliance and uptime               |
+--------------------------------------------------+
                          |
                          v
+--------------------------------------------------+
|         Final Step: Remove Locks (if needed)     |
|         after audit or before cleanup            |
+--------------------------------------------------+
                          |
                          v
+--------------------------------------------------+
|              End of Lab Workflow                 |
+--------------------------------------------------+
```
---
---

