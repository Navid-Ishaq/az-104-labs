# Lab 20: Create a SQL database

**Duration:** 1h 0m

---
---

After logging in with your credentials:

1. Navigate to **Create a resource** from the home page or portal menu.

2. Choose **Databases**, then select **SQL Database**.

3. Fill in the SQL Database form:

   * Select an existing **resource group**.
   * Provide a **database name** (e.g., `MyDatabase`).
   * Click **Create new** under **Server**, then:

     * Enter a unique **server name**.
     * Set **location** to `East US`.
     * Choose **SQL authentication**.
     * Define a **server admin login** (e.g., `DbAdmin`) and **password**.
     * Click **OK** to create the server.
   * Select the newly created server.
   * Set **Want to use SQL elastic pool** to `No`.
   * Under **Compute + Storage**, choose **Basic** tier and click **Apply**.
   * Set **Backup storage redundancy** to **Locally-redundant backup storage**.

4. Proceed to the **Networking** tab and:

   * Set **Connectivity method** to `Public endpoint`.

5. Click **Review + Create**, then click **Create**.

6. After deployment, go to **SQL databases**, then select your new database.

7. From the overview page, click on the **server name** to open the SQL server settings.

8. Go to **Networking**, set **Public network access** to **Selected networks**.

9. Click **+ Add your client IPv4 address** to add your current IP.

10. Enable the checkbox for **Allow Azure services and resources to access this server**.

11. Click **Save** to apply firewall settings.

12. Return to the SQL database blade and select **Query editor**.

13. Sign in using the SQL admin password.

14. In the query editor, paste and run the following script to create four tables:

```sql
-- Create Person table
CREATE TABLE person (
  personid INT IDENTITY PRIMARY KEY,
  firstname NVARCHAR(128) NOT NULL,
  middelinitial NVARCHAR(10),
  lastname NVARCHAR(128) NOT NULL,
  dateofbirth DATE NOT NULL
);

-- Create Student table
CREATE TABLE student (
  studentid INT IDENTITY PRIMARY KEY,
  personid INT REFERENCES person (personid),
  email NVARCHAR(256)
);

-- Create Course table
CREATE TABLE course (
  courseid INT IDENTITY PRIMARY KEY,
  NAME NVARCHAR(50) NOT NULL,
  teacher NVARCHAR(256) NOT NULL
);

-- Create Credit table
CREATE TABLE credit (
  studentid INT REFERENCES student (studentid),
  courseid INT REFERENCES course (courseid),
  grade DECIMAL(5, 2) CHECK (grade <= 100.00),
  attempt TINYINT,
  CONSTRAINT UQ_studentgrades UNIQUE CLUSTERED (studentid, courseid, grade, attempt)
);
```

15. After successful execution, check the **Tables** section to confirm that all four tables were created.

Delete all the resources.

---
---

## **Structured Lab Summary – Create a SQL Database**

### **Purpose of the Lab**

The purpose of this lab is to **create an Azure SQL Database**, configure its **server-level firewall rules**, connect securely to the database, and **execute SQL scripts** to create tables. This hands-on experience helps learners understand how to manage **relational databases** in the cloud using **Azure SQL Database**, a fully managed Platform as a Service (PaaS) offering.

This lab is especially relevant for **Azure administrators**, **database managers**, or learners preparing for **AZ-104** certification, as it demonstrates real-world tasks such as provisioning databases, securing access, and managing schema through the portal.

---

### **Azure Tools Utilized in the Lab**

#### 1. **Azure SQL Database**

* **Description**: A fully managed relational database-as-a-service (DBaaS) built on **SQL Server** technologies.
* **Role in Lab**: The main component being created and configured. It stores structured data and is accessed via SQL queries.
* **Example**: A student information system can use **Azure SQL Database** to store data in tables like `student`, `course`, and `credit`.

#### 2. **Azure Portal**

* **Description**: A web-based user interface for managing Azure resources.
* **Role in Lab**: Used to create resources like SQL databases, configure settings, and access built-in tools like the **Query Editor**.
* **Example**: You create the SQL database using the **Create a resource** option from the **Azure Portal** home screen.

#### 3. **Resource Group**

* **Description**: A container that holds related Azure resources.
* **Role in Lab**: All components such as the SQL database and its server are grouped here for easier management.
* **Example**: The database is deployed under **rg\_eastus\_lab12345**.

#### 4. **SQL Server (logical)**

* **Description**: A container for one or more SQL databases; provides an endpoint for connectivity and manages authentication.
* **Role in Lab**: Hosts the **SQL Database**. It includes admin credentials and firewall settings.
* **Example**: You create a new logical SQL server named **myuniquesqlserver123** with an admin login and password.

#### 5. **Firewall Rules**

* **Description**: Security feature that allows or blocks traffic based on IP addresses.
* **Role in Lab**: Configured to allow public IP access to the SQL server so users can connect from their local machines.
* **Example**: Adding your public IP to allow Visual Studio or the Azure portal’s **Query Editor** to access the database.

#### 6. **Query Editor (in Portal)**

* **Description**: A browser-based SQL tool integrated into the Azure portal.
* **Role in Lab**: Used to connect to the newly created database and run SQL scripts to create tables.
* **Example**: You paste SQL code to create `person`, `student`, `course`, and `credit` tables directly in the editor.

#### 7. **SQL Script**

* **Description**: SQL code used to perform database operations such as creating tables or inserting data.
* **Role in Lab**: Used to define and create a database schema with relationships.
* **Example**: The `CREATE TABLE` statement sets up the structure for the `student` and `course` tables with foreign keys.

#### 8. **Compute + Storage Configuration**

* **Description**: Determines the performance and size of the SQL database.
* **Role in Lab**: Set to **Basic tier** in the lab for cost-effective use suitable for small workloads.
* **Example**: You configure the database for **Basic (5 DTUs)** performance level with locally redundant backup.

---

### **Clarifying Real-World Example**

Imagine a college IT department needs a cloud-based system to manage student records. Using this lab:

* They **create a SQL database** on Azure to avoid on-prem hardware.
* They **configure firewall rules** so staff can access it securely from campus.
* They **create relational tables** (`student`, `course`, `credit`) to store and relate academic data.

This lab replicates exactly this kind of enterprise-grade task, simplified for learning and practical understanding.

---
---

## **Realistic Scenario: Setting Up a Student Database System on Azure**

### **Background**

**David** is a junior **Cloud Administrator** at a small college. His manager, **Lisa**, assigns him the task of moving their old student records database to the **cloud** so that teachers can securely access it anytime without relying on outdated servers.

Lisa wants David to use **Azure SQL Database** to store data like **student names**, **courses**, and **grades** because it's secure, scalable, and doesn’t require hardware maintenance.

---

### **Step-by-Step Story**

**1. Creating the Database in the Cloud**

After logging in to the **Azure portal**, David goes to **Create a resource** and chooses **SQL Database** from the **Azure Marketplace**. He enters the database name as **StudentDB** and creates a new **SQL Server** called **eastus-student-sql** with **SQL authentication**, setting a secure admin username and password.

> ✅ This step helps centralize all student data in a secure cloud-based system managed through **Azure**.

---

**2. Configuring Performance and Storage**

David configures the **Compute + Storage** to use the **Basic service tier**, which is perfect for a lightweight student app. He selects **Locally-redundant backup storage** to keep backups within the same region, ensuring data safety without incurring high costs.

> ✅ This allows the system to run at a lower cost while still being backed up safely.

---

**3. Setting Public Access to the Server**

To allow remote access from the college office, David sets up **Public network access** and adds his **client IP** to the **firewall rules**. He also enables the setting to **allow Azure services** to access the server.

> ✅ This ensures only authorized users (like teachers) from the campus can access the database, keeping it secure.

---

**4. Connecting to the Database**

David opens **Query Editor** inside the Azure portal. He enters the **SQL admin credentials** and connects successfully to the newly created **StudentDB**.

> ✅ This gives him direct access to run SQL commands and build the database schema without needing extra tools.

---

**5. Creating Tables for Data Storage**

Using a **SQL script**, David creates four tables:

* **person**: To store names and birthdates.
* **student**: Linked to person data with email.
* **course**: List of courses and teachers.
* **credit**: Tracks course grades and attempts.

> ✅ This structure represents a real-world **relational database** useful for tracking academic records.

```sql
CREATE TABLE student (
  studentid INT IDENTITY PRIMARY KEY,
  personid INT REFERENCES person(personid),
  email NVARCHAR(256)
);
```

---

**6. Viewing the Results**

After running the script, David sees all the tables listed under the **Tables** tab in the portal. Everything looks good, and the schema reflects exactly what Lisa asked for.

> ✅ David now has a functioning cloud-based system that teachers can use to manage student data.

---

### **Outcome**

David successfully used **Azure SQL Database**, **Firewall Rules**, **Query Editor**, and **SQL scripting** to build a database system from scratch in the cloud. His work not only modernized the college’s infrastructure but also made data access secure and easier for staff.

---

### **Business Impact**

* **Cost-effective**: No hardware required, pay only for what’s used.
* **Secure access**: Only known IPs can connect.
* **Efficient setup**: No manual database installation or configuration needed.
* **Reliable backups**: Data is automatically backed up using **Azure redundancy options**.

---
---
Here's a **comic-style explanation** of how **David** completed his Azure SQL Database task — 
---

### 🎬 Scene 1: The Challenge Begins

Meet **David**, a friendly IT guy at a small college. His boss, **Lisa**, has a big request:
“Can you move our student database to the **cloud**, please?”
David nods, opens his laptop, and logs into the **Azure portal**.

---

### 🏗️ Scene 2: Building the Database

David clicks **Create a resource**, picks **SQL Database**, and names it **StudentDB**.
But wait! Databases need a server. So, he builds a new **SQL Server**, sets up a strong **admin username and password**, and chooses the **East US** region.
Easy peasy!

---

### ⚙️ Scene 3: Making It Work for Everyone

Next, David tweaks the **compute settings** to **Basic** — perfect for their small data load.
He selects **Locally-redundant backup storage** to keep copies safe nearby.
He sets **public access** and adds his computer’s **IP address** to the **firewall**, so he (and teachers) can connect securely.

---

### 🧠 Scene 4: Time for Some Brainpower

David opens the built-in **Query Editor**, logs in using his new credentials, and runs some **SQL scripts**.
He builds tables like **person**, **student**, **course**, and **credit**. Each one stores different pieces of school info.
“Look, the tables showed up! It worked!” he says with a smile.

---

### 🎉 Scene 5: Mission Accomplished

Lisa checks the setup and is thrilled:
“Wow! The database is live, safe, and everyone can use it. Great job!”
David gives himself a little fist bump.
He built a real **cloud-based database** using **Azure SQL Database**, all without touching a single server!

---

### ✅ Final Verdict

Yes, **David** **successfully completed his assigned task**. He used **Azure SQL Database**, set up **secure access**, built **tables** with **SQL**, and ensured the college now has a modern, cloud-ready system.

---
---
## Lab-Based Conceptual MCQs

1. **What is the primary purpose of creating a server-level IP firewall rule in Azure SQL Database?**
   - (a) To restrict access based on subscription
   - (b) To allow client applications to connect to the SQL server from specific IP addresses
   - (c) To encrypt data in transit
   - (d) To prevent internal Azure services from accessing the database  
   **Correct answer: (b)**  
   *Explanation: IP firewall rules allow only specified IP addresses to access the SQL Server, providing a basic level of network security.*

2. **Why should you configure the SQL Database to use ‘Locally-redundant backup storage’?**
   - (a) To replicate data across multiple regions
   - (b) To reduce costs while maintaining availability within the same region
   - (c) To provide geo-redundancy for disaster recovery
   - (d) To increase compute performance  
   **Correct answer: (b)**  
   *Explanation: Locally-redundant storage is a cost-effective option for applications that don’t require geo-redundancy.*

3. **In Azure, what is the purpose of choosing 'Basic' under compute + storage tier for SQL Database?**
   - (a) To enable autoscaling
   - (b) To support high-performance applications
   - (c) To support lightweight workloads with minimal cost
   - (d) To enforce geo-replication  
   **Correct answer: (c)**  
   *Explanation: The Basic tier is intended for smaller, less demanding workloads like development or testing.*

4. **What is the benefit of enabling 'Allow Azure services and resources to access this server' in Networking settings?**
   - (a) It makes the server public to everyone
   - (b) It disables external IP connections
   - (c) It allows trusted Azure services to connect securely
   - (d) It hides the server from all Azure services  
   **Correct answer: (c)**  
   *Explanation: This option allows services hosted in Azure to interact with the SQL server without IP whitelisting.*

5. **Which method is used to connect and manage an Azure SQL database directly through the portal?**
   - (a) SQL Agent
   - (b) Query Editor
   - (c) Azure CLI
   - (d) SSMS  
   **Correct answer: (b)**  
   *Explanation: The built-in Query Editor in the Azure portal enables quick management and querying without additional tools.*

6. **What does the 'Create new server' option during database creation allow you to configure?**
   - (a) Application gateway
   - (b) Virtual network
   - (c) SQL server name, location, and admin credentials
   - (d) Blob storage configuration  
   **Correct answer: (c)**  
   *Explanation: A new server setup includes basic configuration like server name, admin login, and location.*

7. **What is the role of a resource group in Azure when creating services like SQL Database?**
   - (a) It defines a network boundary
   - (b) It acts as a billing unit
   - (c) It groups resources for unified management and lifecycle
   - (d) It replaces the need for a virtual network  
   **Correct answer: (c)**  
   *Explanation: Resource groups allow you to organize and manage resources collectively by lifecycle and permissions.*

8. **Which port must be open to connect to an Azure SQL Server from a client application?**
   - (a) 22
   - (b) 80
   - (c) 1433
   - (d) 3389  
   **Correct answer: (c)**  
   *Explanation: SQL Server uses TCP port 1433 for communication and must be open for external connections.*

9. **When creating a table with a foreign key in SQL, what does it enforce?**
   - (a) Data encryption
   - (b) Indexing strategy
   - (c) Referential integrity between tables
   - (d) Auto backup policies  
   **Correct answer: (c)**  
   *Explanation: Foreign keys link records across tables and ensure consistent relationships in a relational schema.*

10. **Why is it important to check 'Query succeeded' when executing SQL scripts in Azure Query Editor?**
   - (a) To confirm authentication
   - (b) To ensure scripts ran without error
   - (c) To validate your firewall rules
   - (d) To schedule backups  
   **Correct answer: (b)**  
   *Explanation: A 'Query succeeded' message confirms that your SQL script executed as intended without syntax or runtime errors.*

---
---
## Professional Job Interview Questions – AZ-104 Labs

### 1. You are tasked with provisioning a new **Azure SQL Database** for a lightweight internal application. Which configuration would best balance cost and functionality?
(a) Business Critical tier with geo-redundant storage  
(b) **Basic tier with locally-redundant backup storage**  
(c) Hyperscale tier with zone-redundant backup  
(d) Premium tier with multiple read replicas  
**Correct answer: (b)**  
_The Basic tier is appropriate for less demanding workloads, which aligns with internal or development use, and locally-redundant backup provides cost-effective storage._

### 2. A developer needs to access the **SQL Database** from their machine outside Azure. What should you do?
(a) Use a VPN gateway  
(b) Add client IP to server-level firewall rules  
(c) Assign the developer a Reader role  
(d) Enable private endpoint  
**Correct answer: (b)**  
_Enabling the client’s IP via a firewall rule opens port 1433 and permits secure public access to the SQL server._

### 3. You are reviewing the configuration of a newly created SQL database. What setting ensures the database is isolated and not part of a pool?
(a) Use SQL elastic pool  
(b) Set compute to General Purpose  
(c) **Select "No" for elastic pool usage**  
(d) Assign to a managed instance  
**Correct answer: (c)**  
_Selecting "No" ensures the database runs independently without shared resources of an elastic pool._

### 4. A team requests a cost-efficient Azure SQL deployment with minimum resource allocation. Which compute configuration should you use?
(a) Serverless with autoscale  
(b) Premium tier with maximum DTUs  
(c) **Basic tier with 5 DTUs**  
(d) General Purpose with zone redundancy  
**Correct answer: (c)**  
_The Basic tier provides minimal but sufficient performance for development/test environments at the lowest cost._

### 5. A new database admin needs to manage the SQL server but not other Azure resources. What is the most appropriate access model?
(a) Contributor role at the subscription level  
(b) **SQL Authentication with admin credentials**  
(c) Owner role at the resource group level  
(d) Reader role on SQL server  
**Correct answer: (b)**  
_SQL Authentication at the server level allows granular access limited to database management._

### 6. Why is it important to configure the **connectivity method** to Public endpoint when setting up the SQL Database?
(a) Allows internal apps in Azure VNet only  
(b) Enables connection over ExpressRoute  
(c) **Allows connections from outside Azure via internet**  
(d) Limits access to Azure VM only  
**Correct answer: (c)**  
_Configuring a public endpoint is essential when developers or apps outside Azure need access to the database._

### 7. A developer needs to run queries directly from the portal. Which feature should be enabled?
(a) Performance Insights  
(b) Diagnostic Settings  
(c) Advanced Data Security  
(d) **Query Editor**  
**Correct answer: (d)**  
_The built-in Query Editor lets users run and test SQL queries directly in the portal interface._

### 8. You are tasked with ensuring connectivity to the SQL server from external resources. What Azure service configuration is essential?
(a) Azure Monitor  
(b) NSG Inbound Rule  
(c) Private DNS Zone  
(d) **Public network access with firewall rules**  
**Correct answer: (d)**  
_Public access must be explicitly allowed and secured with IP-based firewall rules._

### 9. The engineering team wants to build relational data structures. Which SQL object should you help them create first?
(a) Stored Procedures  
(b) Views  
(c) **Tables**  
(d) Functions  
**Correct answer: (c)**  
_Tables are the foundational database objects where data is stored in a structured format._

### 10. You are asked to set a constraint to avoid duplicate student-course-grade combinations. Which SQL feature will you implement?
(a) Foreign key constraint  
(b) Primary key  
(c) **Unique constraint with clustered index**  
(d) NOT NULL constraint  
**Correct answer: (c)**  
_The unique clustered constraint enforces data integrity by disallowing duplicates across defined columns._

---
---
Here's a light, comic-style summary to help a layman understand the lab in a fun and friendly tone, while still focusing on the **key concepts**:

---

🌤️ **Chapter 1: The Cloudy Mission Begins**

Meet **Alex**, an aspiring Azure Admin. One fine morning, Alex is asked to create a **SQL database** in the **cloud**. “Easy-peasy,” Alex smiles, as he logs in to the **Azure Portal** and clicks on **Create a resource**. The journey begins!

---

🏗️ **Chapter 2: Building the Database Castle**

Alex finds the **SQL Database** tile, names it **WhizDatabase** (just a placeholder, of course), and creates a shiny new **SQL Server** to hold it. He chooses the **Basic** tier because it’s light on the wallet and perfect for testing.

---

🛡️ **Chapter 3: Let the Right People In**

But wait! How will Alex connect to the database? He quickly adds a **firewall rule** to let his computer talk to the server. He also checks the box for **Allow Azure services**, just in case teammates need access too. Smart move!

---

🧠 **Chapter 4: Tables, Please!**

With the doors open, Alex opens the **Query Editor** and types in a spell (well, some **SQL commands**) to create four tables: **Person**, **Student**, **Course**, and **Credit**. “Boom!” — the tables appear. Success!

---

🎓 **Chapter 5: Lesson Learned**

Alex leans back, proud. He’s built a working **Azure SQL Database**, enabled access, and created structured data — just like a real-life cloud admin would in a company setting. And of course, he remembers to **delete all the resources** at the end to save costs.

---

🎉 **The End (But Really, Just the Beginning)**

Alex now understands how to use **Azure SQL**, control **firewall access**, and write basic **SQL scripts** in the portal. With that, he levels up in his journey toward becoming a certified **AZ-104** pro! 🧢💼

---
---

## **Text-Based Diagram for the Lab: Create a SQL Database in Azure**

---

```
+----------------------------+
|  Start Lab (Logged In)    |
+------------+-------------+
             |
             v
+----------------------------+
|  Create SQL Database       |
|  - Choose Resource Group   |
|  - Name: WhizDatabase      |
|  - Create New SQL Server   |
+------------+-------------+
             |
             v
+----------------------------+
| Configure Server Settings  |
|  - Region: East US         |
|  - Authentication: SQL     |
|  - Admin login/password    |
+------------+-------------+
             |
             v
+----------------------------+
| Choose Configuration       |
|  - Basic Tier              |
|  - No Elastic Pool         |
|  - Local Redundancy        |
+------------+-------------+
             |
             v
+----------------------------+
|  Set Networking            |
|  - Public Endpoint         |
+------------+-------------+
             |
             v
+----------------------------+
|  Review & Create Database  |
+------------+-------------+
             |
             v
+----------------------------+
| Add Firewall Rule          |
|  - Allow My IP             |
|  - Allow Azure Services    |
+------------+-------------+
             |
             v
+----------------------------+
|  Connect via Query Editor  |
|  - Enter Admin Password    |
+------------+-------------+
             |
             v
+----------------------------+
|  Create Tables (SQL Query) |
|  - Person                  |
|  - Student                 |
|  - Course                  |
|  - Credit                  |
+------------+-------------+
             |
             v
+----------------------------+
|  View Tables               |
|  - Tables Confirmed        |
+------------+-------------+
             |
             v
+----------------------------+
|  Delete All Resources      |
+----------------------------+
```

---

✅ **Summary for Layman**:
This diagram shows how the user logs in, creates a SQL database, sets up server rules and firewall access, runs SQL code to create tables, and finally deletes everything to clean up. It's a smooth journey from setup to finish — just follow the arrows! 🎯

---
---

