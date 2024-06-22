# Setting Up a Google Cloud VM for R and Python with VSCode

This guide is aimed at helping researchers set up a virtual machine capable of running R and Python in the cloud using Google Cloud Platform (GCP).  It primarily documents first-hand experience setting up and using a virtual machine on the Google Cloud Platform (GCP).  Similar setups can be achieved with AWS and Microsoft Azure, though I have no experience with these platforms. This has been an invaluable tool for me since the beginning of my PhD, and has drastically increased my productivity across many projects.

This guide is a mix of personal experience and tips with some more standard instructions on how to set up your own virtual work environment.  It is written with a view to aid applied economics researchers. I have borrowed from many sources, and tried my best to correctly attribute these.

We will first confugure our Cloud-based server using the Google Cloud Virtual Machine (VM) and Visual Studio Code (VSCode). You'll be able to leverage the VM's resources – like additional processing power and memory – for your coding projects while working within your VSCode setup.

This guide has been prepared by Peter John Lambert, Yannick Schindler, Suraj Rajesh, Yifan Wang, Juan Bautista Sosa, Tongmeng Xie, Pauline Butcher, Thiemo Fetzer, and Luca Barbato.

We welcome any questions or feedback, which you can leave here (link to "issues" section of the guides repo).

---

# **Guide Overview**

We will cover the following steps to set up your local machine for remote development using a Google Cloud Virtual Machine (VM):

- [Why do I need my own virtual machine? A Pros and Cons](#why-do-i-need-my-own-virtual-machine-a-pros-and-cons-tbc)
  - Understand the advantages and costs of using a virtual machine, helping you decide if it's the right solution for your needs.

- [Step 1: Install and Configure VSCode](#step-1-install-and-configure-vscode)
  - Set up Visual Studio Code, a powerful code editor that supports remote development.

- [Step 2: Create a Google Account](#step-2-create-a-google-account)
  - Create a Google account, which is necessary for accessing Google Cloud services.

- [Step 3: Set up a Google Cloud Account](#step-3-set-up-a-google-cloud-account)
  - Configure your Google Cloud account and start using VM instances.

- [Step 4: Create a Virtual Machine (VM)](#step-4-create-a-virtual-machine-vm)
  - Create and configure a new virtual machine on Google Cloud, including specific recommendations on the configuration of the VM.

- [Step 5: Generate and Configure SSH Keys](#step-5-generate-and-configure-ssh-keys)
  - Generate SSH key pairs and configure them to securely connect to your virtual machine from VSCode.

- [Step 6: Connect to the VM Using VSCode](#step-6-connect-to-the-vm-using-vscode)
  - Connect your local VSCode setup to the virtual machine, enabling remote development.

- [Step 7: Install Necessary Scripts and Tools on the VM](#step-7-install-necessary-scripts-and-tools-on-the-vm)
  - Install essential scripts and tools on your virtual machine, ensuring it's ready for development tasks.

- [Step 8: Open an R Script in VSCode](#step-8-open-an-r-script-in-vscode)
  - Create and run R scripts in VSCode, leveraging the power of the virtual machine.

- [Step 9: Open a Python Notebook in VSCode](#step-9-open-a-python-notebook-in-vscode)
  - Create and run Python notebooks in VSCode, allowing interactive development on the virtual machine.

- [Step 10: Starting and Stopping the VM](#step-10-starting-and-stopping-the-vm)
  - Manage the start and stop operations of your virtual machine.

- [Step 11: Create a Static IP Address](#step-11-create-a-static-ip-address)
  - Assign a static IP address to your virtual machine to avoid reconfiguration issues when the machine restarts.

- [Step 12: Installing GitHub Copilot](#step-12-installing-github-copilot)
  - Set up GitHub Copilot in VSCode to enhance your programming experience.


---

## **Why do I need my own virtual machine? A Pros and Cons (TBC)**

There are at least three reasons to setup a virtual machine: (1) Flexibility, (2) Scalability, (3) Productivity. Reasons not to setup are the technical barriers to entry (though this guide aims to offset this!) and cost.  On cost, I would argue that the relevant counterfactual would be purchasing a mid-range laptop (32GB of memory or higher) which will depreciate, puts an upper bound on the power available to you, and requires liquidity to purchase.

(1) Flexibility

While it is very common for universities to have their own computational resources for working with big data, I have found that having my own server affords a great deal more flexibility.  The most obvious advantage is that I can turn the machine on and off as needed, and do not have to submit jobs to a schedule nor compete for resources with others.  The ability to work in real-time drastically increases productivity and avoids lengthy wait times, which (for me) disrupt my workflow substantially.  Another way in which a virtual machine offers flexibility is in costs.  Apart from the cost of data storage, you will not pay for any computational resources when not using the machine (unlike personal hardware).  And if a project is going to be dormant for a while, you can download the data to a personal hard disk and shudder the virtual machine completely - at which point your costs become 0.

(2) Scalability

The best feature of the Google Cloud

---

## **Step 1: Install and Configure VSCode**

First, we need to install and configure Visual Studio Code (VSCode), a popular code editor that supports remote development.

### **1.1 Install VSCode**

- Download and install VSCode from [the official website](https://code.visualstudio.com/).

### **1.2 Install the Remote SSH Extension**

- Open VSCode.
- Click on the Extensions tab on the left sidebar
  
  <img width="900" alt="step_1 2 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/348d6a3d-8269-4175-b0cc-ea5c2c88da37">

- Search for "Remote - SSH: Editing Configuration Files" and click "Install" to add the extension to VSCode.
  
  <img width="900" alt="Step_1 2 2" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/4b9e1027-b4a3-4466-8582-c82938eb390b">

---

## **Step 2: Create a Google Account**

To use Google Cloud services, you need a Google account. If you don't already have one, [follow these steps](https://support.google.com/mail/answer/56256?hl=en-GB) to create a Gmail account.

<img width="900" alt="step_2" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/1cfbdc9d-5491-45ea-aa0d-2742e7f8db08">

---

## **Step 3: Set up a Google Cloud Account**

Now that you have a Google account, you can set up your Google Cloud account to start using VM instances.

### **3.1 Visit Google Cloud**

Navigate to [Google Cloud](https://cloud.google.com/), and you will automatically be prompted to log in with your Gmail account.

### **3.2 Set Up Your Account**

- Click on the "START FREE" button at the upper right corner of the page.

  <img width="900" alt="Step_3 2" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/68f122e1-096a-4062-80ed-2052da3c1cce">

- Choose your country and organization when prompted.
- Add billing information to your account. You will receive $300 worth of free Google Cloud credits to get started.
- If you need more detailed instructions, refer to [this guide](https://www.optimizesmart.com/how-to-create-a-new-google-cloud-platform-accoun).

---

## **Step 4: Create a Virtual Machine (VM)**

In this step, you will create a new VM in your Google Cloud account.

### **4.1 Create a New Project**

-  On the top left, you would be able to view and click on 'Select a project' (1)

- Then, on the subsequent window, select ‘New Project’ (2)

  <img width="900" alt="step_4 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/83ba9cb8-cecb-4cc0-8104-678841c6d06c">


### **4.2 Create an Instance**

- Navigate to the [Google Cloud Console](https://console.cloud.google.com/).
   
- In the left-hand menu, click on "Compute Engine" and then "VM instances".

  <img width="900" alt="step_4 2" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/7dd41b4b-3e40-4849-9031-d93067fe3729">

-  Select "Create Instance" and configure the settings.
 
   <img width="900" alt="step_4 2 2" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/1cae86cb-999f-4263-86dc-6284dbac2405">


### **4.3 Configure the VM**

### **4.3.1 General Configuration**

- Name: Give your VM a name.
- Region and Zone: Select the location for your VM. The default ("us-central1-a") is usually the cheapest.
- Machine Type: Choose a machine type based on your needs. For beginners, "e2-medium" (2 vCPUs, 4 GB memory) is a good starting point.
  
  <img width="900" alt="step_4 3 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/80d2e590-9b73-4793-bafc-39f9913837a6">

### **4.3.2 Configure the Bootdisk**
- Click "Change" next to the Boot disk section.
- In the Operating System dropdown, select "Ubuntu".
- In the Version dropdown, select "Ubuntu 18.04 LTS".

  <img width="900" alt="step_4 3 2 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/5be5826b-42eb-417f-8038-c52986ab70ba">

- Click "Select" to confirm.
- For additional storage capacity, navigate to 'Disks' and click on 'ADD NEW DISKS'.
- Customise the boot disk size based on your task requirements; this will be charged regardless of VM usage intensity.
  
  <img width="900" alt="step_4 3 2" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/ba5335c3-db6f-48f3-9012-ff6a825cef0a">

### **4.4 Selecting “Spot” instances**

You can reduce costs by selecting "Spot" instances under the VM provisioning model, which are significantly cheaper. However, Google can temporarily shut down the VM when the instance is not in use or if there is higher demand for a particular period. In general, this could happen once or twice a week, but it depends on a case-by-case basis.

<img width="900" alt="step_4 4" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/3b969969-ce5c-4616-bc53-f3c70514e6a0">

### **4.5 Additional Settings**

- In “Firewall”, enable options like "Allow HTTP traffic" and "Allow HTTPS traffic"
  
  <img width="900" alt="step_4 5 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/eb0b7033-ce10-4ccb-a6e6-8919db7e1829">

- In "Management", enable "Deletion protection"
  
  <img width="900" alt="step_4 5 2" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/bb355bc8-0492-4591-8e05-74a699c973e6">

### **4.6 Create the VM**

- Click "Create" to start your VM. It will automatically start, and costs will begin to accrue
  
  <img width="900" alt="step_4 6" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/6343a9c5-f14a-44a6-8a50-d334c11b938f">

### **4.7 Monitor Your Costs**

- You can monitor your costs in the billing section of the navigation menu or the quick access menu
  
  <img width="900" alt="step_4 7" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/fe68635b-0f38-4f64-95e4-d6f35ab236e2">

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
Then the output would look like:

![step_5 1 a 1](https://github.com/Applied-Economics-With-AI/guides/assets/172032819/2f05128f-541f-4c1d-8076-becf0f0bde22)

Locate the generated keys. The file ending in `.pub` is the public key, and the other file is the private key. 

![step_5 1 a 2](https://github.com/Applied-Economics-With-AI/guides/assets/172032819/2492a970-b5b4-4cee-b4f5-5d90769a96d2)

Open the public key file with a text editor and copy its contents.

![step_5 1 a 3](https://github.com/Applied-Economics-With-AI/guides/assets/172032819/8ece9e59-d1d2-4cb8-97bd-88c6d6e28419)

### **5.1.b Generate SSH Keys (Mac)**

Creating an SSH key on a Mac to connect to a Google Cloud VM via Visual Studio Code is similar to the process on Windows. Here are the instructions you need to follow:

**Open Terminal**:

You can find Terminal in the Applications > Utilities folder, or use Spotlight search (Cmd + Space) and type "Terminal"

<img width="1470" alt="step_5 1 b 6" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/2f9fc856-3ac7-4182-b141-c1d8085700e6">

**Generate the SSH key**:

Run the following command in the Terminal:

```bash
ssh-keygen -t rsa -f ~/.ssh/[key_filename] -C "[your_email@example.com]" -b 2048
```

Replace [key_filename] with the desired name for your key (e.g., google_cloud_vm_key), and [your_email@example.com] with your email address.

For instance, to generate an SSH key with the external IP 34.46.40.16 using your username rsuraj02 the command will be 

`ssh-keygen -t rsa -f ~/.ssh/google_cloud_vm_key -C "rsuraj02@example.com" -b 2048`

<img width="980" alt="step_5 1 b 2" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/d0364490-8f37-4036-a8da-75390f099004">

**Follow the prompts**:

- You will be asked to specify the location to save the key. The default location is usually fine (~/.ssh/), but you can specify a different path if needed.
  
- You will also be prompted to enter a passphrase for added security. Press Enter if you do not want to set a passphrase.
  
<img width="592" alt="step_5 1 b" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/3ce6f81f-e052-4d21-936a-ffffccdc8904">

**Save paths to public and private keys:**

Once the keys are generated, save the paths to both the private and public keys displayed in the terminal. The path with the extension '.pub' is the public key.

<img width="597" alt="step_5 1 b 3" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/448cd726-1650-4589-97cf-21e21bd77d45">

**View the public key:**

Enter the below command to view and copy the public key:

```bash
cat ~/.ssh/google_cloud_vm_key.pub
```
<img width="1467" alt="step_5 1 b 4" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/39d65feb-d41a-4487-95f1-493a0e57b695">

### **5.2 Add SSH Key to Google Cloud VM**

- Navigate to the [Google Cloud Console](https://console.cloud.google.com/).

- In the left-hand menu, click on "Compute Engine".

     <img width="900" alt="step_10 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/9f1eae9f-2250-4b08-a4f0-80b4f6d8f1a8">
    
- Click on your VM instance name.
   
   <img width="900" alt="step_11 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/ae7d13fc-ef0d-4643-8185-0e520cd4d904">
  
- Click "Edit" and navigate to the SSH key section.
  
  <img width="900" alt="step_5 2" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/097e1a68-048a-44a7-8617-32dfe27114b2">

- Click "Add Item" and paste your public key. Save the changes.
  
  <img width="900" alt="step_5 2 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/91844144-9b1f-4109-b8e0-f1660dd59175">

  <img width="900" alt="step_5 2 2" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/b1f0d1a0-9193-4a53-bc9e-29351ad10987">

- Reset the VM instance to apply the changes
  
  <img width="900" alt="step_5 2 3" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/6d805ff9-9a16-4011-9917-d3ae0c7bf96c">

---

## **Step 6: Connect to the VM Using VSCode**

With your SSH keys configured, you can now connect to the VM using VSCode.

### **6.1 Configure SSH in VSCode**

- Press `Ctrl + Shift + P` (Windows) or `Cmd + Shift + P` (Mac) to open the Command Palette
  

- Type "Remote-SSH: Connect to Host" and select it
  
 <img width="900" alt="step_6 1 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/5345322a-81c9-4ca7-b538-2ad10d7c1a64">


- Click "Configure SSH Hosts" and choose the file where your SSH key is stored

  <img width="900" alt="step_6 1 2" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/cf533ef4-f11c-4eef-a622-3c5cb6582769">


- Add the following details:

```markdown
Host [VM name]
HostName [External IP of the VM]
User [Google Cloud username]
IdentityFile [Path to your private key]
```

<img width="900" alt="step_6 1 3" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/65673f93-0743-4d2b-8403-a17fbef2ee69">

- The External IP can be found by navigating to ‘Compute Engine’

![step_6 1 4](https://github.com/Applied-Economics-With-AI/guides/assets/172032819/76bcccc8-be58-4e7b-b871-9f80e33ab989)


### **6.2 Connect to the VM**

- Press `Ctrl + Shift + P` (Windows) or `Cmd + Shift + P` (Mac) and select "Remote-SSH: Connect to Host"
  
  <img width="900" alt="step_6 1 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/5345322a-81c9-4ca7-b538-2ad10d7c1a64">

- Choose the configured host

  <img width="900" alt="step_6 2 2" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/1f341376-79f7-4245-97a6-eec68104ffdf">

- Select "Linux" as the system type and continue (may not be required to choose system type in Mac)

---

## **Step 7: Install Necessary Scripts and Tools on the VM**

Once connected, you can install the necessary tools and scripts on your VM.

## **7.1 Open a terminal on the VM**

- Open the terminal in VSCode by clicking on the icon shown below.
  
  <img width="900" alt="step_7 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/6d56e3de-d645-4524-95f0-893121df487d">


## **7.2: Update and Install Necessary Packages**
First, we need to update the package list and install essential packages that are commonly required for software development and system operations. These packages include tools for handling software properties, package management, and development libraries.
  ```bash
sudo apt-get update
sudo apt-get install -y software-properties-common dirmngr ed gpg-agent \
     less locales vim-tiny wget ca-certificates \
     build-essential libcurl4-openssl-dev libssl-dev libxml2-dev

sudo apt update
sudo apt upgrade
  ```
## **7.3: Add R Repositories and Install R**

Next, we will add the Comprehensive R Archive Network (CRAN) repository to our sources list and import the public key to ensure secure package installation. We then install the R base package and its development tools, which are crucial for running R and building packages.
  ```bash
sudo sh -c 'echo "deb https://cloud.r-project.org/bin/linux/ubuntu jammy-cran40/" >> /etc/apt/sources.list'
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
sudo apt-get update
sudo apt upgrade
sudo apt-get install -y r-base r-base-dev

sudo apt-get install -y libfontconfig1-dev libharfbuzz-dev libfribidi-dev libfreetype6-dev \
    libpng-dev libtiff5-dev libjpeg-dev libcairo2-dev libudunits2-dev libpoppler-cpp-dev \
    libgdal-dev cmake

sudo apt update
sudo apt upgrade
  ```
## **7.4: Install Core R Packages**

We then install essential R packages for data manipulation, visualization, and development, which are widely used in data science and will provide a solid foundation for your projects.
 ```bash
sudo Rscript -e "install.packages(c('tidyverse', 'dplyr', 'ggplot2', 'devtools', 'formatR', 'remotes', 'selectr', 'languageserver', 'rmarkdown', 'httpgd', 'data.table'), repos='http://cran.rstudio.com/')"
 ```
## **7.5: Install Additional R Packages**
In addition to core packages, we install specific R packages that are useful for various data science tasks, including text processing, statistical modeling, and advanced plotting.
 ```bash
sudo Rscript -e "install.packages(c('fixest', 'devtools', 'janitor', 'lubridate', 'doParallel', 'tmaptools', 'rmarkdown', 'textclean', 'qdapRegex', 'quanteda', 'tokenizers', 'stringi', 'DescTools', 'readtext', 'rvest', 'xml2', 'DescTools', 'zoo', 'stargazer', 'readxl', 'ggplot2', 'scales', 'ggpubr', 'ggpmisc', 'egg', 'extrafont'), repos='http://cran.rstudio.com/')"
 ```
## **7.6: Install Python and pip**
Python is a versatile programming language commonly used in data science. We install Python and pip, a package manager for Python, to facilitate the installation of Python packages.
 ```bash
sudo apt-get install -y python3 python3-pip
 ```
## **7.7: Install Radian**
Radian is an enhanced R console that provides multiline editing and rich syntax highlighting. We install Radian to improve the R programming experience.

 ```bash
Copy code
pip3 install -U radian

#Ensure the path to Radian is included in the PATH environment variable
echo $PATH
nano ~/.bashrc
#Add the following line to ~/.bashrc**
export PATH=$PATH:/home/YOUR_USER_NAME/.local/bin
source ~/.bashrc
echo $PATH
 ```

## **7.8: Install VSCode and Extensions**

ReturnVisual Studio Code (VSCode) is a powerful code editor with numerous extensions for various programming languages. We install VSCode and essential extensions for Python, R, and other development tools.
```bash
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -o root -g root -m 644 packages.microsoft.gpg /usr/share/keyrings/
sudo sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
rm -f packages.microsoft.gpg

sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install code # or code-insiders

# Install VSCode extensions
code --install-extension mechatroner.rainbow-csv
code --install-extension ms-python.python
code --install-extension ms-toolsai.jupyter
code --install-extension ms-vscode.cpptools
code --install-extension github.copilot
code --install-extension GitHub.copilot-chat
code --install-extension REditorSupport.r
code --install-extension ms-python.vscode-pylance
code --install-extension eamodio.gitlens
code --install-extension vscodevim.vim
code --install-extension RDebugger.r-debugger
```
## **7.9: Set Default Locale**
```bash
Setting the default locale ensures that your system uses the correct language and regional settings, which can prevent issues with software that relies on locale settings.
sudo locale-gen en_US.UTF-8
sudo update-locale LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8
```
## **7.10: Install Additional R Packages from GitHub**
Install additional R packages directly from GitHub for specialized functionalities.
```bash
devtools::install_github("trinker/textclean")
devtools::install_github('Mikata-Project/ggthemr')
extrafont::font_import()
extrafont::loadfonts(device="postscript")
extrafont::fonts()
```
## **7.11: Attach Persistent Disk**
If you need additional storage, attach a persistent disk. Be cautious not to format an existing disk if it contains important data.
```bash
# Get the device name
ls -l /dev/disk/by-id/google-*

# Create a folder and mount the disk
sudo mkdir -p /mnt/disks/pdisk
sudo mount -o discard,defaults /dev/nvme0n2 /mnt/disks/pdisk

# Make the disk read/writable
sudo chmod a+w /mnt/disks/pdisk

# Edit the fstab file to mount the disk on boot
sudo blkid /dev/nvme0n2
sudo vim /etc/fstab
# Add this line to /etc/fstab
UUID=e73634e9-81bd-459d-9286-0af3273150c1 /mnt/disks/pdisk ext4 discard,defaults,nofail 0 2
cat /etc/fstab
```
## **7.12: Install Anaconda with Mamba Compiler**
Anaconda is a popular Python distribution for data science. We install it along with Mamba, a faster package manager, to manage your Python environments and packages efficiently.
```bash
# Get the device name
ls -l /dev/disk/by-id/google-*

# Create a folder and mount the disk
sudo mkdir -p /mnt/disks/pdisk
sudo mount -o discard,defaults /dev/nvme0n2 /mnt/disks/pdisk

# Make the disk read/writable
sudo chmod a+w /mnt/disks/pdisk

# Edit the fstab file to mount the disk on boot
sudo blkid /dev/nvme0n2
sudo vim /etc/fstab
# Add this line to /etc/fstab
UUID=e73634e9-81bd-459d-9286-0af3273150c1 /mnt/disks/pdisk ext4 discard,defaults,nofail 0 2
cat /etc/fstab
```
## **7.13: Configure Radian**
Radian is an enhanced R console for the R language. To configure it in your VSCode settings, first, you need to find where Radian is installed on your VM.

Open the terminal and run the following command:

 ```bash
whereis radian
 ```
This command will display the path where Radian is installed. It might look something like /usr/local/bin/radian. Next, you need to add this path to your VSCode settings to make sure VSCode uses Radian as the R console.

- Press `Ctrl + Shift + P` (Windows) or `Cmd + Shift + P` (Mac) to open the Command Palette.
  
- Type "Preferences: Open Remote Settings" and select it.

![step_7 8](https://github.com/Applied-Economics-With-AI/guides/assets/172032819/de60ed71-05c1-4a17-9dfa-7e115b1815c4)

- In the settings.json file that opens, add the following configuration. Replace /usr/local/bin/radian with the path you found in the previous step:

```bash
{
  "r.bracketedPaste": true,
  "r.rterm.linux": "/home/rsuraj02/.local/bin/radian",
  "r.lsp.path": "/usr/bin/R",
  "r.lsp.debug": true,
  "r.lsp.diagnostics": true,
  "r.rterm.option": [
    "--no-save",
    "--no-restore"
  ],
  "r.plot.useHttpgd": true,
  "terminal.integrated.env.linux": {
    "R_HOME": "/usr/lib/R"
  }
}
 ```
This configuration does the following:
r.bracketedPaste: Enables bracketed paste mode in the R console.
r.rterm.linux: Specifies the path to the Radian executable.
r.plot.useHttpgd: Uses the httpgd package for rendering plots.
Step 7.7.1: Saving Settings
Save the changes to the settings.json file.
Restart VSCode to apply the new settings.

![step_7 8 1](https://github.com/Applied-Economics-With-AI/guides/assets/172032819/0b11f502-78c2-4c9c-824e-4c86779912ba)

---

## **Step 8: Open an R Script in VSCode**

With VSCode configured and connected to your VM, you can start working with R scripts.


### **8.1 Install R**:**
   - Download and install R (version 3.4.0 or higher) for your platform from the [CRAN website](https://cran.r-project.org/).
   - For Windows users: During installation, check the option "Save version number in registry" to allow the R extension in VSCode to automatically find the R executable.
     
     <img width="900" alt="step_8 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/ab570400-ac65-43cd-897b-0bc87fb2e0a3">

### **8.2 Install `languageserver` in R**:
   - Open R and run the following command to install the `languageserver` package to enhance the coding interface:
     ```R
     install.packages("languageserver")
     ```
     <img width="900" alt="step_8 2" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/7fc10d9f-d337-46ae-9a8e-b121f2236e03">

   - Choose the mirror closest to your location

### **8.3 Install R Extension for VSCode**:
   - Open VSCode and go to the Extensions tab on the left sidebar.

     <img width="900" alt="step_1 2 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/348d6a3d-8269-4175-b0cc-ea5c2c88da37">
  
   - Search for "R" and install the extension provided.

     <img width="900" alt="step_8 3 2" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/344a2068-f2a5-44be-a567-a27e2a5ed164">

### **8.4 Create a New R Script**

- In VSCode, click on "File" and then the "New File" as shown below
  
  <img width="900" alt="step_8 4 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/c40a97e2-78db-4f96-a2d9-61a10200866b">

- Click on the R document. An R Document (.R) is a basic script for running R code.

  <img width="900" alt="step_8 4 2" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/fb4e4a0a-8e41-4ee0-8a85-7bb43d130b74">


### **8.5 Write and Run R Code**
- Write your R code in the document or markdown.

   Example:
   ```r
   print('Hello, R!')
    ```
- To run the code, highlight the lines you want to execute and press `Ctrl + Enter` (Windows) or `Cmd + Enter` (Mac). The output will appear in the terminal at the bottom of the VSCode 
  window using the configured Radian console.
  
  <img width="900" alt="step_8 5" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/cc9df9a9-3127-45c5-8c5e-4ae173fa1191">

- Also, if radian is configured correctly, you should be able to view `r$>` in the command line of the terminal
   
<img width="900" alt="step_8 5 2" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/5e5d8453-bda3-4597-a30e-bbd33a5231aa">

---

### **Step 9: Open a Python Notebook in VSCode**
- VSCode also supports Jupyter notebooks, allowing you to work with Python in an interactive environment. Python is already installed through the setup script. To use Python through 
  Jupyter Notebook in VScode 

### **9.1 Install Extensions for VSCode**
- Go to the Extensions tab in VSCode.

  <img width="900" alt="step_1 2 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/348d6a3d-8269-4175-b0cc-ea5c2c88da37">

- Search for "Python" and install the extension provided by Microsoft.

  <img width="900" alt="step_9 1 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/8780ad44-a0d2-426b-8a71-e9b458790b6e">

- Search for "Jupyter" and install the extension provided by Microsoft.
  
  <img width="900" alt="step_9 1 2" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/ee8fd229-20be-4ad7-9fa9-9f00fd99cfda">

### **9.2 Create a New Jupyter Notebook**
- In VSCode, click on "File" and then the "New File" as shown below
  
  <img width="900" alt="step_8 4 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/c40a97e2-78db-4f96-a2d9-61a10200866b">

- Click on Jupyter to use Python in a Jupyter notebook. Name the file with a .ipynb extension, for example, example_notebook.ipynb.
  
  <img width="900" alt="step_9 2" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/dd4fda1d-de8e-442d-9c57-317bc01026cb">
 

### **9.3 Kernel Selection**
Before running any code, ensure that the notebook is using the correct Python kernel. View the top right button as indicated below; if the kernel isn't installed, then select it to choose the Python interpreter installed on your VM.

<img width="900" alt="step_9 3" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/978d9982-1f47-4807-b13a-a4d8e313981f">

### **9.4 Write and Run Python Code**

- Click on the '+ Code' icon to create a new code cell. Click on '+ Markdown' to add a markdown to type in plain text comments, which are useful for writing reports. Refer to https://jupyter.brynmawr.edu/services/public/dblank/Jupyter%20Notebook%20Users%20Manual.ipynb for further guidance in using Jupyter Notebook.
  
Write your Python code in the cell.

Example:
```markdown
python
Copy code
print("Hello, Python!")
```
Click the run icon next to the cell or press `Shift + Enter` (Windows and Mac) to execute the code. The output will appear directly below the cell.

<img width="900" alt="step_9 4" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/dea16e4f-e261-4dd8-a4e3-efd15276513e">

---

## **Step 10: Starting and Stopping the VM**

### **10.1 Starting the VM**

   - Navigate to the [Google Cloud Console](https://console.cloud.google.com/).

   - In the left-hand menu, click on "Compute Engine".

     <img width="900" alt="step_10 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/9f1eae9f-2250-4b08-a4f0-80b4f6d8f1a8">

   - Find your VM in the list and click the "Start" button.

     <img width="900" alt="step_10 1 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/25dfe5f1-8de2-4120-aa30-91c6a94eb557">

### **10.2 Stopping the VM**

   - In the left-hand menu, click on "Compute Engine".
     
     <img width="900" alt="step_10 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/9f1eae9f-2250-4b08-a4f0-80b4f6d8f1a8">

   - Find your VM in the list and click the "Stop" button.
     
     <img width="900" alt="step_10 2" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/72efaabc-ad10-4945-8933-68ed8be455ee">

---

## **Step 11: Create a Static IP Address**

Every time the instance is started, the public IP is modified, requiring modifications to the "SSH configuration" setting in your VScode.  To avoid this, you can assign a static IP address.

### **11.1 Assign the Static IP to Your VM**:

   - Navigate to the [Google Cloud Console](https://console.cloud.google.com/).

   - In the left-hand menu, click on "Compute Engine".

     <img width="900" alt="step_10 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/9f1eae9f-2250-4b08-a4f0-80b4f6d8f1a8">
  
    <img width="900" alt="step_10 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/9f1eae9f-2250-4b08-a4f0-80b4f6d8f1a8">

   - Click on your VM instance name.
   
   <img width="900" alt="step_11 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/ae7d13fc-ef0d-4643-8185-0e520cd4d904">

   - Click "Edit".
     
     <img width="900" alt="step_5 2" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/3ef99823-5e45-4c99-9b85-5089f1782a2c">

   - Navigate to "Network interfaces"
     
     <img width="900" alt="step_12 0" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/5d9909f5-019f-4b7e-b549-9e315c38ef72">

   - Click "External IPv4 Address".
     
     <img width="900" alt="step_12 0 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/38389eaa-526b-4d27-ab03-6fb8597f7ce9">

   - Select "Reserve Static Address"
     
     <img width="900" alt="step_12 0 2" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/faf4a292-f60e-41a7-9b10-b2b59fd9045c">

   - Select a name and click "Reserve"
  
     <img width="900" alt="step_12 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/0a69fe32-e165-408b-a058-a06bd577cb6a">


---

## **Step 12: Installing GitHub Copilot**

### **12.1 Installing GitHub Copilot in VSCode**
   - Open your Visual Studio Code editor.
     
   - Click on the Extensions tab on the left sidebar.
     
     <img width="900" alt="step_1 2 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/348d6a3d-8269-4175-b0cc-ea5c2c88da37">

   - Type "GitHub Copilot" in the search bar and press Enter.
     
   - Click the "Install" button next to the GitHub Copilot extension.

     <img width="900" alt="step_13" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/d2324b7f-5923-4092-b9b3-69af0b3c30af">

### **12.2 Enable GitHub Copilot in VSCode**
   - Once installed, you will be prompted to sign in to your GitHub account. Follow the on-screen instructions to complete the authentication process (**).
     
   - Click on the icon shown below to verify that Copilot is running.
     
     <img width="900" alt="step_12 2 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/d8f63ddd-8a15-417b-b37a-e63230a83194">

     <img width="900" alt="step_12 2 1" src="https://github.com/Applied-Economics-With-AI/guides/assets/172032819/f446a8d2-0f9d-4d36-805f-eaf206feb38e">

   - Open any file or start a new one (see steps 9 and 10). GitHub Copilot will start providing code suggestions as you type.

### **12.3 Using GitHub Copilot**

For detailed instructions and tips on how to use GitHub Copilot effectively in VScode, refer to [GitHub Copilot in VSCode](https://code.visualstudio.com/docs/copilot/overview).

---
This guide should help you navigate the setup process. If you have any questions, reach out to

[placeholder].

---
