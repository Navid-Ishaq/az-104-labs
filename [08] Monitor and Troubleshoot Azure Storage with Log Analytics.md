# Lab 8: Monitor and Troubleshoot Azure Storage with Log Analytics

**Duration:** 1h 0m
---
**After logging in with your credentials:**

### 1. Create a Storage Account

1. In the portal search bar, enter **Storage accounts** and select it.
2. Click **Create**.
3. In the **Basics** tab:

   * Choose the available **Subscription**.
   * Select the available **Resource group**.
   * Enter a unique **Storage account name** (lowercase letters and numbers only).
   * Choose the default **Region**.
   * Set **Performance** to **Standard**.
   * Set **Redundancy** to **Geo-redundant storage (GRS)**.
4. Go to the **Advanced** tab and ensure the **Access tier** is set to **Hot**.
5. Click **Review + create**, then **Create**.
6. Once deployment completes, select **Go to resource**.

---

### 2. Add a Blob Container

1. In the storage account, under **Data storage**, select **Containers**.
2. Click **+ Container**.
3. Name the container **monitor-blobs-container**.
4. Leave other settings at default and click **Create**.

---

### 3. Upload Files to the Blob Container

1. On your local computer, create three text files:

   * `sample1.txt`:

     ```
     Sample File 1 - Blob Monitoring Test  
     This is a test file for upload.
     ```
   * `sample2.txt`:

     ```
     Sample File 2 - Blob Monitoring Test  
     This is another test file for upload.
     ```
   * `sample3.txt`:

     ```
     SampleFile3-BlobMonitoringTest  
     This is another test file for upload.
     ```
2. In the Azure portal, return to **monitor-blobs-container**.
3. Click **Upload** and upload `sample1.txt`.
4. Wait 1 minute, then upload `sample2.txt`.
5. Wait another minute, then upload `sample3.txt`.
6. Wait a few additional minutes to ensure metrics are recorded.

---

### 4. Create a Log Analytics Workspace

1. Search for and select **Log Analytics workspaces**.
2. Click **+ Create**.
3. In the **Basics** tab:

   * Choose the same **Subscription** and **Resource group**.
   * Enter a name like **MonitorLAWorkspace**.
   * Use the default **Region**.
4. Click **Review + create**, then **Create**.

---

### 5. Create a Diagnostic Setting for the Storage Account

1. Open your **Storage account**.
2. Under **Monitoring**, click **Diagnostic settings**.
3. Select the **blob** service if prompted.
4. Click **+ Add diagnostic setting**.
5. Provide a name (e.g., `BlobStorageDiagnostics`).
6. Under **Categories**, select **StorageRead**.
7. Under **Destination**, select **Send to Log Analytics workspace** and choose **MonitorLAWorkspace**.
8. Click **Save**.

---

### 6. Download a Blob to Generate Activity

1. Open **Containers** in the storage account.
2. Select **monitor-blobs-container**.
3. Locate one of the uploaded files.
4. Click the **ellipsis (...)** next to the file and choose **Download**.

---

### 7. View Logged Activity with Log Analytics

1. In the storage account, under **Monitoring**, click **Logs**.
2. Close the **Queries hub**.
3. Switch to **KQL mode**.
4. Paste the following query:

   ```kusto
   StorageBlobLogs
   | where TimeGenerated > ago(1h) and OperationName == "GetBlob"
   | project TimeGenerated, AuthenticationType, RequesterObjectId, OperationName, Uri
   ```
5. Click **Run**.
6. View the results to confirm that the download was logged.

---

**Delete all the resources.**

---

