
```markdown
# Jenkins CI/CD Pipeline Setup Guide

This guide outlines the steps to set up a Jenkins CI/CD pipeline with various integrations including Docker, SonarQube, and OWASP Dependency-Check.

## Prerequisites

- AWS EC2 instance (t2.large recommended)
- Basic knowledge of AWS, Jenkins, and Docker

## Setup Steps

1. **Configure Security Group**
   - Open HTTP (port 80), SSH (port 22), and custom TCP ports (3000-10000)
   - Open UDP port range (52000-52100)
   - Allocate up to 15 GB of storage
  ![alt text](image.png)
  ![alt text](image-1.png)
2. **Launch EC2 Instance**
   - Use t2.large instance type

3. **Update and Upgrade System**
   ```bash
   sudo apt update && sudo apt upgrade -y
   ![alt text](image-2.png)```

4. **Install Java**

5. **Download and Run Jenkins**
   ```bash
   wget https://get.jenkins.io/war-stable/2.426.2/jenkins.war
   java -jar jenkins.war --httpPort=[custom_port]
   ```

6. **Access Jenkins**
   - Navigate to `http://<your-ip>:custom_port`

7. **Retrieve Jenkins Admin Password**
   ```bash
   cat /path/to/jenkins/secrets/initialAdminPassword
  ![alt text](image-3.png)```

8. **Install Suggested Jenkins Plugins**

9. **Install Additional Software**
   - Docker
   - Trivy

10. **Install Jenkins Plugins**
    - SonarQube Scanner
    - OWASP Dependency-Check Plugin
    - Docker Pipeline
  ![alt text](image-4.png)
  ![alt text](image-5.png)
  ![alt text](image-6.png)
11. **Configure Docker Access**
    ```bash
    sudo chmod 666 /var/run/docker.sock
    # or
    sudo usermod -aG docker USER_NAME
    ```

12. **Set Up SonarQube**
    ```bash
    docker run -d -p 9000:9000 sonarqube:lts-community
    ```

13. **Configure Jenkins for SonarQube**
    - Set up tools: Docker, OWASP Dependency-Check, SonarQube Scanner
  ![alt text](image-7.png)
14. **Configure SonarQube in Jenkins**
    - Add SonarQube server information and authentication token
  ![alt text](image-8.png)
  ![alt text](image-9.png)
  ![alt text](image-10.png)
15. **Add Docker Hub Credentials in Jenkins**
     - Go to **Manage Jenkins** > **Manage Credentials**.
     - Add Docker Hub username and password.

  ![alt text](image-11.png)
16. **Create Jenkins Pipeline**
    - Refer to the `Jenkinsfile` in your repository for pipeline syntax

17. **Update Docker Compose**
    - Replace image name in `docker-compose.yml` with your Docker image name
  ![alt text](image-12.png)
18. **Access Final Output**
    - Access final at `http://<your-ip>:8080`
  ![alt text](image-13.png)
## Important Notes

- Remember to delete AWS resources when not in use to avoid unnecessary charges.
- Ensure all security best practices are followed, especially when exposing services to the internet.

## Troubleshooting

If you encounter any issues during the setup, please refer to the official documentation of the respective tools or seek assistance from the community forums.

```

