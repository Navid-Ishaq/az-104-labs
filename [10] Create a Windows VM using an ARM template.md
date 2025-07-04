
**After logging in with your credentials:**

### Step 1: Explore the ARM Template

1. Download the `template.json` file from the provided lab resources and extract it to your local machine.
2. Review the structure of the ARM template. It includes:

   * **Parameters** such as `adminUsername`, `adminPassword`, `dnsLabelPrefix`, and VM configuration options.
   * **Variables** for commonly reused values (e.g., subnet name, virtual network name).
   * **Resources** including a storage account, public IP, network security group (NSG), virtual network (VNet), network interface (NIC), and a virtual machine.
   * **Outputs** to return the public DNS hostname of the deployed VM.

### Step 2: Upload the Template to Cloud Shell

1. Open **Cloud Shell** from the top-right menu in the Azure Portal.
2. Select **Bash** when prompted.
3. If asked to configure storage, select **No storage account required**, and choose the appropriate subscription.
4. Use the **Upload** option in Cloud Shell to upload your `template.json` file into the shell environment.

### Step 3: Deploy the ARM Template

1. Use the following command in Cloud Shell to deploy the template:

   ```bash
   az deployment group create \
     --name <deployment-name> \
     --template-file template.json \
     --parameters '{
       "adminUsername": {"value": "<admin-username>"},
       "adminPassword": {"value": "<admin-password>"}
     }' \
     --resource-group <resource-group-name>
   ```

   Replace the placeholders:

   * `<deployment-name>`: A unique name for this deployment.
   * `<admin-username>`: Your chosen VM administrator username.
   * `<admin-password>`: A strong password (12+ characters) for the VM.
   * `<resource-group-name>`: The name of the target resource group.

2. Wait for the command to complete. This may take several minutes.

### Step 4: Verify Deployment in the Portal

1. In the Azure Portal, navigate to the **Resource groups** blade.
2. Open the resource group used in the deployment.
3. Confirm that resources were successfully created:

   * A Windows virtual machine.
   * Network components such as a NIC, VNet, and NSG.
   * A public IP address.
   * A storage account for diagnostics.

### Step 5: Delete All the Resources

Delete all the resources.

# Lab 10: Create a Windows VM using an ARM template

**Duration:** 30m
```




