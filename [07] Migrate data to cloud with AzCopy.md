# Lab 7: Migrate data to cloud with AzCopy

**Duration:** 45m
Certainly! Here's the requested Azure lab as clean, step-by-step instructions in professional, vendor-neutral format:

---

# Azure Lab Instructions: Migrate Data to Cloud with AzCopy

**After logging in with your credentials:**

---

## Step 1: Create a Storage Account

1. In the Azure Portal, search for **Storage accounts** in the top search bar and select it.
2. Click **+ Create**.
3. Under the **Basics** tab:

   * **Resource group**: Select `rg_eastus_XXXXX`
   * **Storage account name**: Enter a globally unique name (e.g., `whizstorage<yourname>`)
   * **Region**: Select `East US`
   * **Performance**: Select `Standard`
   * **Redundancy**: Select `Geo-redundant storage (GRS)`
4. Go to the **Advanced** tab and set **Hierarchical namespace** to **Enabled**.
5. Click **Review + Create**, then click **Create**.
6. Once deployment is complete, select **Go to resource**.
7. From the left menu, choose **Containers** and click **+ Container**.
8. Name the container `democontainer` and click **Create**.

---

## Step 2: Download and Configure AzCopy

1. Download AzCopy from the official link:
   [https://aka.ms/downloadazcopy-v10-windows](https://aka.ms/downloadazcopy-v10-windows)
2. Extract the downloaded ZIP file to a local folder.
3. Open **Command Prompt** and navigate to the extracted folder using:

   ```
   cd <path-to-azcopy-folder>
   ```
4. Authenticate AzCopy with:

   ```
   azcopy login
   ```
5. Open the browser as instructed in the output, enter the given code, and log in.

---

## Step 3: Upload Files to Azure Blob Storage

1. Prepare your local folder with the files you want to upload.
2. Run the following command to copy files recursively:

   ```
   azcopy copy "<local-folder-path>" "https://<storage-account-name>.blob.core.windows.net/<container-name>" --recursive=true
   ```
3. Go back to the Azure Portal and confirm the files appear in the container.

---

## Step 4: Modify and Sync Data for Testing

1. Add or modify a file in your local folder.
2. Run the sync command to update Blob Storage:

   ```
   azcopy sync "<local-folder-path>" "https://<storage-account-name>.blob.core.windows.net/<container-name>" --recursive=true
   ```
3. Confirm the changes in the Azure container.

---

## Step 5: Create a Scheduled Task for Automated Sync

1. Open Notepad and paste the sync command from Step 4, updating the paths as needed.
2. Save the file as `script.bat` (e.g., `C:\script.bat`).
3. Open **Command Prompt as Administrator** and create a scheduled task:

   ```
   schtasks /CREATE /SC minute /MO 5 /TN "AzCopy Script" /TR C:\script.bat
   ```
4. Add a new file to your local folder and wait for the task to run and sync the file.

---

## Step 6: Final Step

**Delete all the resources.**

---


