# Lab 3: Creating Azure Policies

**Duration:** 30m

---

## **After logging in with your credentials:**

### **Step 1: Create an Azure Policy Assignment to Restrict Allowed Locations**

1. In the Azure portal, search for **Policy** using the top search bar and open the **Policy** service.
2. Click the **Scope selector** (three-dot icon) near the top of the Overview page.
3. From the scope options, select the **target resource group** you want to apply the policy to and click **Select**.
4. In the left-hand menu under the **Authoring** section, choose **Definitions**.
5. In the search bar, type **Allowed locations** and locate the corresponding built-in policy.
6. Click on the **Allowed locations** policy to view its details.
7. Select **Assign policy**.
8. In the **Basics** tab of the assignment:

   * Set **Assignment name** (e.g., *Allow UK South for rg-labresources*).
   * Set **Description** (e.g., *Allow resources to be created in UK South only*).
   * Ensure **Policy enforcement** is **Enabled**.
9. Click **Next** to open the **Parameters** tab.
10. From the dropdown for **Allowed locations**, select **UK South**.
11. Click **Review + create**, then click **Create** to deploy the policy assignment.

---

### **Step 2: Test the Allowed Locations Policy**

1. Search for and open the **Virtual Networks** service.
2. Click **+ Create** to start creating a new virtual network.
3. In the **Basics** tab, configure the following:

   * Select the same **resource group** where the policy was applied.
   * Enter a **name** for the virtual network (e.g., `MyVNet`).
   * Set the **Region** to **East US** (or any region other than UK South).
4. Click **Review + create**. The validation should fail.
5. Click the **validation error** to confirm that the region is disallowed by policy.
6. Go back to the **Basics** tab, change the region to **UK South**, and click **Review + create** again.
7. Once validation passes, click **Create** to deploy the virtual network.

---

**Delete all the resources.**

---
---
---
## **📘 Azure Lab Summary: Enforcing Resource Deployment Compliance with Azure Policy**

---

### **🎯 Purpose of the Lab**

The objective of this lab is to provide hands-on experience with **Azure Policy**, focusing on creating and assigning a **built-in policy definition** that restricts resource deployment to specific Azure regions. Learners will configure a policy at the **resource group level**, test its enforcement by attempting to deploy a resource outside the allowed location, and verify policy compliance in real time. This lab demonstrates how Azure Policy helps enforce **governance**, **compliance**, and **operational standards** in cloud environments.

---

### **🛠 Azure Tools and Services Used**

#### 1. **Azure Policy**

* **Description**: A governance tool that enables the definition and enforcement of rules across Azure resources.
* **Role in the Lab**: Central to the lab’s objective. It is used to create an **"Allowed locations"** policy assignment that restricts where resources can be deployed.

#### 2. **Policy Definition**

* **Description**: A rule or set of rules that define specific conditions and effects (e.g., deny, audit, append) in Azure Policy.
* **Role in the Lab**: The built-in **"Allowed locations"** policy definition is used to restrict allowed regions for resource creation.

#### 3. **Policy Assignment**

* **Description**: The application of a policy definition to a specific scope, such as a resource group or subscription.
* **Role in the Lab**: The policy is assigned at the **resource group** level to enforce that only the **UK South** region is allowed for deployments.

#### 4. **Azure Resource Group**

* **Description**: A logical container for managing and grouping related Azure resources.
* **Role in the Lab**: Acts as the **scope** for the policy assignment. Only resources deployed within this group are affected by the policy.

#### 5. **Virtual Network (VNet)**

* **Description**: A core networking resource in Azure used to establish secure communication between Azure resources.
* **Role in the Lab**: A virtual network is used to **test** policy enforcement. Attempting to deploy it in a disallowed region triggers a validation failure, proving the policy is active.

#### 6. **Azure Portal**

* **Description**: A web-based GUI for managing Azure resources and services.
* **Role in the Lab**: Used to navigate, create policies, assign them, and deploy resources through a graphical interface.

---

### **🔑 Real-World Relevance**

This lab reflects a common enterprise requirement: **restricting resource deployment to approved regions** for regulatory, compliance, data residency, or operational efficiency. Azure Policy helps organizations **standardize configurations**, **minimize risks**, and **automate governance** across large-scale environments.

---
---
---

## **🏢 Scenario: Enforcing Regional Compliance for a Global Finance Company**

**Meet Sarah**, a cloud governance engineer at **FinTechCorp**, a global financial services company. Her team manages dozens of Azure resource groups used by departments across Europe and North America. Recently, the **risk and compliance team** raised a concern: some teams have been unintentionally deploying resources in regions outside their approved geography — specifically outside the **UK**, violating company data residency policies and potentially exposing sensitive customer data to regulatory scrutiny.

Sarah is tasked with solving this using **native Azure governance tools** — without writing custom scripts or relying on third-party tools.

---

### **🎯 Goal: Restrict resource creation to the "UK South" region only for a specific resource group.**

---

### **🔧 Step-by-Step Actions and Their Business Value**

---

### **Step 1: Navigate to Azure Policy**

Sarah logs into the **Azure Portal** and searches for **“Policy”** using the search bar. This takes her to the **Azure Policy dashboard**, where she manages all governance-related definitions and assignments.

> **Why this matters**: Azure Policy is a built-in service that allows her to enforce organizational standards — no additional tools needed.

---

### **Step 2: Assign the “Allowed Locations” Policy**

Sarah chooses the specific **resource group** used by the finance analytics team (`rg-labresources`) as the **scope**.
From the built-in policy definitions, she selects **“Allowed locations”**, clicks **Assign**, and configures it with:

* **Assignment name**: "Allow UK South for rg-labresources"
* **Description**: "Restrict all resources in this group to the UK South region"
* **Policy enforcement**: Enabled
* **Allowed region**: **UK South**

She completes the assignment by clicking **Review + Create**.

> **Why this matters**: Instead of manually checking deployments or relying on human memory, Sarah is now using **policy as code** — an automated way to **prevent non-compliant deployments** before they even happen.

---

### **Step 3: Test the Policy Enforcement**

To validate her work, Sarah tries to create a **virtual network** inside the same resource group (`rg-labresources`) but chooses **East US** as the region.

As expected, deployment **fails validation**, and Azure displays an error:
**"The specified location 'East US' is not allowed by the policy assigned to this resource group."**

Sarah then changes the region to **UK South**, runs the deployment again — and it **succeeds**.

> **Why this matters**: This confirms the policy is working **exactly as intended**. Teams now have **guardrails** in place, not just guidelines.

---

### **💼 Real-World Impact**

By using **Azure Policy** and **Allowed Locations**, Sarah has:

* **Enforced regional compliance** without manual intervention
* **Reduced the risk of regulatory violations**
* **Streamlined governance** across departments
* Provided a scalable solution that can be applied at the subscription level later

---

### **Conclusion**

This lab mirrors the real-world use case of **controlling where data and services live**, which is critical in industries like finance, healthcare, and government. Azure Policy empowers teams like Sarah’s to **automate compliance**, reduce errors, and align cloud usage with organizational strategy.

---
---
---
## Lab-Based Conceptual MCQs

---

### 1. What is the primary purpose of assigning an "Allowed locations" policy in Azure?

**(a)** To improve resource performance in a specific region  
**(b)** To restrict where resources can be deployed for compliance or governance  
**(c)** To lower costs by avoiding expensive regions  
**(d)** To improve redundancy across multiple regions  

**✅ Correct answer: (b)**  
**Explanation**: The "Allowed locations" policy is used to enforce that resources are deployed only in approved regions, often to meet compliance, data residency, or governance requirements.

---

### 2. At which scope can an Azure Policy be assigned?

**(a)** Only at the resource level  
**(b)** Only at the subscription level  
**(c)** At resource, resource group, or subscription level  
**(d)** Only at the tenant root group level  

**✅ Correct answer: (c)**  
**Explanation**: Azure Policies can be assigned at various scopes, including individual resources, resource groups, and subscriptions, depending on the desired reach of enforcement.

---

### 3. What happens if a user attempts to deploy a resource in a disallowed region under an active location policy?

**(a)** The resource is automatically redirected to the nearest allowed region  
**(b)** The deployment fails validation and is blocked  
**(c)** A warning appears, but the deployment continues  
**(d)** The policy is bypassed for that session  

**✅ Correct answer: (b)**  
**Explanation**: Azure Policy enforces rules at deployment time. If a deployment violates the assigned policy, it fails validation and is blocked from proceeding.

---

### 4. Which Azure service is responsible for managing and enforcing governance rules like allowed regions or tag requirements?

**(a)** Azure Monitor  
**(b)** Azure Blueprints  
**(c)** Azure Policy  
**(d)** Azure Advisor  

**✅ Correct answer: (c)**  
**Explanation**: Azure Policy is the service that allows administrators to define and enforce organizational rules and compliance requirements across resources.

---

### 5. How does Azure Policy improve security and compliance in cloud environments?

**(a)** By encrypting all traffic to the Azure portal  
**(b)** By enforcing standards such as allowed regions, naming conventions, or tag policies  
**(c)** By scanning for malware  
**(d)** By automatically updating resource configurations  

**✅ Correct answer: (b)**  
**Explanation**: Azure Policy helps maintain compliance and governance by defining enforceable rules that restrict or allow specific behaviors or configurations within the environment.

---

### 6. Which of the following best describes the relationship between policy **definition** and **assignment**?

**(a)** Definitions are applied only when creating a subscription  
**(b)** Assignment is the creation of a new policy  
**(c)** Definitions define rules, while assignments apply those rules to a scope  
**(d)** Assignment determines which policy definition to use at runtime  

**✅ Correct answer: (c)**  
**Explanation**: Policy definitions contain the logic and rules, while assignments apply those definitions to a specific scope such as a resource group or subscription.

---

### 7. What is a common use case for using the “Allowed locations” policy in enterprise environments?

**(a)** Reducing latency between services  
**(b)** Preventing virtual machine resizing  
**(c)** Ensuring resources are deployed only in approved regions for compliance  
**(d)** Limiting user sign-ins to specific Azure tenants  

**✅ Correct answer: (c)**  
**Explanation**: This policy ensures that teams cannot deploy resources outside approved regions, which is often required for regulatory or legal compliance.

---

### 8. When testing a location policy, why would a deployment to an unapproved region fail before the resource is created?

**(a)** Azure charges a fee for validation  
**(b)** Azure Policy is evaluated during the resource creation validation phase  
**(c)** Resource locks prevent policy bypass  
**(d)** Network settings override policy enforcement  

**✅ Correct answer: (b)**  
**Explanation**: Azure Policy is evaluated during the pre-deployment validation phase. If a policy is violated, the deployment is blocked before any resource is provisioned.

---

### 9. What benefit does assigning a policy at the **resource group level** offer?

**(a)** It only affects storage resources  
**(b)** It bypasses any subscription-wide policies  
**(c)** It allows more granular control over specific workloads or departments  
**(d)** It applies to all Azure tenants globally  

**✅ Correct answer: (c)**  
**Explanation**: Assigning policies at the resource group level allows teams to apply governance rules to specific projects, environments, or departments without affecting the entire subscription.

---

### 10. After applying an "Allowed locations" policy, what would indicate that the policy is working correctly?

**(a)** All resources are encrypted  
**(b)** Resource deployments succeed in any region  
**(c)** Deployments to non-approved regions fail validation  
**(d)** The resource group is automatically locked  

**✅ Correct answer: (c)**  
**Explanation**: A working location policy will cause deployments in non-allowed regions to fail with a validation error, confirming that the enforcement is active and effective.

---
