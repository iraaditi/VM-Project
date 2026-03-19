```markdown
# Multi-Node Automated Web Infrastructure

## Overview
This project demonstrates a fully automated Infrastructure as Code (IaC) pipeline. It provisions three local Ubuntu virtual machines with varying hardware specifications using **Vagrant** and automatically configures them as Nginx web servers using **Ansible**.

## Prerequisites
To run this project on a new machine, you must have the following installed:
* **VirtualBox:** The underlying hypervisor.
* **Vagrant:** To automate hardware provisioning.
* **Git:** To clone this repository.
* **Ansible:** For configuration management (installed via WSL2 on Windows, or natively on Mac/Linux).

## Deployment Instructions

### 1. Clone the Repository and Provision Hardware
Open your host terminal (e.g., Windows PowerShell) and run:
```bash
git clone [https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git](https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git)
cd YOUR_REPO_NAME
vagrant up
# Copy the freshly generated keys into the root of the project
cp ./.vagrant/machines/vm1/virtualbox/private_key ./vm1_key
cp ./.vagrant/machines/vm2/virtualbox/private_key ./vm2_key
cp ./.vagrant/machines/vm3/virtualbox/private_key ./vm3_key

# Secure the keys (Strictly required by SSH)
chmod 600 vm1_key vm2_key vm3_key
# With the infrastructure running and keys secured, deploy the Nginx web servers simultaneously:
ansible-playbook -i inventory.ini setup-web.yml

#Gemini said
Structuring your documentation like this is exactly the kind of repository hygiene expected on enterprise engineering teams, which will be fantastic practice as you head into your software engineering internship at Marvell Technology this summer.

Since you have two different scenarios (waking up tomorrow to keep working vs. showing someone how to download your code from GitHub), it is best to have two distinct sets of instructions.

Here are the two README templates.

README 1: For Your Local PC (The "Next Day" Guide)
You can save this locally as something like LOCAL_DEV_GUIDE.md just for yourself. This assumes you already built the project yesterday, closed your laptop, and just want to turn it back on today.

Markdown
# Local Development Guide: Resuming the Project

This guide is for restarting the local Infrastructure as Code (IaC) environment after the host machine has been rebooted or the VMs have been halted.

## 1. Start the Virtual Machines (Windows PowerShell)
You do not need to rebuild the machines from scratch. Vagrant saved their state.
1. Open Windows PowerShell.
2. Navigate to your project folder:
   ```powershell
   cd C:\Users\rwcir\OneDrive\Desktop\VM-Project
Boot the machines back up:

PowerShell
vagrant up
(Note: This will be much faster than the first time, as it only needs to power them on, not download the OS).

2. Verify the Web Servers
Your Nginx web servers and custom HTML files are saved on the VMs. Open a browser and navigate to the local IPs to confirm they are running:

http://192.168.56.11

http://192.168.56.12

http://192.168.56.13

3. Applying Code Changes (WSL / Ubuntu Terminal)
If you edit the setup-web.yml file to change the website or install new software, you need to push those changes using Ansible.

Open your Ubuntu terminal.

Navigate to the mounted Windows folder:

Bash
cd /mnt/c/Users/rwcir/OneDrive/Desktop/VM-Project
Run the playbook again:

Bash
ansible-playbook -i inventory.ini setup-web.yml
4. Shutting Down
When finished working for the day, save your laptop's RAM by powering off the VMs from Windows PowerShell:

PowerShell
vagrant halt

---

### README 2: For GitHub (The "Fresh Clone" Guide)
This is what your actual `README.md` file on GitHub should look like. This tells a professor, a recruiter, or a teammate exactly how to download your code onto a brand new laptop and make it work from scratch.

```markdown
# Multi-Node Automated Web Infrastructure

## Overview
This project demonstrates a fully automated Infrastructure as Code (IaC) pipeline. It provisions three local Ubuntu virtual machines with varying hardware specifications using **Vagrant** and automatically configures them as Nginx web servers using **Ansible**.

## Prerequisites
To run this project on a new machine, you must have the following installed:
* **VirtualBox:** The underlying hypervisor.
* **Vagrant:** To automate hardware provisioning.
* **Git:** To clone this repository.
* **Ansible:** For configuration management (installed via WSL2 on Windows, or natively on Mac/Linux).

## Deployment Instructions

### 1. Clone the Repository and Provision Hardware
Open your host terminal (e.g., Windows PowerShell) and run:
```bash
git clone [https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git](https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git)
cd YOUR_REPO_NAME
vagrant up
Vagrant will download the Ubuntu 22.04 image and launch all three virtual machines.

2. Secure the New SSH Keys (WSL / Linux Terminal)
Because the .vagrant folder and SSH keys are blocked by .gitignore for security, Vagrant generates brand new keys when vagrant up is run on a new machine. You must copy these new keys to your Ansible environment and secure them.

From your WSL/Linux terminal inside the project directory:

Bash
# Copy the freshly generated keys into the root of the project
cp ./.vagrant/machines/vm1/virtualbox/private_key ./vm1_key
cp ./.vagrant/machines/vm2/virtualbox/private_key ./vm2_key
cp ./.vagrant/machines/vm3/virtualbox/private_key ./vm3_key

# Secure the keys (Strictly required by SSH)
chmod 600 vm1_key vm2_key vm3_key
3. Deploy the Software via Ansible
With the infrastructure running and keys secured, deploy the Nginx web servers simultaneously:

Bash
ansible-playbook -i inventory.ini setup-web.yml

#Verification
Navigate to the statically assigned IP addresses in any web browser to view the deployed web pages:

http://192.168.56.11 (vm1)

http://192.168.56.12 (vm2)

http://192.168.56.13 (vm3)

#To safely halt the machines without destroying data:
vagrant halt
#To completely destroy the environment and free up disk space:
vagrant destroy

```
