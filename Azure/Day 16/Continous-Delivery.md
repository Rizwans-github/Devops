
# 📦 Day 16 – Azure Artifacts in Azure DevOps CI/CD Pipeline

This note explains how Azure Artifacts are used to manage and share packages between microservices (like `vote`, `result`, and `worker`) in a CI/CD setup using Azure DevOps.

---

## ✅ What You’ll Learn

- What Azure Artifacts are
- How to create and use a private Artifact feed
- How to publish and consume internal packages (e.g., npm or NuGet)
- How this improves your pipeline and microservice architecture

---

## 💡 What is Azure Artifacts?

Azure Artifacts is a **package management system** built into Azure DevOps.  
It supports:

- npm (for Node.js)
- NuGet (for .NET)
- Python
- Maven (Java)

Instead of using **public registries**, you can store and share packages **privately** across your projects and pipelines.

---

## 🔧 Step-by-Step Setup

### 1. Create an Artifact Feed

1. Go to **Azure DevOps > Artifacts**
2. Click **+ New Feed**
3. Name it something like `voting-app-feed`
4. Set visibility to:
   - Your project
   - Or entire organization (if needed)

> 🔐 Optional: Manage permissions so pipelines can publish/consume from it.

---

### 2. Update Pipelines to Use the Feed

Let’s say the `result` service uses a shared internal library published as a NuGet/npm package.

Update the pipeline like this:

#### 📄 `azure-pipelines.yml` (result microservice)

For NuGet (example for .NET apps):


