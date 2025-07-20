# Python Azure Pipeline

This guide walks through the complete flow of setting up a CI/CD pipeline for a Python app using Docker and Azure DevOps.

## Simplified Explanation

You're building a Python app. You want to:

* Write and test the code ✅
* Package it using Docker 🐳
* Push it to Azure DevOps ☁️
* Let Azure automatically test it every time you update code 🛠️

Azure DevOps will do the repetitive tasks (install, test, build) every time you push code — this is CI (Continuous Integration).

## Create a Python App

### Folder Structure

```plaintext
my-python-app/
├── app.py
├── requirements.txt
└── test_app.py
```

**app.py**

```python
def add(a, b):
    return a + b

if __name__ == "__main__":
    print(add(3, 4))
```

**test\_app.py**

```python
from app import add

def test_add():
    assert add(3, 4) == 7
```

**requirements.txt**

```
pytest
```

This is a simple calculator-like app with one test.

## Dockerize the App

**Dockerfile**

```Dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["python", "app.py"]
```

**Explanation:**

* Starts from a small Python image
* Copies your code
* Installs requirements
* Runs app.py when the container starts

**Build and Run**

```bash
docker build -t my-python-app .
docker run my-python-app
```

## Push Code to GitHub (Optional)

```bash
git init
git remote add origin https://github.com/your-username/my-python-app.git
git add .
git commit -m "Initial commit"
git push -u origin main
```

## Create Azure DevOps Project

* Go to Azure DevOps
* Click New Project
* Name it something like Python-CI-CD
* Push or import your code into Repos

## Create Azure DevOps Pipeline (CI)

**azure-pipelines.yml**

```yaml
trigger:
  - main

pool:
  vmImage: 'ubuntu-latest'

stages:
  - stage: BuildAndTest
    jobs:
      - job: PythonJob
        steps:
          - task: UsePythonVersion@0
            inputs:
              versionSpec: '3.9'
              addToPath: true
          - script: pip install -r requirements.txt
            displayName: 'Install Dependencies'
          - script: pytest test_app.py
            displayName: 'Run Tests'
```

**What Each Section Does**

| Section   | What it does                                 |
| --------- | -------------------------------------------- |
| `trigger` | Starts pipeline when you push to main branch |
| `pool`    | Uses a clean Ubuntu machine to run tasks     |
| `stage`   | Logical block called BuildAndTest            |
| `job`     | A set of steps that runs together            |
| `steps`   | Actual commands/tasks like install and test  |

## Add Docker Build to Pipeline (Optional)

Add this inside `steps` if you want to build a Docker image too:

```yaml
- script: docker build -t my-python-app .
  displayName: 'Build Docker Image'
```

## After Pipeline Setup: Using ACR and Self-Hosted Agent

### Azure Container Registry (ACR)

* Private place to store Docker images
* Lets Azure services pull prebuilt containers
* Fast, secure, and versioned app delivery

### Pipeline Builds Docker Image

The pipeline runs on an agent and:

* Installs requirements
* Runs tests
* Builds Docker image
* Pushes it to ACR

**Example Docker task in YAML:**

```yaml
- task: Docker@2
  inputs:
    command: buildAndPush
    containerRegistry: 'AzureACRConnection'
    repository: 'my-python-app'
    dockerfile: 'Dockerfile'
    tags: |
      $(Build.BuildId)
      latest
```

## Set Up a Self-Hosted Agent Using Git Bash

Instead of using Microsoft-hosted agents, you can run the pipeline on your own machine:

### Step-by-Step:

**Download Agent**

* From: Azure Pipelines Agent Releases
* Extract to a folder (e.g., `C:\agent`)

**Create Personal Access Token (PAT)**

* Azure DevOps → User Settings → Personal Access Tokens → New Token
* Give access to Agent Pools (Read & Manage)
* Copy the token

**Configure the Agent (in Git Bash)**

```bash
./config.sh --unattended \
  --url https://dev.azure.com/YOUR_ORG \
  --auth pat \
  --token YOUR_TOKEN \
  --pool Default \
  --agent my-agent-name
```

✅ This registers your machine as an agent with Azure DevOps

**Run the Agent**

```bash
./run.sh
```

🎯 Your terminal will say `Listening for jobs...`

## Final Flow Recap

1. You push code to repo → triggers pipeline
2. Pipeline runs (on cloud or your machine)
3. Runs tests, builds Docker image
4. Pushes image to ACR
5. Image is now ready for deployment (App Service, AKS, etc.)

## Addressing Questions

### Why not just use GitHub?

While GitHub supports code versioning and workflows through Actions, Azure DevOps offers a full suite of tools tailored for enterprise environments. It integrates better with Azure services like ACR, AKS, and App Services. For larger teams or projects heavily using Azure, this integration can simplify access management, security, and service connectivity.

### Why use Docker?

Docker packages your application along with all its dependencies into a single container. This ensures consistency across development, testing, and production environments. It prevents the classic "it works on my machine" issue, especially when multiple developers or systems are involved.

### Why use ACR?

Azure Container Registry (ACR) acts as a secure, private Docker registry within your Azure ecosystem. It allows you to store, manage, and version Docker images. With ACR, you get tight integration with Azure services, role-based access control, and geo-replication support to ensure high availability across regions.

### Can't I just put the code for requirements in my source code so it does everything?

You technically can, but that method doesn't scale well in production. Embedding install commands in your app adds complexity and increases startup time. Docker ensures your dependencies are installed once during build, making container start-up faster and more reliable.

### Why push to ACR when I can build the image anywhere?

Building locally is fine for testing, but ACR centralizes image management and access for teams. It ensures that everyone deploys from a consistent, versioned image source. Plus, services like Azure Kubernetes Service (AKS) can pull directly from ACR securely.

### What does building mean if writing code means it's already built?

Writing code is the authoring step. Building refers to converting the source code into an executable form. This could involve dependency resolution, packaging, compiling (if needed), and preparing the code to run in a consistent, controlled environment like a Docker container.

### Is Git Bash necessary for setting up the agent?

Git Bash is recommended on Windows because it offers a Unix-like shell that aligns better with Azure’s bash-based setup scripts. While not mandatory, it helps avoid command compatibility issues that may arise with PowerShell or CMD.

### Can I use a self-hosted agent for all types of projects?

Absolutely. Self-hosted agents offer flexibility in terms of hardware, OS, and installed tools. They’re ideal for custom environments, legacy systems, or when Microsoft-hosted agents don’t support your stack. However, they also require you to manage security, scaling, and maintenance.
