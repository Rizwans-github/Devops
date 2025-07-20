# Azure Virtual Network (VNet) – Beginner Level

## 🔍 What is a VNet?

* A **Virtual Network (VNet)** is your own **private network** within Azure.
* It allows Azure resources to communicate securely.
* Similar to a gated community where each house (resource) can talk to each other.

## 🌐 VNet Components

### 1. Subnets

* Sub-divide the VNet.
* Each subnet has its own **IP range** within the VNet.
* Helps organize and secure resources.

### 2. Network Security Group (NSG)

* Acts like a **firewall**.
* Controls **inbound and outbound traffic**.
* Rules based on IP, port, and protocol.

### 3. Peering

* Connects two VNets **privately** without going over the internet.
* Low latency and high bandwidth.

### 4. Route Table

* Controls **traffic flow** between subnets or to external networks.
* Can redirect traffic to firewalls, gateways, etc.

### 5. Virtual Network Gateway

* Connects Azure VNet to:

  * On-premise networks via **VPN**
  * Other VNets using **VNet-to-VNet** connections

## 💠 Use Cases

* Host secure apps and VMs.
* Isolate environments (e.g., dev, test, prod).
* Route and monitor traffic.
* Hybrid connectivity with on-premises systems.

## ✅ Steps to Create a VNet

1. Go to Azure Portal > Create Resource > Networking > Virtual Network
2. Define **Address Space** (e.g., 10.0.0.0/16)
3. Create **Subnets** (e.g., 10.0.1.0/24 for front-end)
4. Attach **NSGs** to subnets or NICs
5. Enable **VNet Peering** or **Gateway** if needed

## ⚠️ Best Practices

* Plan IP ranges to avoid overlaps
* Use **tags** to manage resources
* Apply **NSGs** at subnet level for centralized security
* Monitor traffic using **Network Watcher**
* Use **Azure Firewall or third-party appliances** if advanced security is needed

## 📌 Example Configuration

### Address Space:

* 10.0.0.0/16

### Subnets:

* Frontend: 10.0.1.0/24
* Backend: 10.0.2.0/24

### NSG Rules Example:

* Allow HTTP (port 80) from Internet to Frontend subnet
* Deny all inbound traffic to Backend subnet except from Frontend

### Peering:

* Peer VNet-A (10.0.0.0/16) with VNet-B (10.1.0.0/16)
* Enable traffic forwarding

## 📍 TL;DR

Azure VNet lets you create a **secure, isolated network** for your cloud resources. It includes tools like **subnets**, **NSGs**, **peering**, and **gateways** to control traffic and connectivity.

Video: [Azure VNet Explained - YouTube](https://www.youtube.com/watch?v=6MaGYkDpuJE)


### 🧠 What is a VNet? 
* Think of a **VNet like a private Wi-Fi** in the cloud.
*  Only your devices (like virtual machines or databases) can connect and talk to each other in that space.
  ### 🧩 VNet Has These Parts: 
  1. **Subnets** = rooms inside the house → Divide your network into smaller groups.
  2. **NSG (Network Security Group)** = door rules → Decide **who can enter** or **leave** each room.
  3. **ASG (Application Security Group)** = group tags → Tag rooms with roles and apply door rules to the whole group.
  4. **Peering** = bridge to another house → Connect your VNet to another VNet.
  5. **Route Table** = GPS map → Tells data where to go. 
 6. **Gateway** = main gate to outside world → Connect your VNet to your **home or office** internet securely.

