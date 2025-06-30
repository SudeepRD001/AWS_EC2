# ☁️ Cloud-Based Development Environment with AWS EC2 & VS Code Remote SSH

This guide walks you through the steps to create a cloud-based development environment using AWS EC2, Git Bash, and VS Code's Remote - SSH extension. You'll be able to clone a GitHub repository and edit code directly on a cloud VM.

---

## 🛠️ Prerequisites

- ✅ AWS account (Free Tier eligible)
- ✅ Git Bash installed on your Windows machine
- ✅ Visual Studio Code installed
- ✅ VS Code "Remote - SSH" extension installed
- ✅ Public GitHub repository (or use ours: [AWS_EC2](https://github.com/SudeepRD001/AWS_EC2))

---

## 🚀 Step 1: Launch an EC2 Instance

1. **Login to AWS Console** → Go to **EC2 Dashboard**
2. Click **Launch Instance**
3. Configuration:
   - **Name**: `dev-instance`
   - **AMI**: Ubuntu Server 22.04 LTS
   - **Instance type**: `t2.micro` (Free Tier)
   - **Key pair**: Create new key pair → RSA → `dev-key.pem`
   - **Network settings**: Allow **SSH (port 22)** from `0.0.0.0/0`
4. Click **Launch Instance**
5. Wait until the instance state = `running`
6. Copy the **Public IPv4 address**

---

## 🗝️ Step 2: Configure SSH on Local Machine

### 2.1 Move PEM File and Set Permissions

1. Open **Git Bash**
2. Run the following:

```bash
mkdir -p ~/.ssh
mv /c/Users/YOUR_USERNAME/Downloads/dev-key.pem ~/.ssh/
chmod 400 ~/.ssh/dev-key.pem
```
Replace YOUR_USERNAME with your Windows username.

### 2.2 SSH into EC2 Ubuntu Instance

This document explains how to connect to your EC2 Ubuntu server using SSH and a private key file.

---

## 📌 Prerequisites

Before proceeding, ensure you have the following:

- An EC2 instance running Ubuntu
- The **public IP** address of your EC2 instance
- Your **private key file** (e.g., `dev-key.pem`) downloaded and saved under `~/.ssh/`

---

## 🔐 Test SSH Connection

Use the following command to SSH into your EC2 instance:

```bash
ssh -i ~/.ssh/dev-key.pem ubuntu@<your-ec2-public-ip>
```
Example:
```bash
ssh -i ~/.ssh/dev-key.pem ubuntu@3.123.45.67
```
✅ If successful, you'll be logged into your EC2 Ubuntu server.

# 🔄 Step 3: Clone the GitHub Repository on EC2

Once you're logged into your EC2 instance via SSH, follow the steps below to install Git and clone the repository.

---

## ⚙️ Install Git and Clone the Repo

```bash
sudo apt update && sudo apt install git -y
git clone https://github.com/SudeepRD001/AWS_EC2.git
cd AWS_EC2
```
✅ Your repo is now on the cloud server.

# 🧠 Step 4: Setup VS Code Remote - SSH

This section explains how to connect your local VS Code to your EC2 instance using the **Remote - SSH** extension.

---

## 4.1 🧩 Install Remote SSH Extension

1. Open **Visual Studio Code**
2. Press `Ctrl + Shift + X` to open the **Extensions** tab
3. Search for: `Remote - SSH`
4. Click **Install** on the official extension by Microsoft

---

## 4.2 ⚙️ Configure SSH in VS Code

1. Press `Ctrl + Shift + P` to open the Command Palette
2. Search and run: `Remote-SSH: Open SSH Configuration File...`
3. Choose this file path when prompted: `C:/Users/YOUR_USERNAME/.ssh/config`

4. Add the following configuration to the file:

```ssh
Host aws-dev
    HostName <your-ec2-public-ip>
    User ubuntu
    IdentityFile C:/Users/YOUR_USERNAME/.ssh/dev-key.pem
    IdentitiesOnly yes
```
🔁 Replace <your-ec2-public-ip> with your actual EC2 instance's public IP address.

## 4.3 🔌 Connect to EC2 from VS Code

Once you've configured your SSH settings, follow these steps to connect to your EC2 instance via VS Code:

---

### 🪟 Steps:

1. Press `Ctrl + Shift + P` to open the **Command Palette**
2. Run the command: `Remote-SSH: Connect to Host...`
3. From the list of configured hosts, select: `aws-dev`
  

4. A new VS Code window will open, and you'll be connected to your EC2 instance.

> ✅ Now you're editing files **live on the cloud** directly from VS Code! 🚀

---

## 🧩 Tips

- You can open folders and edit files just like on your local machine.
- Terminal access is also available from the VS Code terminal (`` Ctrl + ` ``).
- Make sure your EC2 instance is **running** and your network allows outgoing SSH (port 22) connections.

---
# 📝 Step 5: Edit the README or Code Files

Once you're connected to your EC2 instance via VS Code, you can easily modify your project files in real-time.

---

## ✍️ Steps to Edit

1. In VS Code, open the file explorer sidebar (if not visible, press `Ctrl + B`)
2. Navigate to the cloned folder: `AWS_EC2`
3. Open `README.md` or any other file you want to edit
4. Make your changes using the editor
5. Press `Ctrl + S` to save your changes

> ✅ Your updates are saved directly on the cloud server!

---

## 📌 Tip

You can also use the integrated terminal in VS Code (`` Ctrl + ` ``) to run Git commands or execute scripts directly on the EC2 instance.

---
# 🧪 Step 6: Verify Git Status and Commit Changes

After editing your files on the EC2 instance, you can commit and push the changes to your GitHub repository.

---

## ✅ Steps to Commit and Push

```bash
cd /AWS_EC2
git status
git add README.md
git commit -m "Updated README with setup steps"
git push origin main
```
✅ Ensure your repository is forked correctly and that you have push permissions on the remote repo.

## 🔒 Notes

If you face authentication issues while pushing to GitHub:

- Make sure you’ve configured **SSH keys** with your GitHub account  
  OR  
- Use **GitHub CLI** with a **Personal Access Token (PAT)** for HTTPS-based authentication

---

### 📁 Commit Multiple Files

To stage **all modified files** at once, replace `README.md` with `.` in the `git add` command:

```bash
git add .
```
Then continue with commit and push:
```bash
git commit -m "Your commit message"
git push origin main
```
✅ This is useful when you've made changes to multiple files and want to commit them together.

