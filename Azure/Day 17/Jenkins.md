## Jenkins Notes (Till 37:11)

### Setup

* Jenkins is a CI/CD tool.
* Install Jenkins, unlock using the admin password from file.
* Install suggested plugins and create admin user.

### Freestyle Job

* Create a job from dashboard → Freestyle project.
* Configure Git repo, add shell build steps (e.g., `python3 hello.py`).
* Trigger build and check console output.

### Agents

* Jenkins uses master-agent model.
* Add agents via "Manage Nodes and Clouds".
* Install Docker plugin to use Docker agents.
* Use `alpine/socat` to expose Docker socket.

### Docker Agent Setup

* Use image: `jenkins/agent:alpine-jdk11`.
* Set workspace: `/home/jenkins`, add label.
* Restrict jobs to this agent using labels.
* Use custom image for complex builds.
* Poll Git with cron (`*/5 * * * *`) for auto-trigger.

### Jenkins vs Argo CD

* **Jenkins**: Handles CI/CD; script-driven; more control and plugins.
* **Argo CD**: Focused on GitOps-based CD for Kubernetes.

### Key Differences

* Jenkins is general-purpose; Argo CD is Kubernetes-specific.
* Jenkins triggers pipelines; Argo CD syncs K8s with Git state.
* Jenkins needs manual K8s handling; Argo CD automates it.

### Which to Use?

* Use **Jenkins** if: you need CI + non-Kubernetes/CD tasks.
* Use **Argo CD** if: you want GitOps with Kubernetes.

### Replacement?

* Jenkins can push to Argo CD via GitOps.
* Argo CD can't fully replace Jenkins CI.
* Ideal setup: Jenkins for CI → Argo CD for CD.
