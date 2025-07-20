# Python Project CI/CD with Azure DevOps

This guide walks through the complete flow of setting up a CI/CD pipeline for a Python app using Docker and Azure DevOps.

---

## 🧠 Simplified Explanation

You're building a Python app. You want to:

1. Write and test the code ✅
2. Package it using Docker 🐳
3. Push it to Azure DevOps ☁️
4. Let Azure automatically test it every time you update code 🛠️

Azure DevOps will do the boring stuff (install, test, build) **every time you push code** — this is CI (Continuous Integration).

---

## 1. ⚙️ Create a Python App

### Folder Structure

```
my-python-app/
├── app.py
├── requirements.txt
└── test_app.py
```

### app.py

```python
def add(a, b):
    return a + b

if __name__ == "__main__":
    print(add(3, 4))
```

### test\_app.py

```python
from app import add

def test_add():
    assert add(3, 4) == 7
```

### requirements.txt

```
pytest
```

This is a simple calculator-like app with one test.

---

## 2. 🐳 Dockerize the App

### Dockerfile

```dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

CMD ["python", "app.py"]
```

What this does:

* Starts from a small Python image
* Copies your code
* Installs requirements
* Runs `app.py` when the container starts

### Build and Run

```bash
docker build -t my-python-app .
docker run my-python-app
```

Now your app runs inside a container.

---

## 3. 🧑‍💻 Push Code to GitHub (Optional)

```bash
git init
git remote add origin https://github.com/your-username/my-python-app.git
git add .
git commit -m "Initial commit"
git push -u origin main
```

---

## 4. ☁️ Create Azure DevOps Project

1. Go to [https://dev.azure.com](https://dev.azure.com)
2. Click **New Project**
3. Name it something like `Python-CI-CD`
4. Push or import your code into **Repos**

Azure DevOps gives you a full workspace for code + pipelines.

---

## 5. ⏪ Create Azure DevOps Pipeline (CI)

### azure-pipelines.yml

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

---

### 🔍 What Each Section Does

| Section   | What it does                                 |
| --------- | -------------------------------------------- |
| `trigger` | Starts pipeline when you push to main branch |
| `pool`    | Uses a clean Ubuntu machine to run tasks     |
| `stage`   | Logical block called `BuildAndTest`          |
| `job`     | A set of steps that runs together            |
| `steps`   | Actual commands/tasks like install and test  |

---

## 🤖 Add Docker Build to Pipeline (Optional)

Add this inside `steps` if you want to build a Docker image too:

```yaml
- script: docker build -t my-python-app .
  displayName: 'Build Docker Image'
```

---

