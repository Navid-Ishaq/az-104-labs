# Lab 7: Migrate data to cloud with AzCopy

**Duration:** 45m

```markdown
# Azure Lab Instructions: Migrate Data to Cloud with AzCopy

After logging in with your credentials:

## Step 1: Create a Storage Account

1. In the Azure Portal, use the top search bar to search for **Storage accounts** and select it.
2. Click on **+ Create**.
3. Under the **Basics** tab:
   - **Resource group**: Select `rg_eastus_XXXXX`.
   - **Storage account name**: Enter a globally unique name, such as `whizstorage<yourname>`.
   - **Region**: Select `East US`.
   - **Performance**: Select `Standard`.
   - **Redundancy**: Select `Geo-redundant storage (GRS)`.

4. Switch to the **Advanced** tab:
   - Set **Hierarchical namespace** to **Enabled**.

5. Click **Review + Create**, then click **Create**.

6. Once the deployment is complete, click **Go to resource**.
7. From the left-hand menu, select **Containers**, then click **+ Container**.
8. In the **New container** panel:
   - **Name**: Enter `democontainer`.
   - Click **Create**.

## Step 2: Install and Configure AzCopy

1. Download AzCopy from [https://aka.ms/downloadazcopy-v10-windows](https://aka.ms/downloadazcopy-v10-windows).
2. Extract the downloaded `.zip` file.
3. Open the **Command Prompt** and navigate to the extracted AzCopy folder:
```

cd <path-to-azcopy-folder>

```
4. Run the following command to log in:
```

azcopy login

```
5. Follow the instructions in the command output: open the login URL in your browser and enter the provided code.
6. After login is successful, return to the Command Prompt and confirm the **Login succeeded** message.

## Step 3: Upload Data to Azure Blob Storage Using AzCopy

1. Use the following command to upload all files from your local folder to the Blob container:
```

azcopy copy "<local-folder-path>" "https\://<storage-account-name>.blob.core.windows.net/<container-name>" --recursive=true

```
2. Go to your Azure Portal, open your storage account, navigate to **Containers**, and verify the files have been uploaded.

## Step 4: Modify and Sync Data

1. Modify or add a new file to your local source directory.
2. Use the following command to sync new or updated files to the Blob container:
```

azcopy sync "<local-folder-path>" "https\://<storage-account-name>.blob.core.windows.net/<container-name>" --recursive=true

```
3. Verify that the new or modified file appears in the Azure container.

## Step 5: Schedule a Recurring AzCopy Task

1. Open a text editor (like Notepad) and enter the AzCopy sync command with appropriate paths and account/container values.
2. Save the file as `script.bat`.

Example contents:
```

azcopy sync "C:\Your\Local\Folder" "https\://<storage-account-name>.blob.core.windows.net/<container-name>" --recursive=true

```

3. Open **Command Prompt** as Administrator and run the following command to create a scheduled task:
```

schtasks /CREATE /SC minute /MO 5 /TN "AzCopy Script" /TR C:\script.bat

```

4. Add or change files in the local folder to test the scheduled sync functionality.

## Final Step

Delete all the resources.
```
