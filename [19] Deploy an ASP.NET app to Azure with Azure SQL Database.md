# Lab 19: Deploy an ASP.NET app to Azure with Azure SQL Database

**Duration:** 2h 0m

---
---

After logging in with your credentials:

1. **Download and Extract Sample App**

   * Download the sample project ZIP file.
   * Extract it to a local folder on your machine.

2. **Run the ASP.NET App Locally**

   * Open the `.sln` file in Visual Studio.
   * Press `F5` or `Fn+F5` to build and run the app.
   * In the browser, click **Create New** to add sample to-do items.

3. **Publish the App to Azure**

   * In Visual Studio, right-click the project and select **Publish**.
   * Choose **Azure** as the target, then **Azure App Service (Windows)**.
   * Sign in with your Azure credentials if prompted.
   * Click the **+** sign to create a new App Service.

     * Enter a unique app name.
     * Choose the existing resource group.
     * Click **New** next to Hosting Plan, select:

       * Name
       * Region: *East US 2*
       * Size: *B1*
     * Click **OK**, then **Create**.
   * After resources are provisioned, click **Finish**.

4. **Create a SQL Server and Database**

   * In the **Publish** dialog, go to **Service Dependencies**.
   * Next to **SQL Server Database**, click **... > Connect**.
   * Choose **Azure SQL Database**.
   * Click **+ Create new** to provision the database.
   * Click **New** for the SQL Server.

     * Enter a unique server name.
     * Provide an admin username and password.
     * Click **OK**.
   * Click **Create** to provision the database.

5. **Configure the Database Connection**

   * Once the database is created, click **Next**.
   * Enter:

     * Connection string name: *MyDbConnection*
     * Username/password used earlier
   * Ensure **Azure App Settings** is selected.
   * Click **Finish**.

6. **Deploy the App**

   * In the **Publish** tab, click **Publish**.
   * After deployment, the browser will open with the app URL.
   * Add sample to-do items to test the live app.

7. **Access the Database Locally**

   * Open **SQL Server Object Explorer** in Visual Studio.
   * Click **Add SQL Server**.
   * Expand the **Azure** node and select your new database.
   * Enter admin credentials and click **Connect**.
   * When prompted, add your client IP to the SQL firewall.
   * Navigate to **Tables > Todoes**, right-click and choose **View Data**.

8. **Update App with Code First Migrations**

   * Open `Models/Todo.cs` and add a new property:

     ```csharp
     public bool Done { get; set; }
     ```
   * Open **Package Manager Console**, run:

     ```
     Enable-Migrations
     Add-Migration AddProperty
     Update-Database
     ```
   * Update `TodosController.cs`:

     ```csharp
     public ActionResult Create([Bind(Include = "Description,CreatedDate,Done")] Todo todo)
     ```
   * Update `Create.cshtml`, `Index.cshtml` to include the `Done` property using Razor syntax.
   * Save changes and run the app locally to test.

9. **Publish Code First Changes to Azure**

   * Right-click project > **Publish** > **More Actions > Edit**.
   * Under database context settings:

     * Select Azure connection
     * Check **Execute Code First Migrations**
   * Save and publish.
   * Open the app in browser and test the updated functionality.

10. **Enable Log Streaming**

* In the Publish window under **Hosting**, click **... > View Streaming Logs**.
* Observe logs in Visual Studio Output window while the app is running.
* To stop, click **Stop Monitoring**.

Delete all the resources.

---
---

## **Structured Lab Summary: Deploy an ASP.NET App to Azure with Azure SQL Database**

### **Purpose of the Lab**

The primary objective of this lab is to guide learners through the complete process of deploying a web-based **ASP.NET application** to **Azure App Service**, while integrating it with **Azure SQL Database** for persistent data storage. The lab also demonstrates how to perform **Code First Migrations**, configure **firewall settings**, enable **log streaming**, and access the deployed database using **Visual Studio**. This simulates a real-world deployment scenario commonly encountered by cloud administrators and developers.

---

### **Azure Tools Utilized and Their Roles**

1. ### **Azure App Service**

   * **Definition**: A fully managed platform for building, deploying, and scaling web apps.
   * **Role in Lab**: Hosts the deployed **ASP.NET** web application. It abstracts server management and provides a scalable web environment.
   * **Example**: The to-do list app is published to Azure App Service, making it accessible via a public URL.

2. ### **Azure SQL Database**

   * **Definition**: A relational database service built on **SQL Server** engine, offered as a managed service.
   * **Role in Lab**: Stores the to-do list items created in the web application.
   * **Example**: The table `Todoes` stores data like task descriptions and completion status.

3. ### **Visual Studio**

   * **Definition**: An integrated development environment (IDE) used for .NET development.
   * **Role in Lab**: Used to open the solution, edit code, manage dependencies, run migrations, and publish the app to Azure.
   * **Example**: Used to add a new `Done` property to the data model and perform schema updates.

4. ### **Code First Migrations (Entity Framework)**

   * **Definition**: A feature of **Entity Framework** that allows developers to update the database schema using C# code.
   * **Role in Lab**: Enables version-controlled schema changes directly from the model classes.
   * **Example**: A new column `Done` is added to the `Todo` class and applied to the database using `Add-Migration` and `Update-Database`.

5. ### **SQL Server Object Explorer (in Visual Studio)**

   * **Definition**: A tool window in Visual Studio for managing SQL databases.
   * **Role in Lab**: Used to connect to the deployed **Azure SQL Database** and inspect or modify data.
   * **Example**: Used to view the `Todoes` table after adding new tasks from the web UI.

6. ### **Firewall Rules**

   * **Definition**: Security rules that control inbound access to Azure resources.
   * **Role in Lab**: Ensures only authorized IP addresses (like your development machine) can access the Azure SQL Database.
   * **Example**: A rule is created to allow Visual Studio to connect to the SQL database by adding the client’s public IP.

7. ### **Azure Resource Group**

   * **Definition**: A container that holds related resources for an Azure solution.
   * **Role in Lab**: Groups all resources such as App Service, SQL Server, and SQL Database for easier management and deletion.
   * **Example**: All lab-created resources reside under a single resource group to simplify cleanup.

8. ### **Hosting Plan (App Service Plan)**

   * **Definition**: Defines the region, features, and compute resources for an App Service.
   * **Role in Lab**: Determines the pricing tier and performance level of the web application.
   * **Example**: A `B1` plan (1 core, 1.75 GB RAM) is selected during app service creation.

9. ### **Publish Profile in Visual Studio**

   * **Definition**: A configuration file that contains deployment settings for a project.
   * **Role in Lab**: Manages deployment destinations and preferences, including database connections and migration settings.
   * **Example**: The option to "Execute Code First Migrations" is enabled in the publish profile to auto-update the database.

10. ### **Streaming Logs**

* **Definition**: A feature that allows real-time viewing of logs from Azure App Service.
* **Role in Lab**: Helps monitor app behavior, troubleshoot issues, and verify deployments.
* **Example**: Streaming logs are used to confirm app status and track output during deployment.

---

This lab effectively simulates the lifecycle of a cloud application deployment, combining **app hosting**, **data management**, **security**, and **monitoring** — making it a vital hands-on experience for anyone preparing for real-world Azure roles.

---
---

### **Professional Scenario: Deploying a Task Management App to the Cloud**

**Meet Sarah**, a junior cloud developer working for a mid-sized software company that builds productivity tools for clients. Her manager, **Alex**, has assigned her the task of taking their internal **ASP.NET task tracking app**—a to-do list used by team members—and making it available to the whole company over the internet, with reliable **database support**, scalability, and minimal maintenance overhead.

To achieve this, Sarah decides to deploy the application to **Azure App Service** and use **Azure SQL Database** for storing task data. She also plans to use **Code First Migrations** to evolve the database schema as the app grows, and enable **log streaming** for real-time diagnostics.

---

### **Step 1: Prepare the Application Locally**

Sarah first **downloads the source code** for the task app and opens the solution (`DotNetAppSqlDb.sln`) in **Visual Studio**. She runs it locally to verify functionality. After clicking **Create New**, she adds a few to-do tasks like “Update client report” and “Fix login bug” to confirm it works as expected.

🛠️ *This step ensures that the application is functional before deploying it to production. Testing locally helps catch errors early.*

---

### **Step 2: Deploy the Application to Azure**

With the app verified, Sarah right-clicks the project and selects **Publish**. She chooses **Azure App Service (Windows)** as the target platform. She then creates a new **App Service Plan**, selecting a **B1 pricing tier** in **East US 2**, ensuring cost-effective scaling for the team’s expected usage.

💡 ***Azure App Service** provides automatic scaling, built-in load balancing, and easy deployment. This makes it ideal for internal apps without the need for infrastructure management.*

---

### **Step 3: Set Up the SQL Database**

Next, Sarah configures a **SQL Database** to store user tasks. Through the **Publish wizard**, she creates a new **Azure SQL Database** and a new **SQL Server**, defining a unique name, **admin username**, and **password**. She names the database something like `TaskAppDB`.

🛡️ ***Azure SQL Database** is a fully managed relational database. It simplifies backups, patching, and high availability while remaining familiar to developers used to SQL Server.*

---

### **Step 4: Link the Application to the Database**

Sarah configures the **connection string** using the name `MyDbConnection`, which is used by the app’s `DbContext` class. She enters the admin credentials she just created and ensures the connection will be stored in **Azure App Settings** to keep sensitive data secure.

🔗 *This allows the app to securely communicate with the database in the cloud, while keeping configuration clean and separated.*

---

### **Step 5: Publish and Verify the Application**

After linking the app and database, Sarah clicks **Publish**. Visual Studio deploys the app to Azure and opens the browser with the app’s public URL. She adds a few more to-do items to ensure it’s working online.

🎉 *The app is now accessible to any team member with the link. It’s hosted in a secure, scalable environment.*

---

### **Step 6: Access and Inspect the Database**

Sarah wants to verify the data is being saved properly. She opens **SQL Server Object Explorer** in Visual Studio, connects to the new database, and views the `Todoes` table. She can see the same tasks she added via the web app.

🔍 *This helps in troubleshooting and validating database structure and records.*

---

### **Step 7: Add a New Feature with Code First Migrations**

Now, Sarah decides to improve the app by adding a **“Done”** checkbox to mark tasks as completed. She updates the `Todo.cs` model, then uses **Entity Framework Code First Migrations** via the Package Manager Console with commands like:

```bash
Enable-Migrations  
Add-Migration AddDone  
Update-Database
```

She modifies the **Create** and **Index** views to display and toggle the **Done** status.

🚀 *This allows schema evolution without manual database updates, which is safer and more manageable.*

---

### **Step 8: Republish and Apply Migrations in Azure**

To reflect the schema change in the cloud, Sarah republishes the app. In the publish settings, she selects **Execute Code First Migrations**. After deployment, she tests adding tasks and marking them as **Done**, confirming everything works.

🔄 *This ensures that both code and database stay in sync across environments.*

---

### **Step 9: Enable Log Streaming**

To monitor the app’s behavior in real-time, Sarah enables **Streaming Logs** from the Azure App Service. She observes the output in Visual Studio’s console while performing actions in the app.

📈 *Real-time logging helps detect issues quickly and validate backend behavior.*

---

### **Outcome**

Sarah successfully deployed a production-ready **ASP.NET web app** connected to **Azure SQL Database**, added a new feature using **Code First Migrations**, and ensured maintainability with **log streaming**. Her app is now hosted securely, scales as needed, and stores all task data in the cloud.

---

### **Business Relevance**

Sarah’s deployment method saved her company the overhead of managing virtual machines or local databases. Her team now has a **highly available, cloud-native** task manager app with **minimal manual maintenance**, perfect for agile environments.

✅ *This is the exact kind of work expected of certified **Azure Administrators** and **Cloud Developers** in modern enterprises.*

---
---

### ☁️ Comic-Style Summary: "Sarah’s Journey to the Cloud"

👩‍💻 **Meet Sarah**, a junior developer at a growing company. Her boss gives her an exciting mission: “Put our to-do list app on the cloud so the whole team can use it from anywhere!”

---

### 🧳 **Step 1: Get Ready to Fly**

Sarah opens up the **task app project** on her computer using a tool called **Visual Studio**. She clicks "Run" and—boom!—the app opens in her browser. She plays around with it to make sure it works.

📦 "This app looks good. Time to pack it up and send it to the cloud!" she smiles.

---

### 🚀 **Step 2: Launch the App to Azure**

Next, she hits **Publish**, chooses **Azure**, and tells it, “Hey, make me a **web app**!” Azure asks her for a few details like the name and location. She picks **East US 2**, chooses a **budget-friendly hosting plan**, and hits **Create**.

🛠️ Azure builds a cozy new home for her app in the cloud.

---

### 🗃️ **Step 3: Add a Brain – The Database**

But wait! The app needs a place to **store tasks**. Sarah creates a new **Azure SQL Database** and a **SQL Server** to manage it. She sets up a **secure username and password** so no one else can mess with her data.

🔐 "Now my app has a memory!" she thinks proudly.

---

### 🔗 **Step 4: Connect the Dots**

Sarah links her app to the database with a **connection string** called **MyDbConnection**. This tells the app, “Here’s where you save all the to-do items!”

💡 That way, no matter where the app runs, it always knows where to find its data.

---

### 🌐 **Step 5: The Big Moment – Publish**

She hits the **Publish** button again. In seconds, her app is live on the internet with a real web address! She opens it, adds a task, and it works—just like magic.

🎉 “Mission half-complete!” she says.

---

### ⚙️ **Step 6: Make It Smarter**

Sarah wants to add a checkbox to mark tasks as **Done**. She updates the app code, runs a few commands like **Enable-Migrations** and **Update-Database**, and the app’s database structure changes—automatically!

📦 It's like giving the app a new skill without wiping its memory.

---

### 🔁 **Step 7: Send the Upgrade to the Cloud**

She republishes the app with the new checkbox and tells Azure, “Also update the **SQL Database**, please!” Azure does both at once.

Now users can tick off tasks as **Done**, and it even shows up on the homepage!

---

### 🔍 **Step 8: Watch It Live**

To keep an eye on things, Sarah turns on **log streaming**. She can now see live messages about what the app is doing—like a heart monitor for software!

📊 “That’s handy if something goes wrong,” she notes.

---

### 🧹 **Step 9: Clean Up**

Once everything’s working, Sarah deletes all the test resources to avoid any extra costs. She leaves behind a **clean cloud environment**, and a working solution.

---

### ✅ Mission Accomplished!

Sarah finishes the project with a smile. She successfully built, hosted, and updated an app using **Azure App Service**, **Azure SQL Database**, and **Code First Migrations**—all by herself.

💬 Her boss says, “Well done, Sarah! You’ve taken our team’s productivity to the next level.”

---
---

## Lab-Based Conceptual MCQs

**Note:** These questions are based on deploying an **ASP.NET app** with **Azure SQL Database** using **Azure App Service**.

### 1. What is the primary reason for using **Azure App Service** in this lab scenario?
(a) To host containerized applications only  
(b) To deploy and manage scalable web apps without managing infrastructure  
(c) To create desktop applications for local use  
(d) To build mobile apps with local databases  

**Correct answer: (b)**  
**Explanation**: **Azure App Service** provides a fully managed platform for deploying web apps, removing the need to manage servers directly. It's ideal for scalable and reliable web hosting.

---

### 2. Why is it important to create a **SQL Server** before setting up an **Azure SQL Database**?
(a) It automatically scales up database size  
(b) It defines administrative access and network settings for the database  
(c) It acts as a temporary storage for logs  
(d) It is not required and can be skipped  

**Correct answer: (b)**  
**Explanation**: A **SQL Server** in Azure defines the logical container that provides access control and firewall settings for managing one or more **Azure SQL Databases**.

---

### 3. What is the benefit of using **connection strings** in the app configuration?
(a) To configure DNS routing  
(b) To link the app with an external logging service  
(c) To securely define how the app connects to the database  
(d) To enforce server patching policies  

**Correct answer: (c)**  
**Explanation**: A **connection string** provides essential information (such as server, database name, credentials) to establish secure communication between the app and the database.

---

### 4. In the lab, why was the **Code First Migrations** feature used?
(a) To manually export and import database schemas  
(b) To create a new UI for the app  
(c) To update the **database schema** automatically based on code changes  
(d) To improve Visual Studio performance  

**Correct answer: (c)**  
**Explanation**: **Code First Migrations** enables schema changes in the database directly from the code, keeping application and database models in sync.

---

### 5. What role does **Visual Studio** play in this deployment process?
(a) Acts as a cloud hosting platform  
(b) Provides command-line access to virtual machines  
(c) Serves as an integrated development environment for building, testing, and deploying apps  
(d) Manages Azure subscriptions  

**Correct answer: (c)**  
**Explanation**: **Visual Studio** supports end-to-end development and deployment of apps to **Azure**, integrating tools for database management, publishing, and code editing.

---

### 6. Why was it necessary to **open a firewall rule** for the SQL Server?
(a) To enable SSH to virtual machines  
(b) To access the database locally from the development machine  
(c) To expose the web app publicly  
(d) To migrate the server to another region  

**Correct answer: (b)**  
**Explanation**: By default, **Azure SQL Server** only allows connections from specific IPs. Opening a **firewall rule** allows the developer to access the database from their local machine.

---

### 7. How does the **App Service Hosting Plan** affect your application?
(a) It sets up a virtual desktop environment  
(b) It controls the region, performance tier, and scalability of your web app  
(c) It adds extra disk space to your database  
(d) It generates default connection strings for you  

**Correct answer: (b)**  
**Explanation**: The **Hosting Plan** defines how much memory, CPU, and bandwidth your **App Service** gets, as well as its geographical location.

---

### 8. What does enabling **log streaming** allow during app runtime?
(a) Displays Azure billing details in the app  
(b) Tracks real-time activity and issues in the application  
(c) Sends user data to external applications  
(d) Encrypts database connection automatically  

**Correct answer: (b)**  
**Explanation**: **Log streaming** lets developers see live logs from their **App Service**, which helps in identifying runtime issues or application errors instantly.

---

### 9. If the **connection string name** doesn’t match the code reference, what is likely to happen?
(a) The app will switch to offline mode  
(b) The app will store data locally instead  
(c) The app will fail to connect to the database at runtime  
(d) Azure will automatically correct it  

**Correct answer: (c)**  
**Explanation**: The name of the **connection string** in the app settings must match the code reference (e.g., `MyDbConnection`) or the app cannot locate and connect to the database.

---

### 10. What is the main advantage of using **Code First Migrations in Azure**?
(a) It provides a GUI to back up databases  
(b) It enables schema updates during deployment without affecting data  
(c) It exports logs to Azure Blob Storage  
(d) It isolates the database from application updates  

**Correct answer: (b)**  
**Explanation**: **Code First Migrations** in **Azure** allows you to safely update your database schema with code changes while retaining all existing data.

---
---

## Professional Job Interview Questions – AZ-104 Labs

**Note:** All key Azure concepts and tools are consistently formatted in **bold** for clarity.

### 1. A company is migrating a legacy application to Azure and wants to deploy it with minimal configuration overhead. They also need built-in load balancing and automatic scaling. What is the best choice for deployment?

(a) **Azure Virtual Machine**  
(b) **Azure App Service**  
(c) **Azure Kubernetes Service**  
(d) **Azure Functions**

**Correct answer: (b)**  
**Explanation:** **Azure App Service** provides a fully managed platform for building, deploying, and scaling web applications. It supports autoscaling and integrates easily with deployment pipelines.

---

### 2. An administrator needs to ensure a secure connection between their on-premises SQL Server and Azure App Service without exposing the database to the public internet. Which service should they configure?

(a) **Azure Bastion**  
(b) **Point-to-Site VPN**  
(c) **Private Endpoint**  
(d) **Load Balancer**

**Correct answer: (c)**  
**Explanation:** A **Private Endpoint** allows access to services over a private IP in the virtual network, securing communication without traversing the public internet.

---

### 3. After deploying a web app to Azure, the operations team needs to monitor live application logs to debug a startup issue. Which feature should they use?

(a) **Application Insights**  
(b) **Log Analytics Workspace**  
(c) **Log Streaming**  
(d) **Azure Monitor Alerts**

**Correct answer: (c)**  
**Explanation:** **Log Streaming** allows real-time viewing of app logs from an **Azure App Service**, which is ideal for immediate diagnostics.

---

### 4. A team wants to automate schema changes and updates to their Azure SQL Database alongside app deployments. What is the recommended approach?

(a) Use **SQL Management Studio** after publishing the app  
(b) Manually update the schema using a migration script  
(c) Use **Code First Migrations** with **Entity Framework**  
(d) Backup the database and redeploy it with changes

**Correct answer: (c)**  
**Explanation:** **Code First Migrations** is part of **Entity Framework** and allows schema updates to be deployed with the application code.

---

### 5. A developer accidentally exposed the SQL admin credentials in application logs. What should be the first response?

(a) Delete the database  
(b) Regenerate the SQL server  
(c) Rotate the credentials and update the connection strings  
(d) Reboot the web app

**Correct answer: (c)**  
**Explanation:** Rotating credentials ensures compromised credentials are invalidated and updating the connection strings maintains app continuity.

---

### 6. An organization is running its production ASP.NET app on **Azure App Service**. They want to ensure high availability and handle traffic across different regions. What should be configured?

(a) **Traffic Manager**  
(b) **Load Balancer**  
(c) **Availability Zones**  
(d) **Virtual Machine Scale Set**

**Correct answer: (a)**  
**Explanation:** **Traffic Manager** allows geographic routing and high availability by directing traffic based on rules to multiple **App Services** in different regions.

---

### 7. A new feature in an ASP.NET app requires an additional column in the SQL database. How can the update be applied with minimal manual intervention?

(a) Edit the table directly in SQL Server  
(b) Create a new table with the changes  
(c) Use **EF Migrations** and redeploy the app  
(d) Restore an older database backup with schema changes

**Correct answer: (c)**  
**Explanation:** **EF Migrations** supports evolving the database schema through version-controlled code changes and integrates well into CI/CD pipelines.

---

### 8. The database connection from an app hosted in **Azure App Service** is failing due to firewall issues. What should the administrator check first?

(a) Whether **App Insights** is enabled  
(b) If the database allows Azure services to connect  
(c) The number of retries in the connection string  
(d) The app region and hosting plan

**Correct answer: (b)**  
**Explanation:** Azure SQL databases have a firewall setting to allow or deny connections from **Azure services** like **App Service**. This must be enabled for connectivity.

---

### 9. A team wants to reduce cost while running a low-traffic ASP.NET app in Azure. Which configuration would best support this?

(a) Change app to **Isolated Plan**  
(b) Switch to a **Consumption Plan**  
(c) Move to **Basic (B1) App Service Plan**  
(d) Enable **Availability Zones**

**Correct answer: (c)**  
**Explanation:** The **Basic (B1)** plan offers a cost-effective shared compute option for low to moderate traffic apps, with basic features and no autoscaling.

---

### 10. After successful deployment, a developer needs to view and query the Azure SQL database to confirm the schema. Which tool should they use?

(a) **Azure Monitor**  
(b) **SQL Server Object Explorer in Visual Studio**  
(c) **Azure Key Vault**  
(d) **App Configuration**

**Correct answer: (b)**  
**Explanation:** **SQL Server Object Explorer** in **Visual Studio** allows developers to browse and manage **Azure SQL Databases**, making it ideal for confirming schema and structure.

---
---

🎬 **Scene 1: Meet Emma, the Junior Developer**
Emma just joined a startup and got her first cloud assignment: deploy an **ASP.NET web app** using **Azure App Service** and connect it to an **Azure SQL Database**. She looks at the task and says, “Okay, cloud... let’s do this!”

---

💻 **Scene 2: Downloading & Running the App**
Emma downloads the sample project and opens it in **Visual Studio**. She hits **F5** and tada! A to-do list app shows up in her browser. She adds a few test tasks and says, “Nice! Now let’s get this live.”

---

🚀 **Scene 3: Time to Publish the App**
She right-clicks on the project and chooses **Publish**. She picks **Azure App Service**, sets up a **hosting plan**, and lets Azure do its magic. Emma says, “This is like sending my app on a vacation to the cloud!”

---

🗄️ **Scene 4: Adding the Database**
Next, Emma needs to store the tasks. She creates a new **Azure SQL Database**, sets up a **logical server**, and connects it to her app with a **connection string**. “Now my app can remember stuff,” she grins.

---

🧠 **Scene 5: Making the App Smarter**
Emma wants to track which tasks are completed. So she edits the code, adds a **Done** checkbox, and uses **Code First Migrations** to update the **database schema**. One command at a time, she reshapes the backend like a pro!

---

🌐 **Scene 6: Deploy and Test Again**
Emma republishes the updated app. It now shows checkboxes to mark tasks as **Done**, and everything is stored in the **cloud database**. She adds some new to-dos and checks them off happily.

---

🔍 **Scene 7: Watching the Logs**
Curious about how the app runs, Emma turns on **log streaming** in **Visual Studio**. She watches live messages pop up and says, “Wow, it’s like chatting with my app!”

---

🧹 **Final Scene: Clean Up Time**
After everything is working perfectly, Emma deletes all the **resources** from her **resource group** to avoid charges. She smiles and thinks, “Mission complete. I just clouded like a boss!”

---

✅ **Lesson: Cloud Isn’t Scary**
Emma’s journey shows that using **Azure App Service**, **SQL Database**, and **Visual Studio** makes cloud deployment manageable—even fun. With a few clicks and a bit of code, anyone can take their app from laptop to live!

---
---
