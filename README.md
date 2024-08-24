
1\. \*\*Configure Security Group:\*\*

`   `- Open HTTP (port 80), SSH (port 22), and a custom TCP port range (3000-10000).

`   `- Open UDP port range (52000-52100).

`   `- Allocate up to 15 GB of storage.

![A screenshot of a computer

Description automatically generated](Aspose.Words.31ba321f-c3b3-47ee-ab76-f1f8ec06dcf6.001.png)![A screenshot of a computer

Description automatically generated](Aspose.Words.31ba321f-c3b3-47ee-ab76-f1f8ec06dcf6.002.png)

2\. \*\*Launch Instance:\*\*

`    `- I launched the t2.large

3\. \*\*Update and Upgrade:\*\*

`   `- Run the following commands to update and upgrade your instance:

![](Aspose.Words.31ba321f-c3b3-47ee-ab76-f1f8ec06dcf6.003.png)

4\. \*\*Install Java:\*\*

5\. \*\*Download and Run Jenkins:\*\*

`   `- Execute the following commands:

`     `1. Download Jenkins:

`        ````bash

`        `wget https://get.jenkins.io/war-stable/2.426.2/jenkins.war

`        ````

`     `2. Start Jenkins:

`        ````bash

`        `java -jar jenkins.war --httpPort= [  # Change port number if needed except 8080]

`        ````

`   `- Launch a new terminal as Jenkins does not run in the background.

6\. \*\*Access Jenkins:\*\*

`   `- Open a browser and navigate to the IP address of your instance with the port you selected (e.g., `http://<your-ip>: port exposed`).

7\. \*\*Retrieve Jenkins Admin Password:\*\*

`   `- Use the following command to get the Jenkins admin password:

`     ````bash

`     `cat /path/to/jenkins/secrets/initialAdminPassword

`     ````

![A screenshot of a computer screen

Description automatically generated](Aspose.Words.31ba321f-c3b3-47ee-ab76-f1f8ec06dcf6.004.png)

8\. \*\*Install Suggested Plugins:\*\*

`   `- Follow the prompts in Jenkins to install the suggested plugins.

9\. \*\*Install Additional Software:\*\*

`   `- \*\*Docker:\*\* Follow the official Docker documentation to install Docker.

`   `- \*\*Trivy:\*\* Follow the official Trivy documentation to install Trivy.

10\. \*\*Install Jenkins Plugins:\*\*

`    `- Install the following Jenkins plugins:

`      `- \*\*SonarQube Scanner\*\*

`      `- \*\*OWASP Dependency-Check Plugin\*\*

`      `- \*\*Docker Pipeline\*\*

![A screenshot of a computer

Description automatically generated](Aspose.Words.31ba321f-c3b3-47ee-ab76-f1f8ec06dcf6.005.png)

![A screenshot of a computer

Description automatically generated](Aspose.Words.31ba321f-c3b3-47ee-ab76-f1f8ec06dcf6.006.png)

![A screenshot of a chat

Description automatically generated](Aspose.Words.31ba321f-c3b3-47ee-ab76-f1f8ec06dcf6.007.png)

11\. \*\*Permit Docker Access:\*\*

`    `- Allow other users to access Docker by running one of the following commands:

`      ````bash

`      `sudo chmod 666 /var/run/docker.sock

`      `# or

`      `sudo usermod -aG docker USER\_NAME

`      ````

12\. \*\*Set Up SonarQube:\*\*

`    `- Run a SonarQube container and expose it on port 9000:

`      ````bash

`      `docker run -d -p 9000:9000 sonarqube:lts-community

`      ````

13\. \*\*Configure Jenkins for SonarQube:\*\*

`    `- In Jenkins, navigate to \*\*Manage Jenkins\*\* > \*\*Global Tool Configuration\*\*.

`    `- Install the following tools:

`      `- \*\*Docker\*\*

`      `- \*\*OWASP Dependency-Check\*\*

`      `- \*\*SonarQube Scanner\*\*

![A long line of a person's hand

Description automatically generated with medium confidence](Aspose.Words.31ba321f-c3b3-47ee-ab76-f1f8ec06dcf6.008.png)

14\. \*\*Configure SonarQube in Jenkins:\*\*

`    `- Go to \*\*Manage Jenkins\*\* > \*\*Configure System\*\*.

`    `- Add SonarQube server information:

`      `- \*\*SonarQube URL:\*\* `http://<your-ip>:9000`

`      `- \*\*Authentication Token:\*\* Generate a token in SonarQube (go to \*\*Administration\*\* > \*\*Security\*\* > \*\*Users\*\* > \*\*Generate Token\*\*) and paste it in Jenkins under \*\*SonarQube servers\*\*.

![A screenshot of a computer

Description automatically generated](Aspose.Words.31ba321f-c3b3-47ee-ab76-f1f8ec06dcf6.009.png)

![A screenshot of a computer

Description automatically generated](Aspose.Words.31ba321f-c3b3-47ee-ab76-f1f8ec06dcf6.010.png)

![](Aspose.Words.31ba321f-c3b3-47ee-ab76-f1f8ec06dcf6.011.png)

15\. \*\*Add Docker Hub Credentials in Jenkins:\*\*

`    `- Go to \*\*Manage Jenkins\*\* > \*\*Manage Credentials\*\*.

`    `- Add Docker Hub username and password.

![A white paper with black lines

Description automatically generated](Aspose.Words.31ba321f-c3b3-47ee-ab76-f1f8ec06dcf6.012.png)

16\. \*\*Create a Pipeline:\*\*

`    `- Go to \*\*New Item\*\* in Jenkins and create a new pipeline.

`    `- For pipeline syntax, refer to the `Jenkinsfile` provided in your repository.

17\. \*\*Update Docker Compose:\*\*

`    `- Replace the image name in your `docker-compose.yml` file with your Docker image name.

`    `- Build and run the Docker Compose configuration.

![A screenshot of a computer program

Description automatically generated](Aspose.Words.31ba321f-c3b3-47ee-ab76-f1f8ec06dcf6.013.png)

18\. \*\*Access Jenkins:\*\*

`    `- You can now access Jenkins through your browser at `http://<your-ip>:8080`.

![A screenshot of a computer

Description automatically generated](Aspose.Words.31ba321f-c3b3-47ee-ab76-f1f8ec06dcf6.014.png)

\---

Don’t forget to delete the resources.
