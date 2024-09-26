# AWS Elastic Beanstalk Node.js Sample App

This repository contains a sample Node.js web application "Hello World" that is ready to be deployed on **AWS Elastic Beanstalk**. It demonstrates how to configure a **Jenkins pipeline** to automate the deployment of a Node.js application into Elastic Beanstalk while incorporating security scanning via **Snyk**.

---

## Prerequisites

Before proceeding, ensure you have the following:

- **AWS Elastic Beanstalk** environment set up.
- **Jenkins** installed and configured with required plugins (e.g., AWS Elastic Beanstalk Deployment Plugin, Snyk Security Scanner Plugin).
- **Node.js** installed on your local machine for development.
- **Snyk API Token** for security vulnerability scanning.
  
---

## Jenkinsfile

The following `Jenkinsfile` is used to define a CI/CD pipeline for the Node.js sample app that builds, scans for vulnerabilities, and deploys to AWS Elastic Beanstalk.

### Pipeline Overview
The Jenkinsfile defines the following stages:

-- **Install Dependencies:**
Installs the necessary Node.js dependencies using npm install --save.
Verifies that dependencies are successfully installed.
-- **Build Docker Image:**
Builds a Docker image for the Node.js application with the latest tag.
The image is created from the Dockerfile present in the root of the project.
-- **Snyk Security Scan:**
Runs a Snyk scan to detect security vulnerabilities in the project dependencies.
If any vulnerabilities are found, the issues are printed in the Jenkins console log, categorized by severity.
-- **Run Docker Container:**
Checks if a Docker container named my-node-app is already running.
If the container exists but is stopped, it will be started.
If the container doesn’t exist, a new one will be created and started, exposing port 3000.
-- **Post-Pipeline Actions:**
On success, the pipeline logs a success message.
On failure, it logs failure details and prints a list of Docker containers and images for debugging purposes.

### Steps to Set Up and Run the Pipeline
Jenkins Setup:

Create a new pipeline job in Jenkins.
Copy and paste the above Jenkinsfile into your pipeline configuration.
Snyk Integration:

Install the Snyk Plugin in Jenkins.
Add your Snyk API Token to Jenkins credentials with the ID snyk-api-token.
Docker Installation:

Ensure that Docker is installed on your Jenkins agent.
Verify that Docker is properly configured and running.

---

## Local Development

To run the Node.js app locally:

1. Clone the repository:
   ```bash
   git clone https://github.com/VandhanaLude/aws-eb-nodejs-sample.git
   cd aws-eb-nodejs-sample
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the application:
   ```bash
   npm start
   ```

4. Run tests:
   ```bash
   npm test
   ```

---

## Monitoring and Alerts

With the **Snyk Monitor** step in the pipeline, Snyk will continuously monitor your project for new vulnerabilities, and you will receive alerts via the Snyk dashboard and email notifications.

---

## Conclusion

This setup automates the deployment process for a Node.js app on AWS Elastic Beanstalk, integrates **Snyk** to ensure that security vulnerabilities are detected early, and provides a seamless CI/CD workflow.

