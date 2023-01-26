# Jenkins-GitLab-Integration

This project demonstrates how to integrate Jenkins and GitLab using Docker Compose. It includes a Jenkins pipeline that tests the availability of the GitLab container and retries the test if it fails, using the Build Failure Analyzer plugin. This project can be used as a starting point for building a more complex Jenkins-GitLab integration.

Building the Docker Compose:
To build the containers, you need to have Docker and Docker Compose installed on your machine. 

run: docker-compose up -d

this command will start the Jenkins and GitLab containers and make them available on ports 8080 and 80 respectively. The containers will be connected to a custom network called "mynetwork" that allows them to communicate with each other.

The docker-compose.yaml file includes the following services:
Jenkins: This service runs the Jenkins container, exposing port 8080, and mounting the jenkins_data volume to store Jenkins data.
GitLab: This service runs the GitLab container, exposing ports 80 and 443, and mounting the gitlab_data volume to store GitLab data.

Installing the Plugin:
In order to use the Build Failure Analyzer plugin in your Jenkins pipeline, you need to install it from the Jenkins plugin manager. You can do this by navigating to the Jenkins web interface and going to "Manage Jenkins" -> "Manage Plugins" -> "Available" and searching for "Build Failure Analyzer"

Building the Pipeline:
Once you have the plugin installed, you can create a new pipeline in Jenkins and paste the pipeline from my Jenkinsfile 

The pipeline is designed to test the availability of a GitLab container, which is running as a separate container alongside the Jenkins container. The pipeline uses the curl command to send an HTTP request to the GitLab container and check for a successful response. If the response is unsuccessful, the pipeline retries the request up to three times before moving on to the next stage. The pipeline also includes the buildFailureAnalyzer plugin, which is used to analyze the results of the GitLab availability test and determine if the job should be restarted if it fails. This allows for automated testing and retrying of the GitLab container's availability, ensuring that it is always up and running for use by the Jenkins container and other systems.
