# Lab 11: Create a VM with CLI

**Duration:** 30m

_Description will be added soon._

After logging in with your credentials:

### Create a Virtual Machine Using Azure CLI

1. In the Azure Portal, open **Azure Cloud Shell** by selecting the shell icon in the top menu bar.

2. When prompted, choose **Bash**.

3. If required, choose **No storage account required**, select the available subscription, and click **Apply**.

4. Once Cloud Shell initializes, define the administrator credentials securely using variables:

   ```bash
   username="demouser"
   password="YourSecurePassword123"
   ```

5. Create a Windows Server 2019 virtual machine by running the following command. Replace `<resource-group>` with your actual resource group name:

   ```bash
   az vm create \
     --name MyVm \
     --resource-group <resource-group> \
     --image win2019datacenter \
     --size Standard_B1s \
     --admin-username $username \
     --admin-password $password
   ```

   > This command provisions a Windows VM and automatically deploys associated resources such as a virtual network, subnet, public IP, NIC, and network security group.

### Connect to the Virtual Machine via RDP

1. In the Azure Portal, navigate to **Virtual Machines** from the left-hand menu.

2. Select the **MyVm** virtual machine from the list.

3. On the virtual machine's overview page, click **Connect**, then choose **RDP**.

4. Download the **RDP file**, open it, and log in using the previously defined `$username` and `$password`.

   > On Windows: Open the downloaded `.rdp` file and authenticate.
   > On Linux/Mac: Use an RDP client, enter the VM’s public IP, and authenticate with your credentials.

5. Once connected, confirm that the Windows OS boots and is ready for use.

Delete all the resources.


