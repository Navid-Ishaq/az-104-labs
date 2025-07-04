# Lab 9: Create an SMB Azure file share and connect it to a Windows VM using the Azure portal

**Duration:** 1h 0m

---
After logging in with your credentials:
---
1. Navigate to **Storage accounts** and select **Create**.

2. Fill in the required details:

   * Enter a unique **Storage account name**.
   * Set **Region** to East US.
   * Choose **Standard** for Performance.
   * Select **Locally redundant storage (LRS)** for Redundancy.

3. Click **Review + create**, then click **Create**.

4. Once deployment completes, go to the **Storage account** resource.

5. Select **File shares** and then click **+ File Share**.

6. Enter the name `qsfileshare`, choose **Transaction optimized** for the tier.

7. Disable backup if enabled.

8. Click **Review + create**, then **Create**.

9. On your local system, create a `.txt` file named `qsTestFile.txt`.

10. Inside the file share, click **Upload**, browse and upload `qsTestFile.txt`.

11. Search for **Virtual machines**, then click **Create** > **Azure Virtual Machine**.

12. Fill in the following:

    * Select the existing **Resource group**.
    * Provide a name and choose **East US** for Region.
    * Use **Windows Server 2019 Datacenter - x64 Gen2** as the image.
    * Select **Standard B2s** for size.
    * Create a **Username** and **Password**.
    * Allow **RDP** and **HTTP** for inbound ports.

13. Under **Disks**, choose **Standard SSD** for OS disk type.

14. Click **Review + create**, then click **Create**.

15. Once deployed, go to the VM resource and click **Connect** > **Download RDP File**.

16. Use the downloaded file to connect via RDP with your configured credentials.

17. Back in the Azure portal, go to your **Storage account** > **qsfileshare** > **Connect**.

18. Select a **Drive letter**, click **Show script**, then copy the script.

19. Paste and run the script in the VM's **PowerShell** to map the drive.

20. Inside the **Storage account**, navigate to the file share and click **Snapshots**.

21. Click **+ Add snapshot** and confirm to create one.

22. In the VM, modify `qsTestFile.txt` by adding text and save it.

23. Return to Azure portal, create another snapshot.

24. To browse a snapshot, go to **Snapshots**, select the first snapshot, and open `qsTestFile.txt`.

25. To restore from a snapshot, in the Snapshots tab, right-click `qsTestFile.txt`, choose **Restore**, and select **Overwrite original file**.

26. In the VM, verify that the original content of the file has been restored.

27. To delete a snapshot:

* Navigate to the **Storage account** > **Settings** > **Locks** and remove any existing locks.
* Go to the file share > **Snapshots**, select the latest snapshot, and click **Delete**.

28. On the VM, open **File Explorer**, go to the mounted share, right-click `qsTestFile.txt`, and select **Properties**.
29. Under **Previous Versions**, view available snapshots and click **Open** to preview.
30. Optionally, select **Restore** to restore the contents from the snapshot to the original location.

Delete all the resources.
---
---

