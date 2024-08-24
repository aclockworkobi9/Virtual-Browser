// This is a Jenkins Declarative Pipeline script

pipeline {
    // Use any available agent to run the pipeline
    agent any
    
    // Environment variables to be used in the pipeline
    environment {
        // Define SCANNER_HOME environment variable using a SonarQube scanner tool installation
        SCANNER_HOME = tool name: 'sonar-scanner',
    }

    // Define the stages of the pipeline
    stages {

        // Stage to check out the Git repository
        stage('Git-checkout') {
            steps {
                // Clone the repository and checkout the main branch
                git branch: 'main', url: 'https://github.com/aclockworkobi9/Virtual-Browser.git'
            }
        }

        // Stage to perform an OWASP Dependency Check for vulnerabilities
        stage('OWASP Dependency Check') {
            steps {
                // Run OWASP Dependency Check with additional arguments
                dependencyCheck additionalArguments: ' --scan ./ ', odcInstallation: 'DC'
                
                // Publish the Dependency Check report
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }

        // Stage to run SonarQube analysis for code quality and security
        stage('SonarQube') {
            steps {
                // Use SonarQube environment configured in Jenkins
                withSonarQubeEnv('sonar') {
                    // Run SonarQube scanner using the specified SCANNER_HOME and project settings
                    sh '''
                        ${SCANNER_HOME}/bin/sonar-scanner -Dsonar.projectKey=VirtualBrowser \
                        -Dsonar.projectName=VirtualBrowser
                    '''
                }
            }
        }

        // Stage to build and tag a Docker image
        stage('Docker build & Tag Image') {
            steps {
                script {
                    // Use Docker registry credentials to authenticate the build process
                    withDockerRegistry([credentialsId: 'docker-cred', toolName: 'Docker']) {
                        // Change to the directory containing the Dockerfile and build the Docker image
                        dir('home/ubuntu/.Jenkins/workspace/Virtual-Browser/.docker/firefox') {
                            // Build Docker image with the specified tag
                            sh "docker build -t aclockworkboi9/vb:latest ."
                        }
                    }
                }
            }
        }

        // Stage to scan the Docker image for vulnerabilities using Trivy
        stage('Trivy Docker Scan') {
            steps {
                // Run Trivy to scan the specified Docker image
                sh "trivy image aclockworkboi9/vb:latest"
            }
        }

        // Stage to push the Docker image to a Docker registry
        stage('Docker Push Image') {
            steps {
                script {
                    // Use Docker registry credentials to authenticate the push process
                    withDockerRegistry([credentialsId: 'docker-cred', toolName= 'Docker']) {
                        // Push the Docker image to the specified repository
                        sh "docker push aclockworkboi9/vb:latest"
                    }
                }
            }
        }

        // Stage to deploy the application using Docker Compose
        stage('Deploy') {
            steps {
                // Use Docker Compose to deploy the application in detached mode
                sh "docker-compose up -d"
            }
        }
    }
}
