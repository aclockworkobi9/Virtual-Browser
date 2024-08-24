---

1. **Configure Security Group:**
   - Open HTTP (port 80), SSH (port 22), and a custom TCP port range (3000-10000).
   - Open UDP port range (52000-52100).
   - Allocate up to 15 GB of storage.
  ![security_group](https://github.com/user-attachments/assets/241c59e8-5613-4227-bbc8-7f9642ce7915)

  ![storage](https://github.com/user-attachments/assets/effd0542-82a9-4c2d-911e-2f99b7623a6e)



2. **Launch Instance:**

3. **Update and Upgrade:**
   - Run the following commands to update and upgrade your instance:
 ![update_upgrade_cmd](https://github.com/user-attachments/assets/a537d7ae-26d0-4151-9e68-cf289a504bff)


4. **Install Java:**

5. **Download and Run Jenkins:**
   - Execute the following commands:
     1. Download Jenkins:
        ```bash
        wget https://get.jenkins.io/war-stable/2.426.2/jenkins.war
        ```
     2. Start Jenkins:
        ```bash
        java -jar jenkins.war --httpPort=8081  # Change port number if needed
        ```
   - Launch a new terminal as Jenkins does not run in the background.

6. **Access Jenkins:**
   - Open a browser and navigate to the IP address of your instance with the port you selected (e.g., `http://<your-ip>:8081`).

7. **Retrieve Jenkins Admin Password:**
   - Use the following command to get the Jenkins admin password:
     ```bash
     cat /path/to/jenkins/secrets/initialAdminPassword
     ```


 ![jenkins_start_page](https://github.com/user-attachments/assets/bbfe63b6-b960-41e5-a2c5-251905c73d64)


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

 ![Manage_jenkins](https://github.com/user-attachments/assets/388b2486-ef4b-4c16-a194-86ee24f3deab)

 ![sonarqube](https://github.com/user-attachments/assets/279a96d9-4fdd-4593-8ffe-1b42b9a4ee60)

 ![Docker](https://github.com/user-attachments/assets/d961a66e-a1a4-4465-8843-6192b23717c3)


 
 
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
      docker run -d -p 9000:9000 sonarqube:lts
      ```

13. **Configure Jenkins for SonarQube:**
    - In Jenkins, navigate to **Manage Jenkins** > **Global Tool Configuration**.
    - Install the following tools:
      - **Docker**
      - **OWASP Dependency-Check**
      - **SonarQube Scanner**
![docker_unter_tools](https://github.com/user-attachments/assets/bb755c76-c5e4-4170-86ff-b4f791c95a5f)


14. **Configure SonarQube in Jenkins:**
    - Go to **Manage Jenkins** > **Configure System**.
    - Add SonarQube server information:
      - **SonarQube URL:** `http://<your-ip>:9000`
      - **Authentication Token:** Generate a token in SonarQube (go to **Administration** > **Security** > **Users** > **Generate Token**) and paste it in Jenkins under **SonarQube servers**..
 
 ![sonar-admin](https://github.com/user-attachments/assets/c4b70432-fc00-48eb-96eb-0624b512841f)

 ![sonar-users](https://github.com/user-attachments/assets/115ef7e5-5b4a-4809-ad61-b9b78a6dd3cf)

 ![sonar-token](https://github.com/user-attachments/assets/e658e045-1529-4080-ac4b-d043942bf541)


 
15. **Add Docker Hub Credentials in Jenkins:**
    - Go to **Manage Jenkins** > **Manage Credentials**.
    - Add Docker Hub username and password.

![sonar-token-added-jenkins](https://github.com/user-attachments/assets/a6e754ff-198f-4c7a-8b8c-550017c55ef4)



16. **Create a Pipeline:**
    - Go to **New Item** in Jenkins and create a new pipeline.
    - For pipeline syntax, refer to the `Jenkinsfile` provided in your repository.

17. **Update Docker Compose:**
    - Replace the image name in your `docker-compose.yml` file with your Docker image name.
    - Build and run the Docker Compose configuration.
![docker-compose](https://github.com/user-attachments/assets/d6afa4af-debe-4f19-8082-0a0c233a5869)


18. **Access Jenkins:**
    - You can now access Jenkins through your browser at `http://<your-ip>:8080`.
![final_result](https://github.com/user-attachments/assets/5eb9b899-ca91-4dc5-8d73-622d9d0ad756)


---

Don’t forget to delete the resources.
