# 🚀 Deploy Jenkins on Azure VM – Beginner Level

## 1. Why Jenkins on VM?

* Jenkins automates build/test/deploy pipelines.
* Running it on an Azure VM gives you full control over setup and environment.

---

## 2. Choose the Right Azure VM

* Pick General Purpose VM (e.g., B-series or D-series).
* Consider CPU, RAM, and storage based on your Jenkins load.
* Use an OS like Ubuntu or Windows Server.

---

## 3. Types of Azure Virtual Machines

| Type     | Purpose                                |
| -------- | -------------------------------------- |
| D-series | General purpose – balanced             |
| E-series | Memory-optimized – for Redis, etc.     |
| F-series | Compute-optimized – CPU-heavy tasks    |
| L-series | Storage-optimized – I/O intensive apps |
| N-series | GPU – for AI/ML workloads              |
| B-series | Budget-friendly – for learning/demo    |

---

## 4. Create Azure VM

1. In Azure Portal: Create Resource → Virtual Machine.
2. Choose:

   * OS (Ubuntu/Windows),
   * Admin account (SSH key or password),
   * VM size.
3. Under Networking: allow inbound **TCP port 8080** for Jenkins.
4. Review and create.

---

## 🔐 5. Connecting to the VM via SSH

1. Set permissions:

```bash
chmod 600 firstVM_privateKey.pem
```

2. Connect to VM:

```bash
ssh -i firstVM_privateKey.pem azureuser@<public-ip>
```

* Use Git Bash (on Windows) or iTerm (on Mac) to run these commands.

---

## 🚀 6. Deploying Jenkins on the VM

### Update packages & install Java:

```bash
sudo apt update
sudo apt install openjdk-11-jdk -y
```

### Install Jenkins:

```bash
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins -y
```

### Verify status:

```bash
systemctl status jenkins
```

### Access Jenkins:

Open in browser:

```
http://<public-ip>:8080
```

---

## 🔒 7. Opening Ports in Azure (NSG)

* Port 22 (SSH) is open by default.
* To allow Jenkins:

  * Go to Network Security Group (NSG)
  * Create a new inbound rule:

    * **Source**: Any
    * **Destination**: Any
    * **Port**: 8080
    * **Protocol**: Any
    * **Action**: Allow

---

## 🌐 8. Introduction to Virtual Machine Scale Sets (VMSS)

* Like AWS Auto Scaling Groups
* Automatically increases or decreases the number of VMs
* Ideal for handling **fluctuating traffic**
* Will be covered in more detail in later sessions

---

## 📝 Summary of Key Tools & Concepts

| Tool/Concept | Description                                     |
| ------------ | ----------------------------------------------- |
| Hypervisor   | Enables virtualization for VMs                  |
| VM Sizes     | D, E, F, L, N series for different workloads    |
| SSH Keys     | Secure way to log into VMs                      |
| NSG Rules    | Manage traffic to/from VMs                      |
| Jenkins      | Automation server for CI/CD                     |
| VMSS         | Auto-scaling group of VMs for high availability |

---

## ✅ TL;DR

1. Create an Azure VM (Ubuntu/Windows).
2. Open TCP port 8080.
3. Install Java & Jenkins.
4. Access Jenkins via browser.
5. Use proper VM size and add storage as needed.

Happy automating! 🎉

---

## 🧑‍🎓 Explain Like I'm New in College (Beginner-Friendly)

Jenkins is a tool that helps you automate tasks like building, testing, and deploying code. Instead of doing everything manually, Jenkins does it for you, like a smart assistant.

Here's how you set it up on Azure, even if you're just starting out:

* **Step 1**: Use Azure to create a virtual machine — think of it as a computer running in the cloud.
* **Step 2**: Install Java, which is required for Jenkins to run.
* **Step 3**: Install Jenkins, which will be your automation tool.
* **Step 4**: Open a specific port (8080) on your VM so you can access Jenkins through your web browser.
* **Step 5**: Get the admin password from your VM and log into Jenkins from your browser.
* **Step 6**: Set up plugins and your admin account to start using Jenkins.

Even if you're new to Azure or Jenkins, following these steps one by one will help you learn how cloud computing and automation work. It's a great hands-on way to understand DevOps tools in action!
