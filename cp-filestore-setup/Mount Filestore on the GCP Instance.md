# Mount Filestore on the GCP Instance

This guide explains how to automatically mount a [Google Cloud Filestore](https://cloud.google.com/filestore) on a Google Cloud Platform (GCP) instance using a startup script. By following these steps, you will ensure that the Filestore is mounted each time the instance starts, providing persistent and reliable access to your shared storage.

**Author:** [Peter John Lambert](mailto:p.j.lambert@lse.ac.uk), London School of Economics

---

## Prerequisites

Before following this guide, ensure you have:

- ✅ A Google Cloud account with billing enabled
- ✅ A running GCP VM instance (see our [Setting Up a Google Cloud VM guide](../google-cloud-vm-setup/Setting%20Up%20a%20Google%20Cloud%20VM%20with%20VSCode.md) if you need to set one up)
- ✅ A [Google Cloud Filestore instance](https://cloud.google.com/filestore/docs/creating-instances) already created in your project
- ✅ Your Filestore IP address and volume name (found in the [Google Cloud Console](https://console.cloud.google.com/) under **Filestore > Instances**)

> **💡 What is Google Cloud Filestore?**
> 
> Filestore is a managed file storage service for applications that require a filesystem interface and a shared filesystem for data. It's ideal for workloads that require shared storage between multiple VM instances, such as collaborative research projects or large dataset storage.

---

## Step 1: Prepare Your Environment

### **1.1 Login to Google Cloud Console**

Navigate to [Google Cloud Console](https://console.cloud.google.com/) and log in with your Google account.

### **1.2 SSH into Your GCP Instance**

- Go to **Compute Engine** > **VM instances**.
- Click on the **SSH** button next to your instance to open a browser-based SSH session.

  <img width="1047" alt="SSH_position" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/870527e2-01a4-4782-b17d-6789760e719d">

> **💡 Tip:** You can also connect via VSCode using the Remote-SSH extension if you've already configured it (see [our VM setup guide](../google-cloud-vm-setup/Setting%20Up%20a%20Google%20Cloud%20VM%20with%20VSCode.md)).

---

## Step 2: Install Necessary Utilities

Install the NFS (Network File System) utilities required for mounting network storage:

```bash
sudo apt-get update
sudo apt-get install -y nfs-common
```

> **📚 Learn more:** [NFS Documentation](https://wiki.linux-nfs.org/wiki/index.php/Main_Page) | [Ubuntu NFS Guide](https://ubuntu.com/server/docs/service-nfs)

---

## Step 3: Create the Mount Directory

Create a directory where the Filestore will be mounted. For example, to create a directory called `/aeai-filestore`:

```bash
sudo mkdir -p /aeai-filestore
```

> **⚠️ Note:** Replace `/aeai-filestore` with your preferred directory name. Common conventions include:
> - `/mnt/filestore` - standard mount point location
> - `/data` - for data-heavy workloads
> - `/shared` - for collaborative projects

---

## Step 4: Add the Startup Script to Automatically Mount Filestore

To ensure your Filestore is automatically mounted every time your VM starts, we'll add a startup script.

### **4.1 Edit Your Instance**

- In the [Google Cloud Console](https://console.cloud.google.com/), go to **Compute Engine** > **VM instances**.
- Select your instance and click **Edit**.

  <img width="900" alt="edit_position" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/fdc55c91-3429-432f-86fe-d9bee94db450">

### **4.2 Add the Startup Script**

- Scroll down to the **Automation** section.
- In the **Startup script** field, enter a mount command in the following format:

```bash
#!/bin/bash
sudo mount <FILESTORE_IP>:/<VOLUME_NAME> /<MOUNT_DIRECTORY>
```

For example, if your Filestore IP is `10.184.138.132`, your Filestore volume is `/test_fs_vol`, and your mount directory is `/aeai-filestore`, the script would be:

```bash
#!/bin/bash
sudo mount 10.184.138.132:/test_fs_vol /aeai-filestore
```

  <img width="900" alt="startup_script" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/9b4c892c-6951-4d71-a7f5-90ce0bc70ddc">

> **⚠️ Important:** Replace the values with your own:
> - `10.184.138.132` → Your Filestore IP address
> - `/test_fs_vol` → Your Filestore volume name
> - `/aeai-filestore` → Your chosen mount directory

### **4.3 Save the Configuration**

- Scroll down and click **Save** to apply the changes.

### **4.4 Restart Your Instance**

- After saving the configuration, restart your instance to ensure the startup script runs and mounts the Filestore.

> **📚 Learn more:** [GCP Startup Scripts Documentation](https://cloud.google.com/compute/docs/instances/startup-scripts)

---

## Step 5: Verify the Mount

After your instance restarts, verify that the Filestore is correctly mounted.

### **5.1 SSH into Your Instance**

Follow the same steps as **Step 1.2** to SSH into your instance.

### **5.2 Check if the Filestore is Mounted**

```bash
df -h /aeai-filestore
```

You should see output similar to:

```
Filesystem                        Size  Used Avail Use% Mounted on
10.184.138.132:/test_fs_vol       1.0T   50G  950G   5% /aeai-filestore
```

This confirms the Filestore is mounted correctly. You can also verify with:

```bash
mount | grep nfs
```

---

## Troubleshooting

### **Manual Mounting**

If the Filestore is not mounted after restart, try mounting it manually to check for errors:

```bash
sudo mount 10.184.138.132:/test_fs_vol /aeai-filestore
```

### **Check Startup Script Logs**

If there are issues with automatic mounting, check the startup script logs:

```bash
sudo journalctl -u google-startup-scripts.service
```

### **Common Issues**

| Issue | Possible Cause | Solution |
|-------|---------------|----------|
| `mount.nfs: Connection timed out` | Firewall blocking NFS traffic | Ensure your VPC firewall allows NFS traffic (port 2049) |
| `mount.nfs: access denied` | Incorrect permissions | Verify your Filestore access permissions in GCP Console |
| `mount point does not exist` | Directory not created | Run `sudo mkdir -p /your-mount-directory` |
| `mount.nfs: No such device` | NFS utilities not installed | Run `sudo apt-get install -y nfs-common` |

> **📚 Learn more:** [Filestore Troubleshooting Guide](https://cloud.google.com/filestore/docs/troubleshooting)

---

## Step 6 (Optional): Access Files via VS Code

### **6.1 Connect to the VM**

- Press `Ctrl + Shift + P` (Windows) or `Cmd + Shift + P` (Mac) and select "Remote-SSH: Connect to Host"
- Choose the configured host
- Select "Linux" as the system type and continue (may not be required on Mac)

### **6.2 Access the File Explorer**

- Once connected to your GCP instance, click the **File Explorer** icon on the left sidebar (folder icon)
- Click **Open Folder** to open the File Explorer

### **6.3 Navigate to the Mounted Directory**

- In the File Explorer, navigate to the directory where you mounted the Filestore (e.g., `/aeai-filestore`)
- If you don't see the directory immediately, open the root directory (`/`) and navigate through the file system

  <img width="1096" alt="navigate_files" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/b1e3ae65-58fa-47bd-8f90-4c0e8a6ce173">

### **6.4 Interacting with Files**

You can now open, edit, create, and delete files in the Filestore directory directly from VS Code. Changes made here will be available to all VM instances that mount the same Filestore.

---

## Security Considerations

When using shared storage, keep these security best practices in mind:

- **Access Control:** Filestore uses VPC network-based access control. Only VMs in the same VPC (or peered VPCs) can access the Filestore by default.
- **Sensitive Data:** Be cautious about storing sensitive data on shared storage. Consider using [Customer-Managed Encryption Keys (CMEK)](https://cloud.google.com/filestore/docs/cmek) for additional security.
- **Permissions:** Use appropriate Linux file permissions (`chmod`, `chown`) to control access within the mounted filesystem.
- **Backups:** Enable [Filestore backups](https://cloud.google.com/filestore/docs/backups) for critical data.

> **📚 Learn more:** [Filestore Security Best Practices](https://cloud.google.com/filestore/docs/access-control)

---

## Further Reading

### Official Documentation
- [Google Cloud Filestore Documentation](https://cloud.google.com/filestore/docs)
- [Creating Filestore Instances](https://cloud.google.com/filestore/docs/creating-instances)
- [Filestore Pricing](https://cloud.google.com/filestore/pricing)
- [GCP Startup Scripts](https://cloud.google.com/compute/docs/instances/startup-scripts)

### Related Guides
- [Setting Up a Google Cloud VM with VSCode](../google-cloud-vm-setup/Setting%20Up%20a%20Google%20Cloud%20VM%20with%20VSCode.md) - Prerequisite guide for VM setup
- [NFS Best Practices](https://cloud.google.com/filestore/docs/performance)
- [Managing Persistent Disks](https://cloud.google.com/compute/docs/disks)

### Cost Management
- [Filestore Pricing Calculator](https://cloud.google.com/products/calculator)
- [GCP Cost Management](https://cloud.google.com/cost-management)

---

## Summary

By following this guide, your GCP instance will automatically mount the Filestore every time it starts up, ensuring that the storage is available without manual intervention. This is particularly useful for:

- **Research collaboration** - Multiple team members can access the same data
- **Large datasets** - Store data separately from your VM's boot disk
- **Persistent storage** - Data remains available even if you delete and recreate VMs

---

## Questions or Feedback?

If you have any questions or encounter issues with this guide, please:

- [Open an issue](https://github.com/Applied-Economics-With-AI/guides/issues) on our GitHub repository
- Contact: [Peter John Lambert](mailto:p.j.lambert@lse.ac.uk) at LSE

---

*Last updated: January 2026*
