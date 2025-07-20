# Day 10 – Automating Azure Resources with Azure CLI ⚙️  
*My personal notes from the course*  

**Video Duration:** ~20 minutes  
**Source:** Free Azure Course by Abhishek Veeramalla  

---

## 1. What is Azure CLI? (My Understanding)  
- A **command-line tool** to control Azure resources from terminal (like PowerShell or Bash).  
- Works on **Windows/macOS/Linux** – great for automation scripts.  
- Alternative to clicking buttons in the Azure Portal.  

> *Why I care:* If I need to create 100 VMs, CLI is faster than manual clicks!  

---

## 2. Why Use CLI Over Portal?  
- **Reproducible:** Scripts can be saved/versioned (Git).  
- **Automation:** Works with DevOps tools (GitHub Actions, Azure Pipelines).  
- **Large-scale:** Easier to manage many resources.  

---

## 3. How to Install Azure CLI  
*(Trying to remember the options)*:  
- **Windows:** `choco install azure-cli` (via Chocolatey)  
- **macOS:** `brew install azure-cli`  
- **Linux:** `sudo apt install azure-cli` (Debian/Ubuntu)  
- Also available via Docker/Python (`pip install azure-cli`)  

> *Note to self:* Always check official docs for latest install steps.  

---

## 4. Basic Commands I Learned  
```bash
az login                  # Logs me into Azure account
az account list           # Shows my subscriptions
az group create --help    # Get help for any command
```

---

## 5. Creating Resource Groups (My First Try)  
```bash
az group create --name MyTestRG --location eastus
```
- `--name`: What I want to call the group.  
- `--location`: Where it lives (e.g., `eastus`, `westeurope`).  

To list all groups:  
```bash
az group list --output table  # Shows output as a clean table
```

---

## 6. Creating a VM (Example)  
```bash
az vm create \
  --resource-group MyTestRG \
  --name MyFirstVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```
- `\` breaks long commands into readable lines.  
- `--generate-ssh-keys`: Auto-creates SSH keys for secure login.  

---

## 7. Storage Account Automation  
```bash
az storage account create \
  --name mystorage123 \
  --resource-group MyTestRG \
  --location eastus \
  --sku Standard_LRS
```
- `--sku Standard_LRS`: Chooses cheap local storage (other options exist).  

---

## 8. Scripting Tips (New to Me!)  
### Using Variables:  
```bash
LOCATION="eastus"
RESOURCE_GROUP="LearningRG"
az group create --name $RESOURCE_GROUP --location $LOCATION
```

### Loop to Create 3 VMs:  
```bash
for i in 1 2 3; do
  az vm create \
    --resource-group $RESOURCE_GROUP \
    --name VM-$i \
    --image UbuntuLTS \
    --no-wait  # Don't wait for each VM to finish
done
```
- `--no-wait`: Lets the script continue without pausing.  

---

## 9. DevOps Integration (Future Learning)  
- Can use CLI in **Azure Pipelines** (YAML).  
- GitHub Actions can run `az` commands too.  

---

## 10. Best Practices (For My Reference)  
1. **Always use variables** – avoids hardcoding names/locations.  
2. **Filter output with `--query`**:  
   ```bash
   az vm list --query "[?name=='MyFirstVM']" -o json
   ```  
3. **Log out in shared systems**:  
   ```bash
   az logout
   ```  

---

✅ **My Summary**  
Azure CLI is powerful for automation. I need to practice:  
- Basic commands daily.  
- Scripting with loops/variables.  
- Integrating with GitHub/Azure DevOps.  

*Next goal:* Try automating a full project (RG + VM + Storage) in one script!  
