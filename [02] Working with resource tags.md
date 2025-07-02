# Lab 2: Working with resource tags

**Duration:** 30m

---
---

### 🚀 Azure Lab – Organizing Resources with Tags

**After logging in with your credentials:**

---

### **Task 1: Create a Virtual Machine**

1. In the Azure Portal, go to **Virtual Machines**.
2. Click **+ Create** > **Azure Virtual Machine**.
3. In the **Basics** tab, enter the following:

   * **Resource Group**: Select or create one (e.g., `rg-labresources`)
   * **VM Name**: `resizeVM`
   * **Region**: `East US`
   * **Availability options**: `No infrastructure redundancy required`
   * **Security type**: `Standard`
   * **Image**: `Windows Server 2019 Datacenter - x64 Gen2`
   * **Size**: Click **See all sizes**, select `B1s`, click **Select**
   * **Username**: `LabUser`
   * **Password**: `StrongPassword@123`
4. Leave **Azure Spot Instance** unchecked.
5. Leave **Public inbound ports** as default.
6. Go to the **Disks** tab and select:

   * **OS Disk Type**: `Standard SSD`
7. Click **Review + Create**, then click **Create**.

---

### **Task 2: Apply Tags to the Virtual Machine**

1. In the **Azure Portal**, go to **Resource Groups**.
2. Open your resource group (e.g., `rg-labresources`).
3. Click on the **resizeVM** virtual machine.
4. In the left panel, select **Tags** under Settings.
5. Add a tag with:

   * **Name**: `Department`
   * **Value**: `IT`
6. Click **Apply**.

---

### **Task 3: Filter Resources by Tag**

1. Go to **Resource Groups** again from the Azure menu.
2. Select your resource group.
3. Click **Add filters** on the toolbar.
4. Select the tag **Department**, choose the value `IT`, then click **Apply**.
5. You should now see all resources tagged as `Department = IT`.

---

**Delete all the resources.**

---
---
---
