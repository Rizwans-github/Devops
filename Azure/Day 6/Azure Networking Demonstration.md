# Day-7: Azure Networking Demo – VNet, Firewall, NSG & Bastion

## 🎯 Objective

* Show how to set up secure communication between VMs using Azure networking tools.
* Demonstrate NSG, Firewall, and Bastion access in a practical project.

## 🔧 Setup Overview

1. **Create Resource Group**

   * Acts as a container to hold all your Azure resources for this demo.

2. **Create Virtual Network (VNet)**

   * Your private network in Azure where all your resources will be placed.

   * Address space: 10.0.0.0/16 (a large range to accommodate multiple subnets)

   * Subnets (dividing the network logically):

     * WebSubnet: 10.0.1.0/24 → For hosting the frontend web server
     * AppSubnet: 10.0.2.0/24 → For backend app logic
     * DBSubnet: 10.0.3.0/24 → For database VM
     * AzureFirewallSubnet: 10.0.4.0/24 → Mandatory name for placing Azure Firewall
     * AzureBastionSubnet: 10.0.5.0/24 → Mandatory name for Azure Bastion service

## 🔐 Security Configurations

### Network Security Groups (NSGs)

* Like mini firewalls for each subnet
* Attach to Web, App, and DB subnets
* Rules set:

  * Allow only HTTP/HTTPS traffic to the web subnet
  * Allow only internal traffic to the DB subnet
  * Deny everything else by default for safety

### Azure Firewall

* Acts as a centralized, stateful firewall
* Deployed in its own subnet: AzureFirewallSubnet
* A custom route table is applied to other subnets so traffic flows through the firewall
* Rules:

  * Allow access to essential Microsoft services (for updates/DNS)
  * Block all other internet traffic unless explicitly allowed

### Azure Bastion

* A secure way to connect to VMs using browser (RDP/SSH) without assigning public IPs
* Keeps your VMs private and reduces attack surface

## 💻 VM Deployment

* Created three virtual machines in their respective subnets:

  * WebVM → Handles web traffic in WebSubnet
  * AppVM → Application logic in AppSubnet
  * DBVM → Stores and processes data in DBSubnet
* Tested RDP/SSH access using Bastion for all VMs

## ✅ Validation Steps

* Checked that subnets can’t be accessed unless rules allow
* Verified all internet traffic routes through the firewall
* Ensured WebVM, AppVM, and DBVM can talk to each other based on rules
* Successfully connected to VMs using Azure Bastion with no public IPs

## 🎓 Analogy for Beginners – College Hostel Example

* **VNet** = Your entire college campus
* **Subnets** = Different hostel blocks (WebBlock, AppBlock, DBBlock)
* **NSGs** = Security guards for each block checking who can enter or leave
* **Azure Firewall** = The main campus gate with strict security and cameras
* **Route Table** = Maps/signboards inside campus directing movement
* **Azure Bastion** = A guest entry gate where friends can visit students without directly entering the hostel (secure entry)
* **VMs** = Students in each block
* Goal: Let students from different blocks talk securely, block outsiders unless permitted, and allow guest visits safely

