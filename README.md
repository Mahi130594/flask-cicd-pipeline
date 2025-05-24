# Flask CI/CD Application

This repository contains a simple Flask application demonstrating a CI/CD pipeline.

## Jenkins CI/CD Pipeline

This section details the setup and execution of the Jenkins pipeline for this application.

### Prerequisites

* A running Jenkins instance (version X.Y.Z or higher).
* Python 3 installed on the Jenkins agent.
* Necessary Jenkins Plugins installed:
    * Pipeline
    * Git
    * Email Extension
    * Credentials (if using SSH for deployment)
* Access to the GitHub repository.
* A staging environment server (e.g., a Linux VM) for deployment.

### Jenkins Job Setup

1.  **Create a New Pipeline Job:**
    * From the Jenkins dashboard, click "New Item".
    * Enter an item name (e.g., `flask-app-pipeline`).
    * Select "Pipeline" and click "OK".
2.  **General Configuration:**
    * (Optional) Provide a description.
3.  **Build Triggers:**
    * Check "GitHub hook trigger for GITScm polling".
4.  **Pipeline Definition:**
    * Select "Pipeline script from SCM".
    * **SCM:** Git
    * **Repository URL:** `https://github.com/your-username/flask-app-cicd.git` (replace `your-username`)
    * **Credentials:** Add your GitHub credentials if your repository is private, otherwise, none are needed.
    * **Branches to build:** `*/main`
    * **Script Path:** `Jenkinsfile`
5.  **Save** the job configuration.

### GitHub Webhook Configuration

To trigger builds automatically on pushes to the `main` branch:

1.  Go to your GitHub repository: `your-username/flask-app-cicd`.
2.  Navigate to `Settings` -> `Webhooks` -> `Add webhook`.
3.  **Payload URL:** `http://your_jenkins_ip:8080/github-webhook/` (replace `your_jenkins_ip`)
4.  **Content type:** `application/json`
5.  **Which events would you like to trigger this webhook?:** Select "Just the push event."
6.  Ensure "Active" is checked.
7.  Click "Add webhook".

### Pipeline Stages

The `Jenkinsfile` defines the following stages:

* **Checkout:** Clones the GitHub repository.
* **Build:** Creates a Python virtual environment and installs dependencies using `pip`.
* **Test:** Executes unit tests using `pytest`.
* **Deploy:** (Simulated/Placeholder) Deploys the application to a staging environment if tests pass. This stage would typically involve `scp`, `ssh` commands, or integration with deployment tools.

### Notifications

Email notifications are configured to send alerts on pipeline success or failure. Ensure the Email Extension plugin is configured in Jenkins.

### Running the Pipeline

* Push changes to the `main` branch of your GitHub repository.
* Manually click "Build Now" in the Jenkins job.

### Screenshots
