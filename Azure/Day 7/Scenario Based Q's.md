# Day-8: Azure Networking Interview Questions – Scenario Based

## 🎯 Purpose

* Prepare for Azure Networking interviews with real-world questions.
* Understand how to approach and answer scenario-based networking problems.

## 📌 Common Interview Scenarios

### 1. **How do you secure communication between two VMs in different subnets?**

* Place VMs in separate subnets within the same VNet to logically isolate traffic.
* Use Network Security Groups (NSGs) on each subnet to restrict traffic.
* Only open required ports (e.g., port 1433 for SQL traffic).
* **Tip:** Always use "Deny by default" strategy and only allow minimal traffic needed for functionality.

### 2. **How do you restrict outbound internet traffic from a subnet?**

* Create a User Defined Route (UDR) with 0.0.0.0/0 pointing to the Azure Firewall’s private IP.
* Attach the route table to the required subnet.
* In Azure Firewall, define rules that allow/deny outbound traffic.
* **Use case:** Enterprises wanting to avoid direct internet access from internal servers.

### 3. **How to allow access to Azure services (e.g., DNS, update servers) while blocking all other internet?**

* In Firewall rules, allow specific service tags like `AzureCloud`, `WindowsUpdate`, or `AzureActiveDirectory`.
* Deny everything else with a catch-all rule.
* **Important:** Ensure firewall has outbound access to these services for platform functionality.

### 4. **How to securely access VMs without public IPs?**

* Use Azure Bastion for secure and private RDP/SSH access over the portal.
* No public IP is assigned to the VM, reducing attack surface.
* **Pro:** No inbound NSG rules needed for RDP/SSH.

### 5. **Difference between NSG and Azure Firewall?**

* **NSG**:

  * Works at L3/L4 (IP & port based)
  * Simple rules; applied per subnet or NIC
  * No logging or advanced features
* **Azure Firewall**:

  * Stateful, works at L3–L7
  * Supports FQDN filtering, application rules, NAT, SNAT
  * Centralized and log-enabled with threat intelligence

### 6. **Difference between NSG and ASG?**

* **NSG (Network Security Group)**: A container of access control rules.

  * Attached to subnets or NICs to allow/deny traffic.
* **ASG (Application Security Group)**: Logical grouping of VMs by function (e.g., all web servers).

  * Used within NSG rules to simplify target referencing.
  * **Example:** Instead of allowing traffic to a specific IP, you allow it to `Web-ASG`.
* **Together:** NSGs define the rules; ASGs help apply them easily to groups of VMs.

### 7. **How would you isolate backend from frontend in a 3-tier app?**

* Create three subnets: Web, App, DB
* Use NSGs:

  * Allow only Web → App (e.g., port 443)
  * Allow App → DB (e.g., port 1433)
  * Block Web ↔ DB directly
* **Result:** Each layer is protected and only talks to the next one.

### 8. **Can two VNets in different regions talk?**

* Yes, using **Global VNet Peering**
* Enables private communication between VNets across regions
* **Benefit:** Uses Microsoft backbone (no internet), low latency
* Remember to allow traffic in NSG and route tables

### 9. **How do you force all internet traffic to go via Azure Firewall?**

* Add a route in the route table: `0.0.0.0/0` next hop = Azure Firewall private IP
* Associate that route table to required subnets
* This ensures even DNS, update checks, and web traffic goes through the firewall

### 10. **Are NSGs stateful or stateless?**

* NSGs are **stateful**.
* If you allow inbound traffic on a port, the response outbound traffic is automatically allowed.

### 11. **Advantages of Resource Groups**

* Logical container for Azure resources.
* Helps manage, monitor, and apply RBAC/permissions at a grouped level.
* Useful for lifecycle management and cost segregation.

### 12. **Custom Data vs User Data in VM provisioning**

* **Custom Data**: Script runs only once at the VM’s first boot.
* **User Data**: Can be fetched and reused; sometimes more flexible for longer use.
* Used to configure VMs post-deployment without manual intervention.

### 13. **Difference between Azure Load Balancer and Application Gateway**

| Feature         | App Gateway (Layer 7) | Load Balancer (Layer 4) |
| --------------- | --------------------- | ----------------------- |
| Routing         | URL, host-based       | IP/port based           |
| SSL Termination | Yes                   | No                      |
| WAF Support     | Yes                   | No                      |

* **App Gateway**: Ideal for web apps, with URL-based routing and WAF support.
* **Load Balancer**: Ideal for non-HTTP workloads (TCP, UDP, RDP, etc.)

### 14. **High-Level Architecture Question Walkthrough**

* DNS resolves domain to public IP.
* Azure Front Door/App Gateway handles SSL and routing.
* Traffic hits frontend (web servers in WebSubnet).
* NSGs control layer-to-layer access.
* AppVMs talk to DBVMs in private network.
* Admins use Bastion to connect securely.

## ✅ Quick Revision Tips

* Understand NSG vs Firewall: use NSGs for basic subnet-level rules; Firewall for advanced, centralized control.
* NSG vs ASG: NSG defines rules; ASG simplifies rule targeting via logical VM grouping.
* Route tables = packet GPS → use to steer traffic as needed.
* Bastion = secure remote access without opening ports
* VNet Peering = internal expressway between VNets (regional or global)
* Use Resource Groups to organize & secure Azure projects.
* Be clear about Layer 4 vs Layer 7 differences in Load Balancing.
