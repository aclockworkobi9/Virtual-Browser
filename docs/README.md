---
1. **Configure Security Group:**
   - Open HTTP (port 80), SSH (port 22), and a custom TCP port range (3000-10000).
   - Open UDP port range (52000-52100).
   - Allocate up to 15 GB of storage.
  ![image](https://github.com/user-attachments/assets/94cd3f8b-aea6-41b3-b4ca-511c4a84631d)
  ![image](https://github.com/user-attachments/assets/bc99f72f-a1ca-465b-a5f8-2154a8fd5c1b)


2. **Launch Instance:**
    - I launched the t2.large
3. **Update and Upgrade:**
   - Run the following commands to update and upgrade your instance:
 ![image](https://github.com/user-attachments/assets/7f10c9aa-2d24-45d2-a137-e07313331304)

4. **Install Java:**

5. **Download and Run Jenkins:**
   - Execute the following commands:
     1. Download Jenkins:
        ```bash
        wget https://get.jenkins.io/war-stable/2.426.2/jenkins.war
        ```
     2. Start Jenkins:
        ```bash
        java -jar jenkins.war --httpPort= [  # Change port number if needed except 8080]
        ```
   - Launch a new terminal as Jenkins does not run in the background.

6. **Access Jenkins:**
   - Open a browser and navigate to the IP address of your instance with the port you selected (e.g., `http://<your-ip>: port exposed`).

7. **Retrieve Jenkins Admin Password:**
   - Use the following command to get the Jenkins admin password:
     ```bash
     cat /path/to/jenkins/secrets/initialAdminPassword
     ```
 ![image](https://github.com/user-attachments/assets/e3d90bb3-a0b7-4544-b805-4532c508e461)

8. **Install Suggested Plugins:**
   - Follow the prompts in Jenkins to install the suggested plugins.

9. **Install Additional Software:**
   - **Docker:** Follow the official Docker documentation to install Docker.
   - **Trivy:** Follow the official Trivy documentation to install Trivy.

10. **Install Jenkins Plugins:**
    - Install the following Jenkins plugins:
      - **SonarQube Scanner**
      - **OWASP Dependency-Check Plugin**
      - **Docker Pipeline**
 ![image](https://github.com/user-attachments/assets/b1a251ae-d6ae-44bd-8f08-98583afe57bd)
 ![image](https://github.com/user-attachments/assets/ca2c7393-8be0-452f-9ce1-63c7ce437673)
 ![image](https://github.com/user-attachments/assets/d9743563-7a2f-4dbe-8619-f7b323e8129c)

 
 
11. **Permit Docker Access:**
    - Allow other users to access Docker by running one of the following commands:
      ```bash
      sudo chmod 666 /var/run/docker.sock
      # or
      sudo usermod -aG docker USER_NAME
      ```

12. **Set Up SonarQube:**
    - Run a SonarQube container and expose it on port 9000:
      ```bash
      docker run -d -p 9000:9000 sonarqube:lts-community
      ```

13. **Configure Jenkins for SonarQube:**
    - In Jenkins, navigate to **Manage Jenkins** > **Global Tool Configuration**.
    - Install the following tools:
      - **Docker**
      - **OWASP Dependency-Check**
      - **SonarQube Scanner**
 ![image](https://github.com/user-attachments/assets/c3104a50-bad2-4229-bdb8-20fcd7e36f77)

14. **Configure SonarQube in Jenkins:**
    - Go to **Manage Jenkins** > **Configure System**.
    - Add SonarQube server information:
      - **SonarQube URL:** `http://<your-ip>:9000`
      - **Authentication Token:** Generate a token in SonarQube (go to **Administration** > **Security** > **Users** > **Generate Token**) and paste it in Jenkins under **SonarQube servers**.
 
 ![image](https://github.com/user-attachments/assets/4ac275ed-af1c-4e2e-804b-ef9a472630b8)
 ![image](https://github.com/user-attachments/assets/028d2724-4a94-4883-9f91-9c08c73b04e1)
 ![image](https://github.com/user-attachments/assets/70ae0b82-8beb-49a1-939a-dc055e03963d)

 
15. **Add Docker Hub Credentials in Jenkins:**
    - Go to **Manage Jenkins** > **Manage Credentials**.
    - Add Docker Hub username and password.
 ![image](https://github.com/user-attachments/assets/1ecca55a-0437-4969-be28-c6e5a67c52f7)


16. **Create a Pipeline:**
    - Go to **New Item** in Jenkins and create a new pipeline.
    - For pipeline syntax, refer to the `Jenkinsfile` provided in your repository.

17. **Update Docker Compose:**
    - Replace the image name in your `docker-compose.yml` file with your Docker image name.
    - Build and run the Docker Compose configuration.
 ![image](https://github.com/user-attachments/assets/a2e40a95-d02c-427a-a836-8eb6faf27d33)

18. **Access Jenkins:**
    - You can now access Jenkins through your browser at `http://<your-ip>:8080`.
 ![image](https://github.com/user-attachments/assets/caf9d1fa-e625-489c-8a3d-f03608192394)

---

Don’t forget to delete the resources.
