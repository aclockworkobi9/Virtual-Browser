
# Jenkins CI/CD Pipeline Setup Guide
This guide outlines the steps to set up a Jenkins CI/CD pipeline with various integrations including Docker, SonarQube, and OWASP Dependency-Check.

## Prerequisites
- AWS EC2 instance (t2.large recommended)
- Basic knowledge of AWS, Jenkins, and Docker

## Setup Steps
1. **Configure Security Group:**
   - Open HTTP (port 80), SSH (port 22), and a custom TCP port range (3000-10000).
   - Open UDP port range (52000-52100).
   - Allocate up to 15 GB of storage.
   
   ![image](https://github.com/user-attachments/assets/f346576b-5991-46ab-bb22-4eba68a43143)
   ![image](https://github.com/user-attachments/assets/9d468090-7aa8-4458-9503-c6e5202170a9)

  
2. **Launch EC2 Instance**
   - Use t2.large instance type

3. **Update and Upgrade System**
```bash
   sudo apt update && sudo apt upgrade -y
 ```
![image](https://github.com/user-attachments/assets/18c25b96-c05b-44ba-9d45-b9a2892b2807)


4. **Install Java**
```bash
   sudo apt install openjdk-11-jdk -y
```

5. **Run Jenkins on a specific port (replace [custom_port] with an actual port number, e.g., 8080)**
```bash
  wget https://get.jenkins.io/war-stable/2.426.2/jenkins.war
  java -jar jenkins.war --httpPort=custom_port [except 8080 because we are running our application on it]
```

6. **Access Jenkins**
   - Navigate to `http://<your-ip>:custom_port [except 8080 because we are running our application on it]`

7. **Retrieve Jenkins Admin Password**
```bash
   cat /path/to/jenkins/secrets/initialAdminPassword
  
```
![image](https://github.com/user-attachments/assets/918abd65-6f26-44ab-a439-301e95363fdf)

8. **Install Suggested Jenkins Plugins**
   - During the initial Jenkins setup, install the suggested plugins when prompted.

9. **Install Additional Software**
   - Docker:
     ```bash
     sudo apt install docker.io -y
     ```
   - Trivy:
     ```bash
     sudo apt-get install wget apt-transport-https gnupg lsb-release
     wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
     echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
     sudo apt-get update
     sudo apt-get install trivy
     ```

10. **Install Jenkins Plugins**
    - Navigate to "Manage Jenkins" > "Manage Plugins" > "Available" tab
    - Search for and install the following plugins:
      - SonarQube Scanner
      - OWASP Dependency-Check Plugin
      - Docker Pipeline

11. **Configure Docker Access**
    Run one of the following commands to grant Jenkins access to Docker:
    ```bash
    sudo chmod 666 /var/run/docker.sock
    # or
    sudo usermod -aG docker jenkins
    ```
    Note: Replace 'jenkins' with the appropriate username if different in your setup.

12. **Set Up SonarQube**
    ```bash
    docker run -d -p 9000:9000 sonarqube:lts-community
    ```

13. **Configure Jenkins for SonarQube**
    - Set up tools: Docker, OWASP Dependency-Check, SonarQube Scanner
  ![image](https://github.com/user-attachments/assets/e88df442-fd68-46fc-a1f1-043a4fb13aa6)

14. **Configure SonarQube in Jenkins**
    - Add SonarQube server information and authentication token
  ![image](https://github.com/user-attachments/assets/7ae0b78f-e6a7-46f9-8907-6e049087c574)

  ![image](https://github.com/user-attachments/assets/08194712-e8b4-4d0c-8b22-ed3998b2483c)

  ![image](https://github.com/user-attachments/assets/5cb1e06e-b212-4ff6-be89-3d3b64c12096)

15. **Add Docker Hub Credentials in Jenkins**
     - Go to **Manage Jenkins** > **Manage Credentials**.
     - Add Docker Hub username and password.

  ![image](https://github.com/user-attachments/assets/b75e617f-3b7a-4d0b-b773-f382b3c3ab08)

16. **Create Jenkins Pipeline**
    - Refer to the `Jenkinsfile` in your repository for pipeline syntax

17. **Update Docker Compose**
    - Replace image name in `docker-compose.yml` with your Docker image name
  ![image](https://github.com/user-attachments/assets/609ea3dc-64a1-421b-835e-7bc5dc2a4e44)

18. **Access Final Output**
    - Access final at `http://<your-ip>:8080`
  ![image](https://github.com/user-attachments/assets/fe1f821a-95d2-4377-bca1-c221cb15af4f)

## Important Notes

- Remember to delete AWS resources when not in use to avoid unnecessary charges.
- Ensure all security best practices are followed, especially when exposing services to the internet.

## Troubleshooting

If you encounter any issues during the setup, please refer to the official documentation of the respective tools or seek assistance from the community forums.

```

