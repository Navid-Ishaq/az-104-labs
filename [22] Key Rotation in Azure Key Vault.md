# Key Rotation in Azure Key Vault

After logging in with your credentials:

## Task 1: Create a Key Vault

1. In the Azure portal, select **+ Create a resource**.
2. In the **Search the Marketplace** box, search for **Key Vault**.
3. Click **Create** under the Key Vault option.
4. In the **Basics** tab, provide the following information:
   - **Resource group**: Select `rg_eastus_XXXXX`
   - **Key vault name**: Enter `whizkey`
   - **Region**: Select `East US`
   - **Pricing tier**: Select `Standard`
   - **Days to retain deleted vaults**: Enter `90`
5. Click **Next**.
6. Under **Permission model**, select **Vault access policy**.
7. Under **Access policies**, select the appropriate username.
8. Leave other settings as default.
9. Click **Review + Create**, then click **Create**.

## Task 2: Create a Key in the Key Vault

1. After the Key Vault is created, click **Go to resource**.
2. In the left-hand menu, select **Keys** under the **Settings** section.
3. Click **+ Generate/Import** to create a new key.
4. In the **Create a key** panel, enter the following:
   - **Options**: Select `Generate`
   - **Name**: Enter `demokey`
   - **Key type**: Select `RSA`
   - **RSA key size**: Select `2048`
   - Leave other fields as default.
5. Click **Create**.

## Task 3: Configure the Key Rotation Policy

1. In the list of keys, click on `demokey`.
2. Select **Rotation policy**.
3. In the **Rotation policy** section, provide the following:
   - **Expiry date**: Enter `1 month`
   - **Enable auto rotation**: Select `Enabled`
   - **Rotation option**: Select `Automatically renew at a given time after creation`
   - **Rotation time**: Enter `18 days`
   - Leave other settings as default.
4. Click **Save**.

## Task 4: Delete the Resources

1. In the Azure portal search bar, type **Resource groups** and select it from the results.
2. Click the name of the relevant resource group (`rg_eastus_XXXXX`).
3. Select all resources listed within the group.
4. Click the **three dots** menu and choose **Delete**.
5. Type `delete` in the confirmation box.
6. Click **Delete** to confirm.

Delete all the resources.
