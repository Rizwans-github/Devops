## 📌 Objective

Automate build and push processes for each microservice using Azure DevOps pipelines.

---

## 🗱️ Microservices Structure

Each service is containerized with its own Dockerfile and isolated build config:

| Service Name       | Language / Framework | Builds to                          |
| ------------------ | -------------------- | ---------------------------------- |
| `auth-svc`         | Node.js              | `username/auth-svc:latest`         |
| `profile-svc`      | Python (Flask)       | `username/profile-svc:latest`      |
| `frontend`         | React                | `username/frontend:latest`         |
| `notification-svc` | .NET                 | `username/notification-svc:latest` |

---

## 🛠️ Step-by-Step Pipeline Creation

### 1. YAML Pipeline per Service

* Navigate **Pipelines → New Pipeline → YAML**.
* Connect to Azure Repos where `microservices-demo` is hosted.
* Save YAML in each service folder: e.g., `auth-svc/azure-pipelines.yml`.

Example (`auth-svc/azure-pipelines.yml`):

```yaml
trigger:
  paths:
    include:
      - auth-svc/**

pool:
  vmImage: 'ubuntu-latest'

variables:
  IMAGE_NAME: 'username/auth-svc'
  TAG: '$(Build.SourceBranchName)-$(Build.BuildId)'

steps:
- task: Docker@2
  displayName: Build & push Docker image
  inputs:
    command: buildAndPush
    containerRegistry: 'DockerHubConnection'
    repository: '$(IMAGE_NAME)'
    dockerfile: 'auth-svc/Dockerfile'
    tags: |
      $(TAG)
      latest

- script: echo "Image $(IMAGE_NAME):$(TAG) built successfully!"
  displayName: 'Confirm build'
```

### 2. Path-Based Triggering

* Ensures only relevant pipelines run on corresponding folder changes.
* Reduces CI execution time and costs.

### 3. Docker Registry Integration

* Use **Service Connection** (`DockerHubConnection`) in Azure DevOps:

  * Navigate: Project Settings → Service connections.
  * Add Docker registry credentials securely (Docker Hub / ACR).
* YAML references this by name.

### 4. Build & Push Logic Breakdown

* `buildAndPush` task:

  * Builds Docker image using service’s Dockerfile.
  * Tags images using branch and build ID (`featureX-123`).
  * Pushes both specific tag and `latest`.
* Tagging strategy:

  * `$(TAG)` for traceability.
  * `latest` for convenience in testing or staging.

### 5. Logging & Validation

* Custom echo script confirms image metadata post-build.
* Consider adding Azure DevOps `Readiness` or `Quality Gate` tasks.

---

## 💡 Advanced Considerations

1. **Secrets Management**

   * Use pipeline variables with `secret: true`.
   * Or link Azure Key Vault for credentials.

2. **Pipeline Templates**

   * Use YAML templates to avoid repetition.
   * Example:

     ```yaml
     # .azure-pipelines-template.yml
     parameters:
       serviceName: ''
     steps:
       - task: Docker@2
         inputs:
           command: buildAndPush
           containerRegistry: 'DockerHubConnection'
           repository: 'username/${{ parameters.serviceName }}'
           dockerfile: '${{ parameters.serviceName }}/Dockerfile'
           tags: |
             $(TAG)
             latest
     ```
   * Then in each service pipeline:

     ```yaml
     trigger:
       paths:
         include:
           - auth-svc/**
     pool: ...
     variables: ...
     steps:
     - template: .azure-pipelines-template.yml
       parameters:
         serviceName: 'auth-svc'
     ```

3. **Caching Dependencies**

   * For Node/Python:

     ```yaml
     - task: Cache@2
       inputs:
         key: 'npm | "$(Agent.OS)" | package-lock.json'
         restoreKeys: |
           npm | "$(Agent.OS)"
         path: ~/.npm
     ```
   * Speeds up CI and reduces build times.

4. **Build Validation**

   * Add `npm test` or `pytest` before Docker build:

     ```yaml
     - script: |
         pip install -r requirements.txt
         pytest --maxfail=1 --disable-warnings -q
       displayName: 'Run Python tests'
     ```

5. **Monorepo vs Polyrepo**

   * This repo uses monorepo, multiple pipelines per path.
   * Could alternatively use single pipeline with multiple jobs:

     ```yaml
     jobs:
     - job: BuildAuth
     - job: BuildProfile
     ```

---

## ✅ Summary

* **CI per service**: isolated, efficient builds.
* **YAML + path filters**: clarity and cost savings.
* **Smart tagging + caching**: traceable and optimized builds.
* **Templates & secrets**: DRY pipelines with secure configs.


