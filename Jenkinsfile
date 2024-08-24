pipeline {
    agent any
    
    environment {
        SCANNER_HOME = tool name: 'sonar-scanner',
    }

    stages {
        stage('Git-checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/aclockworkobi9/Vitual-Browser.git'
            }
        }

        stage('OWASP Dependency Check') {
            steps {
                dependencyCheck additionalArguments: ' --scan ./ ', odcInstallation: 'DC'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }

        stage('SonarQube') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh '''
                        ${SCANNER_HOME}/bin/sonar-scanner -Dsonar.projectKey=VirtualBrowser \
                        -Dsonar.projectName=VirtualBrowser
                    '''
                }
            }
        }

        stage('Docker build & Tag Image') {
            steps {
                script {
                    withDockerRegistry([credentialsId: 'docker-cred', url: '']) {
                        dir('home/ubuntu/.Jenkins/workspace/Virtual-Browser/.docker/firefox') {
                            sh "docker build -t aclockworkboi9/vb:latest ."
                        }
                    }
                }
            }
        }

        stage('Trivy Docker Scan') {
            steps {
                sh "trivy image aclockworkboi9/vb:latest"
            }
        }

        stage('Docker Push Image') {
            steps {
                script {
                    withDockerRegistry([credentialsId: 'docker-cred', url: '']) {
                        sh "docker push aclockworkboi9/vb:latest"
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                sh "docker-compose up -d"
            }
        }
    }
}
