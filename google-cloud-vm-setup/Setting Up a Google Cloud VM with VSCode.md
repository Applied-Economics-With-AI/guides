# Setting Up a Google Cloud VM with VSCode

This guide will show you how to setup your own personal Cloud-based server for conducting applied economics research.  We will first confugure our Cloud-based server using the Google Cloud Virtual Machine (VM) and Visual Studio Code (VSCode). You'll be able to leverage the VM's resources – like additional processing power and memory – for your coding projects while working within your VSCode setup.

---

# **Guide Overview**

We will cover the following steps to set up your local machine for remote development using a Google Cloud Virtual Machine (VM):

- **Prepare Your Tools:** Install the essential VSCode extension for remote connections.
- **Set Up Your Cloud Workspace:** Create your Google Cloud account and explore the free trial options.
- **Launch Your Virtual Machine:** Choose the VM configuration that best suits your project needs.
- **Secure Your Access:** Generate SSH keys to ensure a safe and private connection to your VM.
- **Connect VSCode to the Cloud:** Link your code editor to your new virtual machine.
- **Customize Your Environment:** Install the tools and software you need for your specific workflow.

---

## **Step 1: Install and Configure VSCode**

First, we need to install and configure Visual Studio Code (VSCode), a popular code editor that supports remote development.

### **1.1 Install VSCode**

- Download and install VSCode from [the official website](https://code.visualstudio.com/).

### **1.2 Install the Remote SSH Extension**

- Open VSCode.
- Click on the Extensions tab on the left sidebar
- Search for "Remote - SSH: Editing Configuration Files" and click "Install" to add the extension to VSCode.

---

## **Step 2: Create a Google Account**

To use Google Cloud services, you need a Google account. If you don't already have one, [follow these steps](https://support.google.com/mail/answer/56256?hl=en-GB) to create a Gmail account.

---

## **Step 3: Set-up a Google Cloud Account**

Now that you have a Google account, you can set up your Google Cloud account to start using VM instances.

### **3.1 Visit Google Cloud**

Navigate to [Google Cloud](https://cloud.google.com/) and log in with your Gmail account.

### **3.2 Set Up Your Account**

- Click on the "START FREE" button at the upper right corner of the page.
- Choose your country and organization when prompted.
- Add billing information to your account. You will receive $300 worth of free Google Cloud credits to get started.
- If you need more detailed instructions, refer to [this guide](https://www.optimizesmart.com/how-to-create-a-new-google-cloud-platform-accoun).

---

## **Step 4: Create a Virtual Machine (VM)**

In this step, you will create a new VM in your Google Cloud account.

### **4.1 Create a New Project**

- Go to the Google Cloud Console (1)
- Select ‘New Project’ (2)

<aside>

![Alt text](google-cloud-vm-setup/Images/create_new_project.png)

</aside>

### **4.2 Create an Instance**

- Choose Compute Engine from the ‘Quick Access’ menu in the home/landing page and then on "Create Instance" and configure the settings.

<aside>

![Alt text](google-cloud-vm-setup/Images/create_instance_position.png)

</aside>

- Name: Give your VM a name.
- Region and Zone: Select the location for your VM. The default ("us-central1-a") is usually the cheapest.
- Machine Type: Choose a machine type based on your needs. For beginners, "e2-medium" (2 vCPUs, 4 GB memory) is a good starting point.
- Boot Disk: Customize the boot disk based on your task requirements, this will be charged regardless of VM usage intensity.

### **4.3 Selecting “Spot” instances**

You can reduce costs by selecting "Spot" instances under VM provisioning model, which are significantly cheaper. However, the VM can be temporarily shut down by Google when the instance is not in use or if there is higher demand for a particular period. In general, this could happen around once or twice a week but it depends on a case by case basis.

<aside>


![Alt text](google-cloud-vm-setup/Images/spot_position.png)

</aside>

### **4.4 Additional Settings**

- In “Firewall”, enable options like "Allow HTTP traffic" and "Allow HTTPS traffic"
- In "Management", enable "Deletion protection"

### **4.5 Create the VM**

- Click "Create" to start your VM. It will automatically start, and costs will begin to accrue

### **4.6 Monitor Your Costs**

- You can monitor your costs in the billing section of the navigation menu or the quick access menu

---

## **Step 5: Generate and Configure SSH Keys**

To securely connect VS code to your VM from your local computer, you need to generate SSH key pairs.

### **5.1.a Generate SSH Keys (Windows)**

Open Command Prompt (CMD) and enter the following command:

```bash
ssh-keygen -t rsa -f [directory where you want to save the key] -C [username] -b 2048
```

Here the username is simply your google account username with no dots or dots replaced by ‘_’. For example, if I want to save the key in this directory “C:\Users\wyf19\.ssh\google_cloud_key2” and my username is “wyf1997203lse”. Then the command will become:

```bash
ssh-keygen -t rsa -f C:\Users\wyf19\.ssh\google_cloud_key2 -C wyf1997203lse -b 2048
```

Locate the generated keys. The file ending in `.pub` is the public key, and the other file is the private key. Open the public key file with a text editor and copy its contents.

### **5.1.b Generate SSH Keys (Mac)**

Creating an SSH key on a Mac to connect to a Google Cloud VM via Visual Studio Code is similar to the process on Windows. Here are the instructions you need to follow:

**Open Terminal**:

You can find Terminal in the Applications > Utilities folder, or use Spotlight search (Cmd + Space) and type "Terminal"

**Generate the SSH key**:

Run the following command in the Terminal:

```bash
ssh-keygen -t rsa -f ~/.ssh/[key_filename] -C "[your_email@example.com]" -b 2048
```

Replace [key_filename] with the desired name for your key (e.g., google_cloud_vm_key), and [your_email@example.com] with your email address.

**Follow the prompts**:

- You will be asked to specify the location to save the key. The default location is usually fine (~/.ssh/), but you can specify a different path if needed.
- You will also be prompted to enter a passphrase for added security. Press Enter if you do not want to set a passphrase.

**Save paths to public and private keys:**

Once the keys are generated, save the paths to both the private and public keys displayed in the terminal.

**View the public key:**

Enter the below command to view and copy the public key:

```bash
cat ~/.ssh/google_cloud_vm_key.pub
```

### **5.2 Add SSH Key to Google Cloud VM**

- Go to your VM instance in the Google Cloud Console
- Click "Edit" and navigate to the SSH key section
- Click "Add Item" and paste your public key. Save the changes.
- Reset the VM instance to apply the changes

---

## **Step 6: Connect to the VM Using VSCode**

With your SSH keys configured, you can now connect to the VM using VSCode.

### **6.1 Configure SSH in VSCode**

- Press Ctr + Shift + P to open the Command Palette
- Type "Remote-SSH: Connect to Host" and select it
- Click "Configure SSH Hosts" and choose the file where your SSH key is stored


![Alt text](google-cloud-vm-setup/Images/configuration_SSH.png)
</aside>

- Add the following details:

```markdown
Host [VM name]
HostName [External IP of the VM]
User [Google Cloud username]
IdentityFile [Path to your private key]
```

- The External IP can be found by navigating to ‘Compute Engine’

<aside>

![Alt text](google-cloud-vm-setup/Images/external_IP.png)

</aside>

Note that the external IP could change if you either reset the VM or it crashes, in which case you would have to reconfigure the setup to re-connect it.

### **6.2 Connect to the VM**

- Press `Ctrl` + `Shift` + `P` and select "Remote-SSH: Connect to Host"
- Choose the configured host
- Select "Linux" as the system type and continue (may not be required to choose system type in Mac)

---

## **Step 7: Install Necessary Scripts and Tools on the VM**

Once connected, you can install the necessary tools and scripts on your VM.

### **7.1 Open a Terminal in VSCode and Run Setup Scripts**

Copy and paste the contents of the setup scripts [link placeholder] ( `setup_ubuntu22_script`) into the terminal and run them line by line.

### **7.3 Configure Radian**

Radian is an enhanced R console for the R language. To configure it in your VSCode settings, first, you need to find where Radian is installed on your VM.

Open the terminal and run the following command:

```bash
whereis radian
```

- This command will display the path where Radian is installed. It might look something like /usr/local/bin/radian.

Next, you need to add this path to your VSCode settings to make sure VSCode uses Radian as the R console.

- Press ‘Ctrl + Shift + P’ to open the Command Palette.
- Type "Preferences: Open Remote Settings" and select it.

In the settings.json file that opens, add the following configuration. Replace /usr/local/bin/radian with the path you found in the previous step:

```markdown
{
"r.bracketedPaste": true,
"r.rterm.linux": "/usr/local/bin/radian",
"r.plot.useHttpgd": true
}
```

This configuration does the following:

- r.bracketedPaste: Enables bracketed paste mode in the R console.
- r.rterm.linux: Specifies the path to the Radian executable.
- r.plot.useHttpgd: Uses the httpgd package for rendering plots.

### 7.4 Saving Settings

- Save the changes to the settings.json file
- Restart VSCode to apply the new settings

With these steps, Radian should now be properly configured in VSCode, providing an enhanced R console experience on your remote VM.

---

## **Step 8: Final Steps and Usage**

Now you are ready to use your VM for development.

### **8.1 Explore Files on VM**

- Click "Open Folder" in VSCode and navigate to your home directory on the VM.
- Create project folders and start coding.
- Transfer Files
    - You can drag and drop files to upload to the VM or right-click to download files to your local machine.
- Running Code
    - Write and run your code as usual, now leveraging the resources of your remote VM.

---

You have successfully set up your local machine to interact with a Google Cloud VM using VSCode. You can now take advantage of the VM's resources for your development tasks.

This guide should help you navigate the setup process. If you have any questions, reach out to

[placeholder].

---
