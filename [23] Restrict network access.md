# Lab 23: Restrict Network Access to PaaS Resources with Virtual Network Service Endpoints

After logging in with your credentials:

## Task 1: Create Virtual Network and Subnets

1. Open the Cloud Shell and select **Bash**.
2. Choose your subscription and click **Apply**.
3. Set a variable for the resource group name:
   ```bash
   resourceGroup="<resource-group-name>"
   ```
4. Create a virtual network named `CoreServicesVNet` with a public subnet:
   ```bash
   az network vnet create --name CoreServicesVNet --resource-group $resourceGroup --location eastus --address-prefix 10.0.0.0/16 --subnet-name Public --subnet-prefix 10.0.0.0/24
   ```
5. Add a private subnet with a service endpoint for Azure Storage:
   ```bash
   az network vnet subnet create --name Private --resource-group $resourceGroup --vnet-name CoreServicesVNet --address-prefix 10.0.1.0/24 --service-endpoints Microsoft.Storage
   ```

## Task 2: Create and Configure Network Security Group (NSG)

1. Create an NSG:
   ```bash
   az network nsg create --name ContosoPrivateNSG --resource-group $resourceGroup --location eastus
   ```
2. Add rule to allow Storage access:
   ```bash
   az network nsg rule create --name Allow-Storage-All --nsg-name ContosoPrivateNSG --priority 100 --resource-group $resourceGroup --access Allow --source-address-prefixes VirtualNetwork --source-port-ranges '*' --destination-address-prefixes Storage --destination-port-ranges '*' --direction Outbound --protocol '*'
   ```
3. Add rule to deny internet access:
   ```bash
   az network nsg rule create --name Deny-Internet-All --nsg-name ContosoPrivateNSG --priority 110 --resource-group $resourceGroup --access Deny --source-address-prefixes VirtualNetwork --source-port-ranges '*' --destination-address-prefixes Internet --destination-port-ranges '*' --direction Outbound --protocol '*'
   ```
4. Add rule to allow RDP access:
   ```bash
   az network nsg rule create --name Allow-RDP-All --nsg-name ContosoPrivateNSG --priority 120 --resource-group $resourceGroup --access Allow --source-address-prefixes '*' --source-port-ranges '*' --destination-address-prefixes VirtualNetwork --destination-port-ranges 3389 --direction Inbound --protocol '*'
   ```
5. Associate NSG with the private subnet:
   ```bash
   az network vnet subnet update --name Private --resource-group $resourceGroup --vnet-name CoreServicesVNet --network-security-group ContosoPrivateNSG
   ```

## Task 3: Create Storage Account and Configure Network Access

1. Set the storage account name:
   ```bash
   storageAccountName="contosostorageXXXX"
   ```
2. Create a storage account:
   ```bash
   az storage account create --name $storageAccountName --resource-group $resourceGroup --location eastus --sku Standard_LRS
   ```
3. Retrieve storage account key:
   ```bash
   az storage account keys list --account-name $storageAccountName --resource-group $resourceGroup --output table
   ```
4. Create a file share named `marketing`:
   ```bash
   az storage share create --name marketing --account-name $storageAccountName --quota 1024
   ```
5. Add a network rule for the private subnet:
   ```bash
   az storage account network-rule add --resource-group $resourceGroup --account-name $storageAccountName --vnet-name CoreServicesVNet --subnet Private
   ```
6. Set the default network access action to Deny:
   ```bash
   az storage account update --name $storageAccountName --resource-group $resourceGroup --default-action Deny
   ```

## Task 4: Deploy Virtual Machines

1. Upload `VMs.json` and `VMs.parameters.json` to Cloud Shell.
2. Deploy the ARM template:
   ```bash
   az deployment group create --resource-group $resourceGroup --template-file vms.json --parameters vms.parameters.json
   ```
3. Enter VM password when prompted.

## Task 5: Confirm Access from Virtual Machines

1. Connect to `ContosoPrivate` VM via RDP.
2. Open PowerShell and map the file share:
   ```powershell
   $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
   $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
   New-PSDrive -Name Z -PSProvider FileSystem -Root "\<storage-account-name>.file.core.windows.net\marketing" -Credential $credential
   ```
3. Verify internet access is blocked:
   ```powershell
   ping google.com
   ```
4. Disconnect and repeat steps for `ContosoPublic` VM. Confirm:
   - Access to file share is denied.
   - Internet access is available.

## Task 6: Browse File Share from Azure Portal

1. In the portal, go to the storage account.
2. Open the `marketing` file share.
3. Select **Browse** and verify access is denied (outside private subnet).

## Task 7: Delete the Resources

1. In Azure Portal, go to **Resource groups**.
2. Select your resource group.
3. Select all resources.
4. Click the **Delete** button.
5. Type `delete` to confirm.

Delete all the resources.
