# Lab 24: Creating a Private Endpoint Using an ARM Template

After logging in with your credentials:

## Task 1: Explore the ARM Template

1. Download and extract the ARM template ZIP file.
2. Locate the `template.json` file for deployment.
3. Review the ARM template structure and understand its defined parameters, variables, and resources, which include:
   - SQL Server and Database
   - Virtual Network and Subnet
   - Private Endpoint and Private DNS Zone
   - Virtual Machine and related networking components

## Task 2: Deploy the ARM Template

1. Open the Azure Cloud Shell and select the **Bash** environment.
2. Select your subscription and click **Apply**.
3. Upload the `template.json` file using the **Manage files** > **Upload** option.
4. Deploy the ARM template using the following command (replace placeholders with actual values):
   ```bash
   az deployment group create \
     --name <deployment-name> \
     --resource-group <resource-group-name> \
     --template-file <path-to-template-file> \
     --parameters \
       sqlAdministratorLogin=<sql-username> \
       sqlAdministratorLoginPassword=<sql-password> \
       vmAdminUsername=<vm-username> \
       vmAdminPassword=<vm-password> \
       location=eastus
   ```

## Task 3: Test the Private Endpoint

1. After deployment completes, go to your resource group in the Azure portal to confirm deployment of the private endpoint.
2. Navigate to the virtual machine, select **Connect**, and download the RDP file.
3. Open the RDP file and connect using the credentials specified during deployment.
4. On the VM:
   - Disable Internet Explorer Enhanced Security Configuration.
   - Open PowerShell and run:
     ```powershell
     nslookup <your-sql-server-name>.database.windows.net
     ```
     Replace `<your-sql-server-name>` with your actual SQL server name.
5. Open Internet Explorer and download SQL Server Management Studio from:
   ```
   https://aka.ms/ssmsfullsetup
   ```
6. Install SSMS using default options.
7. Open SSMS and connect using the following:
   - **Server type**: Database Engine
   - **Server name**: `<your-sql-server-name>.database.windows.net`
   - **Authentication**: SQL Server Authentication
     - **Login**: SQL administrator username used in deployment
     - **Password**: SQL administrator password used in deployment
8. Once connected, verify the presence of the `sample-db` database.

## Task 4: Delete the Resources

1. In the Azure portal, go to **Resource groups**.
2. Select your resource group.
3. Select all resources.
4. Click the **Delete** button.
5. Type `delete` to confirm.

Delete all the resources.
