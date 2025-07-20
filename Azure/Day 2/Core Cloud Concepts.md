## ☁️ Core Cloud Concepts

### 1. Virtualization  
- Creates virtual versions of hardware using a hypervisor.  
- Allows multiple virtual machines (VMs) on one physical server.

### 2. Virtual Machine (VM)  
- A software-based computer with its own OS, CPU, memory, and storage.  
- Runs independently via virtualization.

### 3. API (Application Programming Interface)  
- A communication bridge between software components.  
- Enables automation and integration across cloud services.

---

## 🌍 Azure Infrastructure

### 4. Region  
- A geographical area with multiple data centers (e.g., East US, Central India).  
- Reduces latency by deploying services closer to users.

### 5. Availability Zone (AZ)  
- A physically isolated data center within a region.  
- Ensures high availability and fault tolerance.

### 🔁 Why Azure uses Regions & AZs  
- **Latency Reduction**: Faster response for global users.  
- **High Availability**: Deploy across AZs to avoid downtime.  
- **Disaster Recovery**: One AZ/region down? Others take over.

---

## ⚙️ Cloud Capabilities

### 6. Scalability  
- Ability to handle growing workload by increasing resources.  
- Types:  
  - **Vertical Scaling**: More power to the same server  
  - **Horizontal Scaling**: Add more servers

### 7. Elasticity  
- Auto-adjust resources based on real-time demand.  
- Saves cost by scaling down during low usage.

### 8. Agility  
- Rapid deployment and scaling of apps and services.  
- Encourages fast innovation and testing.

### 9. High Availability  
- Ensures apps stay online with minimal downtime.  
- Achieved through redundancy and AZ-based deployment.

### 10. Fault Tolerance  
- System continues operating despite failures in components.  
- Enabled by backups, replicas, and distributed architecture.

### 11. Disaster Recovery  
- Strategy to restore operations after major failures.  
- Includes automated backups, secondary regions, and replication.

### 12. Load Balancing  
- Distributes user traffic across multiple servers.  
- Prevents overload, improves speed, and enhances uptime.

---

## 🧱 Cloud Service Models

### 13. IaaS (Infrastructure as a Service)  
- Provides VMs, storage, and networking.  
- You manage OS, apps, runtime.  
- Example: Azure VM, Azure Storage

### 14. PaaS (Platform as a Service)  
- Provides platform + runtime for app deployment.  
- You manage app and data only.  
- Example: Azure App Service, Azure SQL DB

### 15. SaaS (Software as a Service)  
- Ready-to-use software, no infra management needed.  
- You just use the application.  
- Example: Microsoft Outlook, Teams

---

## 📊 Visual Comparison: IaaS vs PaaS vs SaaS

| Feature            | IaaS                          | PaaS                            | SaaS                          |
|--------------------|-------------------------------|----------------------------------|-------------------------------|
| Stands For         | Infrastructure as a Service   | Platform as a Service            | Software as a Service         |
| What You Manage    | OS, middleware, runtime, app  | App & data only                  | Just usage (end product)      |
| Provider Manages   | Hardware, network, storage    | Infra + OS + runtime             | Everything                    |
| Control Level      | High                          | Medium                           | Low                           |
| Example Services   | Azure VM, Azure Storage       | Azure SQL DB, App Service        | Outlook, Microsoft Teams      |
| Best For           | Custom setups, legacy apps    | Developers building apps         | End-users needing software    |

---
