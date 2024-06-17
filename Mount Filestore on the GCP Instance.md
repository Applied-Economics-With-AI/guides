# Mount Filestore on the GCP Instance

This guide explains how to automatically mount a Filestore on a Google Cloud Platform (GCP) instance using a startup script. By following these steps, you will ensure that the Filestore is mounted each time the instance starts, providing persistent and reliable access to your storage

---

## Step 1: Prepare Your Environment

### **1.1 Login to Google Cloud Console**

Navigate to [Google Cloud](https://cloud.google.com/) and log in with your Gmail account.

### **1.2 SSH into Your GCP Instance**:

- Go to **Compute Engine** > **VM instances**.
- Click on the **SSH** button next to your instance to open a browser-based SSH session.

<aside>

![Alt text](GCVM_setup/images/SSH_position.png)

</aside>

---

## Step 2: Install Necessary Utilities

Install the necessary NFS utilities on your instance:

```bash
sudo apt-get update
sudo apt-get install -y nfs-common
```

---

## Step 3: Create the Mount Directory

Create a directory where the Filestore will be mounted. For example, to create a directory called `/aeai-filestore`, use the following command:

```bash
sudo mkdir -p /test-filestore
```

Replace `/test-filestore` with the directory where you want to mount the Filestore.

---

## Step 4: Add the Startup Script to Automatically Mount Filestore

### **4.1 Edit Your Instance**:

- In the Google Cloud Console, go to **Compute Engine** > **VM instances**.
- Select your instance and click **Edit**.

<aside>


![Alt text](GCVM_setup/images/edit_position.png)

</aside>

### **4.2 Add the Startup Script**:

- Scroll down to the **Automation** section.
- In the **Startup script** field, enter the following script:
    
    For example, if your Filestore IP is `10.184.138.132`, your Filestore volume is `/test_fs_vol`, and your mount directory is `/test-filestore`, the script would be:
    
    ```bash
    #!/bin/bash
    sudo mount 10.184.138.132:/test_fs_vol /test-filestore
    ```
    

<aside>

![Alt text](GCVM_setup/images/startup_script.png)

</aside>

- Replace `/test-filestore` with the directory where you want to mount the Filestore.
- Replace `10.184.138.132` with the IP address of your Filestore.
- Replace `/test_fs_vol` with the path to your Filestore volume.

### **4.3 Save the Configuration**:

- Scroll down and click **Save** to apply the changes.

### **4.4 Restart Your Instance**:

- After saving the configuration, restart your instance to ensure the startup script runs and mounts the Filestore.

---

## Step 5: Verify the Mount

After your instance restarts, verify that the Filestore is correctly mounted.

### **5.1 SSH into Your Instance** (if not already done):

Identical to **1.2** 

### **5.2 Check if the Filestore is Mounted**:

```bash
df -h /test-filestore
```

You should see information about the Filestore, confirming it is mounted correctly at `/test-filestore`.

---

## Troubleshooting

- **Manual Mounting**:
If the Filestore is not mounted, you can manually mount it to check for errors:
    
    ```bash
    sudo mount 10.184.138.132:/test_fs_vol /test-filestore
    ```
    

- **Check Startup Script Logs**:
If there are issues, check the startup script logs to diagnose the problem:
    
    ```bash
    sudo journalctl -u google-startup-scripts.service
    ```
    

---

## Step 6 (Optional): Open the File Explorer in VS Code

### **6.1 Connect to the VM**

- Press `Ctrl` + `Shift` + `P` and select "Remote-SSH: Connect to Host"
- Choose the configured host
- Select "Linux" as the system type and continue (may not be required to choose system type in Mac)

### **6.2 Access the File Explorer**:

- Once connected to your GCP instance, look for the File Explorer icon on the left side of the VS Code window. It looks like a folder. Click this icon and the ‘Open Folder button’ to open the File Explorer.

### **6.2 Navigate to the Mounted Directory**:

- In the File Explorer, navigate to the directory where you mounted the Filestore. This should be `/test-filestore` (or the directory you specified).
- If you don't see the directory immediately, you may need to open the root directory (`/`) and navigate through the file system to find `/test-filestore`.

<aside>


![Alt text](GCVM_setup/images/navigate_files.png)

</aside>

### **6.3 Interacting with Files**:

- You can now open, edit, create, and delete files in the Filestore directory directly from VS Code.

---

By following this guide, your GCP instance will automatically mount the Filestore every time it starts up, ensuring that the storage is available without manually mounting it each time.

---
