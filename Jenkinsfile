pipeline {
    agent any

    environment {
        DOCKER_USER = "salemgaleb"
        IMAGE_NAME = "${DOCKER_USER}/repo-name:${BUILD_NUMBER}"
        DOCKER_CREDENTIALS = "dockerhub-creds"   
    }

    stages {

        stage('Clone Repository') {
            steps {
                checkout scm
                script {
                    echo "Clone the GitHub repo successfull"
                }
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    echo "Bulilding Docker Images..."
                    sh "docker build -t ${IMAGE_NAME} ./backend"
                    sh "docker build -t ${IMAGE_NAME} ./frontend"
                

                }
            }
        }
    }












}